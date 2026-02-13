Ansible Playbooks we can use in this lab
=========================================

The |GitHub| SSLO API Reference repository contains sets of example playbooks to configure SSL Orchestrator:

|


- **Outbound Layer 3 Topology**

  - Deploys an Outbound Layer 3 Transparent Proxy Topology 
  - |outbound-l3-topology-link|: Outbound Layer 3 Transparent Proxy Topology Playbook

|

- **Inline Layer 2 FireEye NX**

  - Deploys an Inline Layer 2 Inspection Service
  - |inline-l2-inspection-service-link| - Inline Layer 2 Inspection Service Playbook
  - Inline Layer 2 - an inline L2 device does not have IP addresses and does not participate in routing. It is effectively no more than a physical presence on the wire. This is specifically for the FireEye service running on 

|

- **Inline Layer 2 Wireshark TAP Service**

  - Deploys an Inline Layer 2 Wireshark TAP Service
  - |inline-l2-wireshark-link|- Inline Layer 2 TAP Service Playbook
  - This is a great option for testing and learning how to build your own custom inspection services. It is also a great option for troubleshooting and learning how to use the API.

|

- **Secure Web Gateway as a Service (SWGaaS)**

  - Deploys an SWGaaS Service.
  - |swgaas-link| - SWGaaS Service Playbook
  - This playbook has dependencies on an existing Secure Web Gateway Per-Request Policy. This is provided within the Lab BIG-IP.  

|

- **Delete** Utility

  - Deletes **all** SSL Orchestrator configuration objects.
  - |delete all SSLO config| - Delete all SSL Orchestrator configuration objects Playbook
  - This is a Nuke and Pave option.


.. |GitHub| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/tree/main" target="_blank"> GitHub </a>

.. |outbound-l3-topology-link| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/blob/main/applications/sslo-config-ssl-outbound.yaml" target="_blank"> Outbound Layer 3 Transparent Proxy</a>

.. |inline-l2-inspection-service-link| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/blob/main/inspection-services/sslo-inspection-service-inlinel2.yaml" target="_blank"> Inline Layer 2 Inspection Service</a>

.. |inline-l2-wireshark-link| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/blob/main/inspection-services/sslo-inspection-service-tap.yaml" target="_blank"> Inline TAP Wireshark Service</a>

.. |swgaas-link| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/blob/main/inspection-services/sslo-inspection-service-swg.yaml" target="_blank"> SWGaaS Service</a>

.. |delete all SSLO config| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/blob/main/utilities/sslo-delete-all.yaml" target="_blank"> Delete SSLO Playbook</a> 