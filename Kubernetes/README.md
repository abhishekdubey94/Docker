# KUBERNETES
* Cluster in kubernetes is assembly of master and one or more nodes.
* A node is virtual machine or a physical computer that is used to run some number of different containers.
* Nodes are managed by the master.
* We interact with master to control the kubernetes cluster.
* Minikube is command line tool to set/create small cluster in the development environment.
* kubectl is the command that is used to manage and interact with the containers in the nodes.
* If using kubernetes from docker-desktop, minikube commands is not reuqired.
* The images should already exist in order to use in Kubernetes.
* In Kubernetes, we have multiple config files each representing an object that we want to create.
* Configuration file defines 'kind' which can refer to Service,Pod,ReplicaContoller,StatefulSet.
* Objects are the things that will created inside the kubernetes cluster to get the application work.
* Pod is used to run multiple container inside it, while service is used to setup a kind of network.
* A Pod is used to run containers which must run together to run the application.
* The apiVersion defines a different set of 'objects' we can use.
* When we start minikube, it runs a virtual machine called Node. This Node will be used by the kubernetes to run different kind of objects
* In kubernetes we cannot create a single container running. It has to be associated with Node and objects.