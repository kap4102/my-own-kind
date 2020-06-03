# Mutli-node Kubernetes Cluster

This is all coded now, see [createcluster.sh](/src/createcluster.sh) and [versions.sh](/src/versions.sh).

## Create the Cluster

Creating the cluster is simple but we'll use the new user interface. The old way still works but the new way is more descriptive.

The new way:

```bash
mokctl create cluster myk8s --with-lb --masters 3 --workers 3
```

is equivalent to the old way:

```bash
mokctl create cluster myk8s --with-lb 3 3
```

For testing multi-master with a front-end load balancer for the master 'nodes' only:

```bash
mokctl create cluster myk8s --with-lb --masters 2 --workers 1
```

There is no limit to the number of workers or masters. The workers are set to talk to the load balancer 'node' rather than the masters, and the kubectl configuration file `/var/tmp/admin-myk8s.conf` also points to the load balancer node. Then it's possible to see what happens when master node(s) are stopped and restarted.

For testing, say, pod placement strategies, only one master is required with no load balancer:

```bash
mokctl create cluster myk8s --masters 1 --workers 8
```

My laptop - Intel(R) Processor 5Y10 CPU @ 0.80GHz, with 8GB RAM has no problem running 9 kubernetes 'nodes'.

Here's the output from the previous command:

```bash
$ mokctl create cluster myk8s --masters 1 --workers 8
  ✓ Creating master container, 'myk8s-master-1'
  ✓ Setting up 'myk8s-master-1'
  ✓ Creating worker container, 'myk8s-worker-1'
  ✓ Setting up 'myk8s-worker-1'
  ✓ Creating worker container, 'myk8s-worker-2'
  ✓ Setting up 'myk8s-worker-2'
  ✓ Creating worker container, 'myk8s-worker-3'
  ✓ Setting up 'myk8s-worker-3'
  ✓ Creating worker container, 'myk8s-worker-4'
  ✓ Setting up 'myk8s-worker-4'
  ✓ Creating worker container, 'myk8s-worker-5'
  ✓ Setting up 'myk8s-worker-5'
  ✓ Creating worker container, 'myk8s-worker-6'
  ✓ Setting up 'myk8s-worker-6'
  ✓ Creating worker container, 'myk8s-worker-7'
  ✓ Setting up 'myk8s-worker-7'
  ✓ Creating worker container, 'myk8s-worker-8'
  ✓ Setting up 'myk8s-worker-8'

Cluster, "myk8s", can be accessed using:

export KUBECONFIG=/var/tmp/admin-myk8s.conf

$
```

And the output from `kubectl`:

```bash
$ kubectl get pods -A
NAMESPACE     NAME                                     READY   STATUS    RESTARTS   AGE
kube-system   coredns-66bff467f8-gtt76                 1/1     Running   0          5m22s
kube-system   coredns-66bff467f8-qw6cs                 1/1     Running   0          5m22s
kube-system   etcd-myk8s-master-1                      1/1     Running   0          5m32s
kube-system   kube-apiserver-myk8s-master-1            1/1     Running   0          5m32s
kube-system   kube-controller-manager-myk8s-master-1   1/1     Running   0          5m32s
kube-system   kube-flannel-ds-amd64-6fjg8              1/1     Running   0          5m4s
kube-system   kube-flannel-ds-amd64-6jmsx              1/1     Running   0          5m23s
kube-system   kube-flannel-ds-amd64-7xtvp              1/1     Running   0          5m
kube-system   kube-flannel-ds-amd64-bqggz              0/1     Pending   0          3m51s
kube-system   kube-flannel-ds-amd64-js98f              1/1     Running   0          4m53s
kube-system   kube-flannel-ds-amd64-t7jps              1/1     Running   0          4m47s
kube-system   kube-flannel-ds-amd64-vzb4c              1/1     Running   0          4m56s
kube-system   kube-flannel-ds-amd64-xkwrm              1/1     Running   0          4m41s
kube-system   kube-flannel-ds-amd64-zcqlb              1/1     Running   0          5m6s
kube-system   kube-proxy-5c7v9                         1/1     Running   0          5m
kube-system   kube-proxy-6c5s8                         1/1     Running   0          4m56s
kube-system   kube-proxy-9tt6q                         1/1     Running   1          4m41s
kube-system   kube-proxy-dss28                         1/1     Running   0          5m4s
kube-system   kube-proxy-f272w                         1/1     Running   0          4m47s
kube-system   kube-proxy-hkbdz                         1/1     Running   0          5m6s
kube-system   kube-proxy-rhmw9                         1/1     Running   0          4m53s
kube-system   kube-proxy-rrfx6                         1/1     Running   0          5m22s
kube-system   kube-proxy-w8x6j                         0/1     Pending   0          3m51s
kube-system   kube-scheduler-myk8s-master-1            1/1     Running   0          5m32s
$ kubectl get nodes  
NAME             STATUS     ROLES    AGE     VERSION
myk8s-master-1   Ready      master   5m51s   v1.18.3
myk8s-worker-1   Ready      <none>   5m15s   v1.18.3
myk8s-worker-2   Ready      <none>   5m13s   v1.18.3
myk8s-worker-3   Ready      <none>   5m9s    v1.18.3
myk8s-worker-4   Ready      <none>   5m5s    v1.18.3
myk8s-worker-5   Ready      <none>   5m2s    v1.18.3
myk8s-worker-6   Ready      <none>   4m57s   v1.18.3
myk8s-worker-7   Ready      <none>   4m50s   v1.18.3
myk8s-worker-8   NotReady   <none>   4m3s    v1.18.3

```

The eighth worker did not get set up correctly. It could be fixed manually or the cluster deleted and the creation tried again. The worker nodes are created quite fast, so a delay, waiting until all services are started, would help here. As would being able to add and delete worker nodes after a cluster is built. On faster machines this might not be an issue until even larger clusters are created, so it does need fixing. Both suggested fixes are relatively straight forward to implement so when I need it I will do it, unless someone else does it first :)

> Actually, when I went to delete the cluster I found that Podman was broken, with "too many watched files". The error was:
> 
> "Error: error creating libpod runtime: error configuring CNI network plugin: could not create new watcher too many open files"
> 
> And to be able to delete the cluster I had to increase the max_user_instances:
> 
> `echo "256"> /proc/sys/fs/inotify/max_user_instances`
> 
> This is a temporary fix, until the computer is rebooted. I will probably make it permanent later using sysctl.
> 
> I then re-ran the create cluster command and it worked without error. This makes sense for my laptop since I have OwnCloud running, which establishes a number of watches for all my owncloud directories.
> 
> All 9 'nodes' were up and ready within 2 minutes.

That's it!

## What's Next

Next we learn how to Upgrade a cluster - TODO.
