Lab 1.2: HTTP Service
---------------------

Task 1 - Create SSLO HTTP Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A service is a collection of security devices that will receive decrypted traffic from the SSLO solution. In this section, the HTTP Service will be created. An HTTP Service would typically be a Secure Web Proxy. The proxy could explicit or transparent.


1. Login to the BIG-IP with Firefox

2. Navigate to :menuselection:`SSL Orchestrator --> Deployment --> Deployment Settings` and
   click:

   |image4|

3. On the menu across the top of the main window pane, navigate to :menuselection:`Services --> HTTP Services` and click:

   |image9|

4. Click :guilabel:`Create` on the far right:

   |image10|

5. Enter the following information:

   .. list-table::
      :widths: 50 50
      :header-rows: 1
      :stub-columns: 1


      * - **Property**
        - **Value**
      * - Name
        - ssloS_HTTP_service
      * - Proxy Type
        - Explicit
      * - To Service VLAN
        - ssloN_HTTP_in.app/ssloN_HTTP_in
      * - Node --> IP Address
        - 198.19.96.66 (click :guilabel:`Add`)
      * - From Service VLAN
        - ssloN_HTTP_out.app/ssloN_HTTP_out

   .. NOTE:: 
      For :guilabel:`To Service VLAN` and :guilabel:`From Service VLAN`,
      use the drop-down menu to select the correct value.

6. Once your settings look like the following screenshot, click :guilabel:`Finish`:

   |image11|

.. |image4| image:: /_static/image4.png
.. |image9| image:: /_static/image9.png
    :width: 80%
.. |image10| image:: /_static/image10.png
    :width: 80%
.. |image11| image:: /_static/image11.png
    :width: 80%

