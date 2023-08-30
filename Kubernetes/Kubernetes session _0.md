# Kubernetes session #0:

Kubernetes is a popular orchestration tool that helps automate various diffferent deployment processes mainly the deployment of containerised applications.
Kubernetes offers many features two of which are health checking and horizantal scaling which intertwined provide a fully automated deployment of clusters that are self-healing and auto-scaling with the right configuration.

## Architecture:
Kubernetes clusters follow the Master-Worker architectural pattern. Where primary nodes control worker nodes, where each type of node has a well defined set of responsabilities.
### 1. Worker nodes responsabilities:
Worker nodes contain a containerized runtime, allowing them to create what we call pods, which in turn contain the containers hosting the various applications.
A worker node can have multiple pods running on it, relative to its computing capabilities.
The worker nodes also need to have components allowing for network access for example, such components can be <b>kubelet, kube-proxy, and the container runtime</b>
### 2. Primary/Head nodes responsabilities: 
Primary nodes are the overseer of the whole unloading of containers (apps) onto pods, it has the responsabilities of storing information about different nodes, planning which container goes where, and so on. For this it uses many control plane components such as ETCD, Kube-scheduler, Kube-apiserver, kube-controller-manager, cloud-controller-manager and others </b>
### Conclusion: 
In short</b>, the architecture of a kubernetes cluster is Master-Worker, where the Master is the control plane, containing Primary nodes who uses many built-in components to fulfill their responsabilities, and the Worker being the many worker nodes responsible for loading applications (containers) into pods. Using many components each being responsible for a certain task.

## Components in-depth:
In this section we are going to be looking over what each of the components in the various nodes's roles are.

### 1. Worker node components:
- **kubelet:**
An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
The kubelet takes a set of PodSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy.
The kubelet doesn't manage containers which were not created by Kubernetes.
- **kube-proxy:**
kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.
kube-proxy maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.
kube-proxy uses the operating system packet filtering layer if there is one and it's available. Otherwise, kube-proxy forwards the traffic itself.
- **Container runtime:**
The container runtime is the software that is responsible for running containers.
Kubernetes supports container runtimes such as containerd, CRI-O, and any other implementation of the Kubernetes CRI (Container Runtime Interface).

### 2. Primary node 
 - **kube-apiserver:**
The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.
The main implementation of a Kubernetes API server is kube-apiserver. kube-apiserver is designed to scale horizontally—that is, it scales by deploying more instances. You can run several instances of kube-apiserver and balance traffic between those instances.
- **etcd:**
Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.
If your Kubernetes cluster uses etcd as its backing store, make sure you have a back up plan for the data.
You can find in-depth information about etcd in the official documentation.

- **kube-scheduler:**
Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.
Factors taken into account for scheduling decisions include: individual and collective resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and deadlines.
- **kube-controller-manager:**
Control plane component that runs controller processes.
Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process.
There are many different types of controllers. Some examples of them are:
	- Node controller: Responsible for noticing and responding when nodes go down.
	- Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
    - EndpointSlice controller: Populates EndpointSlice objects (to provide a link between Services and Pods).
    - ServiceAccount controller: Create default ServiceAccounts for new namespaces.

- **cloud-controller-manager:**
A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.
The cloud-controller-manager only runs controllers that are specific to your cloud provider. If you are running Kubernetes on your own premises, or in a learning environment inside your own PC, the cluster does not have a cloud controller manager.
As with the kube-controller-manager, the cloud-controller-manager combines several logically independent control loops into a single binary that you run as a single process. You can scale horizontally (run more than one copy) to improve performance or to help tolerate failures.
The following controllers can have cloud provider dependencies:
	- Node controller: For checking the cloud provider to determine if a node has been deleted in the cloud after it stops responding
    - Route controller: For setting up routes in the underlying cloud infrastructure
    - Service controller: For creating, updating and deleting cloud provider load balancers

![368b0e5221bea6ab8976cc191a42d5f6.png](../_resources/368b0e5221bea6ab8976cc191a42d5f6.png)