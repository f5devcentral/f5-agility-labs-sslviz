.. role:: red
.. role:: bred

Step 2: Configure an Explicit Proxy deployment through Guided Configuration
---------------------------------------------------------------------------

In the SSL Orchestrator dashboard view, select the :guilabel:`Topologies` tab
(bottom) and click :guilabel:`Add`.

- **Configuration review and prerequisites** - take a moment to review the
  topology options and workflow configuration, then click :guilabel:`Next`.

- **Topology Properties**

  - **Name**: provide some name (ex. ":red:`lab3_explicit`")

  - **Protocol**: :red:`TCP`

  - **IP Family**: :red:`IPv4`

  - **Topology**: select :red:`L3 Explicit Proxy`

  - Click :guilabel:`Save & Next`

- **SSL Configurations** - the existing outbound SSL settings from Lab 1 can be
  re-used here.

  - Select :guilabel:`Use Existing`, and select the existing
    :red:`lab1_outbound` SSL profile.

  - Click :guilabel:`Save & Next`

  - Click :guilabel:`OK` to acknowledge the profile warning.

    .. warning:: Whenever repurposing a topology setting, a warning will
       appear: “There are other configuration items that are referencing this
       item. Editing this item will affect the referencing ones mentioned
       below”. Click OK to acknowledge.

- **Services List** - there are no new services to create.

  - Click :guilabel:`Save & Next`

- **Service Chain List** - there are no new service chains to create.

  - Click :guilabel:`Save & Next`

- **Security Policy** - the existing outbound Security Policy from Lab 1 can be
  re-used here.

  - **Type**: Select :guilabel:`Use Existing` and select the existing
    outbound settings.

  - **Proxy Connect**: this option is only available for the outbound
    explicit proxy topology and defines an upstream proxy chain. With
    this setting enabled, SSLO can egress to an upstream (external)
    explicit proxy gateway. An example of this might be a cloud
    gateway solution. Select a pool that points to the upstream
    explicit proxy, and optionally any (HTTP Basic) credentials needed
    to access this proxy. For this lab, leave this setting disabled.

  - Click :guilabel:`Save & Next`

- **Interception Rule** - an explicit proxy requires a unique IP address and
  port listener.

  - **IPV4 Address**: :red:`10.1.10.150`

  - **Port**: :red:`3128`

  - **Access Profile**: if enabling explicit proxy authentication, select an
    existing SWG-Explicit access profile here. For this lab, leave it set to
    :red:`None`.

  - **VLANs**: select :red:`client-vlan` and move it to the right column

  - Click :guilabel:`Save & Next`

- **Egress Setting** - traffic egress settings are now defined per-topology and
  manage both the gateway route and outbound SNAT settings.

  - **Manage SNAT Settings** - enables per-topology instance SNAT settings. For
    this lab, select :red:`Auto Map`.

  - **Gateways** - enables per-topology instance gateway routing. Options are
    to use the system default route, to use an existing gateway pool, or to
    create a new gateway. For this lab, select :red:`Use Existing Gateway
    Pool`, then select the ":red:`-ex-pool-4`" gateway pool.

  - Click :guilabel:`Save & Next`

- **Log Settings** - log settings are defined per-topology. In
  environments where multiple topologies are deployed, this can help to
  streamline troubleshooting by reducing debug logging to the affected
  topology.

- **Summary** - the summary page presents an expandable list of all of the
  workflow-configured objects. To expand the details for any given setting,
  click the corresponding arrow icon on the far right. To edit any given
  setting, click the corresponding :guilabel:`pencil icon`. Clicking the
  :guilabel:`pencil icon` will send the workflow back to the selected
  settings page.

- When satisfied with the defined settings, click :guilabel:`Deploy`.
