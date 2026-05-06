# Install
    wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz
    tar -xvf node_exporter-1.8.2.linux-amd64.tar.gz
    cd node_exporter-1.8.2.linux-amd64
# Run manually
    ./node_exporter

# Systemd Service
    sudo vi /etc/systemd/system/node_exporter.service

    
    [Unit]
    Description=Node Exporter
    After=network.target

    [Service]
    ExecStart=/home/ubuntu/node_exporter-1.8.2.linux-amd64/node_exporter
    Restart=always

    [Install]
    WantedBy=multi-user.target
# RUN
    sudo systemctl daemon-reload
    sudo systemctl enable node_exporter
    sudo systemctl start node_exporter
