LAB 2 – Working with Pinned certificate sites
=============================================

A few companies have chosen to enhance the protection of their SSL
   websites by adding a process called as **Pinning**. 

Pinning requires a client that is controlled by the same company as well. When a
   certificate is pinned, the native client will not accept a certificate
   issued by any other entity. By intercepting traffic, we are issuing a
   certificate on the fly that is issued by **f5labs.com** in this lab.

Since this certificate is not issued by the entity that is trusted by
   the native client, the client will not allow further function. A great
   example is Dropbox, with its Dropbox native client (not visiting the
   website through the browser).

This lab is designed to demonstrate the impact of pinned certificates
   with SSLo Orchestrator intercepting the traffic and how-to workaround to
   make sure that these clients are enabled to work if required by company
   policy.

.. toctree::
   :maxdepth: 1
   :glob:

   scenario*
   step*
