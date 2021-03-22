# Dockershame

This project will create a k8s cluster in your machine using virtualbox as your hypervisor
and it will be fully automated via kubeadm, ansible and vagrant. The default scenario will deploy
one master node and 2 workers, but it can be easily escalated as long as you have the hardware
resources to do so. The default base operating system for your cluster nodes will be Ubuntu 20.04
and the container runtime is going to be containerd but it can be changed to CRI-O.

Everything was tested on a machine running Archlinux, but theoretically it will work on a variety
of other platforms as long as the minimum requirements are satisfied.

## Getting Started

Once you've fulfilled the requirements, just clone the project, move to its root and run:

```
$ vagrant up
```

### Prerequisites

The general requirements to get this project running are ansible, virtualbox and vagrant.

### Installing

```
# Ansible
$ sudo pacman -S --noconfirm --needed ansible sshpass

# Virtualbox
$ sudo pacman -S --noconfirm --neded virtualbox virtualbox-host-modules-arch virtualbox-guest-iso
$ yay -S virtualbox-ext-oracle

# Vagrant
$ sudo pacman -S --noconfirm --needed vagrant

# You can select the CRI by changing the value of the variable
# cri in the file vars/main.yml, the possible values so far are
# containerd and crio

$ vagrant up
# Once cluster done, you can list the VMs
$ vagrant status

# You can then ssh into each node
$ vagrant ssh master
$ vagrant ssh worker1
$ vagrant ssh worker2

# Inside the master's terminal
# you can list all pods in all namespaces
# to verify everything is running as expected
vagrant@master:~$ kubectl get no
vagrant@master:~$ kubectl get po -A
```

### TODOs:

* Add [cilium](https://cilium.io/) as another CNI option

## Authors

* [Aristides Gonzalez](https://github.com/ariguillegp)

## Inspiration

* https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/
* https://github.com/walidshaari/Certified-Kubernetes-Security-Specialist
