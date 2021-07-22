Letting iptables see bridged traffic
lsmod | grep br_netfilter
sudo modprobe br_netfilter
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

sudo sysctl --system

CRE docker INSTALL

Install using the repository
Update the apt package index and install packages to allow apt to use a repository over HTTPS:

sudo -i 

    apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

 

Add Docker’s official GPG key:

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

Use the following command to set up the stable repository.

echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

Install Docker Engine

Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:

apt-get update

apt-get install docker-ce docker-ce-cli containerd.io

Configure the Docker daemon, in particular to use systemd for the management of the container’s cgroups

sudo mkdir /etc/docker
cat <<EOF | sudo tee /etc/docker/daemon.json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF

Restart Docker and enable on boot:
{
sudo systemctl enable docker
sudo systemctl daemon-reload
sudo systemctl restart docker
}
Update the apt package index and install packages needed to use the Kubernetes apt repository:

    apt-get update
    apt-get install -y apt-transport-https curl


Download the Google Cloud public signing key:

curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg

Add the Kubernetes apt repository:

echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

Update apt package index, install kubelet, kubeadm and kubectl, and pin their version:

sudo apt-get update
sudo apt-get install kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

---
root@kubemaster:~# ifconfig enp0s8

kubeadm init --pod-network-cidr 10.244.0.0/16 --apiserver-advertise-address=192.168.56.2

--
kubeadm join 192.168.56.2:6443 --token l3oa5t.ylrhs4boaqvk05cb \
        --discovery-token-ca-cert-hash sha256:fc25766668430c7fd7487a3edfb27438380e02f2af9b6d31ab1d105af9c8a2c8 
--
10.244.1.0/24
logout
vagrant@kubemaster:~# 

mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

{WEAVE NETWORK}
  vagrant@kubemaster:~$ kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
 
 {CALICO NETWORK}
 wget https://docs.projectcalico.org/manifests/calico.yaml

 kubectl apply -f calico.yaml
 
vagrant@kubemaster:~$ watch kubectl get pods -n calico-system

 On all worker nodes --

root@kubenode01:~#
kubeadm join 192.168.56.2:6443 --token eqwjbm.u7xu5uqr1fq928iq \
        --discovery-token-ca-cert-hash sha256:924e12209e56e8f7fd32fd097aa096cdfebcb2d5b84fb72259e80eac98923e14 
recent
kubeadm join 192.168.56.2:6443 --token m23yzz.d29oay7dlti6sqsj \
        --discovery-token-ca-cert-hash sha256:53be38e9ec69338f89aee0bca25e1f127ba3dd42fb029d133bc8364576e71a6b docker-compose --version

{Bash Auto completion}

source <(kubectl completion bash) # setup autocomplete in bash into the current shell, bash-completion package should be installed first.
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.

alias k=kubectl
complete -F __start_kubectl k

{
  kubeadm join 192.168.56.2:6443 --token rnl7kc.fccb5q3047yqjdf8 \
        --discovery-token-ca-cert-hash sha256:eb17c1d1820e6a146a8d5aef07d6d75526b38308f897f6b1b51c00d4a8522b3c 
}