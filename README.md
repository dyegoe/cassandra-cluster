# Cassandra Cluster

This playbook covers a preparation of servers to compose a Cassandra cluster using docker images.

## Limitations and improvements

- For the firewall rules, I decided to go with an specific network interface to get the IPv4. It limits which kind of setup this ansible can cover.
- The swarm role has the same limitation as mentioned above.

## Ansible

### Pre tasks

- Update all packages beforehand.
- Install Python PIP.

### Roles

#### users_mgmt

Create users on machine based on the `group_vars/all/users.yml` file. This file is encrypted using `ansible_vault`. Password stored `~/.vault_password_cassandra`.

#### firewall

Configure UFW.

- Reset all rules before apply anything.

#### docker_config

Install and configure Docker.

#### reboot_check

Verify if any restart is needed by the system.

#### docker_swarm_manager_init

Configure swarm manager node. It runs only for the `swarm_manager` group.

#### docker_swarm_nodes

Join Swarm nodes. It runs only for the `swarm_nodes` group.

#### cassandra

There is a `docker-compose.yml` template under `roles/cassandra/templates`.

## References

- [https://docs.docker.com/compose/compose-file/](https://docs.docker.com/compose/compose-file/)
- [https://docs.docker.com/engine/swarm/swarm-tutorial/inspect-service/](https://docs.docker.com/engine/swarm/swarm-tutorial/inspect-service/)
- [https://docs.docker.com/engine/reference/commandline/service_update/](https://docs.docker.com/engine/reference/commandline/service_update/)
- [https://ralph.blog.imixs.com/2019/06/24/cassandra-and-docker-swarm/](https://ralph.blog.imixs.com/2019/06/24/cassandra-and-docker-swarm/)
- [https://hub.docker.com/_/cassandra](https://hub.docker.com/_/cassandra)
- [https://docs.ansible.com/ansible/latest/modules/docker_stack_module.html](https://docs.ansible.com/ansible/latest/modules/docker_stack_module.html)
