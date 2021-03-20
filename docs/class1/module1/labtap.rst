.. role:: red
.. role:: bred

Add a TAP service (optional - time permitting)
=======================================================

.. image:: ../images/gc-path-3.png
   :align: center

Configure a TAP service to add to the ICAP service configured previously.

.. image:: ../images/module1-5.png

Click :red:`Add Service`, then either select a service from the catalog and
click :red:`Add`, or simply double-click the service to go
to its configuration page.


TAP service
~~~~~~~~~~~

A TAP service is a passive device that simply receives a copy of traffic.

-  Click on :red:`Add Service`.

-  Select the :red:`Cisco Firepower Thread Defense TAP`
   service from the catalog and click :red:`Add`, or simply double-click it.

-  **Name** - provide a unique name to this service (example ":red:`TAP`").

-  **Mac Address** - for a tap service that is not directly connected to the
   F5, enter the device's MAC address. For a tap service that is directly
   connected to the F5, the MAC address does not matter and can be
   arbitrarily defined. For this lab, enter :red:`12:12:12:12:12:12`.

-  **VLAN** - this defines the interface connecting the F5 to the TAP
   service. Click :red:`Create New` and provide a unique name (ex.
   :red:`TAP_in`).

-  **Interface** - select the :red:`1.7` interface without a tag.

-  **Enable Port Remap** - this setting allows SSLO to remap the port of
   HTTPS traffic flowing to this service. For this lab, leave the option
   :red:`disabled (unchecked)`.

- Click :red:`Save`.

The **TAP service** for this lab has now been configured.

- Click :red:`Save & Next` to continue to the next stage.

.. image:: ../images/module1-6.png

