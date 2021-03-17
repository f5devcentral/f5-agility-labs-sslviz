.. role:: red
.. role:: bred


Create "Topology Director" Virtual Server and iRule
=======================================================

-  First,  import the **SSLOLIB** and **sslo-layer-rule.tcl** files from the Github repository. This has already been done for you.

   - `SSLOLIB <https://github.com/f5devcentral/sslo-script-tools/blob/main/internal-layered-architecture/SSLOLIB>`_

   - `SSLO-Topology-Director (sslo-layering-rule.tcl) <https://raw.githubusercontent.com/f5devcentral/sslo-script-tools/main/internal-layered-architecture/sslo-layering-rule.tcl>`_

-  Navigate to  **Local Traffic > Virtual Servers > iRules** and review each iRule.

.. image:: ../images/internal-layered-irules-1.png
   :alt: Internal Layered Architecture iRules


-  Make the following changes to the **SSLO-Topology-Director** iRule:

   -  Set necessary static configuration values in RULE_INIT as required ...

   -  Modify the **SSLO-Topology-Director** iRule with the following steering commands:
   -  x


-  Navigate to **Local Traffic > Virtual Servers > Virtual Server List** to create the layered topology virtual server.

-  Click on the **Create** button to add a new Virtual Server and configure the following setings:

   -  Name: ``Topology-Director_vs``
   -  Type: ``Standard``
   -  Source: ``0.0.0.0/0``
   -  Destination Address: ``10.1.10.200``
   -  Destination Port: ``3128``
   -  Protocol: ``TCP``
   -  VLAN Enabled On: ``client-vlan``
   -  Address/Port Translation: ``disabled``
   -  Default Persistence Profile: ``ssl``
   -  iRule: ``SSLO-Topology-Director``

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

|


**Traffic selector commands** (to be used in traffic switching iRule)

-  Call the "target" proc with the following parameters ([topology name], ${sni}, [message])

   -  [topology name] is the base name of the defined topology
   -  ${sni} is static here and returns the server name indication value (SNI) for logging
   -  [message] is any string message to send to the log (ex. which rule matched)
   -  return is added at the end of each command to cancel any further matching
   -  Example: call SSLOLIB::target "bypass" ${sni} "SRCIP"

-  Use the following commands to query the proc function for matches (all return true or false) All commands run in CLIENTSSL_CLIENTHELLO to act on SSL traffic.

   .. code-block:: bash

      Source IP Detection (static IP, IP subnet, data group match)
         SRCIP IP:<ip/subnet>
         SRCIP DG:<data group name> (address-type data group)
         if { [call SSLOLIB::SRCIP IP:10.1.0.0/16] } { call SSLOLIB::target "topology name" ${sni} "SRCIP" ; return }
         if { [call SSLOLIB::SRCIP DG:my_sip_list] } { call SSLOLIB::target "topology name" ${sni} "SRCIP" ; return }

      Source Port Detection (static port, port range, data group match)
         SRCPORT PORT:<port/port-range>
         SRCPORT DG:<data group name> (integer-type data group)
         if { [call SSLOLIB::SRCPORT PORT:15000] } { call SSLOLIB::target "topology name" ${sni} "SRCPORT" ; return }
         if { [call SSLOLIB::SRCPORT PORT:1000-60000] } { call SSLOLIB::target "topology name" ${sni} "SRCPORT" ; return }
         if { [call SSLOLIB::SRCPORT DG:my-sport-list] } { call SSLOLIB::target "topology name" ${sni} "SRCPORT" ; return }

      Destination IP Detection (static IP, IP subnet, data group match)
         DSTIP IP:<ip/subnet>
         DSTIP DG:<data group name> (address-type data group)
         if { [call SSLOLIB::DSTIP IP:93.184.216.34] } { call SSLOLIB::target "topology name" ${sni} "DSTIP" ; return }
         if { [call SSLOLIB::DSTIP DG:my-dip-list] } { call SSLOLIB::target "topology name" ${sni} "DSTIP" ; return }

      Destination Port Detection (static port, port range, data group match)
         DSTPORT PORT:<port/port-range>
         DSTPORT DG:<data group name> (integer-type data group)
         if { [call SSLOLIB::DSTPORT PORT:443] } { call SSLOLIB::target "topology name" ${sni} "DSTPORT" ; return }
         if { [call SSLOLIB::DSTPORT PORT:1-1024] } { call SSLOLIB::target "topology name" ${sni} "DSTPORT" ; return }
         if { [call SSLOLIB::DSTPORT DG:my-dport-list] } { call SSLOLIB::target "topology name" ${sni} "DSTPORT" ; return }

      SNI Detection (static URL, category match, data group match)
         SNI URL:<static url>
         SNI URLGLOB:<static url> (ends_with match)
         if { [call SSLOLIB::SNI URL:www.example.com] } { call SSLOLIB::target "topology name" ${sni} "SNIURL" ; return }
         if { [call SSLOLIB::SNI URLGLOB:.example.com] } { call SSLOLIB::target "topology name" ${sni} "SNIURLGLOB" ; return }

         SNI CAT:<category name or list of categories>
         if { [call SSLOLIB::SNI CAT:/Common/Financial_Data_and_Services] } { call SSLOLIB::target "topology name" ${sni} "SNICAT" ; return }
         if { [call SSLOLIB::SNI CAT:$static::URLCAT_Finance_Health] } { call SSLOLIB::target "topology name" ${sni} "SNICAT" ; return }

         SNI DG:<data group name> (string-type data group)
         SNI DGGLOB:<data group name> (ends_with match)
         if { [call SSLOLIB::SNI DG:my-sni-list] } { call SSLOLIB::target "topology name" ${sni} "SNIDG" ; return }
         if { [call SSLOLIB::SNI DGGLOB:my-sniglob-list] } { call SSLOLIB::target "topology name" ${sni} "SNIDGGLOB" ; return }

      Combinations: above selectors can be used in combinations as required. Example:
         if { ([call SSLOLIB::SRCIP IP:10.1.0.0/16]) and ([call SSLOLIB::DSTIP IP:93.184.216.34]) }