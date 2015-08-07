# Redis Master-Slave Setup.

This playbook will setup a Redis Master, and Redis Slaves to that Master.

## How to Start

First have launch the 3 or 4 Ubuntu 14.04 servers(Yes, this playbook only works with Ubuntu 14.04). Designate one as the redis-master(Redis Master), and rest of them as redis-slaves(Redis Slaves), appropriately list them in the `./hosts` file.

    [redis-master]
    rmaster ansible_ssh_host=10.10.0.6

    [redis-slaves]
    10.10.0.7
    10.10.0.8
    10.10.0.9

> NOTE: You might have to setup proxies on the `./base-redis/tasks/main.yml` and `./common/tasks/main.yml`, remove it if you do not need it.

    ...
      environment:
        http_proxy: http://myproxy.in:8080
        https_proxy: http://myproxy.in:8080


Once you have done the edits, you are ready to go.

    $ ansible-playbook -i hosts site.yml

This should setup the redis cluster with single redis-master and 3 redis-slaves. If you want add sentinels to the picture. You just need to modify the hosts file, and something like this.
    
    ...
    ...
    [redis-sentinels]
    10.10.0.6
    10.10.0.7
    10.10.0.8
    10.10.0.9

Now you should rerun the, `ansible-playbook -i hosts site.yml`.