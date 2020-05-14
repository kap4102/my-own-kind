# KTHW 02 Client Tools

```bash
# ---------------------------------------------------------
# Kubernetes the Hard Way - using `mokctl` from My Own Kind
# ---------------------------------------------------------
# 02-client-tools
# Install CFSSL

# Let's do all this in a container so the host is kept clean
# We'll start a container with podman and create a new
# directory to use as a volume mount, where we'll put
# all the certificates.

podman ps
mkdir -p kthw
podman run -d -v /root:$PWD/kthw --name kthw fedora /sbin/init
podman exec -ti kthw bash
dnf install wget
y
# Installing the Client Tools
wget -q --show-progress --https-only --timestamping \\
  https://storage.googleapis.com/kubernetes-the-hard-way/cfssl/linux/cfssl \\
  https://storage.googleapis.com/kubernetes-the-hard-way/cfssl/linux/cfssljson
chmod +x cfssl cfssljson
sudo mv cfssl cfssljson /usr/local/bin/
# Verification
cfssl version
cfssljson --version
# Install kubectl
# Linux
wget https://storage.googleapis.com/kubernetes-release/release/v1.15.3/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
# Verification
kubectl version --client
exit
ls kthw
# ------------------------------------
# Next: Provisioning Compute Resources
# ------------------------------------

```