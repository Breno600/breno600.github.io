---
layout: post
title: "Kubectl Tips Commands"
subtitle: "Kubectl Tips Commands"
category: devlog
tags: blog kubernetes kubectl tips
related_posts:
  - _posts/devlog/kubernetes/2023-11-24-kubernetes-services-kind.md
---

* this unordered seed list will be replaced by the toc
{:toc}

## Kubectl Tips Commands

In this blog you have tips to easy your life with o command kubectl and manager your cluster kubernetes with more effectiveness

## 1 - Alias

Some alias <br>

```bash
alias k='kubectl' // Use example: k get pods
alias kdp='kubectl describe pod' // Use example: kdp nginx
alias kf='kubectl create -f' // Use example: kf deployment.yaml
alias kgn='kubectl get namespaces' // Use example: kgn
alias kga='k get pod --all-namespaces' // Use example: kga
```

## 2 - Set default namespace (with alias)

When you are working or debugging an application and need to pass the namespace parameter all the time :/

```bash
alias dn='kubectl config set-context $(kubectl config current-context)'# use example dn --namespace=mynamespace
```

## 3 - Create YAML from kubectl commands

With this command you can create yamls kubernetes for example (Deployment, Pods, Service, jobs and etc). Is a manner very easy to you have your yamls and you can use in a DevOps pipeline.

```bash
kubectl run busybox --image=busybox --dry-run=client -o yaml --restart=Never > yamlfile.yaml## JOB
kubectl create job my-job --dry-run=client -o yaml --image=busybox -- date  > yamlfile.yaml## DEPLOYMENT
kubectl create deployment --image nginx my-deployment --dry-run=client -o yaml > nginx-deployment.yaml## SERVICE
kubectl create service clusterip nginx-service --tcp=80:8080 --dry-run=client -o yaml > nginx-service.yaml
```

## 4 - Viewing resource utilization
With the command **kubectl top RESOURCE** you can see the utilization of memory and cpu.

```bash
# Nodes resources
kubectl top node

# Pods resources
kubectl top pod
```

Certainly, nothing is created, everything is transformed :)

Ref: https://kubernetes.io/docs/home/

Read more [Kubernetes Service Kind](kubernetes-services-kind){:.heading.flip-title}
{:.read-more}