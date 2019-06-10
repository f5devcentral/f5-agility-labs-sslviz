.. role:: red
.. role:: bred

.. image:: ../images/image19.png

Lab 1.11: Summary
-----------------

The summary page presents an expandable list of all of the workflow-configured
objects. To expand the details for any given setting, click the corresponding
arrow icon on the far right. To edit any given setting, click the corresponding
pencil icon. Clicking the pencil icon will send the workflow back to the
selected settings page.

- When satisfied with the defined settings, click :guilabel:`Deploy`.

.. attention:: Be patient it can take a few minutes to deploy the topology.

Upon successfully deploying the configuration, SSL Orchestrator will now
display a **Dashboard** view:

.. image:: ../images/image20.png

The **Interception Rules** tab shows the listeners that were created per the
selected topology.

.. image:: ../images/image21.png

In the above list:

- The **-in-t-4** listener defines normal TCP IPv4 traffic.

- The **-in-u-4** listener defines normal UDP IPv4 traffic.

- The **-ot-4** listener defines normal non-TCP/non-UDP IPv4 traffic.

- The **-ftp, -ftps, -pop3, -smtp25, -smtp587** listeners create paths for each
  respective protocol.

.. attention:: This completes the configuration of SSL Orchestrator as a
   transparent forward proxy. At this point an internal client should be able
   to browse out to external (Internet) resources, and decrypted traffic will
   flow across the security services.
