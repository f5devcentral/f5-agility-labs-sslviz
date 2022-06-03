Ansible Modules for SSL Orchestrator
================================================================================

F5 offers the following Ansible collections to create, edit, update, and delete configuration objects for BIG-IP and BIG-IQ:

- F5 Imperative Collection for Ansible (f5_modules)
- F5 Declarative Collection for Ansible (f5_bigip)

General documentation can be found here: |f5_ansible_link|

f5_modules
--------------------------------------------------------------------------------
This is the original collection that leverages F5's *imperative* API calls to provide granular BIG-IP object configuration.

The complete module list is here: |f5_modules_link|


f5_bigip
--------------------------------------------------------------------------------
This is a newer collection that leverages F5's *declarative* API extensions such as those available with the  |f5_atc_link|. SSL Orchestrator configuration modules are also available here.

The complete module list is here: |f5_bigip_link|

|

.. attention::

   As of May, 2022, the SSL Orchestrator modules are available as a pre-release **preview**, so they may contain bugs and are subject to change in functionality and/or usage syntax.

|

This lab uses modules from both collections.


**Additional references:**

- |galaxy_f5_modules_link|
- |galaxy_f5_bigip_link|


.. |f5_atc_link| raw:: html

      <a href="https://www.f5.com/products/automation-and-orchestration/" target="_blank"> F5 Automation Toolchain </a>

.. |f5_ansible_link| raw:: html

      <a href="https://clouddocs.f5.com/products/orchestration/ansible/devel/" target="_blank"> F5 Ansible Collections </a>

.. |f5_modules_link| raw:: html

      <a href="https://clouddocs.f5.com/products/orchestration/ansible/devel/modules/module_index.html" target="_blank"> f5_modules </a>

.. |f5_bigip_link| raw:: html

      <a href="https://clouddocs.f5.com/products/orchestration/ansible/devel/f5_bigip/modules_2_0/module_index.html" target="_blank"> f5_bigip </a>

.. |galaxy_f5_modules_link| raw:: html

      <a href="https://galaxy.ansible.com/f5networks/f5_modules" target="_blank"> Ansible Galaxy > f5_modules </a>

.. |galaxy_f5_bigip_link| raw:: html

      <a href="https://galaxy.ansible.com/f5networks/f5_bigip" target="_blank"> Ansible Galaxy > f5_bigip </a>
