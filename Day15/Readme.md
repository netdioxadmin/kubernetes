# Node Labels
To get node labels
``` kubectl get nodes --show-labels```

Output
```NAME               STATUS   ROLES           AGE   VERSION    LABELS
master.vaves.in    Ready    control-plane   8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=master.vaves.in,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
worker1.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker1.vaves.in,kubernetes.io/os=linux
worker2.vaves.in   Ready    <none>          8d    v1.30.13   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker2.vaves.in,kubernetes.io/os=linux
```