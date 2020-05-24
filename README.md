# Intro
This repository is a practical part for Slurm school kubernetes course.
Slides available on Slurm github repo: https://github.com/southbridgeio/slurm-school-k8s

# Basic abstracitons:
- Lesson 1: Pod
- Lesson 2: ReplicaSet
- Lesson 3: Deployments
- Lesson 4: Probes

## Featured lessons
- Lesson 5: ConfigMap
- Lesson 6: Secrets
- Lesson 7: Service
- Lesson 8: Job, CronJob
- Lesson 9: Network
- Lesson 10: Ingress
- Lesson 11: DataStore. Persistent Volume (PV). Persistent Volume Claim (PVC)

# Feature reading:
https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-lifetime
There are different kinds of resources for creating Pods:
Use a Deployment , ReplicaSet or StatefulSet for Pods that are not expected to terminate, for example, web servers.
Use a Job for Pods that are expected to terminate once their work is complete; for example, batch computations. Jobs are appropriate only for Pods with restartPolicy equal to OnFailure or Never.
Use a DaemonSet for Pods that need to run one per eligible node.

Kubeclt cli https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

API https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/