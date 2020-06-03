# Mokctl Help Text

```none
$ mokctl -h

Usage: mokctl [-h] <command> [subcommand] [ARGS...]

Global options:

  --help
  -h     - This help text

Where command can be one of:

  create - Add item(s) to the system.
  delete - Delete item(s) from the system.
  build  - Build item(s) used by the system.
  get    - Get details about items in the system.
  exec   - 'Log in' to the container.

CREATE subcommands are:

  cluster - Create a local kubernetes cluster.

create cluster [flags] options:

 Format:
  create cluster NAME [ [NUM_MASTERS] [NUM_WORKERS] ]
  NAME        - The name of the cluster. This will be used as
                the prefix in the name for newly created
                docker containers.
  NUM_MASTERS - The number of master containers.
  NUM_WORKERS - The number of worker containers. If NUM_WORKERS is
                zero then the 'node-role.kubernetes.io/master' taint
                will be removed from master nodes so that pods are
                schedulable.

 Flags:
  --skipmastersetup - Create the master container but don't set it
         up. Useful for manually installing kubernetes. Kubeadm, 
         kubelet and kubectl will be installed at the requested 
         version. With this option the worker will also be skipped.
         See also '--k8sver' flag.
  --skipworkersetup - The same as '--skipmastersetup', but skips
         setting up the worker only.
  --with-lb - Add a haproxy load balancer. The software will be installed
         and set up to reverse proxy to the master node(s), unless
         --skiplbsetup is used.
  --k8sver VERSION - Unimplemented.
  --masters - The number of master containers to create.
  --workers - The number of worker containers to create. If NUM_WORKERS is
              zero then the 'node-role.kubernetes.io/master' taint will be
              removed from master nodes so that pods are schedulable.
  --tailf - Show the log output whilst creating the cluster.

DELETE subcommands are:

  cluster - Delete a local kubernetes cluster.

delete cluster options:

 Format:
  delete cluster NAME
  NAME        - The name of the cluster to delete

BUILD subcommands are:

  image - Creates the docker 'mok-centos-7' container image.

build image options:

 Format:
  build image

 Flags:
  --tailf - Show the build output whilst building.
  --get-prebuilt-image - Instead of building a 'node' image
         locally, download it from a container registry instead.

GET subcommands are:

  cluster(s) - list all mokctl managed clusters.

get cluster(s) options:

 Format:
  get cluster(s) [NAME]
  NAME        - (optional) The name of the cluster to get
                details about.

EXEC has no subcommands. Exec into a container.

exec options:

 Format:
  exec [NAME]
  NAME        - (optional) The name of the container to 'log in' to.
                If NAME is not given then the user will be offered
                a choice of containers to log in to. If there is only
                one cluster and one node then it will 'log in' to the
                only available container.

EXAMPLES

Get a list of mok clusters

  mokctl get clusters

Build the image used for masters and workers:

  mokctl build image

Create a single node cluster:
Note that the master node will be made schedulable for pods.

  mokctl create cluster mycluster --masters 1

Create a single master and single node cluster:
Note that the master node will NOT be schedulable for pods.

  mokctl create cluster mycluster --masters 1 --workers 2

Delete a cluster:

  mokctl delete cluster mycluster


```

## Command Help

Use `-h` after the command, for example:

```none
$ mokctl create -h
CREATE subcommands are:

  cluster - Create a local kubernetes cluster.

create cluster [flags] options:

 Format:
  create cluster NAME [ [NUM_MASTERS] [NUM_WORKERS] ]
  NAME        - The name of the cluster. This will be used as
                the prefix in the name for newly created
                docker containers.
  NUM_MASTERS - The number of master containers.
  NUM_WORKERS - The number of worker containers. If NUM_WORKERS is
                zero then the 'node-role.kubernetes.io/master' taint
                will be removed from master nodes so that pods are
                schedulable.

 Flags:
  --skipmastersetup - Create the master container but don't set it
         up. Useful for manually installing kubernetes. Kubeadm, 
         kubelet and kubectl will be installed at the requested 
         version. With this option the worker will also be skipped.
         See also '--k8sver' flag.
  --skipworkersetup - The same as '--skipmastersetup', but skips
         setting up the worker only.
  --with-lb - Add a haproxy load balancer. The software will be installed
         and set up to reverse proxy to the master node(s), unless
         --skiplbsetup is used.
  --k8sver VERSION - Unimplemented.
  --masters - The number of master containers to create.
  --workers - The number of worker containers to create. If NUM_WORKERS is
              zero then the 'node-role.kubernetes.io/master' taint will be
              removed from master nodes so that pods are schedulable.
  --tailf - Show the log output whilst creating the cluster.


```

Two different formats are supported:

```none
mokctl create cluster NAME 1 0
mokctl create cluster NAME 1 2
```

OR, equivalently:

```none
mokctl create cluster NAME --masters 1
mokctl create cluster NAME --masters 1 --workers 2
```

That's it!
