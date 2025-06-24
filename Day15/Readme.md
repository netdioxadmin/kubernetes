🚀 Understanding Node Labels in Kubernetes

Node labels are a powerful mechanism in Kubernetes to control where your pods run. Here's a quick walkthrough I did during one of my recent sessions 👇

🔍 Viewing Existing Node Labels

```
kubectl get nodes --show-labels
```

Sample output:

```NAME               STATUS   ROLES           VERSION    LABELS
master.vaves.in    Ready    control-plane   v1.30.13   ... node-role.kubernetes.io/control-plane= ...
worker1.vaves.in   Ready    <none>          v1.30.13   ... kubernetes.io/hostname=worker1.vaves.in ...
worker2.vaves.in   Ready    <none>          v1.30.13   ... kubernetes.io/hostname=worker2.vaves.in ...
```

🏷️ Adding Custom Labels to Nodes
To classify nodes based on disk type, I labeled them as follows:
```
kubectl label node worker1.vaves.in disk=nvme
kubectl label node worker2.vaves.in disk=hdd
```

✅ After applying, labels are visible:
```
worker1.vaves.in ... disk=nvme ...
worker2.vaves.in ... disk=hdd ...
```

📦 Scheduling a Pod Using nodeSelector
I scheduled an NGINX pod using a nodeSelector to target the nvme disk node. Verifying the pod:
```
kubectl get pods -o wide -n ipgeolocation
```

Output:
```
nginx   1/1 Running   10.244.1.7   worker1.vaves.in

The pod landed on worker1.vaves.in as expected. ✅
```
🧹 Removing Node Labels
```
kubectl label node worker1.vaves.in disk-
kubectl label node worker2.vaves.in disk-
```
Checking again:
```
kubectl get nodes --show-labels
```
The custom disk labels are gone.

🤔 But What Happens to the Pod?
Even after removing the labels, the pod remains running:
```
kubectl get pods -o wide -n ipgeolocation

nginx   1/1 Running   10.244.1.7   worker1.vaves.in
```
Why? Because this is a standalone pod, not managed by a Deployment. Kubernetes schedules pods at creation based on the labels at that time — it doesn’t re-evaluate if labels change after the pod is scheduled.

🧠 Takeaway:

    Use labels to manage pod placement smartly.

    Once scheduled, pods don’t migrate automatically when labels are removed or changed — unless managed by higher-level controllers.

If you're working with Kubernetes, mastering node labeling and scheduling logic is key to building smart, efficient clusters.