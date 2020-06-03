# Trouble-shooting Tips

#### `mokctl create ...` doesn't work

> Some troubleshooting steps:
> 
> * Make sure Cgroups2 is disabled.
>   
>   After a kernel upgrade this might also need to be done. Run:
>   
>   `sudo grubby --update-kernel=ALL --args="systemd.unified_cgroup_hierarchy=0"`
>   
>   Then reboot the machine and try again.
> 
> * Try deleting the cluster and trying again!
> 
> * It's something else. Use `--tailf` to troubleshoot, for example:
>   
>   `mokctl create cluster myclust --masters1 --tailf`
>   
>   Something shown might stand out.
> 
> * It still doesn't work.
>   
>   Try installing `docker` and use the installation steps for non-linux.
> 
> * Try increasing the number of inotify watchers, for example:
>   
>   `echo "256"> /proc/sys/fs/inotify/max_user_instances`.
> 
> * Disable the firewall temporarily to see if it fixes the problem.
> 
> * Disable selinux to see if it fixes the problem.

#### `mokctl build image` doesn't work

> Try to:
> 
> * Run the build with `--get-prebuilt-image`.
>   
>   To download a prebuilt image.
> 
> * Run the build with `--tailf`.
>   
>   To watch the log as it's running.
