.. role:: red
.. role:: bred

Lab 4.2: Configure an Existing Application deployment through Guided Configuration
----------------------------------------------------------------------------------

- **Configuration review and prerequisites** – take a moment to review the
  topology options and workflow configuration, then click Next.

- **Topology Properties**

  - **Name**: provide some name (ex. “existing\_app\_1”)

  - **IP Family**: IPv4

  - **Topology**: select Existing Application

  - Click Save & Next

- **Services List** – there are no new services to create.

  - Click Save & Next

- **Services Chain List** – there are no new service chains to create.

  - Click Save & Next

- **Security Policy** – the security policy requirements are specific to each
  organization, though an inbound security policy would likely be less complex
  than an outbound policy.

  .. note:: SSL Orchestrator sends all traffic through an inline layer 3 or
     HTTP device in the same direction – entering through the service’s
     “inbound” interface. It is likely, therefore, that the layer 3 device may
     not be able to correctly route both outbound (forward proxy) and inbound
     (reverse proxy) traffic at the same time. Please see the appendix,
     “Routing considerations for layer 3 devices” for more details.

  Minimally remove the built-in “Pinners\_Rule”, edit the “All Traffic” policy
  to add the service chain with the L2 and TAP services (only), and click Save
  & Next.

- **Summary** – the summary page presents an expandable list of all of the
  workflow-configured objects. To expand the details for any given setting,
  click the corresponding arrow icon on the far right. To edit any given
  setting, click the corresponding pencil icon. Clicking the pencil icon will
  send the workflow back to the selected settings page.

  - When satisfied with the defined settings, click Deploy.
