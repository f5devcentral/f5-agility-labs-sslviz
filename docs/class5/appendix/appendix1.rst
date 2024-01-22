
Appendix 1 - Explore the Debug Utility
================================================================================

Ephemeral access to BIG-IP instance command shell can be executed
through the Debug utility subsystem in Central Manager. This utility
provides additional troubleshooting capabilities for data plane issues.

This appendix explores the basic Debug utility setup to access a BIG-IP
Next instance command shell. For expanded information on the Debug
utility and its various options, visit the official reference:
https://clouddocs.f5.com/bigip-next/latest/support/debug_utility.html


Create an SSH Key
--------------------------------------------------------------------------------

#. In Windows (PowerShell), Mac, and Linux, issue the following command: ``ssh-keygen``. 

#. When prompted, assigning a passphrase is optional, but if
   set it will be needed for all future use of this SSH key. 

   When the operation completes, you'll be left with two files - one with a ".pub"
   extension (the public key), and another with the same name but without
   the extension (the private key). The public key will be shared with the
   remote system (Central Manager and BIG-IP Next instance). 

#. Open the public key in a text editor and copy the contents.


Access the Debug Utility
--------------------------------------------------------------------------------

#. In the F5 Central Manager UI, click on the **Manage Instances** button,
   or select **Infrastructure** from the left side menu. 

#. Under **Instances** - **My Instances**, click on a BIG-IP Next instance to
   display the properties drawer.

#. In the left side menu of the properties drawer, navigate to **Debug**. 

#. Click the **Proceed** button. 

#. Paste the contents of the previously create SSH public key in the window or click
   the Browse button to select this file. 

#. When ready, click the **Start Debug Session** button. A new black box will appear 
   in the drawer with instructions on how to access the BIG-IP Next command shell.

   If you used the default options when creating the SSH key (for example: ``/home/student/.ssh/id_rsa``), then follow the instructions as displayed.


   .. code-block:: bash

      ssh admin@10.1.1.7 -p 2222

   If you used a different filename when creating the SSH key, specify this
   private key explicitly in the SSH command with the -i argument.

   .. code-block:: bash

      ssh -i mykey admin@10.1.1.7 -p 2222

   Once inside the BIG-IP Next command shell, you will have access to
   various commands for troubleshooting data plan issues, including:

   -  tmctl - displays various TMM traffic processing statistics.

   -  bdt_cli - displays TMM networking information such as ARP and route
      entries.

   -  tcpdump - captures and replays packets sent and received on network
      interfaces.

   -  wget - retrieves files using HTTP, HTTPS, FTP, and FTPS.

   -  ping - tests reachability of remote hosts on IP networks using ICMP.

   -  traceroute - displays the packet route in hops to a remote host.

#. To stop debugging, close the SSH window then click the **Stop Debug Session**
   button in the Central Manager UI.


Test Network Traffic with TCPDUMP
--------------------------------------------------------------------------------

You can use the ``tcpdump`` command in the BIG-IP
Next debug shell to view the traffic flowing to/from the BIG-IP Next
instance data plane.

#. In this lab environment, the client facing VLAN is named
   **clientside**, and the server facing VLAN is named **serverside**. You
   can verify these names with the following command:

   .. code-block:: bash

      ip link


#. Assuming an application has been deployed on the BIG-IP Next instance,
   start a tcpdump capture listening on the **clientside** VLAN:

   .. code-block:: bash

      tcpdump -lnni clientside


#. From a client browser, access the application deployed to the BIG-IP
   Next instance. This should generate traffic in the tcpdump capture window.
