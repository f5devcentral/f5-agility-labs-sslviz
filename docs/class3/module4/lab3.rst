Example Ansible Playbooks
================================================================================

The GitHub repository's **ansible** directory contains a set of example playbooks to configure SSL Orchestrator:

- **Inbound Layer 3 Topology**

  - *config-sslo-inbound-l3-complete.yaml*: Deploys an inbound layer 3 Topology with 2 L3 Services, 2 Service Chains, Security Policy, VIP, SSL Profiles, and an application Pool.

- **Inbound existing application Topology**

  - *config-sslo-existing-app-1sslo.yaml*: Deploy an SSL Orchestrator **existing application** configuration with Services, Service Chains, and Security Policy.
  - *config-sslo-existing-app-2ltm.yaml*: Deploy a simple LTM application (VIP, SSL Profiles, Pool) and attach the SSL Orchestrator **existing application** Security Policy.

- **Delete** Utility

  - *utility-sslo-delete-all.yaml*: Delete all SSL Orchestrator configuration objects.

- **Revoke license** Utility

  - *utility-revoke-license.yaml*: Revoke BIG-IP license so that it can be re-used.
