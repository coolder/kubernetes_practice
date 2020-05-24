# Basic abstracitons: Probes

## Definition from official documentation:
A Probe is a diagnostic performed periodically by the kubelet on a Container.
There are 3 probe types:
- startupProbe - indicates whether application with containers started. You should specify a startup probe that checks the same endpoint as the liveness probe. *When should you use it?* If your Container usually starts in more than initialDelaySeconds + failureThreshold × periodSeconds.
- readinessProbe - indicates whether the container is ready to handle requests. *When should you use it?* If you’d like to start sending traffic to a Pod only when a probe succeeds.
- livenessProbe - classic healthcheck. indicates whether container is still alive. *When should you use it?* If the process in your Container is able to crash on its own whenever it encounters an issue or becomes unhealthy, you do not necessarily need a liveness probe; the kubelet will automatically perform the correct action in accordance with the Pod’s restartPolicy.

Each probe has one of three results: Success, Failure and Unknown.

To perform probes you can use 3 kind of handlers: ExecAction, TCPSocketAction, HTTPGetAction

[Official documentation|https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-probes]

## Template
### Related fields
- spec.containers.livenessProbe
- spec.containers.livenessProbe.exec - ExecAction probe config
- spec.containers.startupProbe
- spec.containers.readynessProbe
- spec.containers.<probe_type>Probe.initialDelaySeconds - wait before start probes
- spec.containers.<probe_type>Probe.periodSeconds - probes execution period.
- spec.containers.<probe_type>Probe.failureThreshold - 
- spec.containers.ports.name - name for named port

## Good to know
- Pod restart policy: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#restart-policy

## Practice
Quick start examples got from [official documentation|https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/]

- liveness probes. ExecAction handler.
```
# create testing pod
$ kubectl apply -f 1_liveness_exec_probe.yaml

# verify that pod is running and not restarted.
$ kubectl get po liveness-exec

# due to configuration checks will start in 5 seconds since start and will be executed every 5 seconds.
# In Containter at it's point we are going to create a /tmp/healthy file which will be available for probes for 30 seconds since container start.

# If you describe Pod after 35 seconds since start you will find a warning from probe
$ kubectl describe po liveness-exec 
# From output: Liveness probe failed: cat: can't open '/tmp/healthy': No such file or directory

# When Kubernetes timeout expire this container will be restarted
# If you get this Pod in some minutes you will notice that Restart count was incremented 
$ kubectl get po liveness-exec

# You will notice that after a while Pod state will get a value CrashLoopBackOff. Try to investigate why it happens ;)
```
- startup probes. HTTPGetAction handler. Port names.
```
# create testing pod
$ kubectl apply -f 2_startup_http_probe.yaml
```

- rediness probes. TCPSocketAction handler.
```
# create testing pod
$ kubectl apply -f 3_rediness_tcp_probe.yaml
```