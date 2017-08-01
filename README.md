### [S2I](https://github.com/openshift/source-to-image) builder image for [Blue Jay](https://blue-jay.github.io/)
```
$ make build VERSION=1.8
```

Push to hub.docker.com
```
$ export DOCKER_ID_USER="username"
$ docker tag openshift/blueprint-go-18-centos7 docker.io/username/blueprint-go-18-centos7
$ docker push docker.io/username/blueprint-go-18-centos7
```

### Credit
Forked from https://github.com/openshift-s2i/s2i-go
