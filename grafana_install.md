### Install Grafana
* Reference: https://grafana.com/grafana/download?edition=oss
```bash
sudo yum install -y https://dl.grafana.com/oss/release/grafana-10.2.2-1.x86_64.rpm
```
* Enable and start the service
```bash
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
sudo systemctl status grafana-server
```

#### Configure Grafana
* Navigate to the config directory
```bash
cd /etc/grafana/
```
* List config files
```bash
ls
grafana.ini  ldap.toml  provisioning
```
* Create custom config file
```bash
sudo cp grafana.ini custom.ini
```
* Open the custom file
```bash
sudo vi custom.ini 
```
