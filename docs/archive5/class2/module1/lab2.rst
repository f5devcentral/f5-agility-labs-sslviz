.. role:: red
.. role:: bred

Create a new Cisco Firepower Threat Defense TAP service
================================================================================

-  Select **SSL Orchestrator** from the left-hand menu and then click on **Configuration**

-  Select the **Services** tab in the middle of the main display area. Notice that the already configured HTTP Service, **ssloS\_SquidProxy**, is already present.

-  Click the **Add** button above the list of services

-  Type  ``firepower`` in the **Search** box

-  Select **Cisco Firepower Threat Defense TAP** and click the **Add** button

.. image:: ../images/ciscofp-1.png
   :alt: Cisco Firepower Service Configuration

|

-  On the **Service Properties** screen enter the following values:

   -  **Name -** enter ``CiscoFP`` as the name for this service.

   -  **Description -** enter ``Cisco Firepower TAP``.

   -  **MAC Address -** for a TAP service that is not directly connected to F5 SSLO, enter the device's actual MAC address. For a TAP service that is directly connected to F5 SSLO, the MAC address does not matter and can be arbitrarily defined. For this lab, enter ``12:12:12:12:12:12``.

   -  **VLAN -** this defines the interface connecting F5 SSLO to the TAP service. Select **Create New** and ``TAP_in`` as the name.

   -  **Interface -** select the **1.6** interface.

   -  **Tag -** this is the 802.1q VLAN tag for service. Leave it **empty** since this service is connected to an untagged interface.

   -  **Enable Port Remap -** this setting allows SSLO to remap the port of HTTPS traffic flowing to this service. For this lab, leave the option **disabled** (unchecked).


.. image:: ../images/ciscofp-2.png
   :alt: Cisco Firepower Service Configuration

|

-  Click the **Save & Next** button.
