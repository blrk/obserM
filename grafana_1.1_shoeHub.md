### Create my first Dashboard form a container app
* https://github.com/aussiearef/ShoeHubV2/tree/main
* Create a container
```bash
  docker run -p 8020:80 -i aussiearef/shoehub
```
* Append the target in Prometheus.yml
* vi /etc/prometheus/prometheus.yml
```bash
- job_name: 'shoehub'
    static_configs:
      - targets: ['192.168.122.168:8030']
```