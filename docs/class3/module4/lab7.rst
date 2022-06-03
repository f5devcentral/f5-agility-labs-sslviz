Deploy SSL Orchestrator Topology
================================================================================

In the BASH Terminal, deploy an Inbound L3 Topology by executing the following:

   .. code-block:: bash

      ansible-playbook -e @ansible_vars.yaml playbooks/config-sslo-inbound-l3-complete.yaml

You will see each task being run in sequence. Wait for the playbook to complete.

.. image:: ./images/ansible-4.png
   :align: left

When finished, you will see a summary ("play recap") indicating how many tasks made configuration changes.
