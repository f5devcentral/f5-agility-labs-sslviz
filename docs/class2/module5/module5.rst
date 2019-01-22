Lab 4 – Create an SSLO for existing applications
================================================

SSL Orchestrator defines an existing application as a typical reverse proxy LTM
virtual server, performing its own SSL handling and traffic management. The
Existing Application SSLO topology therefore only needs to create the
components that this virtual server can consume, specifically the services,
service chains, and security policy. The Existing Application SSLO workflow
skips SSL management and interception rules, and ultimately produces an
SSLO-type per-request policy that can be attached to an existing LTM virtual
server.

This lab will consist of an abbreviated set of steps, as all of the relevant
objects created in Lab 1 (services, service chains and security policies) will
be fully re-usable here. If any of these objects have not been created, please
review Lab 1 for more detailed configuration instructions.

**Step 1: Review the lab diagram and map out the services and endpoints**

Review the same step in Lab 1 for more details. This lab uses the exact same
environment, so SSL settings, services, service chains and security policy will
be re-used.

**Step 2: Create an LTM application**

For the lab, create a simple LTM application,

- **Create a pool** – use one (or multiple) of the internal webserver IPs and
  select port 80.

   - 10.20.0.90:80

   - 10.20.0.91:80

   - 10.20.0.92:80

- **Create a client SSL profile** – use the wildcard.f5demolabs.com certificate
  and private key.

- **Create an LTM virtual server** – use the following basic settings,

   - **Destination Address/Mask**: 10.30.0.205

   - **Service Port**: 443

   - **HTTP Profile**: http

   - **SSL Profile (Client)**: wildcard.f5demolabs.com SSL profile

   - **VLANs and Tunnels**: outbound VLAN

   - **Source Address Translation**: Auto Map

   - **Pool**: previously-created pool

- **Test access to the LTM virtual server** – the webserver should be
  accessible via HTTPS request to the LTM virtual server.

   - Optionally create a Hosts entry on the client by editing /etc/hosts
     (as root) to point 10.30.0.205 to
     `www.f5demolabs.com <http://www.f5demolabs.com>`__, and test access to
     https://www.f5demolabs.com. The certificate is a wildcard, so any
     \*.f5demolabs.com hostname would also work.

**Step 3: Configure an Existing Application deployment through Guided Configuration**

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

  SSL Orchestrator sends all traffic through an inline layer 3 or HTTP device
  in the same direction – entering through the service’s “inbound” interface.
  It is likely, therefore, that the layer 3 device may not be able to correctly
  route both outbound (forward proxy) and inbound (reverse proxy) traffic at
  the same time. Please see the appendix, “Routing considerations for layer 3
  devices” for more details.

  Minimally remove the built-in “Pinners\_Rule”, edit the “All Traffic” policy
  to add the service chain with the L2 and TAP services (only), and click Save
  & Next.

- **Summary** – the summary page presents an expandable list of all of the
  workflow-configured objects. To expand the details for any given setting,
  click the corresponding arrow icon on the far right. To edit any given
  setting, click the corresponding pencil icon. Clicking the pencil icon will
  send the workflow back to the selected settings page.

   - When satisfied with the defined settings, click Deploy.

**Step 4: Attach the SSLO objects to an existing LTM application**

The Existing Application topology workflow produces a single SSLO per-request
policy. To attach this to the LTM virtual server, edit the virtual server
properties.

- **Access Policy (Access Profile**): attach the single
  “ssloDefault\_accessProfile”.

- **Access Policy (Per-Request Policy)**: attach the existing application
  per-request policy.
