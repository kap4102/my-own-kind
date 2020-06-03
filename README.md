# My Own Kind

![](docs/images/install-mokctl-linux.gif)

View a [Transcript of the screenscast](/cmdline-player/install-mokctl-linux.md).

## Summary

Build a verifiably conformant kubernetes cluster in containers.

## Documentation

The FAQ, Kubernetes the Hard Way using `mokctl`, integrating the Parser in your own project, and how `mokctl` was created are all in [Documentation](/docs/README.md).

## Try mokctl

Take note of the [Status](#status) below and the [Releases](https://github.com/mclarkson/my-own-kind/releases) page.

### For All Operating Systems

> Note for **Linux** users: Cgroups 2 must be disabled. See [Install Linux](/docs/install-linux.md).

Ensure [Docker](https://www.docker.com/get-started) or [Moby](https://github.com/moby/moby) are installed first.

Add the following to your shell startup file, for example `~/.bashrc` or `~/.zshrc`:

```bash
alias mokbox='docker run --rm -ti --hostname mokbox --name mokbox -v /var/run/docker.sock:/var/run/docker.sock -v /var/tmp:/var/tmp myownkind/mokbox'
```

Close the terminal and start it again so the alias is created.

Then 'log in' to the work container:

```bash
mokbox
```

Use `mokctl` and `kubectl`, which are already installed in the 'mokbox' container:

```bash
mokctl build image --get-prebuilt-image

mokctl create cluster myk8s --masters 1

export KUBECONFIG=/var/tmp/admin-myk8s.conf

kubectl get pods -A
```

Type `exit` or `Ctrl-d` to 'log out' of the mokbox. The mokbox container will be deleted but the kubernetes cluster will remain, as will the `kubectl` file,`/var/tmp/admin-myk8s.conf`.

To remove the `mokctl` created kubernetes cluster:

```bash
mokbox

export KUBECONFIG=/var/tmp/admin-myk8s.conf

mokctl delete cluster myk8s

exit

```

Two docker images will remain, 'myownkind/mokbox' and 'myownkind/mok-centos-7-v1.18.3'. Remove them to reclaim disk space, or keep them around to be able to quickly build kubernetes clusters.

See also:

* [Mokctl on Docker Hub](https://hub.docker.com/repository/docker/myownkind/mokctl) - to alias the `mokctl` command only, no mokbox.

* [Linux installation options](/docs/install-linux.md)

## Status

`mokctl`

* stable version - not yet.

* development version - 0.8.1-alpha

**Mokctl Utility**

| OS        | Termnal          | Status                       |
| --------- | ---------------- | ---------------------------- |
| Fedora 31 | Gnome Terminal   | Works - must disable cgroup2 |
| Fedora 32 | Gnome Terminal   | Works - must disable cgroup2 |
| Mac OS    | Default terminal | ?                            |
| Windows   | Cygwin           | ?                            |

## Contributing

All types of contributions are welcome, from bug reports, giving this project a STAR, success stories, feature requests, fixing typppos, to coding. Also check the [CONTRIBUTING.md](/CONTRIBUTING.md) document.
