Lab 2: Create a 1-box Explicit Proxy SSLO
==========================================

An explicit proxy is fundamentally a proxy service that the client is
aware of; and there are a number of facilities by which to get client
traffic to an explicit proxy. The easiest option, and the one used in
this lab, is to manually configure the client browser for explicit proxy
access and point it at the SSL Orchestrator’s explicit proxy ingress
listener. Other options include Proxy Auto-Configuration (PAC) scripts
and Web Proxy Autodiscovery Protocol (WPAD), two techniques often
employed by gateway devices to more intelligently steer traffic through
potentially multiple outbound paths. In this lab you’ll be modifying the
transparent proxy configuration from Lab 1 to support explicit proxy.
All other settings, including security service definitions, service
chains and traffic classifiers, can remain unchanged.

Step 1: Un-deploy the transparent proxy SSLO configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This process will create additional ingress listening services in the
SSL Orchestrator configuration, so it’s important to first un-deploy the
deployed SSLO before moving on.

Step 2: Configure the SSL Orchestrator General Properties
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the General Properties section of the SSL Orchestrator configuration,
make the following modifications:

-  **Which proxy schemes do you want to implement?** – select
   ``Implement explicit proxy only``.

-  **On which VLAN(s) should the explicit proxy listen?** – select the
   client side inbound VLAN.

-  **What IPv4 address and port should the explicit proxy use?** – enter
   an IP address in the client side inbound VLAN subnet, which in this
   case is ``10.20.0.0/24``. So for example, ``10.20.0.150`` and the
   common explicit proxy port ``3128`` or ``8080``.

-  Click the **Finished** button.

Step 3: Save and deploy the configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Click the **Save** button and then the **Deploy** button. This will
create an additional ingress listener on the IPv4 address and port
specified above.

Step 4: Test
~~~~~~~~~~~~

On a browser on the Windows client desktop, change the browser’s proxy
settings to match the IPv4 address and port defined above, and then test
outbound access.

You can also test from cURL using the following command line syntax:

``curl -vk --proxy 10.20.0.150:3128 https://www.bing.com``