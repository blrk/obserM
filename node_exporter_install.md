### Install and configure node exporter (client - containersec)
* Download the binary files - https://prometheus.io/download/#node_exporter
```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz
```
* Extract the file
```bash
tar -xvf node_exporter-1.8.2.linux-amd64.tar.gz
```
* Navigate into the directory 
```bash
cd node_exporter-1.8.2.linux-amd64
```
#### Configure prometheus to add the node exporter
* Open the prometheus.yml
```bash
sudo vi /etc/prometheus/prometheus.yml 
```
* Add the following configuration
```bash
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "docker server"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["192.168.122.168:9100"]
```
* Stop and start the service
```bash
sudo systemctl stop prometheus.service 
sudo systemctl start prometheus.service 
sudo systemctl status prometheus.service 
```
#### Run node exporter as service in client (containersec)
* Create user and group
```bash
sudo groupadd --system prometheus
sudo useradd -s /sbin/nologin --system -g prometheus prometheus
```
* Create a directory 
```bash
sudo mkdir /var/lib/node
```
* move the node exporter the created directory
```bash
sudo mv node_exporter /var/lib/node/
```
* Create a service file
```bash
sudo tee /etc/systemd/system/node.service<<EOF
[Unit]
Description=Prometheus Node Exporter
Documentation=https://prometheus.io/docs/introduction/overview/
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
User=prometheus
Group=prometheus
ExecReload=/bin/kill -HUP $MAINPID
ExecStart=/var/lib/node/node_exporter

SyslogIdentifier=prometheus_node_exporter
Restart=always

[Install]
WantedBy=multi-user.target
EOF
```
* Change the file ownership
```bash
sudo chown prometheus:prometheus /var/lib/node/
sudo chown prometheus:prometheus /var/lib/node/*
```
* Set the permission
```bash
sudo chmod 775 /var/lib/node/
sudo chmod 775 /var/lib/node/*
```
* Start the service
```bash
sudo systemctl daemon-reload 
sudo systemctl start node.service 
sudo systemctl enable node.service 
sudo systemctl status node.service 
```
#### SELinux Blocking: Follow the steps if SELinux block the execution
* Apply the Permanent SELinux Context: Use the semanage fcontext command to add a permanent rule for the file. This tells SELinux to always apply the specified context to the file in the future.
```bash
sudo semanage fcontext -a -t bin_t '/var/lib/node/node_exporter'
```
* Restore the Context: Once you have added the permanent rule, apply it to the file using restorecon. This ensures the current context is updated according to the new policy
```bash
sudo restorecon -v /var/lib/node/node_exporter
```
* Verify the Change: To confirm that the context is now correctly set and persistent, check the file's SELinux context again:
```bash
ls -Z /var/lib/node/node_exporter
```
* It should now permanently show the correct context (bin_t in this case).
* Test Persistence: To verify that the change is persistent across reboots or relabeling, you can test by running
```bash
sudo restorecon -v /var/lib/node/node_exporter
```
* Reboot the service and test. 