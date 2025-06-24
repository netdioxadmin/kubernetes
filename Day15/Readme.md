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

Printing Labels
``` NAME               STATUS   ROLES           AGE   VERSION    LABELS
master.vaves.in    Ready    control-plane   8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=master.vaves.in,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
worker1.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,disk=nvme,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker1.vaves.in,kubernetes.io/os=linux
worker2.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,disk=hdd,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker2.vaves.in,kubernetes.io/os=linux   
```
Here `disk=hdd` is applied to worker2 and `disk=nvme` to worker1 

### Now We are going to create a node in work1 with label. 

check nginx.yml in file