# prometheus
Workable configs and rules for Prometheus 2.0

Based on https://github.com/stefanprodan/dockprom

Changed the alert rules, added cAdvisor and blackbox exporters.

1. cAdvisor exporter should be installed on each instance which you want to monitor: 

```
docker run --volume=/:/rootfs:ro --volume=/var/run:/var/run:rw --volume=/var/lib/docker/:/var/lib/docker:ro \
--volume=/cgroup:/cgroup:ro --volume=/sys:/sys:ro --publish=9200:8080 --privileged=true --detach=true \
--restart=always --name=jop_cadvisor google/cadvisor:v0.25.0
```

Use <instance_ip>:9200 for access to cAdvisor metrics.

2. Blackbox exporter should be installed on monitoring server only:

```
docker run -d -p 9115:9115 --restart=always -v /root/dockprom/blackbox:/config --name blackbox \
prom/blackbox-exporter:v0.12.0 --config.file=/config/config.yml
```
