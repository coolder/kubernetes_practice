# Basic abstracitons: Pod

## Definition from official documentation:
_Pods_ are the smallest deployable units of computing that can be created and managed in Kubernetes. It is a group of one or more containers with shared storage/network, and a specification for how to run the containers. Containers within a Pod share an IP address and port space, and can find each other via localhost.
[Official documentation] (https://kubernetes.io/docs/concepts/workloads/pods/pod/)

## Template
### Related fields
- apiVersion - version of resource template *required*
- kind - kind of the resource described with the template *required*
- metadata.name - resource name. *required*
- spec - resource configuration itself
- spec.containers - containers description.

## Best practices:
- one Pod one Container
- Pod should execute one function (as same as docker image)
- setup kubectl builtin completion: $ kubectl completion -h

## Good to know:
- Kubernetes scales with Pod.
- Pod lifecicle: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/
- Each Pod has a service container created automatically which define Pod network namespace.

## Practice log
- run quick start pod within 1_quick_start_pod.yaml template. Pod template got from [off. doc: https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/#pod-templates].
```
# create your first pod
$ kubectl create -f 1_quick_start_pod.yaml

# look at pod configuration
$ kubectl describe pod hello | less

# check that pod executed correctly
$ kubectl logs hello

# clean up
$ kubectl delete pod hello

```

- run test nginx pod
```
$ kubectl create -f 2_simple_nginx_pod.yaml
$ kubectl describe po
$ kubectl delete po nginx
```

## Notes:
### New commands:
- kubectl create -f <template_file_name>
- kubectl get <resource_type> <resource_name>
- kubectl describe <abstraction> <name>
- kubectl logs <pod_name>
- kubectl delete <abstraction> <name>

### Commands shortcuts:
- kubectl => k
- pod => po