# Kubernetes

kubectl: stand for Kubernetes Control

Kubernetes Cluster: A set of nodes + a master to manage them

Node: a virtual machine that could run several docker containers

Pod: wraps up a container or multiple containers

Deployment: Monitor a set of pods, make sure they are running and restarts them if they crash

Service: manage networks. Provide an easy-to-remember URL to access a running container

A kubernetes Config file:

 - tells Kubernetes about the different Deployments, Pods, and Services (referred to as "Objects") that we want to create
 - Written in YAML syntax
 - always store these files with the project source code. They are the documentation!
 - indentation: 2 spaces

example config file: `posts.yaml`

	apiVersion: v1     # https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-apiversion-definition-guide.html
	kind: Pod          # we are creating a pod
	metadata:          # data that helps identify the object (in this case, the pod)
	  name: posts      # the name of the pod is posts
	spec:              # the attributes that will be applied to the object
	  containers:
	    - name: posts  # inside it is a container named posts
	      image: zixuanzhao/posts:0.0.1  # the container is created using this image
                                        # if we don't specify the version of image, kubernetes will pull the latest image from dockerhub 

run it using `kubectl apply -f posts.yaml`

	NAME READY STATUS RESTARTS AGE
	      1/1

READY: 1/1 there's one copy of the pod trying to be executed, and one copy successfully running

### Commands

 - `kubectl get pods`: see all the pods
 - `kubectl exec -it [pod_name] [cmd]` execute the command in a running pod. If there are multiple containers in the pod, it will prompt you to choose inside which container you want to run the command
 - `kubectl logs [pod_name]` print out all the logs of a pod
 - `kubectl delete pod [pod_name]` delete the pod
 - `kubectl describe pod [pod_name]` print out information about the running pod

### Deployment

 - manages the pods
 - if you want to update the version of the docker images running inside the pods, deployment will create the new pods, manage the new ones, and destroy the old ones
 - example config file `posts-depl.yaml`

		apiVersion: apps/v1
		kind: Deployment
		metadata:
		  name: posts-depl
		spec:
		  replicas: 1              # number of pods
		  selector:                # tell kubernetes the info about the pods that we want it to manage (how to find the pods)
		    matchLabels:           # the pods will have labels described by the following line
		      app: posts           # This can be done randomly
		  template:                # config info about the pod
		    metadata:
		      labels:
		        app: posts
		    spec:
		      containers:
		        - name: posts
		          image: zixuanzhao/posts:0.0.1

 - commands:
   - `kubectl apply -f posts-depl.yaml` create the deployment
   - `kubectl get deployments`
   - `kubectl describe deployment [depl-name]` 
   - `kubectl delete deployment [depl-name]` all the associated pods will be deleted as well
 - update the image used by the deployment
   - the image used in the depl config file must use the latest tag
   - update the code
   - build the image
   - push the image to docker hub
   - run `kubectl rollout restart deployment [depl-name]`

### Service (networking between pods)

 - types of services
   - Cluster IP: for communication between the pods in our cluster
   - Node port: make a pod accessible from outside the cluster (usually only used for development purposes)
   - Load Balancer: make a pod accessible from outside the cluster (the right way)
   - External Name
 - example config file for Node port service `posts-srv.yaml`

		apiVersion: v1
		kind: Service
		metadata:
		  name: posts-srv
		spec:
		  type: NodePort
		  selector:
		    app: posts
		  ports: 
		    - name: posts                   # doesn't matter
		      protocol: TCP
		      port: 4000                    # port of the node port service
		      targetPort: 4000              # the port that we are eventually directing the traffic to
 - `kubectl get services`
 - `kubectl describe service [srv-name]`
 - nodePort (randomly assigned by kubernetes): to access the service from outside the cluster

#### ClusterIP

 - clusterIP yaml file (putting the deployment and the service together)
 
		apiVersion: apps/v1
		kind: Deployment
		metadata:
		  name: posts-depl
		spec:
		  replicas: 1              # number of pods
		  selector:                # tell kubernetes the info about the pods that we want it to manage
		    matchLabels:           # the pods will have labels described by the following line
		      app: posts           # This can be done randomly
		  template:                # config info about the pod
		    metadata:
		      labels:
		        app: posts
		    spec:
		      containers:
		        - name: posts
		          image: zixuanzhao/posts:0.0.1
		---
		apiVersion: v1
		kind: Service
		metadata:
		  name: posts-srv
		spec:
		  selector:                # direct incoming traffic to the pod with lable app: posts
		    app: posts  
		  type: ClusterIP          # Even if we don't specify this, it will default to ClusterIP service
		  ports:
		    - name: posts
		      protocol: TCP
		      port: 4000
		      targetPort: 4000
 - once you set up cluster IP services for each pod, the container inside the pod can access another container using the service names

k8s is short for kubernetes

#### Load Balancer Service

 - two things: 
   - load balancer: Tells Kubernetes to reach out to its provider (AWS, Azure, Google Cloud) and provision a load balancer. Gets traffic into a single pod.
   - Ingress or Ingress Controller: A pod with a set of routing rules to distributed traffic to other services.
 - ingress-nginx
 - `ingress-srv.yaml`

        apiVersion: networking.k8s.io/v1beta1
        kind: Ingress
        metadata:
          name: ingress-srv
          annotations:
            kubernetes.io/ingress.class: nginx
            nginx.ingress.kubernetes.io/use-regex: 'true'
        spec:
          rules:
            - host: posts.com
              http:
                paths:
                  - path: /posts
                    backend:
                      serviceName: posts-clusterip-srv
                      servicePort: 4000
                  - path: ... /?(.*)
                    ...

#### SKaffold

 - `skaffold.yaml`

        apiVersion: skaffold/v2alpha3
        kind: Config
        deploy:
          kubectl:
            manifests:
              - ./infra/k8s/*
        build:
          local:
            push: false
          artifacts:
            - image: zixuanzhao/client         
              context: client                   # the folder
              docker:
                dockerfile: Dockerfile
              sync:
                manual:
                  - src: 'src/**/*.js'          # if it matches (is a javascript file), when there's changes, throw it into the pod, otherwise create new docker images
                    dest: .
           - image: ...
             ...

 - `skaffold dev`
                    
#### Secrets

 - `kubectl get secrets`
 - `kubectl delete secret secret-name`
 - `kubectl create secret generic jwt-secret --from-literal=JWK_KEY=asdf`