.. role:: red
.. role:: bred

Add DNS and Logging settings
------------------------------------


Minimally, an explicit proxy requires DNS settings to be configured. To enable
this navigate to the SSLO Dashboard by selecting
:menuselection:`SSL Orchestrator --> Configuration` on the left menu. Once the
dashboard has loaded, click :guilabel:`System Settings`.

In the DNS Settings section make the following modifications:

-  **DNS Query Resolution** - select :red:`Local Forwarding Nameserver`.

-  **Local Forwarding Nameserver(s)** - enter :red:`10.1.20.1`.

-  **Gateway Configuration** - If using a remote DNS forwarder, that is,
   anything not on a local subnet to the F5 (ex. 8.8.8.8), a route must
   also be configured to allow SSLO to reach this remote DNS. If a
   system gateway route has already been defined, select
   :guilabel:`Default Route` here. Otherwise, select
   :guilabel:`Create New` and enter the local gateway route.
   In this lab that is :red:`10.1.20.1`.

Click :guilabel:`Deploy` to commit the changes.
