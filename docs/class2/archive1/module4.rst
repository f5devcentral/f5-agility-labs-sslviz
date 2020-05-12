Handling certificate pinning
================================================

Some organizations have chosen to enhance the protection and integrity of their applications by implementing **Certificate Pinning**. This requires the application developer to configure their native app to trust one (or more) specific certificate(s). When a certificate is pinned, the client will not accept a certificate issued by any entity other than those it has been explicitly configured to trust.

When SSL Orchestrator intercepts encrypted traffic, it issues a new certificate that is signed by a Certificate Authority which clients must trust - typically from their own internal/private CA (in this lab, the issuer is the **f5labs.com** CA). However, this will break applications that have implemented Certificate Pinning since this forged certificate is not trusted by the client. An example of an application that uses Certificate Pinning is **Dropbox**. The native (note: installed client, not web browser) Dropbox client will not connect to Dropbox servers if SSL/TLS interception is enabled.

This lab is designed to demonstrate the impact of Certificate Pinning when SSL Orchestrator intercepts the traffic. You will also learn how to apply a bypass to allow these client applications to function properly (when required by company policy).

.. toctree::
   :maxdepth: 1
   :glob:

   scenario*
   lab*