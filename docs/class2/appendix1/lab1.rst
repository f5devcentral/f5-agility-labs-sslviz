.. role:: red
.. role:: bred

Bypass Decryption for Office 365 Traffic
============================================

In this step, create a new **Security Policy** rule to bypass SSL decryption and all services for the custom Office 365 URL category that was created by the Office 365 URL Cateogry automation script.

-  Navigate to the **Security Policy** tab and edit the rules for your existing Topology.

-  Click :red:`Add` to create a new rule.

-  **Name** - provide a unique name for the rule (ex. ":red:`O365_bypass`").

-  **Conditions** - Select **Category Lookup (All)** from the drop-down list and then add 
   the :red:`Office_365_Managed_All` URL category. Start typing the category name to narrow the list.

   .. NOTE::
      The **Category Lookup (All)** condition provides categorization for
      TLS SNI, HTTP Connect and HTTP Host information.

   .. image:: ../images/appendix1-1-1.png
      :align: center

-  **Action** - select :red:`Allow`.

-  **SSL Forward Proxy Action** - select :red:`Bypass`.

-  **Service Chain** - select :red:`None`.

-  Click :red:`OK`.

   .. image:: ../images/appendix1-1-2.png
      :align: center


-  Click :red:`Save & Next` to continue to the next stage.
