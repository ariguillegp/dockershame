# Overview

This project will create a k8s cluster in your machine using virtualbox as your hypervisor
and it will be fully automated via kubeadm, ansible and vagrant. The default scenario will become
one master node and 2 workers, but it can be easily scalated as long as you have the hardware
resources to do so. The only command that needs to be run is:

```
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
vagrant@master:~$ kubectl get po -A
```
