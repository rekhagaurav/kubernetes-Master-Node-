# kubernetes-Master-Node
How to create cluster in Kubernetes.

Launch 2 Ec2 Instance(Ubuntu) of Instance type is t2(Large).
1-Master node Instance     2- Slaves Node Instance
Connect both instance with putty with public ip.

sudo su
apt update -y 
# Then install docker 
apt install docker.io -y
docker --version

systemctl start docker
systemctl enable docker

# Enter the signing key 
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add

# if it's showing Error then install Curl
sudo apt-get install curl


# create a source list 
nano /etc/apt/sources.list.d/kubernetes.list

# Then deploy this xenial inside the source list
deb http://apt.kubernetes.io/ kubernetes-xenial main

# for comingout with source list press
(ctrl+x)+(shift+y)+enter

# Then again update 
apt-get update

# install kubelet,kubeadm,kubectl then
apt-get install -y kubelet kubeadm kubectl kubernetes-cni


# BOOTSTRAPPING THE MASTER NODE (IN MASTER)

kubeadm init
# After this you will get 2 commands 1 for master and other for nodes
Example: mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config


chown $(id -u):$(id -g) $HOME/.kube/config

# BOOTSTRAPING THE SLAVES NODES (IN SLAVES)


e.g- kubeadm join 172.31.6.165:6443 --token kl9fhu.co2n90v3rxtqllrs --discovery-token-ca-cert-hash sha256:b0f8003d23dbf445e0132a53d7aa1922bdef8d553d9eca06e65c928322b3e7c0

# Then check in master node 
kubectl get node

# you will get how many slaves is there.





















