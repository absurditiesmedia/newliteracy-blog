---
title: Horizontal Scaling in Kubernetes
description: Horizontal scaling allows kubernetes to spin up instances as server load demands.
tags: ["kubernetes", "development", "devops", "system administration"]
publishDate: "8 May 2024" 
coverImage:
    src: "../../assets/kubernetes_logo.png"
    alt: "kubernetes logo"
---
Horizontal scaling in Kubernetes refers to dynamically adjusting the number of application instances (pods) based on workload changes to maintain optimal performance. Unlike vertical scaling, which increases resources per instance, horizontal scaling adds or removes instances.

## How Horizontal Scaling Works in Kubernetes

Kubernetes employs controllers like the Horizontal Pod Autoscaler (HPA) to manage horizontal scaling:

### 1. Horizontal Pod Autoscaler (HPA)

The HPA adjusts pod replicas based on observed metrics (e.g., CPU utilization):

### 2. Metrics Server

Kubernetes Metrics Server collects and aggregates resource usage data essential for scaling decisions.

### 3. Configuration

To enable horizontal scaling, define an HPA resource specifying metrics and thresholds.

## Steps to Implement Horizontal Scaling

Ensure Metrics Server is Running:

`kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml`

Create a deployment:

`deployment.yaml:`
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: webapp
  template:
    metadata:
      labels:
        app: webapp
    spec:
      containers:
      - name: webapp
        image: webapp:latest
        ports:
        - containerPort: 80
        resources:
          requests:
            cpu: 100m
          limits:
            cpu: 200m
```

Define an HPA Resource:

`hpa.yaml`
```
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: webapp-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: webapp
  minReplicas: 2
  maxReplicas: 10
  targetCPUUtilizationPercentage: 50
```

Apply the configuration:

In the terminal:
```
kubectl apply -f deployment.yaml
kubectl apply -f hpa.yaml
```

Suppose CPU utilization reaches 80%, HPA scales up to 4 pods; at 20%, it scales down to 2.


## Conclusion

Horizontal scaling in Kubernetes, managed by the Horizontal Pod Autoscaler, optimizes application performance by dynamically adjusting pod replicas based on workload demands.

[<< prev: What is Kubernetes?: Where and Why You Should Use It.](/posts/where-why-use-kubernetes/)