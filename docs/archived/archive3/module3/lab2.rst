.. role:: red
.. role:: bred

Lab 3.2: [Optional] Add explicit proxy authentication
-----------------------------------------------------

Enabling explicit proxy authentication in SSLO requires two steps:

#. **Create an SWG-Explicit access policy** - explicit proxy authentication is
   defined as an access policy of type SWG-Explicit.

   .. image:: ../images/image23.png

   This policy will typically contain an HTTP 407 Response challenge, and then
   some form of authentication, which could be HTTP Basic, NTLM or Kerberos.

   .. image:: ../images/image24.png

#. **Apply the new access policy to an Explicit Proxy topology** - attach the
   SWG-Explicit access policy by creating or editing an Explicit proxy SSLO
   topology. On the Interception Rules page, select the new policy under the
   :red:`Access Profile` option.
