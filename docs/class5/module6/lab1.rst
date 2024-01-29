About SSL Orchestrator Configuration Automation
==============================================================================

Automation support adds an exciting new perspective to the F5 BIG-IP SSL
Orchestrator that was not previously available in the BIG-IP "Classic" version.

There are two main drivers for programmability:

#. **Configuration**: Where an API is used (instead of a GUI/CLI) to deploy the
   general configuration of the product. While this is typically less
   important in typical data center appliance use cases, it is highly desirable
   in cloud and other "orchestrated" deployments, where you might need
   to programmatically spin up entire security and application
   architectures quickly. For example, deploying applications
   "on-demand" through a multi-cloud networking (MCN) workflow generally demands programmability.

#. **Policy Manipulation**: The SSL Orchestrator policy represents a
   "tunable" control surface to address changing traffic behaviors and
   various events. Administrators can programmatically adjust the
   policy to reflect real-time traffic conditions.

This module explores some basic programmability aspects of the BIG-IP Next SSL
Orchestrator, both to control configuration, and to manipulate the
policy. 

|

.. note::
   The following instructions assume basic connectivity to the lab
   environment, and administrative access to the lab's network and virtual
   machine configurations. 

