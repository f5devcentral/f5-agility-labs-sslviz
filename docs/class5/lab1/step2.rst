.. raw:: html
   <style> .red {color:red} </style>

.. role:: red

Step 2: Create a new service for the Cisco Firepower device
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Select ***SSL Orchestrator->Configuration*** from the main menu

-  Select ***Services*** from the menu on the displayed screen on the
   right. Notice that the already configured HTTP Type inspection
   service ***ssloS\_SQID*** is already present.

-  Press the ***Add*** button shown below the menu display line

-  Type \ *firepower* in the ***Search*** box below the ***Service
   Settings***

-  Select ***Cisco Firepower Threat Defense TAP*** and press the
   ***Add*** button and enter values as shown below

   -  **Name –** provide a unique name to this service (example
      *Cisco\_FP*).

   -  **Description –** provide a description as needed (example :red: *Cisco
      Firepower Tap device*).

   -  **MAC Address –** for a tap service that is not directly connected
      to the F5, enter the device’s actual mac address. For a tap
      service that is directly connected to the F5, the Mac Address does
      not matter and can be arbitrarily defined. For this lab, enter
      :red: *12:12:12:12:12:12.*

   -  **VLAN –** this defines the interface connecting the F5 to the TAP
      service. Click *Create New* and provide a unique name (example :red: 
      *TAP\_in*).

   -  **Interface –** select the :red: *1.3* interface.

   -  **Tag –** this is the 802.1q VLAN tag for service. Leave it
      :red: *empty* as we will be using an untagged interface.

   -  **Enable Port Remap –** this setting allows SSLO to remap thee
      port of HTTPS traffic flowing to this service. For this lab, leave
      the option :red: *disabled (unchecked)*.

-  Click :red: *Save & Next* button.
