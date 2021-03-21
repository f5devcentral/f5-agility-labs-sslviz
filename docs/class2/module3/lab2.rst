.. role:: red
.. role:: bred

Create Secondary Topology
===========================

You will need to add an L3 Explicit topology for the outbound application server traffic. This topology will decrypt TLS and send traffic to a service chain consisting of:

   #. New ICAP-based antivirus service
   #. Existing Cisco Firepower TAP service


L3 Explicit Topology
------------------------

-  Navigate to **SSL Orchestrator > Configuration** and **Add** a new topology.

-  Scroll to the bottom of the page and click on the **Next** button.

-  Enter ``appsvr_explicit`` as the topology name.

-  Select the **L3 Explicit Proxy** topology type.

-  Click the **Save & Next** button to continue.


SSL Configurations
-------------------

-  In the **CA Certificate Key Chain** section, click on the pencil icon to edit.

-  Select **subrsa.f5labs.com** for both **Certificate** and **Key**.

.. note:: This is the self-signed CA certificate and private key that will by used by SSL Orchestrator to sign the re-issued or "forged" certificates delivered to clients for outbound SSL forward proxy traffic.  This is also the CA certificate that must be imported into the client's browser trusted certificates store.

.. image:: ../images/clientssl.png
   :align: left

.. warning:: 
   Ensure that you are editing the **CA Certificate Key Chain** shown above, not the *Certificate Key Chain*.  They look very similar.

|

-  Click **Done**. The **SSL** settings have now been configured.

-  Click the **Save & Next** button to continue.


ICAP service
---------------

-  On the **Services List** screen, click the **Add** button.

-  Type  ``icap`` in the **Search** box

-  Select **Generic ICAP** and click the **Add** button

.. image:: ../images/service-icap-1.png
   :alt: ICAP Service
   :align: left


-  On the **Service Properties** screen, enter the following values:

   -  Enter ``CLAM_AV`` in the **Name** field.

   -  Enter ``ClamAV`` in the **Description** field.

   -  In the **ICAP Devices** section, click on the **Add** button.

   -  Enter ``198.19.97.50`` in the **IP Address** field.

   -  Leave the **Port** set to ``1344`` (default for ICAP).

   -  Click on **Done** to add the ICAP device.

   .. image:: ../images/service-icap-2.png
      :alt: ICAP Service
      :align: left

   -  Enter ``/avscan`` in the **Request Modification URI Path** field.
   
   -  Enter ``/avscan`` in the **Response Modification URI Path** field.

   -  Enter ``1048576`` in the **Preview Max Length(bytes)** field.

   .. image:: ../images/service-icap-3.png
      :alt: ICAP Service
      :align: left

   -  Click **Save** to return to the **Services List**.


.. image:: ../images/services-after-icap.png
   :alt: Services List After Adding ICAP
   :align: left

-  Click the **Save & Next** button to continue.


Service Chain
----------------

You now need to create a new Service Chain containing the CLAM_AV and Cisco Firepower TAP services.

-  On the **Services Chain List** screen, click the **Add** button.

-  On the **Services Chain Properties** screen, enter the following values:

   -  Enter ``CAV_CiscoFP`` in the **Name** field.

   -  Enter ``ClamAV and Cisco Firepower TAP`` in the **Description** field.

   -  **Services -** select the **CLAM_AV** and **CiscoFP_TAP** services under **Services Available** and move them to **Selected Service Chain Order**

   .. image:: ../images/internal-layered-new-sc.png
      :alt: New service chain for Clam AV and Cisco Firepower TAP
      :align: left

-  Click the **Save** button to return to the **Service Chain List**.

-  Click the **Save & Next** button to continue.


Security Policy
-----------------

You now need to create a new Security Policy for the **appsvr_explicit** topology.

-  On the **Security Policy** screen, select the **Create New** radio button to reveal the configuration options.

-  Modify the **All Traffic** rule by clicking on the pencil icon.

-  Select the **ssloSC\_SC\_CAV\_CiscoFP** Service Chain.

-  Click the **OK** button.

.. image:: ../images/internal-layered-policy.png
   :alt: New security policy for application server traffic
   :align: left

-  Click the **Save & Next** button to continue.


Interception Rule / Proxy Server Settings
-------------------------------------------

-  Skip down to the **Proxy Server Settings** section.

-  Enter ``10.1.10.175`` in the  **IPV4 Address** field.

-  Leave the **Port** set to ``3128`` (default value).

-  In the **VLANs** section, select the **/Common/zzz-vlan** VLAN and and move it to Selected column.


.. image:: ../images/internal-layered-interception.png
   :alt: New security policy for application server traffic
   :align: left


-  Click the **Save & Next** button.

Egress Settings
-----------------

-  On the Egress Setting screen, select **Auto Map** in the **Manage SNAT Settings** field.

.. image:: ../images/internal-layered-egress.png
   :alt: 
   :align: left


-  Click the **Save & Next** button.

Log Settings
--------------

-  On the Log Settings screen, leave all the default values.

.. image:: ../images/internal-layered-log.png
   :alt: 
   :align: left


-  Click the **Save & Next** button to continue.


Summary
----------

.. image:: ../images/internal-layered-deploy.png
   :alt: 
   :align: left


-  Click the **Deploy** button.

-  Click the **OK** button to confirm that you want to make the changes.

-  When successfully deployed, click the **OK** button to return to the SSL Orchestrator Configuration screen.



You should now have two L3 Explicit topologies. The third topology is an L3 Outbound (transparent) topology that is not applicable to your lab exercises.

.. image:: ../images/internal-layered-dashboard.png
   :alt: 
   :align: left

