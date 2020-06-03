# Documentation

* [Mokctl command help](/docs/man-mokctl.md).

* [Frequently asked questions](faq.md).

* [How to use the Parser library in your own project](parser.md).

* [Troubleshooting](troubleshoot.md).

## Kubernetes the Hard Way - on your laptop

A remake of the original [Bootstrap Kubernetes the hard way on Google Cloud Platform. No scripts.](https://github.com/kelseyhightower/kubernetes-the-hard-way) with slight configuration changes, only where necessary, to make it work with My Own Kind.

The labs are guaranteed to work if using the same setup as used in the screencasts (Fedora 32 and Podman), as the documentation, screencasts and transcripts are all created by  `cmdline-player` and `scr2md.sh`, which takes about 50 minutes.

Mokctl is used to create seven bare container nodes: a load balancer, 3 controller nodes and 3 worker nodes without melting your laptop.

| Document                                                                                                               | Transcript + Screencast                  |
| ---------------------------------------------------------------------------------------------------------------------- |:----------------------------------------:|
| [Start Page](/docs/k8shardway.md)                                                                                      |                                          |
| [01-prerequisites.md](/docs/kubernetes-the-hard-way/01-prerequisites.md)                                               |                                          |
| [02-client-tools.md](/docs/kubernetes-the-hard-way/02-client-tools.md)                                                 | [kthw-2.md](/cmdline-player/kthw-2.md)   |
| [03-compute-resources.md](/docs/kubernetes-the-hard-way/03-compute-resources.md)                                       | [kthw-3.md](/cmdline-player/kthw-3.md)   |
| [04-certificate-authority.md](/docs/kubernetes-the-hard-way/04-certificate-authority.md)                               | [kthw-4.md](/cmdline-player/kthw-4.md)   |
| [05-kubernetes-configuration-files.md](/docs/kubernetes-the-hard-way/05-kubernetes-configuration-files.md)             | [kthw-5.md](/cmdline-player/kthw-5.md)   |
| [06-data-encryption-keys.md](/docs/kubernetes-the-hard-way/06-data-encryption-keys.md)                                 | [kthw-6.md](/cmdline-player/kthw-6.md)   |
| [07-bootstrapping-etcd.md](/docs/kubernetes-the-hard-way/07-bootstrapping-etcd.md)                                     | [kthw-7.md](/cmdline-player/kthw-7.md)   |
| [08-bootstrapping-kubernetes-controllers.md](/docs/kubernetes-the-hard-way/08-bootstrapping-kubernetes-controllers.md) | [kthw-8.md](/cmdline-player/kthw-8.md)   |
| [09-bootstrapping-kubernetes-workers.md](/docs/kubernetes-the-hard-way/09-bootstrapping-kubernetes-workers.md)         | [kthw-9.md](/cmdline-player/kthw-9.md)   |
| [10-configuring-kubectl.md](/docs/kubernetes-the-hard-way/10-configuring-kubectl.md)                                   | [kthw-10.md](/cmdline-player/kthw-10.md) |
| [11-pod-network-routes.md](/docs/kubernetes-the-hard-way/11-pod-network-routes.md)                                     | [kthw-11.md](/cmdline-player/kthw-11.md) |
| [12-dns-addon.md](/docs/kubernetes-the-hard-way/12-dns-addon.md)                                                       | [kthw-12.md](/cmdline-player/kthw-12.md) |
| [13-smoke-test](/docs/kubernetes-the-hard-way/13-smoke-test.md)                                                        | [kthw-13.md](/cmdline-player/kthw-13.md) |
| [14-cleanup.md](/docs/kubernetes-the-hard-way/14-cleanup.md)                                                           | [kthw-14.md](/cmdline-player/kthw-14.md) |

## How Mokctl was made

The following resources will help when following the documentation below.

- [Certified Kubernetes Administrator (CKA) with Practice Exam Tests](https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests/)
- [Kubernetes in Action by Marko Luksa](https://www.goodreads.com/book/show/34013922-kubernetes-in-action)

Send a Pull Request to add to this list.

## Let's get started

1. [Single Node](/docs/build.md)
   
   Setting up a single node cluster in containers by hand.

2. [Package](/docs/package.md)
   
   Packaging the commands we used into an application.

3. [Testing and Fixing](/docs/testfix.md)
   
   Finding and fixing any problems.

4. [Kubernetes the Hard Way](/docs/k8shardway.md)
   
   The classic remade for MOK. A 7 node cluster without blowing up your laptop!

5. [Multi Node](/docs/multinode.md)
   
   Build a bigger cluster using our package.

6. Upgrade
   
   We can install any version of kubernetes. Let's try installing an older cluster and upgrading it.

7. Add-ons
   
   Trying popluar kubernetes add-ons.
