# Jenkins

## Docker
```
$ docker volume create jenkins-data

$ docker run -d --name jenkins -p 8080:8080 -p 50000:50000 -v jenkins-data:/var/jenkins_home -e JAVA_OPTS=-Djava.util.logging.config.file=/var/jenkins_home/log.properties jenkins/jenkins:2.60.3-alpine
```

## Kubernetes

### Namespace
```
$ kubectl create ns jenkins
```

### Volumes
```
$ kubectl apply -n jenkins -f jenkins-local-volume.yaml
```

### Deployment
```
$ kubectl apply -n jenkins -f jenkins-deployment.yaml
```

```
$ kubectl -n jenkins get pods
```

### Getting the Jenkins password
```
$ kubectl -n jenkins logs <jenkins-pod-name>
```

#### Kubernetes Port Forward
```
$ kubectl -n jenkins port-forward <jenkins-pod-name> 8080
```

#### Config Kubernetes
Go to Manage Jenkins -> Manage Plugins -> Available, search for "Kubernetes", install the plugin and restart Jenkins.
Go to Manage Jenkins -> Manage Nodes and Clouds -> Config Clouds -> Add a new cloud.