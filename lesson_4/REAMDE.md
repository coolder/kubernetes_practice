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

## Good to know
- Pod restart policy: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#restart-policy

## Practice
Quick start examples got from [official documentation|https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/]

