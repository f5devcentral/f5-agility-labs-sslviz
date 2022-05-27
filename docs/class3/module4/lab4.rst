Install F5 Ansible Collections
================================================================================

To work with Ansible in this lab environment, you must first change the Ansible directory permissions and then switch to that directory.

   .. code-block:: bash

      cd ~/sslo-cloud-templates
      chmod o-w ansible
      cd ansible


While the SSL Orchestrator configuration modules are in the F5 Declarative Ansible collection, you will also need some of the modules from the F5 Imperative Ansible collection to perform this lab.

|

.. attention::

   In order to avoid breaking changes from F5 Ansible collection updates (remember that the SSL Orchestrator modules are still in preview and subject to change before GA), a snapshot of the tested modules have been included in the lab files (sslo-cloud-templates/ansible/collections/\*). The following instructions are provided for reference only.

|

*Install both F5 Ansible collections:*

   *ansible-galaxy collection install f5networks.f5_bigip f5networks.f5_modules -f* **!!! DO NOT EXECUTE THIS COMMAND !!!**

|

Example output:

.. image:: ./images/ansible-1.png
   :align: left
