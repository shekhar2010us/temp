## Monitoring with Docker

[Google cAdvisor Monitoring](https://hub.docker.com/r/google/cadvisor)


```docker
sudo docker run --volume=/:/rootfs:ro --volume=/var/run:/var/run:rw --volume=/sys:/sys:ro --volume=/var/lib/docker/:/var/lib/docker:ro --publish=8080:8080 --detach=true --name=cadvisor1 google/cadvisor:latest
```

Head over to `http://<aws_public_ip>:8080` and your cAdvisor monitoring should be live.
