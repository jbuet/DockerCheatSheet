# DockerCheatSheet
https://github.com/wsargent/docker-cheat-sheet 

# Dockerfile
https://docs.docker.com/engine/reference/builder/

# Docker Compose
https://docs.docker.com/compose/compose-file/ 

# Docker Swarm
Puertos: https://www.bretfisher.com/docker-swarm-firewall-ports/ 
Backup:  https://success.docker.com/article/backup-restore-swarm-manager
Tshoot: https://github.com/project-sunbird/sunbird-devops/wiki/Docker-swarm-troubleshooting 

### Crear servicios y stack
docker service create: crear servicio

docker stack deploy -c docker-compose.yml *stack*


### obtener servicios y stacks
En un swarm, sólo se pueden ejecutar comandos en los nodos master. El nodo master Leader es el que finalmente ejecuta los comandos, es decir, si nos conectamos a un master que no es el leader y ejecutamos una consulta, ésta instrucción será redireccionada al nodo master **leader**.


docker stack ls: obtiene todos los stacks
docker stack services *servicio*: detalle de los servicios de un stack
docker service ps *servicio*: detalle de un servicio
docker service ls: obtiene todos los servicios que corren sobre el docker host/swarm



### Win10 Docker-machine 

 docker-machine create -d hyperv --hyperv-virtual-switch "name of vswitch" node-1
 docker-machine create -d hyperv --hyperv-virtual-switch "name of vswitch" node-2
 docker-machine create -d hyperv --hyperv-virtual-switch "name of vswitch" node-3

# Kubernetes

Cluster:
kubectl cluster-info dump 
kubectl cluster-info dump --all-namespaces --output-directory=*path*
versiones de api soportadas: kubectl api-versions 

Nodos:
kubectl get nodes 
kubectl get nodes -o yaml 


### Cambiar output
 agregar "-o *formato*
 * -o wide
 * -o json
 * -o yaml


Logs dentro del cluster:
* https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/#looking-at-logs

Eventos:
kubectl get events
kubectl get events -n *namespace*
kubectl get events --all-namespaces

Detalle de recursos:
* pods: kubectl describe pod *nombre de pod*
* nodos: kubectl describe node *nombre de nodo*

### K8 en Docker for Windows

Setear contexto K8:
kubectl config use-context docker-for-desktop

###### Deploy de dashboard:
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/aio/deploy/recommended/kubernetes-dashboard.yaml

kubectl proxy

Ingresar: http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/

Mas info: https://github.com/kubernetes/dashboard 

###### Login al Dashboard
Crear usuario rbac: https://github.com/kubernetes/dashboard/wiki/Creating-sample-user#create-service-account 

Token de autenticación:
kubectl -n kube-system describe secret ((kubectl -n kube-system get secret  | sls admin-user) -split "\s+")[0] 



### K8 on prem con kubeadm
https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/

* Instalar docker engine  https://get.docker.com/
* Instalar kubeadm https://kubernetes.io/docs/setup/independent/install-kubeadm/ 
* Abrir puertos necesarios master/node


Configurar kubectl en master (control-plane)
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

