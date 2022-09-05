# Working with Docker Toolbox: Notesheet

## Test local installation

```shell
docker-machine --version
docker --version
docker run --rm hello-world
docker image prune -a
```

## [Containerize an application](https://docs.docker.com/engine/docker-overview/)

```shell
(vim Dockerfile)
docker build -t <tagname>
docker image ls
```

## Publish a container

```shell
docker-machine status
docker run --publish <host_port:cont_port> --detach --name <alias> <image:tag?>
docker container ls
curl $(docker-machine ip):<host_port>
docker rm --force <alias>
```

## Register an image

```shell
docker login
docker tag <image:tag?> <uname/repo:tag?>
docker push <user>/<image:tag?>
```

## [Clean up unused objects](https://docs.docker.com/config/pruning/)

```shell
docker image ls
docker container ls --all
docker volume ls
docker image prune -a <filter?>
docker container prune <filter?>
docker volume prune <filter?>
```

## [Add shared folders](https://web.archive.org/web/20190322045136/https://docs.docker.com/toolbox/toolbox_install_windows/#optional-add-shared-directories)

```shell
docker-machine ssh
sudo vi /mnt/sda1/var/lib/boot2docker/profile

# Add shared folder to docker machine in VirtualBox settings
# FOLDER_NAME must match the assigned name for the above
mkdir /home/docker/<FOLDER_NAME>
sudo mount -t vboxsf -o uid=1000,gid=1000 <FOLDER_NAME> /home/docker/<FOLDER_NAME>
# type :wq to save and quit vi
exit

docker-machine stop
docker-machine start
```

---

## [Orchestrate with Kubernetes](https://kubernetes.io/docs/concepts/)

### Set up local cluster

```shell
minikube status
(minikube delete)
minikube start
```

### Compose YAML file & deploy

```shell
(vim compose.yaml)
kubectl apply -f <compose_file>
curl $(minikube ip):<host_port>
```

### Troubleshooting

```shell
kubectl get pods
kubectl get deployments
kubectl get services
kubectl logs <pod>
kubectl describe pods <pod?>
```

### Tear down resources

```shell
kubectl delete -f <compose_file>
```

---

## [Orchestrate with Docker Swarm](https://docs.docker.com/engine/swarm/)

### Set up local swarm

```shell
docker system info | grep -i swarm
docker swarm init
```

### Compose stackfile & deploy

```shell
(vim stackfile.yaml)
docker stack deploy -c <stack_file> <stack_prefix>
curl $(docker-machine ip):<host_port>
```

### Troubleshooting

```shell
docker stack ls
docker service ls
```

### Tear down resources

```shell
docker stack rm <stack_prefix>
```

---
