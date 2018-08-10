Lab 1.5: L3 Service
-------------------

Task 1 - Create SSLO L3 Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A :guilabel:`Service` is a collection of security devices that will
receive decrypted traffic from the SSLO solution. In this section, an
:guilabel:`L3 Service` will be created. An L3 Service would
typically be an IDS/IPS, DLP, or Next-Gen Firewall (NGFW).

1. Login to the BIG-IP with Firefox

2. Navigate to :menuselection:`SSL Orchestrator --> Deployment --> Deployment Settings` and
   click:

   |image4|

3. On the menu across the top of the main window pane navigate to :menuselection:`Services --> L3 Services` and click:

   |image18|

4. Click :guilabel:`Create` on the far right:

   |image19|

5. Enter the following values: 

   .. list-table::
      :widths: 50 50
      :header-rows: 1
      :stub-columns: 1


      * - **Property**
        - **Value**
      * - Name
        - ssloS_L3_service
      * - To Service VLAN
        - ssloN_L3_in.app/ssloN_L3_in
      * - Node --> IP Address
        - 198.19.64.64 (click :guilabel:`Add`)
      * - From Service VLAN
        - ssloN_L3_out.app/ssloN_L3_out

   .. NOTE::
      For :guilabel:`To Service VLAN` and :guilabel:`From Service VLAN`,
      use the drop-down menu to select the correct value.

6. Once your settings look like the following screenshot, click :guilabel:`Finished`:

   |image20|


.. |image4| image:: /_static/image4.png
   :width: 3.69444in
   :height: 2.95833in
.. |image18| image:: /_static/image18.png
   :width: 5.25000in
   :height: 1.69391in
.. |image19| image:: /_static/image19.png
   :width: 4.59191in
   :height: 0.95370in
.. |image20| image:: /_static/image20.png
   :width: 4.90741in
   :height: 6.74902in

