Working with pinned certificate sites
================================================

Some organizations have chosen to enhance the protection of their applications
by using a process called **Certificate Pinning**. This requires that the application
developer configures their native client to trust one (or more) specific certificate(s). When a
certificate is pinned, the client will not accept a certificate issued by any other entity.

When SSL Orchestrator intercepts encrypted traffic, it issues a new certificate that is
signed by a Certificate Authority which clients must trust (in this lab, the issuer is
the **f5labs.com** CA). However, this will break applications that use Certificate
Pinning since this forged certificate is not trusted by the client. One application that
uses Certificate Pinning is **Dropbox**. The native (note: installed client, not web
browser) Dropbox client will not connect to Dropbox servers if SSL/TLS interception is enabled.

This lab is designed to demonstrate the impact of Certificate Pinning
when SSL Orchestrator intercepts the traffic. You will also learn how to apply a bypass
to allow these client applications to function properly (when required by company policy).

.. toctree::
   :maxdepth: 1
   :glob:

   scenario*
   lab*
