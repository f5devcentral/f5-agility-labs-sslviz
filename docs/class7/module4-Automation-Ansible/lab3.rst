Example Ansible Playbooks
================================================================================

The |GitHub| SSLO API Reference repository contains sets of example playbooks to configure SSL Orchestrator:

- **Outbound Layer 3 Topology**

  - *sslo-config-ssl-outbound.yaml*: Deploys an Outbound Layer 3 Transparent Proxy Topology 
  - |outbound-l3-topology-link|: Outbound Layer 3 Transparent Proxy Topology Playbook

- **Inline Layer 2**

  - *inspection-service-inlinel2.yaml*: Deploys an Inline Layer 2 Inspection Service
  - |inline-l2-topology-link|: Inline Layer 2 Inspection Service Playbook

- **Modify Existing Outbound Topology**


- **Delete** Utility

  - *utility-sslo-delete-all.yaml*: Delete all SSL Orchestrator configuration objects.

- **Revoke license** Utility

  - *utility-revoke-license.yaml*: Revoke BIG-IP license so that it can be re-used.


.. |GitHub| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/tree/main" target="_blank"> GitHub </a>

.. |outbound-l3-topology-link| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/blob/main/applications/sslo-config-ssl-outbound.yaml" target="_blank"> Outbound Layer 3 Transparent Proxy Topology Playbook </a>

 .. |inline-l2-topology-link| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/blob/main/inspection-services/sslo-inspection-service-inlinel2.yaml" target="_blank"> Inline Layer 2 Inspection Service Playbook </a>