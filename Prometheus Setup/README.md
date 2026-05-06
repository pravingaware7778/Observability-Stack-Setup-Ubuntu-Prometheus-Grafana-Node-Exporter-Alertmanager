# Install
    wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
    tar -xvf prometheus-2.52.0.linux-amd64.tar.gz
    cd prometheus-2.52.0.linux-amd64

# Prometheus Config
    vi prometheus.yml
# prometheus.yml
    global:
      scrape_interval: 5s

    rule_files:
      - "alert_rules.yml"

    scrape_configs:
     - job_name: 'node_exporter'
        static_configs:
          - targets: ['localhost:9100']

    alerting:
     alertmanagers:
         - static_configs:
             - targets:
                - localhost:9093
# Alert Rules
     vi alert_rules.yml
# alert_rules.yml
    groups:
     - name: node_alerts
       rules:
     - alert: HighCPUUsage
       expr: 100 - (avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100) > 80
       for: 1m
       labels:
        severity: warning
       annotations:
         summary: "High CPU Usage"
         description: "CPU usage is above 80%"
# Prometheus Service
    sudo vi /etc/systemd/system/prometheus.service
## prometheus.service
    [Unit]
    Description=Prometheus
    After=network.target

    [Service]
    ExecStart=/home/ubuntu/prometheus-2.52.0.linux-amd64/prometheus \
      --config.file=/home/ubuntu/prometheus-2.52.0.linux-amd64/prometheus.yml
    Restart=always

    [Install]
    WantedBy=multi-user.target
# RUN
    sudo systemctl daemon-reload
    sudo systemctl enable prometheus
    sudo systemctl start prometheus
         
