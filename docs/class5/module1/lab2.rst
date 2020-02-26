.. role:: raw-html(raw)
   :format: html

Create a new service for the Cisco Firepower device
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Select **SSL Orchestrator->Configuration** from the main menu

-  Select the **Services** tab in the middle of the main display area. Notice that the already configured HTTP Service, **ssloS\_SQID**, is already present.

-  Press the **Add** button above the list of services

-  Type  :raw-html:`<i><font color="red">firepower</font></i>` in the **Search** box

-  Select **Cisco Firepower Threat Defense TAP** and press the
   **Add** button
   
-  On the **Service Properties** screen enter the following values:

   -  **Name -** provide a unique name to this service (example
      :raw-html:`<i><font color="red">Cisco_FP</font></i>`).

   -  **Description -** provide a description as needed (example :raw-html:`<i><font color="red">Cisco
      Firepower TAP</font></i>`).

   -  **MAC Address -** for a TAP service that is not directly connected
      to F5 SSLO, enter the device’s actual MAC address. For a TAP
      service that is directly connected to F5 SSLO, the MAC address does
      not matter and can be arbitrarily defined. For this lab, enter
      :raw-html:`<i><font color="red">12:12:12:12:12:12</font></i>`

   -  **VLAN -** this defines the interface connecting F5 SSLO to the TAP
      service. Click **Create New** and provide a unique name (example
      :raw-html:`<i><font color="red">TAP_in</font></i>`).

   -  **Interface -** select the :raw-html:`<i><font color="red">1.3</font></i>` interface.

   -  **Tag -** this is the 802.1q VLAN tag for service. Leave it
      :raw-html:`<i><font color="red">empty</font></i>` as we will be using an untagged interface.

   -  **Enable Port Remap -** this setting allows SSLO to remap thee
      port of HTTPS traffic flowing to this service. For this lab, leave
      the option :raw-html:`<i><font color="red">disabled (unchecked)</font></i>`.

-  Click the :raw-html:`<i><font color="red">Save & Next</font></i>` button.
