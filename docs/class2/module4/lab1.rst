.. role:: red
.. role:: bred

Lab 4.1: Create an LTM application
----------------------------------

For the lab, create a simple LTM Virtual Server:

#. **Create a pool** - go to :menuselection:`Local Traffic --> Pools --> Pool List` and click
   :guilabel:`Create`.

   - Set a name of your choice
   - Use :red:`"http"` health monitor
   - Add the following pool members using (the internal webserver IPs) and
     service port 80
     
     - 10.20.0.90
     - 10.20.0.91
     - 10.20.0.92

   - Click :guilabel:`Finished`

#. **Create a client SSL profile** - go to :menuselection:`Local Traffic --> Profiles --> SSL
   --> Client` and click :guilabel:`Create`.
   
   - Set a name of your choice
   - Modify the "Certificate Key Chain" by adding :red:`wildcard.f5labs.com`
     certificate and private key.
   - Click :guilabel:`Finished`

#. **Create an LTM virtual server** - go to :menuselection:`Local Traffic --> Virtual Server
   List` and click :guilabel:`Create`.
   
   - Set a name of your choice
   - **Destination Address/Mask**: :red:`10.30.0.205`
   - **Service Port**: :red:`443`
   - **HTTP Profile**: :red:`http`
   - **SSL Profile (Client)**: :red:`previously created Client SSL profile`
   - **VLANs and Tunnels**: Select :red:`Enabled on...` option, and then :red:`outbound` VLAN
   - **Source Address Translation**: :red:`Auto Map`
   - **Default Pool**: :red:`previously created pool`
   - Click :guilabel:`Finished`

#. **Test access to the LTM virtual server**

   - RDP to the :bred:`Inbound Windows client`.
   - The webserver should be accessible via HTTPS request to the LTM virtual
     server IP.
   - Optionally add a static host entry in the local Windows hosts file
     (C:\\Windows\\System32\\drivers\\etc\\hosts) for:

     - www.f5labs.com = 10.30.0.205

     .. note:: A shortcut to the "hosts" file can be found on the desktop.
   
   - Test access to https://www.f5labs.com. 
     
   .. note:: The certificate is a wildcard, so any \*.f5labs.com hostname
      would also work.

   .. image:: ../images/vs-test.png
   
