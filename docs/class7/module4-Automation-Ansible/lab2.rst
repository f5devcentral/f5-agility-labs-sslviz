Ansible Modules for F5 BIG-IP SSL Orchestrator
==============================================

Ansible offers the following collections for F5 BIG-IP to create, edit, update, and delete configurations:
*These links will take you to Ansible Galaxy site*

- F5 Imperative Collection for Ansible: |galaxy_f5_modules_link|
- F5 Declarative Collection for Ansible: |galaxy_f5_bigip_link|


F5 CloudDocs Reference for SSL Orchestrator:

- F5 SSL Orchestrator Collection Overview: |f5_ssl_orchestrator_collection_link|
- F5 SSL Orchestrator API Reference: |f5_ssl_orchestrator_api_link|
- General documentation can be found here: |f5_ansible_link|

|

Ansible Imperative Collection: f5networks.f5_modules
--------------------------------------------------------------------------------
This is the original collection that leverages F5's *imperative* API calls to provide granular BIG-IP object configuration.

The complete F5 CloudDocs module list is here: |f5_modules_link|


Ansible Declarative Collection: f5networks.f5_bigip
--------------------------------------------------------------------------------
This is a newer collection that leverages F5's *declarative* automation toolchain, such as those available with the |f5_atc_link|. SSL Orchestrator configuration modules are also available here.

The complete F5 CloudDocs module list is here: |f5_bigip_link|

|


This lab uses modules from both f5networks.f5_modules and f5networks.f5_bigip collections.




.. |f5_ssl_orchestrator_collection_link| raw:: html

      <a href="https://clouddocs.f5.com/products/orchestration/ansible/devel/sslo/sslo-collection.html" target="_blank"> SSLO Collection</a>

.. |f5_ssl_orchestrator_api_link| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/tree/main" target="_blank"> SSLO API Reference</a>

.. |f5_atc_link| raw:: html

      <a href="https://www.f5.com/products/automation-and-orchestration/" target="_blank"> F5 Automation Toolchain (ATO)</a>

.. |f5_ansible_link| raw:: html

      <a href="https://clouddocs.f5.com/products/orchestration/ansible/devel/" target="_blank"> F5 Ansible Collections</a>

.. |f5_modules_link| raw:: html

      <a href="https://clouddocs.f5.com/products/orchestration/ansible/devel/modules/module_index.html" target="_blank"> f5_modules</a>

.. |f5_bigip_link| raw:: html

      <a href="https://clouddocs.f5.com/products/orchestration/ansible/devel/f5_bigip/modules_2_0/module_index.html" target="_blank"> f5_bigip</a>

.. |galaxy_f5_modules_link| raw:: html

      <a href="https://galaxy.ansible.com/f5networks/f5_modules" target="_blank"> F5Networks.f5_modules</a>

.. |galaxy_f5_bigip_link| raw:: html

      <a href="https://galaxy.ansible.com/f5networks/f5_bigip" target="_blank"> F5Networks.f5_bigip</a>