Module 6 - Create Outbound Channels for Services
================================================

An inline security device may need to access external resources. For example,
an inline HTTP explicit proxy service would minimally need access to DNS
services, while any security device may need to “phone home” for software and
license updates, and to maintain malware signatures. Inline layer 3 devices,
specifically, default route back to SSLO, so this is the path they would
normally take to reach those external services. However, service-originating
traffic is not “tagged” by SSLO, so cannot natively pass through the SSLO
inspection zone. Therefore, to allow an internal service to reach external
resources, separate service channels can be created that define listeners for
specific source, destination, port and protocol combinations. Service channel
requires an abbreviated L3 Outbound topology workflow.

.. important:: Service-originating traffic cannot pass through the SSLO
   inspection zone, so the L3 Outbound service channel configuration must not
   define SSL and security policy settings.

.. toctree::
   :maxdepth: 1
   :glob:

   lab*
