**[https://www.youtube.com/watch?v=X48VuDVv0do&list=LL&index=2&t=144s](https://www.youtube.com/watch?v=X48VuDVv0do&list=LL&index=2&t=144s)

  

Kubernetes

  

Is a open source container orchestrations tool. Basically manages containerized(Docker or others) applications in different deployment environments: physical, virtual, cloud.

  

Advantages:

- High availability or no downtime
- Scalability or high performance
- Disaster recovery, backup and restore

  

Main Components:

- Pod: Smallest Unit of K8s; Abstraction over container, like this you don’t directly deal with the container, just with the kubernetes layer; Usually one application per pod. 
    

How the pods communicate on kubernetes? K8s offers a virtual network that gives each pod an internal IP. But pods are very ephemeral, they easily die and when a new one is created to replace it, it will receive a new IP address.

![](https://lh4.googleusercontent.com/foUeTIioG9j0aEWeK6Zpd38SVJ1TylvO56v_dBo20NdjIBkuZrCrbQehsy_GadldEANtPKyIvpojAtD6QfkR-rx_WaYlSwMj9bOx-5mp3OEF_txWrEg-IAnSuT3idS5epmxm_zVyhwy3Bw2Ns75W)

- Service and Ingress: A service is a permanent IP Address that can be attached to each pod. The lifecycle of a pod and service are not related, so even if the pod dies, the service IP will stay. You use services to do the communication between pods.
    

To make your application accessible from the browser, you need an external service. But external url using the IP of nodes are not friendly, you normally want to use a domain name and to do that you use ingress. With Ingress you can have a secure and beautiful URL that will forward the access to the service.

  

![](https://lh3.googleusercontent.com/rXr_giFPc89S-8Lnrw3VAdhGkML-JIMMrDbFYtNjbvJqSDjCk29skhLb9Mcs2RcNnmyAFp4DYzfhDR9eLMUwTFfA-GUPhGenS1nugK4hRqtbkONF6phhdaLHa9JRCeYpJWrGTM7c4fxNpAPXFaXa)

  

- Config Map and Secret: Let’s say you want to use a database, for this you use a service to connect with the database and the database URL are put in the built application. But if you change, per example, the name of the database, you would have to rebuild the image, push to a repository, pull it in your pod and restart the whole thing. To avoid this type of situations, kubernetes has a component called Config Map that contains the external configuration of your application. Secret is just like config Map, but used to store sensitive data like credentials and uses base64
    

![](https://lh5.googleusercontent.com/grmoqCnzyJIDShZETYIf-MKGytgobMOdAJx2_Pn_LB3NxWxaUTkUGMpSX28l3_IHDPMIKWnPW3xKl8qEXDOxLtiQQGOUTOH9_nMUma4GVeufKJ7vf2zdxQCGf9hS-EA05vnNVnDC8OS3A7ScvsHX) 

- Volumes: Let’s say you have a database in one pod and for some reason the pod dies, you would lose all the data. To solve this, you can use volumes, that attach a storage to your pod that can be local(on the same server node that the pod is running) or it could be on a remote storage that is outside the kubernetes cluster (could be a cloud storage, your storage, etc). Think of the storage as a hard drive plugged into the k8s cluster because the kubernetes doesn’t deal with any data persistence.
    
- Deployment and stateful set: What happens if there are user accessing my application and the pod dies? Or you need to restart the pod? You would have a downtime where the user could not access the application. To avoid this, we make replicas on other nodes that are also connected to the service. but you don’t have to do this by hand. You just make a blueprint and say how many replicas you want to be made. This blueprint is called Deployment. Like this you can easily scale up or scale down your application and if one of you pods die, the system will redirect your user to a replica.
    

But you can replicate via Deployment the database because the database have states and you would have to deal with data inconsistencies. To do this, you use another component called stateful set. But, deploying database applications using stateful set is not easy. It’s a common practice to host the database application outside the kubernetes cluster

  

![](https://lh4.googleusercontent.com/FAMpCWkqMDD-0fUdL_trqmHTr9wl4i2FwrZMQE3BuJQMkd4flo6putOTAVxP4oIVrknyY8pkX0anFrsggOOfrZz6FpkMSgfurMc3jQMfWz0WagyHFjLf0ePNKsaG5arBWvsNvaQ7YcdzNGmyZ3Uo)

  

Basic Kubernetes Architecture

  

Kubernetes has two types of nodes: master and slave(or worker). This will explain how kubernetes is automated and how the cluster is self managed, etc.

We already know that a node can have multiple pods running inside, for this to work is necessary that each have installed three processes that will schedule and manage those pods.

- Container runtime: Because a node has containers running inside it, it needs the container runtime.
    
- Kubelet: Is the processes that actualy schedule the nodes. Kubeletes interacts with the node and the container. Kubelet is responsible for starting the pod with the container inside.
    

You can have multiple worker nodes with the same pods and those processes and the way those nodes communicate is through a service that acts like load balacer(a user tries to access and is redirected to the node less busy). 

- Kube proxy: The process that is responsible for forwarding services to pods. This process is smart and directs the comunications of one pod to other that is the same node, avoiding the overhed os sending the request to another node(machine)  
    

![](https://lh4.googleusercontent.com/5UKMQm6m48hQFjhRG_07U543gPLUcBg0eO7PGQlRTwFgQAidcXU-QAhzvzBnNhogBQpg5gxEgv1KXrD3OxK5czjbMhrFUiOocS35PV0xrbrc90aTyFRyRQpGeANZg9bF_jaonl2Hys8ZPe4SIyQD)

Now, the question that arises is how you interact with those worker nodes? How to schedule a pod, how monitor to see if they die, how to add a new pod or restart one? All of those managing processes are done by a master node. There are four processes that run on master nodes

- Api server: When the dev wants to deal with the application, it deals with the api-server through some ui. Is the cluster gateway that receive updates, requests, etc. Also acts like a authentication gatekeeper
    

![](https://lh4.googleusercontent.com/2v7R7950UUXzR2aO9I05Q5vlJGatFMDGfS5VSEHn4W_8QytRtEWaBKxtBAhwSxCyBS4RQBZFA8TCoA4uYRCgRzN7gir4KBn0lBxM1q6SyznhdPIcdNZkOfsEWgraqAnMFn7ax7NQhkNpDvutt2_w) 

- Scheduler: If you send a request to schedule a new pod, it will fal on the api server and foward to the scheduler. Bur the scheduler has a smart way of deciding in which node to run the pod base on how much resources the pod you are trying to run will need and how much each worker node is being used. Is godd to make clear that the scheduler just decide in which node the pod will run, who executes is kubelet 
    

![](https://lh3.googleusercontent.com/Ve13AQ7bXbqK2hxBen54XTbjDhFjq5iQSydO7LcoxVfOf4aF8CUx4yhanJELWGWNcw5frJDukMmJZc3yC5SsZ2SesbRYjHfzXdW1FDGwPdf6Z6_MfF1lGRYq66byiCCZGygMoJljRidTpT3i5TxK)

- Controller manager:Detects state changes like a pod dying and tries to reestore the state the fastest posible. Does this by sending a resquest to the scheduler
    

![](https://lh6.googleusercontent.com/VEVLGlOBs-ryHhRsQMGr4y4iSxFnESEhHltZ9fhDesLdaEfz5VwXjB7Skp6i1iTE9h7v9F4lEYU19M2ltAXrBsQEzo6oiQbzUqL12hTWx-XSEKccrsNvg7U50yMfcppENHHihM956OBPGZQyMm5U)

- etcd: key value store that stores or update the state of every pod and this data is used by the other master processes
    

![](https://lh6.googleusercontent.com/qcWFF5RIdhO9GHZmFp6O-GFvdmHxOF08iEC07RKmwhaghAltgC91bppFn04sljBAVoOzT50FvN3AvyhJgRlujDpUWt-x9JF5xEWs7qyGa9cuqcu8TWNuwASYGZR4CMmUmeZmuaoNoEN73xhaKRLk)

In a real application, you will have more than one master node so that is more secure and can deal with bigger traffic. The api server has a lod balancer and the ectd has a distribuited storage across all masters

![](https://lh6.googleusercontent.com/PtM3dF41c5dPtiO-n9ZA3fSZkkA36iBnGpyFSu8Vz46Ex9jdAQPtFukH6J3bA9lklCH7jnQ5m8guPxKSdRgpCZ9Zh0iGcvK5YIPS7IbFSGKE9lnERidAkQN6Ptzyxcrjg4kguE2vRHm2dd8rAlkR)

  

Namespaces

  

Are a form of organizing your pods inside the cluster. Is a good practice to give you a easy overview of the project an good when working on teams because avoids one group interfering with what the other is doing. Another use of namespaces is that you can set a staging and a development enviroment in the same cluster  

![](https://lh6.googleusercontent.com/e_dtXD0dY3MD5bje49zPo6HCoK9UEX7PlMb61G0-R4rAFE7-yTWh2USyqa4EiuP3SfZXn7XCTGp6tsAS605KLGOT6kAVSxRWLzA24X73iBpya4y18W7YeAwkYP8GTABAO0hHYyyO-CpBL5rMm72C)

![](https://lh4.googleusercontent.com/jHIRW-yMftXRGAkw4oZvkud_mw5Lnu7z72fBOVfJcZ5jIUoAoDXCB09p7A7r_A4mGKcz3hT_8M8YA7ebppdzoqpgtcnriFQpPcX9VgGnjy0jQHzX6ikQMzkzodojttdFCiYesQqtwQfxkTaULXlZ)

![](https://lh4.googleusercontent.com/jHIRW-yMftXRGAkw4oZvkud_mw5Lnu7z72fBOVfJcZ5jIUoAoDXCB09p7A7r_A4mGKcz3hT_8M8YA7ebppdzoqpgtcnriFQpPcX9VgGnjy0jQHzX6ikQMzkzodojttdFCiYesQqtwQfxkTaULXlZ)**