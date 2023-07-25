- # Limits
  title:: KK Limits
- CPU is **NOT** the issue (it will throttle as necessary)
- Mem **IS** the issue. Mem management is determined by the requests per POD irrespective of Actual Usage or Limits defined
- Over alloc of POD mem leads to evaluation of all Requests, then Limits followed by QoS determination (1. BestEffort (no resources defined), 2. Burstable (Request < Limits) , 3. Guaranteed Where Request = Limits are equal size).  Lookout for application memory leaks leading to **OOM**, or spike in demand - increase in resource intensive workloads, or heavy resource usage by container/pods on same node - all can lead to **OOM**.
- *==Note:==*
  > Kind: ResourceQuota define the limits applicable to the *Namespace*
  > Kind: LimitRange defines limits for a *Pod* or *Container*
  > Otherwise the requests are tailored as content within a Pod or Container
- Strategies for OOM remedy/diagnostics
  > kubectl get pods - check status and restart count
  > kubectl logs for a specific container
  > kubectl top - reflects biggest resource capacity and utilisation
-