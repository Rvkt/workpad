# Phase 3: Kubernetes and Orchestration

Part of [[DevOps Roadmap - Index|Senior DevOps Engineer Roadmap]]. Previous: [[Phase 2 - Containers and Docker]]. Next: [[Phase 4 - Infrastructure as Code and Cloud Fundamentals]].

**Duration:** Weeks 5–6
**Objective:** Deploy, scale, and operate containerized workloads on Kubernetes.

## Week 5: Kubernetes Core Concepts

### Cluster Architecture

- [ ] Understand the control plane: API server, etcd, scheduler, controller manager.
- [ ] Understand nodes, kubelet, and the container runtime.
- [ ] Set up a local cluster with kind or minikube.
- [ ] `kubectl` fundamentals: `get`, `describe`, `logs`, `exec`, `apply`.

### Core Workload Objects

- [ ] Pods as the smallest deployable unit, and why they're rarely created directly.
- [ ] Deployments for stateless workloads and rolling updates.
- [ ] ReplicaSets and how Deployments manage them.
- [ ] Services: ClusterIP, NodePort, LoadBalancer, and when each applies.
- [ ] Ingress for HTTP routing into the cluster.
- [ ] ConfigMaps and Secrets for configuration injection.

### Practical Tasks

- [ ] Deploy the roadmap project's container image to a local Kubernetes cluster using a Deployment and a Service.
- [ ] Expose the service externally and verify traffic reaches the application.
- [ ] Inject configuration via a ConfigMap and a secret via a Secret, verifying both inside the running pod.
- [ ] Perform a rolling update and observe zero-downtime deployment behavior.

**Deliverable:** The roadmap application running on Kubernetes, reachable externally, configured via native Kubernetes objects.

## Week 6: Scaling, Storage and Troubleshooting

### Scaling and Resilience

- [ ] Resource requests and limits, and why both matter.
- [ ] Horizontal Pod Autoscaler based on CPU/memory metrics.
- [ ] Liveness and readiness probes, and the difference between them.
- [ ] Pod disruption budgets.
- [ ] Rolling update strategy tuning (`maxSurge`, `maxUnavailable`).

### Storage and State

- [ ] PersistentVolumes and PersistentVolumeClaims.
- [ ] StorageClasses and dynamic provisioning.
- [ ] StatefulSets for stateful workloads and why they differ from Deployments.

### Packaging and Troubleshooting

- [ ] Helm charts: templating, values files, releases.
- [ ] Kustomize as a templating-free alternative for environment overlays.
- [ ] Debugging a CrashLoopBackOff pod methodically (`describe`, `logs`, `logs --previous`).
- [ ] Debugging a pod stuck in Pending (resource constraints, scheduling issues).
- [ ] `kubectl exec` into a running pod for live debugging.

### Practical Tasks

- [ ] Set resource requests/limits and configure an HPA for the roadmap deployment; load-test it to trigger scaling.
- [ ] Add liveness and readiness probes, then deliberately break the readiness check and observe traffic routing change.
- [ ] Package the application as a Helm chart with environment-specific values files.
- [ ] Deliberately misconfigure a pod (bad image, insufficient resources) and diagnose it from symptoms alone.

**Deliverable:** A scalable, self-healing deployment with the diagnostic skill to debug common failure modes without guessing.
