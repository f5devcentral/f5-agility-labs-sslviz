.. role:: red

Implement SSL Orchestrator topology steering
==============================================


**Installation**

#. Import this SSLOLIB iRule (name "SSLOLIB")

#. Build a set of "dummy" VLANs. A topology must be bound to a unique VLAN. But since the topologies in this architecture
   won't be listening on an actual client-facing VLAN, you will need to create a separate dummy VLAN for each topology you
   intend to create. A dummy VLAN is basically a VLAN with no interface assigned. In the BIG-IP UI, under Network -> VLANs,
   click Create. Give your VLAN a name and click Finished. It will ask you to confirm since you're not attaching an interface.
   Click OK to continue. Repeat this step by creating unique VLAN names for each topology you are planning to use.

#. Build semi-static SSL Orchestrator topologies based on common actions (ex. allow, intercept, service chain)

   Minimally create a normal "intercept" topology and a separate "bypass" topology

   Intercept topology:

   L3 outbound topology configuration, normal topology settings, SSL config, services, service chain
   No security policy rules - just a single ALL rule with TLS intercept action (and service chain)
   Attach to a "dummy" VLAN
   Bypass topology:

   L3 outbound topology configuration, skip SSL config, re-use services, service chains
   No security policy rules - just a single ALL rule with TLS bypass action (and service chain)
   Attached to a separate "dummy" VLAN
   Create any additional topologies as required, as separate functions based on discrete actions (allow/block, intercept/bypass, service chain)

#. Import the traffic switching iRule

   Set necessary static configuration values in RULE_INIT as required

   Define any URL category lists in RULE_INIT as required (see example). Use the following command to get a list of URL categories:


   .. code-block:: bash

      tmsh list sys url-db url-category |grep "sys url-db url-category " |awk -F" " '{print $4}'

#. Create a client-facing topology switching VIP

   Type: Standard
   Source: 0.0.0.0/0
   Destination: 0.0.0.0/0:0
   Protocol: TCP
   VLAN: client-facing VLAN
   Address/Port Translation: disabled
   Default Persistence Profile: ssl
   iRule: traffic switching iRule

#. Modify the traffic switching iRule with the required detection commands. See below.


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