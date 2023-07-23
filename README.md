# Installation ([official doc](https://www.jenkins.io/doc/book/installing/docker/))
## On macOS and Linux
### Create the network 'jenkins'
```
docker network create jenkins
```

### Build the Jenkins BlueOcean Docker Image
```
docker build -t myjenkins-blueocean:2.401.1-1 .
```

### Run the Container
```
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.401.1-1
```