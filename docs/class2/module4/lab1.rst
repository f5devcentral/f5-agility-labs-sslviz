.. role:: red
.. role:: bred

Lab 4.1: Create an LTM application
----------------------------------

.. note:: Review the lab diagram and map out the services and endpoints.
   This lab uses the exact same environment. SSL settings, services, service
   chains and security policy will be re-used.

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
