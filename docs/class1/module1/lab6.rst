Lab 1.6: TAP Service
--------------------

Task 1 - Create SSLO TAP Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A :guilabel:`Service` is a collection of security devices that will
receive decrypted traffic from the SSLO solution. In this section, a
:guilabel:`TAP Service` will be created. A TAP Service would
typically be an IDS/IPS. 

1. Login to the BIG-IP with Firefox

2. Navigate to :menuselection:`SSL Orchestrator --> Deployment --> Deployment Settings` and click:

   |image4|

3. On the menu across the top of the main window pane navigate to :menuselection:`Services --> TAP Services` and click:

   |image21|

4. Click :guilabel:`Create` on the far right:

   |image22|

5. Enter the following values:

   .. list-table::
      :widths: 50 50
      :header-rows: 1
      :stub-columns: 1


      * - **Property**
        - **Value**
      * - Name
        - ssloS_TAP_service
      * - MAC Address
        - 2c:c2:60:22:e4:23
      * - VLAN
        - ssloN_TAP_in.app/ssloN_TAP_in
      * - Interface
        - 1.4

   .. NOTE::
      For :guilabel:`VLAN`, use the drop-down menu to select the correct value.


6. Once your settings look like the following screenshot, click :guilabel:`Finished`:

   |image23|

.. |image4| image:: /_static/image4.png
.. |image21| image:: /_static/image21.png
   :width: 5.41667in
   :height: 1.76678in
.. |image22| image:: /_static/image22.png
   :width: 5.01852in
   :height: 1.01067in
.. |image23| image:: /_static/image23.png
   :width: 4.97222in
   :height: 3.33091in

