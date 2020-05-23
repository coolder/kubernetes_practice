# Basic abstracitons: Pod

## Definition from official documentation:
_Pods_ are the smallest deployable units of computing that can be created and managed in Kubernetes. It is a group of one or more containers with shared storage/network, and a specification for how to run the containers. Containers within a Pod share an IP address and port space, and can find each other via localhost.
Link: https://kubernetes.io/docs/concepts/workloads/pods/pod/

## Best practices:
- one Pod one Container
- Pod should execute one function (as same as docker image)

## Good to know:
- Kubernetes scales with Pod.
