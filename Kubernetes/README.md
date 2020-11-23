# KUBERNETES
* It is a system for running different containers over multiple different machines.
* It is useful when we need to run many different containers with different images.
* Cluster in kubernetes is assembly of master and one or more nodes.
* A node is virtual machine or a physical computer that is used to run some number of different containers.
* Nodes are managed by the master.
* A master is node i.e. a machine or vm with a set of programs to manage nodes.
* We interact with master to control the kubernetes cluster.
* Minikube is command line tool to set/create small cluster in the development environment.
* kubectl is the command that is used to manage and interact with the containers in the nodes.
* If using kubernetes from docker-desktop, minikube commands is not required.
* The images should already exist in order to use in Kubernetes. Kubernetes does not build the image.
* In Kubernetes, we have multiple config files each representing an object that we want to create.
* Configuration file defines 'kind' of object we are creating which can refer to Service,Pod,ReplicaContoller,StatefulSet.
* Objects are the things that will created inside the kubernetes cluster to get the application work.
* Pod is used to run multiple container inside it, while service is used to setup a kind of network.
* A Pod is used to run containers which must run together(tightly coupled) to run the other container in the pod or application.
* The apiVersion defines scopes or types of objects we can use.
* When we start minikube, it runs a virtual machine called Node. This Node will be used by the kubernetes to run different kind of objects
* In kubernetes we cannot create a single container running. It has to be associated with Node and objects.
* The object service is used to do networking tasks.
* A service can have subtype i.e. ClusterIP, NodePort, LoadBalancer, Ingres. Every subtype serves a different purpose.
* NodePort is specifically used for opening up ports of the container to outside world.
* The service finds the running pod through "selector" parameter in service config file. It should match the label in pod config file.
* In NodePort Service, we have 3 kinds of port.
    * port - It is used when a Pod inside the node wants to communicate other Pod.
    * targetPort - It is the port that is exposed by the container which we are targetting.
    * nodePort - It is the port that is visible to the outside world.
* For Docker Desktop, the ip will be localhost while for minikube it will be different. Get it using command "minikube ip"
* The master continuously checks if the required number of containers are running. If not then it instantly runs the container.
* Two ways to give deployment commands to the master node
    * Imperative Deployments - Do exactly these steps to arrive at this container setup.
    * Declarative Deployments - Our container setup should look like this, let master node handle it.
* Master checks the object name and kind to determine which pod it has to update.
* Only the image can be changed while updating the Pod config. (not the ports, name, containers)
* To solve above issue, we have one more kind of objects i.e. Deployment.
* Deployment object maintains a set of identical pods, ensuring that they have the correct config and that the right number exists
* Every single pod that is created is assigned its own IP which is internal to the virtual machine /node and can change when we create new Pod. That is why service is used to connect to the pod.
* When an image is updated, there is no way that deployment object can get the change.
    * Delete the pods and deploy the config
    * Use version with the image name and change it when image is change
    * Build the image with version and then update
* In services, the ClusterIP object allows any other object in the cluster to access object pointed by ClusterIP. 
* Unlike NodePort, ClusterIP does not allow outside world to interact with the object.
### Commands
* kubectl cluster-info - Gives information about the cluster
* kubectl apply -f &lt;config file&gt; - To load the config files or objects in the cluster.
* kubectl get &lt;object kind&gt; - print the status of all the running objects.
* kubectl describe &lt;object type&gt; &lt;object name&gt; - To get the detailed info about an object
* kubectl delete -f &lt;config file&gt; - to delete the object
* kubectl set image &lt;object_type&gt;/&lt;object_name&gt; &lt;container_name&gt; = &lt;new image to use&gt; - To update the image deployed