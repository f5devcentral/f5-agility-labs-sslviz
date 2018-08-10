Lab 2.1: Inbound Interception Rules
-----------------------------------

Task 1 - Create a new Interception Rule
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to :menuselection:`SSL Orchestrator --> Deployment --> Interception Rules`

   |image45|

#. In the top, right hand corner, click :guilabel:`Create Inbound Rule...`

   |image46|

Task 2 - Create Wildcard Listener
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this step we will create a listener to intercept all inbound HTTPS
traffic. After the configuration steps, this will be saved as a
wildcard virtual server listening on port 443.
   
#. Under the :guilabel:`General Properties` section, configure the
   following values:

   .. list-table::
      :widths: 50 50
      :header-rows: 1
      :stub-columns: 1


      * - **Property**
        - **Value**
      * - Name
        - ssl_inbound_listener
      * - Destination Address/Mask
        - 0.0.0.0/0
      * - Service Port
        - 443

   |image47|

#. Under the :guilabel:`Security Policy` section, select
   :guilabel:`Create New`.

   |image48|

   The configuration GUI will redirect to the SSL settings
   configuration page.

#. In the :guilabel:`General Settings` section of the Security Policy,
   set the name to `ssloT_inbound_ssl`.

   .. NOTE::
      For **Inbound** configurations the :guilabel:`Forward Proxy`
      option should be `disabled`

   |image49|

#. Under the :guilabel:`Client-side SSL` section, choose
   `wildcard.f5demolabs.com.crt` and `wildcard.f5demolabs.com.key` from
   the respective drop-down menus and click :guilabel:`Add`.

   |image50|

#. Under the section :guilabel:`Server-side SSL`, configure the
   following values:

   .. list-table::
      :widths: 50 50
      :header-rows: 1
      :stub-columns: 1


      * - **Property**
        - **Value**
      * - Expire Certificate Response Control
        - ignore
      * - Untrusted Certificate Response Control
        - ignore
  
   |serverside_ssl|

#. Review the settings and click :guilabel:`Finished`. This will
   redirect back to the original :guilabel:`Inbound Listener`
   configuration screen.

Task 3 - Configure VLAN Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this step, we will define which VLAN interface that our listener
will accept connections.

.. NOTE::
   Since we are configuring only for inbound traffic, it is important
   that the wildcard listener only accept connections on the incoming
   interface. In this case, the VLAN labeled `outbound`.

#. In the :guilabel:`VLANs` section, choose the `/Common/outbound` VLAN
   from the :guilabel:`Available List` and click the left arrow to move
   it into :guilabel:`Selected`.

   |image51|


#. Under the :guilabel:`Security Policy` section, configure these values:

   .. list-table::
      :widths: 50 50
      :header-rows: 1
      :stub-columns: 1


      * - **Property**
        - **Value**
      * - L7 Profile Type
        - HTTP
      * - L7 Profile
        - /Common/http
      * - Access Profile
        - /Common/ssloP_outbound_ssl.app/ssloP_outbound_ssl_accessProfile
      * - Per Request Policy
        - Create New

   |image52|

#. Once redirected to the :guilabel:`New Inbound Rule` configuration: 

   i. Create a name for the rule
   ii. Add ICAP, TAP, and L2 services to the :guilabel:`Intercept Chain` section
   iii. Repeat step (ii) for the :guilabel:`Non Intercept Chain`
   iv. Click :guilabel:`Finished`

   |image53|

#. Verify the settings under :guilabel:`Security Policy`.

   |image54|

#. Click :guilabel:`Finish`

.. |image45| image:: /_static/image41.png
   :width: 5.75000in
   :height: 1.44444in
.. |image46| image:: /_static/image42.png
   :width: 6.50000in
   :height: 2.19792in
.. |image47| image:: /_static/image43.png
   :width: 6.50000in
   :height: 3.01111in
.. |image48| image:: /_static/image44.png
   :width: 5.54167in
   :height: 1.09722in
.. |image49| image:: /_static/image45.png
   :width: 6.50000in
   :height: 1.77292in
.. |image50| image:: /_static/image46.png
   :width: 6.50000in
   :height: 1.59722in
.. |image51| image:: /_static/image47.png
   :width: 6.50000in
   :height: 1.24514in
.. |image52| image:: /_static/image48.png
   :width: 6.50000in
   :height: 3.18264in
.. |image53| image:: /_static/image49.png
   :width: 6.50000in
   :height: 2.93958in
.. |image54| image:: /_static/image50.png
   :width: 6.50000in
   :height: 1.69931in
.. |serverside_ssl| image:: /_static/class1-module2-lab1-serverssl.png
