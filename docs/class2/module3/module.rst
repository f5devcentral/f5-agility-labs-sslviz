Internal Layered SSL Orchestrator Architecture
================================================

In this lab, you will learn how to implement an *internal* layered SSL Orchestrator architecture to conditionally steer traffic to various SSLO topologies. This 2-tiered architecture enables support for more complex deployment scenarios, while also helping to simplify the SSL Orchestrator configuration.


.. note::
   This methodology is documented in the following Github repository:
   `F5 SSL Orchestrator Layered Architecture Configuration <https://github.com/f5devcentral/sslo-script-tools/tree/main/internal-layered-architecture>`_.
   
   It consists of a set of iRules which reduce deployment complexity by treating SSL Orchestator topologies as functions.


.. toctree::
   :maxdepth: 1
   :glob:

   scenario*
   lab*