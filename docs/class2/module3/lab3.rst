.. role:: red
.. role:: bred


Layered Virtual Server and Topology Steering iRule
===================================================

-  The **SSLOLIB** and **sslo-layer-rule.tcl** files from the `f5devcentral/sslo-script-tools <https://github.com/f5devcentral/sslo-script-tools/tree/main/internal-layered-architecture>`_ Github repository have already been imported for you. You can skip to the next step.

-  Navigate to  **Local Traffic > Virtual Servers > iRules > Datagroup List** to view the data groups.

.. image:: ../images/dg-appservers_list-1.png
   :alt: View Data Groups

-  Click on the **appserver_list** data group to view the list of server subnets/addresses. Traffic from these source IPs will be directed to the **appserver_explicit** topology. Note that IP address **10.1.10.50** is the **Ubuntu18.04 Client** machine (representing an application server).

.. image:: ../images/dg-appservers_list-2.png
   :alt: Data Group: appservers_list

-  Navigate to  **Local Traffic > Virtual Servers > iRules > iRules List** and review the two iRules.

.. image:: ../images/internal-layered-irules-1.png
   :alt: Internal Layered Architecture iRules


The SSLOLIB iRule contains functions that allow the topology steering rule to easily match on various attributes and then target specific SSL Orchestrator topologies.

.. warning::
   Do not modify the SSLOLIB iRule.

.. image:: ../images/irule-sslolib.png
   :alt: View SSLOLIB iRule

The topology steering iRule ('SSLO-Topology-Director') contains your steering logic and defines the topology steering conditions.

-  Modify the **SSLO-Topology-Director** iRule with the following values:

   -  **Line 21:** Replace ``intercept`` with ``f5labs_explicit``. This defines the default SSL Orchestrator topology to use (if there is no other match).
   -  Insert 2 blank lines at **line 40**.
   -  Copy **line 43** into **line 40**.
   -  **Line 40**: Replace ``my-srcip-dg`` with ``appserver_list``. This defines the data group to check for source address matches.
   -  **Line 40**: Replace ``bypass`` with ``appserver_explicit``. This defines the topology to use if there is a source address match.

.. image:: ../images/irule-topology-director.png
   :alt: Changes to SSLO-Topology-Director iRule

.. note::
   Lines beginning with '#' (green colored) are code comments and act as documentation for these iRules.


-  Navigate to **Local Traffic > Virtual Servers > Virtual Server List** to create the topology steering virtual server.

-  Click on the **Create** button to add a new Virtual Server and configure the following settings:

   -  Name: ``Topology-Director_vs``
   -  Type: **Standard**
   -  Source: ``0.0.0.0/0``
   -  Destination Address: ``10.1.10.200``
   -  Destination Port: ``3128``
   -  Protocol: **TCP**
   -  VLAN Enabled On: **client-vlan**
   -  Address/Port Translation: **disabled**
   -  Default Persistence Profile: **ssl**
   -  iRule: **SSLO-Topology-Director**

.. image:: ../images/topology-director-vs-1.png
   :alt: 

|

.. image:: ../images/topology-director-vs-1b.png
   :alt: 

|

.. image:: ../images/topology-director-vs-1c.png
   :alt: 

|

.. image:: ../images/topology-director-vs-1d.png
   :alt: 

- Click on **Finished** to create the new virtual server.