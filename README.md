# PrometheusMonitoringTutorial

Please make sure to update the configuration files with below details:
            Public IP where your applications are hosted
to and from email ID to send and receive notification alerts
smtp hostname
encrypted username and password for SMTP


Below are the commands that I have used in the video tutorial
Video link:


#install docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo bash get-docker.sh
cd /var/run/;sudo chmod 777 docker.pid docker.sock

#Prometheus installation
docker run -d --name prometheus --restart always -p 9090:9090 -v /etc/prometheus:/etc/prometheus/ prom/prometheus

#Node Exporter Installation
docker run -p 9100:9100 -d --restart always --name node-exporter prom/node-exporter

#Cadvisor Installation
docker run --volume=/:/rootfs:ro --volume=/var/run:/var/run:rw --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro --volume=/var/lib/docker/:/var/lib/docker:ro --restart always --publish=8085:8080 --detach=true --privileged=true --name=cadvisor google/cadvisor:latest --logtostderr --v=2

#Grafana Installation
docker run -d --restart always --name grafana -p 3000:3000 -v "grafana_new:/var/lib/grafana" grafana/grafana

#AlertManager Installation
docker run --name alertmanager -d -p 9093:9093 -v /etc/prometheus/:/etc/alertmanager quay.io/prometheus/alertmanager
