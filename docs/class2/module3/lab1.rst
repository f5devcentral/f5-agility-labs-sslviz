.. role:: red
.. role:: bred

Create Empty VLAN
===================

A topology must be bound to a unique VLAN. Since the topologies in this architecture
won't be listening on an actual client-facing VLAN, you will need to create a separate empty VLAN for each topology you
intend to create. A empty VLAN has no interfaces assigned.

- Navigate to **Network > VLANs** and click on the **Create** button to add a new VLAN
- Name this VLAN:  ``zzz-vlan`` and then click on **Finished**. Do not select any interfaces.

   .. image:: ../images/create-vlan.png
      :alt: Empty VLAN

- Since you are not attaching any interfaces to this VLAN, you will receive a confirmation pop-up.

   .. image:: ../images/vlan-confirm-empty.png
      :alt: Empty VLAN Confirmation

-  Click on **OK** to continue.

|

   .. image:: ../images/vlan-empty.png
      :alt: Empty VLAN Confirmation


