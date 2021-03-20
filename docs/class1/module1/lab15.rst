.. role:: red
.. role:: bred

Configure and Test Selective Decryption by URL Category
=======================================================

This test will demonstrate that:

- Traffic to select URLs (Financial and Medical) are no longer decrypted.

Enable SSL bypass
------------------ 

Return to your SSL Orchestrator configuration browser tab on your local workstation. 
From the left-hand menu, navigate to :red:`SSL Orchestrator > Configuration`. 
Click on the :red:`sslo_L3_out` topology. In the list presented in black text, 
find the row labeled :red:`Security Policy`. Click on the pencil on the right.  

Rule list before URL-based selective decryption

- Click Add

   .. image:: ../images/addurlf.png

Create a an additional rule for "Financial Data and
Services" and "Health and Medicine" URL categories.

-  Click :red:`Add` to create a new rule.

-  **Name** - provide a unique name for the rule (ex. ":red:`urlf_bypass`").

-  **Conditions** - Select **Category Lookup (All)** from the drop-down list
   and then add the :red:`Financial Data and Services` and :red:`Health and Medicine`
   URL categories. Start typing the category name to narrow the list.

   .. NOTE::
      The **Category Lookup (All)** condition provides categorization for
      TLS SNI, HTTP Connect and HTTP Host information.

-  **Action** - select :red:`Allow`.

-  **SSL Forward Proxy Action** - select :red:`Intercept`.

-  **Service Chain** - select the :red:`all_services` service chain.

-  Click :red:`OK`.

   .. image:: ../images/urlfdetails.png

Rule list after URL-based selective decryption
   .. image:: ../images/updatedpolicylist.png

.. image:: ../images/reentrantdeploy.png
   :scale: 50 %
   :align: center

Financial and Medical site test
---------------------------------

Return to your Ubuntu client RDP session.
Open a web browser (e.g., Firefox, Chromium) on the outbound client system and
navigate to https://bcbs.com. Once the site opens in the browser, 
check the server certificate of the site and notice that it is still issued 
by the local CA configured in SSLO. This is because even though we created a rule
for financial and medical sites, the SSL Forward Proxy Action is set to Intercept.

   .. image:: ../images/bcbsafter.png

   .. image:: ../images/wellsafter.png

Reconfiguring the SSLO Security Policy to bypass Financial and Medical sites
============================================================================

Return to your SSL Orchestrator configuration browser tab on your local workstation. 
From the left-hand menu, navigate to :red:`SSL Orchestrator > Configuration`. 
Click on the :red:`sslo_L3_out` topology. In the list presented in black text, 
find the row labeled :red:`Security Policy`. Click on the pencil on the right. 
In the security policy, find the rule named :red:`urlf_bypass` and click on the pencil
on the right.  

-  **SSL Forward Proxy Action** - select the :red:`bypass` option.
