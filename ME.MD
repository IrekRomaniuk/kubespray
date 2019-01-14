## Prep

ssh-copy-id -i ~/.ssh/id_rsa.pub netlab@10.29.95.90
sudo visudo
netlab ALL=(ALL) NOPASSWD: ALL


## How to run

```
ansible-playbook -i inventory/netlab/hosts.ini --become --become-user=root cluster.yml
ansible-playbook -vv -i inventory/netlab/hosts.ini --become --become-user=root cluster.yml -b -v --private-key=~/.ssh/id_rsa
```
# CHANGES

## all.yml

#### Added by me
ansible_user: netlab
#### Upstream dns servers used by dnsmasq
upstream_dns_servers:
  - 10.29.21.215
  - 10.34.21.215
  - 8.8.8.8
#### The read-only port for the Kubelet to serve on with no authentication/authorization. Uncomment to enable.
kube_read_only_port: 10255 

### Internal loadbalancers for apiservers
loadbalancer_apiserver_localhost: true


## k8s-cluster.yml

#### Kubernetes internal network for services, unused block of space.
kube_service_addresses: 192.168.128.0/17

#### internal network. When used, it will assign IP
#### addresses from this range to individual pods.
#### This network must be unused in your network infrastructure!
kube_pods_subnet: 10.29.196.0/24

### Removed from repo

inventory/local
contrib
.github
.git
.gitmodules
.gitlab-ci.yml
