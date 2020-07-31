```
docker run -d -p 9080:8080 -p 443:8081 --name gw-01 --env-file env.ggz.conf --log-driver local --log-opt max-size=10m -v /~/docker-gw:/etc/docker/ mcr.microsoft.com/azure-api-management/gateway:latest

docker run -d -p 9080:8080 -p 443:8081 --name gw-01 --env-file env.ggz.conf --log-driver local --log-opt max-size=10m -v /home/user/dockers-logs/docker-gw:/etc/docker/ mcr.microsoft.com/azure-api-management/gateway:latest

docker run \
      --log-driver local --log-opt max-size=10m \
      -v /home/user/dockers-logs/docker-echo:/etc/docker/ \
      alpine echo hello world


```

```
docker inspect --format='{{.LogPath}}' container_id
docker inspect --format='{{.LogPath}}' 6335bcb8ff61

```
-v /~/docker-gw:/etc/docker/

```


```
docker run -it -p 24224:24224 -v /mnt/d/MyGitHub/Azure-APIM-Self-Hosted-Gateway/fluentd.conf:/fluentd/etc/fluentd.conf -e FLUENTD_CONF=fluentd.conf fluent/fluentd:latest
docker run -d -p 9080:8080 -p 443:8081 --name gw-01 --env-file env.ggz.conf --log-driver=fluentd --log-opt fluentd-address=localhost:24224 mcr.microsoft.com/azure-api-management/gateway:latest
```