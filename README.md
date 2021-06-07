# NGLP Ansible

This repository contains two Ansible playbooks for deploying an NGLP stack. One is for local deployments, and one for
remote deployments.

Both use docker-compose for orchestrating containers, though the `docker-compose.yml` file is templated. Additionally,
the remote deployment sets up nginx on the host machine to reverse-proxy the containers — with X.509 certificates
for HTTPS provisioned by certbot — and to set up a firewall with firewalld.

The following plumbing between containers also takes place:

* an ElasticSearch user is set up for Kibana, and the credentials passed to Kibana
* an OpenID Connect client is set up in Keycloak, and the credentials passed to Kibana

We use [autoheal](https://hub.docker.com/r/willfarrell/autoheal/) to restart unhealthy containers.


## Remote deployment

This deploys to nglp-test.cottagelabs.com. Once you can SSH to that machine as root, it should be as simple as:

```bash
$ ansible-galaxy collection install -r requirements.yml
$ ansible-playbook nglp.yml
```


## Local deployment

You'll need some Python packages installed system-wide:

Fedora:

```bash
$ sudo dnf install docker-compose python3-cryptography python3-passlib
```

Debian or Ubuntu:

```bash
$ sudo apt install docker-compose python3-cryptography python3-passlib
```

And then set up locally with Ansible:

```bash
$ ansible-galaxy collection install -r requirements.yml
$ ansible-playbook nglp-local.yml
```
