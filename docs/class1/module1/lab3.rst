Lab 1.3: ICAP Service
---------------------

Task 1 - Create SSLO ICAP Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A :guilabel:`Service` is a collection of security devices that will
receive decrypted traffic from the SSLO solution. In this section, an
:guilabel:`ICAP Service` will be created. An ICAP Service would
typically be an Anti-Virus or DLP solution. It is important to have the
correct :guilabel:`Request` and :guilabel:`Response` URIs for the
solution and the appropriate :guilabel:`Preview Max Length`.

1. Login to the BIG-IP with Firefox

2. Navigate to :menuselection:`SSL Orchestrator --> Deployment --> Deployment Settings` and
   click:

   |image4|

3. On the menu across the top of the main window pane, navigate to :menuselection:`Services --> ICAP Services` and click:

   |image12|

4. Click :guilabel:`Create` on the far right

   |image13|

5. Enter the following values:

   .. list-table::
      :widths: 50 50
      :header-rows: 1
      :stub-columns: 1


      * - **Property**
        - **Value**
      * - Name
        - ssloS_ICAP_service
      * - ICAP Devices --> IP Address
        - 10.70.0.10 (click :guilabel:`Add`)
      * - Request
        - Replace `/req` with `/squidclamav`
      * - Response
        - Replace `/res` with `/squidclamav`
      * - Preview Max Length
        - 1048576

6. Once your settings look like the following screenshot, click :guilabel:`Finish`:

   |image14|

.. |image4| image:: /_static/image4.png
.. |image12| image:: /_static/image12.png
   :width: 4.37963in
   :height: 1.57358in
.. |image13| image:: /_static/image13.png
   :width: 4.62963in
   :height: 1.04661in
.. |image14| image:: /_static/image14.png
   :width: 4.37037in
   :height: 4.58515in

