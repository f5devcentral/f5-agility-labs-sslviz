Example Ansible Playbooks
================================================================================

The GitHub repository's **ansible** directory contains a set of example playbooks to configure SSL Orchestrator:

- **Inbound layer 3 topology**
  - Deploys SSL Orchestrator Topology with 2 L3 Services, 2 Service Chains, Security Policy, VIP, SSL Profiles, and an application Pool.

- **Inbound existing application topology**
  - Deploy a simple LTM application (VIP, SSL Profiles, Pool)
  - Deploy SSL Orchestrator Topology with Services, Service Chains, and Security Policy. It also attaches itself to the LTM application VIP.

- Utility to **delete all SSL Orchestrator configuration** objects.

- Utility to **revoke the BIG-IP license** (so that it can be re-used).
