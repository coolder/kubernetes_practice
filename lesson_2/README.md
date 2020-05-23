# Basic abstracitons: ReplicaSet

## Definitions from official documentation

ReplicaSet is a parent of Pod's.
A ReplicaSet’s purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

A ReplicaSet ensures that a specified number of pod replicas are running at any given time, and doesn't monitor for any other changes. There are high level asbstactions to do so.

[Official documentation] (https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

### Relation between ReplicaSet selector and Pod labels
Replica set working with only pod's which have same label specified in selector ReplicaSet field.

## Template
### Related fields
- spec.replicas - quantity of pod replicas defined with the template
- spec.selector - define observer rules.
- spec.selector.matchLabel - defines pod's label names to observe.
- spec.template - describe Pod template

## Practice log
- run ReplicaSet from official documentation
```
$ kubectl apply -f 1_quick_start_replica_set.yaml

# check that ReplicaSet frontend is created and DESIRED, CURRENT and READY counts are equal to 3
$ kubectl describe rs
$ kubectl describe rs frontend

# verify that pods defined by this replica set are really running
# pay attention on creation time
$ kubectl get po

# kill one random pod to be sure that replica set maintain desired count
$ kubectl delete pod frontend-<hash>

# check that new pod at place of deleted was created. check live time field.
$ kubectl get pod

# clean up 
$ kubectl delete rs frontend
```

- Offtop: in this lesson we have seen new command _kubectl apply_ . In difference of _kubectl create_ this command not only creates new resources when it doesn't exists but even apply new configuration on running resources. Here is a quick check for this.
```
# create new config with create command
$ kubectl create -f 1_quick_start_replica_set.yaml

# repeate same command to be sure that it will fail
$ kubectl create -f 1_quick_start_replica_set.yaml

# on other hand apply command on top of this won't fail, it only return a warning that this config already exists.
$ kubectl apply -f 1_quick_start_replica_set.yaml

# clean up resources
$ kubectl delete rs frontend

# check that you can even create resources with apply
$ kubectl apply -f 1_quick_start_replica_set.yaml
$ kubectl get rs frontend

# if you execute twice same command you will be notified (without warning) that config updated.
$ kubectl apply -f 1_quick_start_replica_set.yaml

# clean up resources
$ kubectl delete rs frontend
```

- check if Replica set remove extra pod. To do so, we need to get a Pod template from lesson_1 and add tier label to it which will be accepted by ReplicaSet (selector field).
```
# create ReplicaSet
$ kubectl create -f 1_quick_start_replica_set.yaml

# check ReplicaSet pod's
$ kubectl get pod

# create new extra pod for ReplicaSet
$ kubectl create -f 1_1_extra_pod.yaml

# right after this command check pod's
$ kubectl get pod

# you should see that your extra pod is in Termination state because it's recognised by ReplicaSet as an extra Pod.
```

- scale ReplicaSet from cli. We can scale replica set manually from CLI. But it's a bad practice to do so bypassing template
```
# check that you have 3 Pod replicas
$ kubectl get rs frontend

# set desired ReplicaSet count to 4
$ kubectl scale --replicas=4 replicaset frontend

# check that you have 4 Pod replicas
$ kubectl get rs frontend

# final cleanup
$ kubectl delete rs frontend
```

## New commands
- kubectl apply -f <file_name>
- kubectl scale --replicas=<count> <resource_type> <resource_name> (https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#scale)

### Useful links
- kubectl cli references: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

### Shortcuts

- replicaSet => rs

