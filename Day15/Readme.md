# Node Labels
To get node labels
``` kubectl get nodes --show-labels```

Output
```NAME               STATUS   ROLES           AGE   VERSION    LABELS
master.vaves.in    Ready    control-plane   8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=master.vaves.in,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
worker1.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker1.vaves.in,kubernetes.io/os=linux
worker2.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker2.vaves.in,kubernetes.io/os=linux
```

## To add our on Label to a node

- Here I am applying disk label to each node.

``` kubectl label node worker1.vaves.in disk=nvme```
``` kubectl label node worker2.vaves.in disk=hdd```

### Printing Labels
``` NAME               STATUS   ROLES           AGE   VERSION    LABELS
master.vaves.in    Ready    control-plane   8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=master.vaves.in,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
worker1.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,disk=nvme,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker1.vaves.in,kubernetes.io/os=linux
worker2.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,disk=hdd,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker2.vaves.in,kubernetes.io/os=linux   
```
Here `disk=hdd` is applied to worker2 and `disk=nvme` to worker1 

### Now We are going to create a node in work1 with label. 

### Check nginx.yml in file

```  kubectl get pods -o wide -n ipgeolocation ```

#### Output

``` 
nginx                                      1/1     Running   0             40s   10.244.1.7   worker1.vaves.in   <none>           <none>
```
Here you can see that the node is running in worker one since I have applied the nodeselector and `nvme` and the label is set to node. 

### How to remove the label

``` 
kubectl label node worker1.vaves.in disk-
kubectl label node worker2.vaves.in disk-
```
After this listing labels
```
[root@master Day15]# kubectl get nodes --show-labels
NAME               STATUS   ROLES           AGE   VERSION    LABELS
master.vaves.in    Ready    control-plane   8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=master.vaves.in,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
worker1.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker1.vaves.in,kubernetes.io/os=linux
worker2.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker2.vaves.in,kubernetes.io/os=linux
```
Here we can see the lables are nolonger available there. But what happens to the pod? Lets check.

```
kubectl get pods -o wide -n ipgeolocation
```
```
nginx                                      1/1     Running   0             10m   10.244.1.7   worker1.vaves.in   <none>           <none>
```

You can see the pod is still running. This is due to the fact that we have run normal pod not a deployment. Also the dicition to go to which pod is made when pode is being scheduled, not after running or pod is up. 