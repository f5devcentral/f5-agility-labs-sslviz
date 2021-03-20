.. role:: red
.. role:: bred

Begin creating the initial deployment via Guided Configuration
========================================================================================

The SSL Orchestrator Guided Configuration presents a streamlined user experience. This workflow-based architecture provides
intuitive, re-entrant configuration steps tailored to the selected
topology.

The following steps will walk through the :red:`Guided Configuration` UI to build a
simple transparent forward proxy.


Initialization
------------------
From the left-hand menu, navigate to
:red:`SSL Orchestrator > Configuration`. 

.. image:: ../images/gcstart.png
   :align: center

If this is the first
time accessing SSLO in a new BIG-IP build, the Guided Configuration UI will
automatically load and deploy the built-in SSLO package as shown below.

.. image:: ../images/module1-1.png
   :align: center


Configuration review and prerequisites
-------------------------------------------

Take a moment to review the topology options and workflow configuration steps
involved. Optionally satisfy any of the :red:`DNS, NTP and Route` prerequisites
from this page. Keep in mind, however, that aside from NTP, the SSLO GC will
provide an opportunity to define DNS and route settings later in the workflow.

.. NOTE::
   DNS and NTP settings have already been defined in this lab.

.. image:: ../images/module1-2.png
   :align: center

Click :red:`Next` to continue to the next stage.