.. role:: red
.. role:: bred

Lab 6.1: Create an L3 Outbound service channel through Guided Configuration
---------------------------------------------------------------------------

.. note:: For this lab, the inline proxy service simply needs external DNS
   access to 8.8.8.8 UDP.

- **Configuration review and prerequisites** – take a moment to review the
  topology options and workflow configuration, then click Next.

- **Topology Properties**

  - **Name**: provide some name (ex. "proxy_sc_dns")
  - **Protocol**: UDP
  - **IP Family**: IPv4
  - **Topology**: select L3 Outbound
  - Click Save & Next

- **Services List** – there are no new services to create.

  - Click Save & Next

- **Services Chain List** – there are no new service chains to create.

  - Click Save & Next

- **Security Policy** – service channel traffic cannot pass through the
  inspection services, so the security policy must be empty, with the "All
  Traffic" rule set to Allow, bypass SSL, and with no assigned service chain.

  - Click Save & Next

- **Interception Rule**

  - Select Custom outbound rule type and click Show Advanced Setting (top
    right).

  - **Source Address** – this will be the source address of the inline proxy
    server. The proxy server’s default route is through its outbound
    interface, so the source address in this case will be 198.19.96.136/32.

  - **Destination Address/Mask** – the destination address is the specific
    target service, in this case Google DNS at 8.8.8.8/32.

  - **Port** – this will be port 53 for DNS.

  - **VLANs** – this will be the security service’s outbound-side VLAN, so in
    this case the Proxy_out VLAN.

  - **Protocol Settings (L7 Profile Type)** – select None.

  - **Protocol Settings (L7 Profile)** – select None.

  - Click Save & Next

- **Summary** – the summary page presents an expandable list of all of the
  workflow-configured objects. To expand the details for any given setting,
  click the corresponding arrow icon on the far right. To edit any given
  setting, click the corresponding pencil icon. Clicking the pencil icon will
  send the workflow back to the selected settings page.

  - When satisfied with the defined settings, click Deploy.

- **Test** – to verify the service channel is working, SSH to the proxy service
  and attempt to perform a DNS query to 8.8.8.8,

  dig @8.8.8.8 `www.example.com <http://www.example.com>`__

  Assuming this works, the proxy service can be configured to use this DNS
  service. Additional service channels can be created to provide direct access
  to other applications.

  A service channel works by creating a more specific listener on the
  destination side of the security service, based on some combination of
  source, destination, destination port and protocol (TCP/UDP). This can have
  adverse and unintentional effects if a service channel is defined too
  loosely. For example, if a service channel is simply defined with a
  destination IP (ex. 93.184.216.34), port (443), and protocol (TCP), outbound
  user traffic legitimately trying to get to https://www.example.com will be
  incorrectly subverted through the service channel.
