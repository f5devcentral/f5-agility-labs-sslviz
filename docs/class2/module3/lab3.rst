.. role:: red
.. role:: bred

Lab 3.3: [Optional] Add explicit proxy authentication
-----------------------------------------------------

Enabling explicit proxy authentication in SSLO requires two steps:

#. **Create an SWG-Explicit access policy** – explicit proxy authentication is
   defined as an access policy of type SWG-Explicit.

   .. image:: ../images/image23.png

   This policy will typically contain an HTTP 407 Response challenge, and then
   some form of authentication, which could HTTP Basic, NTLM or Kerberos.

   .. image:: ../images/image24.png

#. **Create or edit an Explicit Proxy SSLO topology and attach the SWG-Explicit
   access policy** – to attach the SWG-Explicit access policy to SSLO, create
   or edit an Explicit proxy SSLO topology. On the Interception Rules page,
   select this policy under the **Access Profile** option.
