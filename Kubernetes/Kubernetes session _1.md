# Kubernetes session #1

## Review  points:
- Pods is the smallet unit in K8s, what we create are deployments which are an abstraction over pods.

## Lesson notes:

### Deployment: 
 - To create a deployment using kubectl, we run the following command :
`kubectl create deployment NAME --image=image [options]`
- To see status and general info about deployments : 
`kubectl get deployment`
> When I create a deployment, what I'm realistically creating is the blueprint for a pod, it has the most basic configuration for deployment, the only customized conf is its name and image, and the rest is default. 