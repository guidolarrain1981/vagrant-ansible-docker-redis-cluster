# Vagrant to implement Ansible playbook to deploy Redis cluster in docker containers

### Requirement

- vagrant
- virtualbox
- ansible
- python
- python-pip

# High Availability Redis
This `Vagrantfile` is based on `redis:3` and `haproxy:1.7`. It creates a three node Redis cluster with [redis-sentinel](https://redis.io/topics/sentinel) and haproxy. The proxy node will always route traffic to the current master node. Sentinel will handle automation failover.

## Usage
```sh
git clone https://github.com/guidolarrain1981/vagrant-ansible-docker-redis-cluster.git
cd vagrant-ansible-docker-redis-cluster
vagrant up
```

## Table of ports
Service       |  Host Port  | Container Port |
:--------------:|:-----------:|:---------------:
redis_proxy     | 6379        | 6379
redis_proxy     | 9000        | 9000
redis_1         | 32786       | 6379
redis_2         | 32788       | 6379
redis_3         | 32787       | 6379

#### Notes
This deploys a complete redis sentinel cluster using docker images from https://github.com/guidolarrain1981/docker-redis forked from https://github.com/jmferrer/docker-redis
