.. role:: red
.. role:: bred

Lab 7.1: Deleting a topology
----------------------------

Deleting a topology will also delete any relying Interception Rules. The
deletion process performs a complex set of REST-based tasks, therefore only one
topology can be deleted at a time. In the SSLO UI, select a topology and click
the Delete button. Confirm that both the topology and respective interception
rules are removed.

Deleting other objects
~~~~~~~~~~~~~~~~~~~~~~

While deleting a topology also removes its respective interception rules, it
does not remove the other objects - services, service chains, security policies
and SSL settings. These can all be removed individually, however must be
deleted in a hierarchical order. Once the topology and interception rules have
been deleted,

- :red:`SSL Settings` can be deleted any time
- Delete any unused :red:`Security Policies`
- Delete any unused :red:`Service Chains`
- Delete any unused :red:`Services`

Deleting everything
~~~~~~~~~~~~~~~~~~~

To completely remove the SSLO configuration and start from scratch:

#. In the SSLO UI

   - click :guilabel:`Delete Configurations` and then click :guilabel:`OK`.
   
   .. note:: This process will take some time as SSLO walks through all of the
      objects and dependencies to remove all configurations.

#. Under the
   :menuselection:`iApps menu --> Application Services --> Applications LX`
   
   - "un-deploy" any remaining SSL orchestrator objects. If using any other
     Guided Configuration engine (ex. Access GC), ensure that only SSLO objects
     are deleted here.

#. Under the
   :menuselection:`iApps menu --> Templates --> Templates LX`

   - Delete all of the SSL Orchestrator templates.

#. Under the
   :menuselection:`iApps menu --> Package management LX`

   - Delete the SSL Orchestrator package.

   .. attention:: The next time the SSL Orchestrator configuration menu is
      accessed, SSLO will automatically restore the on-box package.
