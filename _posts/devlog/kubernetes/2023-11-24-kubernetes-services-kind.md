---
layout: post
title: "Kubernetes Service Kinds"
subtitle: "Kubernetes Service Kinds"
category: devlog
tags: blog kubernetes kubectl tips
---

* this unordered seed list will be replaced by the toc
{:toc}

## Kubernetes Service Kinds

![alt text](https://spaceliftio.wpcomstaging.com/wp-content/uploads/2022/10/124.kubernetes-view-pod-logs.png "Kubernetes Service")


## Introduction
A Kubernetes service associates a set of pods with an abstract service name and persistent IP address. This enables pods to discover each other and route requests to each other. A service uses labels and selectors to match pods with other applications. For example, a service might connect the front end of an application to a back end, each running in a separate Deployment within the cluster.

## ClusterIP
**ClusterIP** is the default service type in Kubernetes. It receives a cluster-internal IP address, making its pods only accessible from within the cluster. If necessary, you can set a specific clusterIP in the service manifest, but it must be within the cluster IP range.

## NodePort
A **NodePort** service builds on top of the ClusterIP service, exposing it to a port accessible from outside the cluster. If you do not specify a port number, Kubernetes automatically chooses a free port. The kube-proxy component on each node is responsible for listening on the node’s external ports and forwarding client traffic from the NodePort to the ClusterIP.

## LoadBalancer
A **LoadBalancer** service is based on the NodePort service, and adds the ability to configure external load balancers in public and private clouds. It exposes services running within the cluster by forwarding network traffic to cluster nodes.

The **LoadBalancer** service type lets you dynamically implement external load balancers. This typically requires an integration running inside the Kubernetes cluster, which performs a watch on LoadBalancer services.

## ExternalName
An **ExternalName** service maps the service to a DNS name instead of a selector. You define the name using the spec:externalName parameter. It returns a CNAME record matching the contents of the externalName field (for example, my.service.domain.com), without using a proxy.

## Debugging
The following **debugging procedure** will help you identify which part of the service communication chain is broken.

1 -  Check if the service exists:

```
kubectl get svc <service-name>
```

2 - Try to access the service via DNS name in the same namespace:

```
nslookup <service-name>
```

3 - Try to access the service via DNS name in another namespace:

```
nslookup <service-name>.<namespace>
```

If this succeeds, it means you need to change the client application to access the service in another namespace, or run it in the same namespace as the service.

4 - Check if DNS works in the cluster:

```
nslookup kubernetes.default
```

Ref: https://kubernetes.io/docs/home/
