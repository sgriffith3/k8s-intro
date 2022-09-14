# Lesson 01: A Kind Start

**K**ubernetes **in** **D**ocker ([kind(https://kind.sigs.k8s.io/)) is a very useful tool for getting started learning kubernetes. It installs quickly, starts easily, and provides a very lightweight dev environment.

## PreReqs
Make sure you have golang (1.17+) installed. [Go Installation Documentation](https://go.dev/doc/install)

## 

1. Install Kind

    `go install sigs.k8s.io/kind@v0.15.0`

2. Create a Kubernetes Cluster (Single Node)

    `kind create cluster`

    ℹ️ If "kind" is not found, make sure your PATH is set correctly (I had to add ~/go/bin)
    
    ℹ️ If you are getting a permission denied error for docker

    https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket
    
    > Also, instead of logging out, or using `su - ${USER}`, you can just do `newgrp docker`

3. Once that cluster has been created successfully, it is time to learn some Kubernetes commands. Try each of these out:

|Command|Description|
|---|---|
|`kubectl get nodes`|ist the cluster nodes|
|`kubectl get pods`|list pods in the current namespace|
|`kubectl get pods -A`|list pods in all namespaces|
|`kubectl get ns`|list all namespaces|
|`kubectl describe ns defualt`|inspect the namespace called "default"|

4. Make and Access a Pod.

    1. Create a pod using the container image nginx.

        `kubectl run ng --image nginx`
        
    0. Take a somewhat deeper look at the pod.

        `kubectl get pods ng -o wide`
        
        > Note the pod IP address. We will need it for step 5.ii

    0. Temporarily expose the container's port 80.

        `kubectl port-forward ng 1111:80`
        
    0. In another terminal, curl your locally exposed port. This could also be viewed in a browser.

        `curl 127.0.0.1:1111`
        
    > <kbd>Ctrl</kbd> <kbd>c</kbd> to stop port forwarding.

5. Access your node

    1. Use docker to enter a bash session of your node.

        `docker exec -it kind-control-plane bash`
        
    0. Check out the routes set in this node.

        `ip route`
        
        > Note that one of these routes should have the IP address of your pod listed. See step  4.ii


## Summary
**Congrats!** You have just:
- Created a Kubernetes Cluster
- Inspected existing resources
- Created a new Pod
- Temporarily exposed and accessed the container within the Pod
- Learned more about a kubernetes node




