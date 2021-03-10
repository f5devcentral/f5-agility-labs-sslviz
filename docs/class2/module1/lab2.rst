.. role:: red

Create a new Cisco Firepower Threat Defense TAP service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Select **SSL Orchestrator** from the left-hand menu and then click on **Configuration**

-  Select the **Services** tab in the middle of the main display area. Notice that the already configured HTTP Service, **ssloS\_Squid_Proxy**, is already present.

-  Click the **Add** button above the list of services

-  Type  :red:`firepower` in the **Search** box

-  Select **Cisco Firepower Threat Defense TAP** and click the **Add** button
   
-  On the **Service Properties** screen enter the following values:

   -  **Name -** provide a unique name to this service (ex. :red:`CiscoFP`).

   -  **Description -** provide a description as needed (ex. :red:`Cisco Firepower TAP`).

   -  **MAC Address -** for a TAP service that is not directly connected to F5 SSLO, enter the device's actual MAC address. For a TAP service that is directly connected to F5 SSLO, the MAC address does not matter and can be arbitrarily defined. For this lab, enter :red:`12:12:12:12:12:12`

   -  **VLAN -** this defines the interface connecting F5 SSLO to the TAP service. Select **Create New** and provide a unique name (ex. :red:`TAP_in`).

   -  **Interface -** select the :red:`1.6` interface.

   -  **Tag -** this is the 802.1q VLAN tag for service. Leave it :red:`empty` since this service is connected to an untagged interface.

   -  **Enable Port Remap -** this setting allows SSLO to remap the port of HTTPS traffic flowing to this service. For this lab, leave the option :red:`disabled (unchecked)`.

-  Click the **Save & Next** button.