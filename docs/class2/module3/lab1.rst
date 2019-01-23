.. role:: red
.. role:: bred

Lab 3.1: Configure an Explicit Proxy deployment through Guided Configuration
----------------------------------------------------------------------------

.. note:: Review the same step in Module 1 for more details. This lab uses the
   exact same environment, so SSL settings, services, service chains and
   security policy will be re-used.

- **Configuration review and prerequisites** - take a moment to review the
  topology options and workflow configuration, then click :red:`Next`.

- **Topology Properties**

  - **Name**: provide some name (ex. ":red:`sslo_explicit`")

  - **Protocol**: :red:`TCP`

  - **IP Family**: :red:`IPv4`

  - **Topology**: select :red:`L3 Explicit Proxy`

  - Click :red:`Save & Next`

- **SSL Configurations** - the existing outbound SSL settings from Lab 1 can be
  re-used here.

  - **SSL Profile**: :red:`Use Existing`, select existing outbound SSL
    settings.

  - Click :red:`Save & Next`

    .. note:: Whenever repurposing a topology setting, a warning will appear,
       "There are other configuration items that are referencing this item.
       Editing this item will affect the referencing ones mentioned below".
       Click OK to acknowledge.

- **Services List** - there are no new services to create.

  - Click :red:`Save & Next`

- **Service Chain List** - there are no new service chains to create.

  - Click :red:`Save & Next`

- **Security Policy** - the existing outbound Security Policy from Lab 1 can be
  re-used here.

  - **Type**: :red:`Use Existing`, select existing outbound SSL settings.

  - Click :red:`Save & Next`

- **Interception Rule** - an explicit proxy requires a unique IP address and
  port listener.

  - **IPV4 Address**: :red:`10.20.0.150`

  - **Port**: :red:`3128`

  - **Access Profile**: if enabling explicit proxy authentication, select an
    existing SWG-Explicit access profile here.

  - **VLANs**: :red:`client-net`

  - Click :red:`Save & Next`

- **Egress Setting** - traffic egress settings are now defined per-topology and
  manage both the gateway route and outbound SNAT settings.

  - **Manage SNAT Settings** - enables per-topology instance SNAT settings. For
    this lab, select :red:`Auto Map`.

  - **Gateways** - enables per-topology instance gateway routing. Options are
    to use the system default route, to use an existing gateway pool, or to
    create a new gateway. For this lab, select :red:`Use Existing Gateway
    Pool`, then select the ":red:`-ex-pool-4`" gateway pool.

  - Click :red:`Save & Next`

- **Summary** - the summary page presents an expandable list of all of the
  workflow-configured objects. To expand the details for any given setting,
  click the corresponding arrow icon on the far right. To edit any given
  setting, click the corresponding pencil icon. Clicking the pencil icon will
  send the workflow back to the selected settings page.

  - When satisfied with the defined settings, click :red:`Deploy`.

- **Testing** - configure the browser to use :red:`10.20.0.150:3128` for
  explicit proxy access. An explicit proxy request test can also be done using
  command-line cURL:

  .. code-block:: bash

     curl -vk –proxy 10.20.0.150:3128 https://www.example.com
