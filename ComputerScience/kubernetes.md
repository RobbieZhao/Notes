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
	spec:
	  containers:
	    - name: posts  # inside it is a container named pod
	      image: zixuanzhao/posts:0.0.1  # the container is created using this image

run it using `kubectl apply -f posts.yaml`

	NAME READY STATUS RESTARTS AGE
	      1/1

READY: 1/1 there's one copy of the pod trying to be executed, and one copy successfully running

see all the pods: `kubectl get pods`

k8s is short for kubernetes

