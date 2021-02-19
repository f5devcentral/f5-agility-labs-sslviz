.. role:: red
.. role:: bred

Appendix 1 - Using the 'ntopng' Service for Traffic Analysis
=============================================================

This lab environment contains an additional traffic analysis service, running on the inline L3 service, using the community version of **ntopng**. It is provided here as an additional visual tool for displaying decrypted traffic flows.

.. image:: ../images/appendix1-1.png
   :align: center

Additional information about the NTOPNG utility can be found at:
   - Primary reference: https://www.ntop.org
   - Installation reference: http://packages.ntop.org/apt/


Accessing the ntopng Tool
-------------------------

-  In the UDF UI, select the **Access** drop down selection on the **Service - Inline L3** VM, then select **NTOPNG**. This will open a new browser tab and display the NTOPNG UI.

-  If it prompts for credentials, login as user :red:`admin` with password :red:`ntopng`.

-  Browse internet on the Outbound Client to pass traffic through SSLO to view real-time analysis of traffic through the Inline L3 service.
