.. role:: red
.. role:: bred

Lab 3.2: Add DNS and Logging settings
-------------------------------------

Minimally an explicit proxy requires DNS settings. To enable this for the L3
Explicit topology, in the SSLO UI click System Settings.

- **DNS Query Resolution** – select Local Forwarding Nameserver.

- **Local Forwarding Nameserver(s)** – enter 10.30.0.1.

- **[Optional] Logging Level** – select the logging level most appropriate for
  the deployment. Keep in mind, however, that DEBUG logging produces an
  enormous amount of local Syslog traffic and is not recommended when
  processing production traffic flows.

- Click Deploy to commit the changes.

**[Optional] Add explicit proxy authentication**

Enabling explicit proxy authentication in SSLO requires two steps,

- **Create an SWG-Explicit access policy** – explicit proxy authentication is
  defined as an access policy of type SWG-Explicit.

  .. image:: ../images/image23.png

  This policy will typically contain an HTTP 407 Response challenge, and then
  some form of authentication, which could HTTP Basic, NTLM or Kerberos.

  .. image:: ../images/image24.png

- **Create or edit an Explicit Proxy SSLO topology and attach the SWG-Explicit
  access policy** – to attach the SWG-Explicit access policy to SSLO, create or
  edit an Explicit proxy SSLO topology. On the Interception Rules page, select
  this policy under the **Access Profile** option.
