.. role:: red
.. role:: bred

Guided Configuration Services List
===================================

.. image:: ../images/gc-path-3.png
   :align: center

The Services List page is used to define security
services that attach to SSLO. The SSLO Guided Configuration includes a services catalog that contains common product
integrations. Beneath each of these catalog options is one of the
five basic service types. The service catalog also provides "generic"
security services. Depending on screen resolution, it may be
necessary to scroll down to see additional services.

.. image:: ../images/module1-40.png

.. image:: ../images/module1-41.png

We will initially create one ICAP security service. If time allows, you may create more services using the subsequent optional labs.  

For this lab, 

- Click :red:`Add Service`, and select Generic ICAP Service from the catalog and click :red:`Add`, or simply double-click the service to go to its configuration page.

.. note:: The only fields that need to be edited are the ones explicitly mentioned in these bullets.  The other fields may be left with their default value.

- Name - CLAM_AV

- ICAP Devices - Click :red:`Add`, enter :red:`198.19.97.50` for the IP Address, and :red:`1344` for the Port, and then click :red:`Done`.

- Request Modification URI Path - /avscan

- Response Modification URI Path - /avscan

- Preview Max Length(bytes) - 1048576

-  Click :red:`Save`.

.. image:: ../images/module1-41.png
   :align: center



The image below shows the service list with the new ICAP service.

.. image:: ../images/module1-42.png

The first :red:`Service` has now been configured.

-  Click :red:`Save & Next` to continue to the next stage.

.. image:: ../images/module1-4.png

.. note:: There are no additional hands-on steps that need to be taken by the student before proceeding to the next section.  The information below is intended to provide additional context on the ICAP Service.


ICAP service
~~~~~~~~~~~~

An ICAP service is an RFC 3507-defined service that
provides some set of services over the ICAP protocol.

-  Click on :red:`Add Service`.

-  Select the :red:`Generic ICAP Service` from the
   catalog and click :red:`Add`, or simply double-click it.

-  **Name** - provide a unique name to this service (example ":red:`CLAM_AV`").

- **IP Family** - this setting defines the IP family used with this layer 3
   service. Leave it set to :red:`IPv4`.

-  **ICAP Devices** - this defines the IP address of the ICAP service, used
   for passing traffic to this device. Multiple load balanced IP addresses
   can be defined here. Click :red:`Add`, enter :red:`198.19.97.50` for the
   IP Address, and :red:`1344` for the Port, and then click :red:`Done`.

-  **Device Monitor** - security service definitions can use
   specific custom monitors. For this lab, leave it set to the default
   :red:`/Common/tcp`.

-  **ICAP Headers** - options are **Default** or **Custom**. Selecting
   **Custom** allows you to specify additional ICAP headers. For this lab,
   leave the setting at :red:`Default`.

-  **OneConnect** - the F5 OneConnect profile improves performance by reusing
   TCP connections to ICAP servers to process multiple transactions. If the
   ICAP servers do not support multiple ICAP transactions per TCP connection,
   do not enable this option. For this lab, leave the OneConnect setting
   :red:`enabled (checked)`.

-  **Request Modification URI Path** - this is the RFC 3507-defined URI request path to
   the ICAP service. Each ICAP security vendor will differ with respect to
   request and response URIs, and preview length, so it is important to
   review the vendor's documentation. In this lab, enter :red:`/avscan`.

-  **Response Modification URI Path** - this is the RFC 3507-defined URI response path to
   the ICAP service. Each ICAP security vendor will differ with respect to
   request and response URIs, and preview length, so it is important to
   review the vendor's documentation. In this lab, enter :red:`/avscan`.

-  **Preview Max Length(bytes)** - this defines the maximum length of the
   ICAP preview. Each ICAP security vendor will differ with respect to
   request and response URIs, and preview length, so it is important to
   review the vendor's documentation. A zero-length preview length implies
   that data will be streamed to the ICAP service, similar to an HTTP
   100/Expect process, while any positive integer preview length defines the
   amount of data (in bytes) that are transmitted first, before streaming the
   remaining content. The ICAP service in this lab environment does not
   support a complete stream, so requires a modest amount of initial preview.
   In this lab, enter :red:`1048576`.

-  **Service Down Action** - SSLO also natively monitors the load balanced
   pool of security devices. If all pool members fail, SSLO can actively
   bypass this service (**Ignore**), or stop all traffic (**Reset**,
   **Drop**). For this lab, leave it set to :red:`Ignore`.

-  **HTTP Version** - this defines whether SSLO sends HTTP/1.1 or HTTP/1.0
   requests to the ICAP service. The lab's ICAP service supports both.

-  **ICAP Policy** - an ICAP policy is a pre-defined LTM CPM policy that can
   be configured to control access to the ICAP service based on attributes of
   the HTTP request or response. ICAP processing is enabled by default, so an
   ICAP CPM policy can be used to disable the request and/or response ADAPT
   profiles. Leave this :red:`blank (--Select--)`

