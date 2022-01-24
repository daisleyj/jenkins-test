# Jenkins Test

## Run Jenkins in a container locally

```shell
docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts-jdk11
```

## Run Jenkins as a service on Docker Swarm

```shell
docker stack deploy jenkins-stack --compose-file docker-compose.yaml
```

