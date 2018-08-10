Lab 1.4: L2 Service
-------------------

Task 1 - Create SSLO L2 Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A :guilabel:`Service` is a collection of security devices that will
receive decrypted traffic from the SSLO solution. In this section an
:guilabel:`L2 Service` will be created. An L2 Service could be an
IDS/IPS or DLP solution. Some refer to this as a "Bump in the Wire."

1. Login to the BIG-IP with Firefox

2. Navigate to :menuselection:`SSL Orchestrator --> Deployment --> Deployment Settings` and
   click:

   |image4|

3. On the menu across the top of the main window pane, navigate to :menuselection:`Services --> L2 Services` and click:

   |image15|

4. Click :guilabel:`Create` on the far right:

   |image16|

5. Enter the following values:

   .. list-table::
      :widths: 50 50
      :header-rows: 1
      :stub-columns: 1


      * - **Property**
        - **Value**
      * - Name
        - ssloS_L2_service
      * - Paths --> From BIGIP VLAN
        - ssloN_L2_in.app/ssloN_L2_in
      * - Paths --> To BIGIP VLAN
        - ssloN_L2_out.app/ssloN_L2_out (click :guilabel:`Add`)

6. Once your settings look like the following screenshot, click :guilabel:`Finished`:

   |image17|

.. |image4| image:: /_static/image4.png
.. |image15| image:: /_static/image15.png
   :width: 5.27778in
   :height: 1.76681in
.. |image16| image:: /_static/image16.png
   :width: 4.66042in
   :height: 1.00926in
.. |image17| image:: /_static/image17.png
   :width: 4.63168in
   :height: 5.13889in


