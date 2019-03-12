.. role:: red
.. role:: bred

Lab 4.1: Create an LTM application
----------------------------------

For the lab, create a simple LTM Virtual Server:

#. **Create a pool** - go to Local Traffic --> Pools --> Pool List and click
   :red:`Create`. Set a name of your choice and add the following pool members
   using (the internal webserver IPs) and select port 80.

   - 10.20.0.90:80
   - 10.20.0.91:80
   - 10.20.0.92:80

#. **Create a client SSL profile** - go to Local Traffic --> Profiles --> SSL
   --> Client and click :red:`Create`. Set a name of your choice and use the
   :red:`wildcard.f5labs.com` certificate and private key.

#. **Create an LTM virtual server** - go to Local Traffic --> Virtual Server
   List and click :red:`Create`. Set a name of your choice and use the
   following basic settings:

   - **Destination Address/Mask**: :red:`10.30.0.205`
   - **Service Port**: :red:`443`
   - **HTTP Profile**: :red:`http`
   - **SSL Profile (Client)**: :red:`previously created Client SSL profile`
   - **VLANs and Tunnels**: :red:`outbound VLAN`
   - **Source Address Translation**: :red:`Auto Map`
   - **Pool**: :red:`previously created pool`

#. **Test access to the LTM virtual server**

   - RDP to the **Inbound** Windows client.
   - The webserver should be accessible via HTTPS request to the LTM virtual
     server IP.
   - Optionally add a static host entry in the local Windows hosts file
     (C:\Windows\System32\drivers\etc\hosts) for:

     - www.f5labs.com = 10.30.0.205
     - Test access to https://www.f5labs.com. 
     
     .. note:: The certificate is a wildcard, so any \*.f5labs.com hostname
        would also work.
