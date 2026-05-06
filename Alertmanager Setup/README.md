# Install
    wget https://github.com/prometheus/alertmanager/releases/download/v0.27.0/alertmanager-0.27.0.linux-amd64.tar.gz     
    tar -xvf alertmanager-0.27.0.linux-amd64.tar.gz
    cd alertmanager-0.27.0.linux-amd64
# Alertmanager Config
    vi alertmanager.yml
## alertmanager.yml

    global:
      smtp_smarthost: 'smtp.gmail.com:587'
      smtp_from: 'your-email@gmail.com'
      smtp_auth_username: 'your-email@gmail.com'
      smtp_auth_password: 'your-app-password'

    route:
      receiver: 'email-alert'

    receivers:
    - name: 'email-alert'
      email_configs:
      - to: 'your-email@gmail.com'

# Alertmanager Service
     sudo vi /etc/systemd/system/alertmanager.service
## alertmanager.service
    [Unit] 
    Description=Alertmanager
    After=network.target

    [Service]
    ExecStart=/home/ubuntu/alertmanager-0.27.0.linux-amd64/alertmanager \
      --config.file=/home/ubuntu/alertmanager-0.27.0.linux-amd64/alertmanager.yml
    Restart=always

    [Install]
    WantedBy=multi-user.target

# RUN
    sudo systemctl daemon-reload
    sudo systemctl enable alertmanager
    sudo systemctl start alertmanager
