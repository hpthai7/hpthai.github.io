# Kubernetes Cheat Sheet


## What is Kubernetes

Kubernetes is a sophisticated tool for the orchestration of containers in mass deployment. It provides an effective ways
to define the software components, resources and deploy them in a controllable and effective manner. The strongest points
of Kubernetes is:

- The abstraction of infrastructure layer to deployment layer. This allows developers and administrators concentrate on
the development stage and less worry about the management of the underlying hardware settings.

- The ability to maintain the accessibility to services

# Tips

## Install microk8s to have an all-on-one environment for development

## Use [kubens and kubectx](https://github.com/ahmetb/kubectx) to switch between clusters and namespaces in kubectl

## Troubleshooting

Normally, a k8s basic production-ready deployment features three main resources: ingresses, deployments and services. Further deployment schemes can include other resources such as daemonsets, jobs, storages... Due to the complexity of Kubernetes, it's not always simple to find out the problems or errors during the deployment process.

Some debugging procedures are to the rescue:

- [Kubernetes troubleshooting official guideline](https://kubernetes.io/docs/tasks/debug-application-cluster/troubleshooting/).
This is the comprehensive instructions provided by Kubernetes itself.

- [Visual diagram](https://learnk8s.io/troubleshooting-deployments). This efficient diagram was created by the team at learnk8s.io.
It allows us to debug the deployment in a visual manner. We can easily locate where the problem is in the diagram and find out debugging
possibilities.

{{< pdf-viewer url="https://learnk8s.io/a/troubleshooting-kubernetes.pdf" >}}
