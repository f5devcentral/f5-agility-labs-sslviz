.. role:: red
.. role:: bred

Lab 3.1: Configure an explicit proxy SSLO deployment through Guided Configuration
---------------------------------------------------------------------------------

.. note:: Review the same step in Module 1 for more details. This lab uses the
   exact same environment, so SSL settings, services, service chains and
   security policy will be re-used.

- **Configuration review and prerequisites** – take a moment to review the
  topology options and workflow configuration, then click Next.

- **Topology Properties**

  - **Name**: provide some name (ex. "sslo\_explicit")

  - **Protocol**: TCP

  - **IP Family**: IPv4

  - **Topology**: select L3 Explicit Proxy

  - Click Save & Next

- **SSL Configurations** – the existing outbound SSL settings from Lab 1 can be
  re-used here.

  - **SSL Profile**: Use Existing, select existing outbound SSL settings.

  - Click Save & Next

    Whenever repurposing a topology setting, a warning will appear, "There are
    other configuration items that are referencing this item. Editing this
    item will affect the referencing ones mentioned below". Click OK to
    acknowledge.

- **Services List** – there are no new services to create.

  - Click Save & Next

- **Service Chain List** – there are no new service chains to create.

  - Click Save & Next

- **Security Policy** – the existing outbound Security Policy from Lab 1 can be
  re-used here.

  - **Type**: Use Existing, select existing outbound SSL settings.

  - Click Save & Next

- **Interception Rule** – an explicit proxy requires a unique IP address and
  port listener.

  - **IPV4 Address**: 10.20.0.150

  - **Port**: 3128

  - **Access Profile**: if enabling explicit proxy authentication, select an
    existing SWG-Explicit access profile here.

  - **VLANs**: client-net

  - Click Save & Next

- **Egress Setting** – traffic egress settings are now defined per-topology and
  manage both the gateway route and outbound SNAT settings.

- **Manage SNAT Settings** – enables per-topology instance SNAT settings. For
  this lab, select Auto Map.

- **Gateways** – enables per-topology instance gateway routing. Options are to
  use the system default route, to use an existing gateway pool, or to create a
  new gateway. For this lab, select Use Existing Gateway Pool, then select the
  "-ex-pool-4" gateway pool.

  - Click Save & Next

- **Summary** – the summary page presents an expandable list of all of the
  workflow-configured objects. To expand the details for any given setting,
  click the corresponding arrow icon on the far right. To edit any given
  setting, click the corresponding pencil icon. Clicking the pencil icon will
  send the workflow back to the selected settings page.

  - When satisfied with the defined settings, click Deploy.

- **Testing** – configure the browser to use 10.20.0.150:3128 for explicit
  proxy access. An explicit proxy request test can also be done using
  command-line cURL:

  curl -vk –proxy 10.20.0.150:3128 https://www.example.com
