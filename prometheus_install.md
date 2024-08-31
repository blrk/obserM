#### Install Prometheus
* Download the package form https://prometheus.io/download/
```bash
wget https://github.com/prometheus/prometheus/releases/download/v2.54.1/prometheus-2.54.1.linux-amd64.tar.gz
```
* Create a user and Group
```bash
sudo groupadd --system prometheus
sudo useradd -s /sbin/nologin --system -g prometheus prometheus
```
* Create a log directory
```bash
sudo mkdir /var/lib/prometheus
```
* Make directories
```bash
sudo mkdir -p /etc/prometheus/rules
sudo mkdir -p /etc/prometheus/rules.s
sudo mkdir -p /etc/prometheus/files_sd
```
* Extract the tar file
```bash
tar -xvf prometheus-2.54.1.linux-amd64.tar.gz
```
* Navigate to the extracted directory 
```bash
cd prometheus-2.54.1.linux-amd64/
```
* Move the prometheus binary to bin of /usr
```bash
sudo mv prometheus /usr/local/bin/
```
* Verify the access
```bash
prometheus --version
prometheus, version 2.54.1 (branch: HEAD, revision: e6cfa720fbe6280153fab13090a483dbd40bece3)
  build user:       root@812ffd741951
  build date:       20240827-10:56:41
  go version:       go1.22.6
  platform:         linux/amd64
  tags:             netgo,builtinassets,stringlabels
```
* Move the prometheus.yml file
```bash
mv prometheus.yml /etc/prometheus/prometheus.yml
```
* Create a linux service file
```bash
sudo tee /etc/systemd/system/prometheus.service<<EOF
[Unit]
Description=Prometheus
Documentation=https://prometheus.io/docs/introduction/overview/
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
User=prometheus
Group=prometheus
ExecReload=/bin/kill -HUP $MAINPID
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/var/lib/prometheus \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries \
  --web.listen-address=0.0.0.0:9090 \
  #--web.external-url=

SyslogIdentifier=prometheus
Restart=always

[Install]
WantedBy=multi-user.target
EOF
```
* Change the ownership
```bash
sudo chown -R prometheus:prometheus /etc/prometheus/
sudo chown -R prometheus:prometheus /etc/prometheus/*
```
* Add privilage
```bash
sudo chmod 755 /etc/prometheus/
```
* Change ownership of log directory
```bash
sudo chown -R prometheus:prometheus /var/lib/prometheus/
```
* start service
```bash
sudo systemctl daemon-reload 
sudo systemctl start prometheus.service 
sudo systemctl status prometheus.service 
```
* Verify the service in browser
```bash
http://<ip>:9090
```





