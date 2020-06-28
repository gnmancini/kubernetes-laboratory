# kubernetes-laboratory
Kubernetes Laboratory to practice for CKA

These are a few playbooks to install a kubernetes cluster without HA to practice the CKA exam.

# This cluster is just for testing purpose.

## Prerequisites

1. Update the /etc/hosts on each server to have all the hosts with their ips and in the laptop/desktop where you will run these playbooks.

2. Update the name of each host to have a FQDN name with
   Ex.
   hostnamectl set-hostname kube01.test.lan

3. Update the ip for each host in 
   sites/hosts_vars/kube01.yml 
   sites/hosts_vars/kube02.yml
   sites/hosts_vars/kube03.yml
   sites/hosts_vars/kube04.yml
   sites/hosts_vars/kube05.yml

4. Add the public key on each kvm host
   ssh-copy-id -i ~/.ssh/mykey root@kube01.test.lan
   
5. Disable firewall in all hosts.
   systemctl stop firewalld; systemctl disable firewalld


Step by step:
Installing the base of kubelet,etc.
   ansible-playbook playbooks/kubernetes-base.yml -i sites/inventory --diff

Installing the kubernetes master.
   ansible-playbook playbook/kubernetes-master.yml -i sites/inventory --diff

Installing the kubernetes cni.
   ansible-playbook playbook/kubernetes-calico.yml -i sites/inventory --diff

Installing the kubernetes workers.
   ansible-playbook playbook/kubernetes-worker.yml -i sites/inventory --diff


Final check:
To check everything is fine ssh into kube01.test.lan and run:
   kubectl get nodes -o wide
   
   
If you find any problem, fix it yourself :-)