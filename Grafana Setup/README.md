# Grafana Setup

    wget https://dl.grafana.com/enterprise/release/grafana-enterprise_10.4.2_amd64.deb
    sudo dpkg -i grafana-enterprise_10.4.2_amd64.deb
    sudo apt-get install -f -y

    sudo systemctl enable grafana-server
    sudo systemctl start grafana-server
