# K8S Logging Architecture
https://kubernetes.io/docs/concepts/cluster-administration/logging/

# Docker Configure logging drivers
https://docs.docker.com/config/containers/logging/configure/

# Docker Local File logging driver
https://docs.docker.com/config/containers/logging/local/


```
# log-driver=local

docker run \
 -d -p 9080:8080 -p 443:8081 --name gw-01 \
 --env-file env.ggz.conf \
 --log-driver local --log-opt max-size=10m \
 -v /mnt/d/MyGitHub/Azure-APIM-Self-Hosted-Gateway/dockers-logs/log-driver/local/docker-gw:/etc/docker/ \
 mcr.microsoft.com/azure-api-management/gateway:latest

docker run -d -p 9080:8080 -p 443:8081 --name gw-01 --env-file env.ggz.conf --log-driver local --log-opt max-size=10m -v /home/user/dockers-logs/docker-gw:/etc/docker/ mcr.microsoft.com/azure-api-management/gateway:latest

docker run \
      --log-driver local --log-opt max-size=10m \
      -v /mnt/d/MyGitHub/Azure-APIM-Self-Hosted-Gateway/dockers-logs/log-driver/local/docker-gw/docker-echo:/etc/docker/ \
      alpine echo hello world

```


```
docker inspect --format='{{.LogPath}}' container_id
docker inspect --format='{{.LogPath}}' 6335bcb8ff61

```

# Docker Fluentd Logging Driver
https://docs.fluentd.org/container-deployment/docker-logging-driver

```
# log-driver=fluentd

docker run -it -p 24224:24224 \
 -v /mnt/d/MyGitHub/Azure-APIM-Self-Hosted-Gateway/fluentd.stdout.conf:/fluentd/etc/fluentd.conf \
 -e FLUENTD_CONF=fluentd.conf \
 fluent/fluentd:latest

docker run -it -p 24224:24224 \
 -v /mnt/d/MyGitHub/Azure-APIM-Self-Hosted-Gateway/fluentd.fileout.conf:/fluentd/etc/fluentd.conf \
 -v /mnt/d/MyGitHub/Azure-APIM-Self-Hosted-Gateway/logs2:/var/log/fluent \
 -e FLUENTD_CONF=fluentd.conf \
 fluent/fluentd:latest

docker run \
 -d -p 9080:8080 \
 -p 443:8081 \
 --name gw-01 \
 --env-file env.ggz.conf \
 --log-driver=fluentd \
 --log-opt fluentd-address=localhost:24224 \
 mcr.microsoft.com/azure-api-management/gateway:latest


```