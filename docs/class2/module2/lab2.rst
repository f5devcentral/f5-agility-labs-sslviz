.. role:: red
.. role:: bred

Enable NTLM authentication on explicit proxy topology
================================================================================

The **f5labs_explicit** topology does not perform user authentication by default. You will now enable NTLM authentication for all users who connect to the explicit proxy.

-  From the Main menu on the left, select **SSL Orchestrator > Configuration**

-  In the Topology list click on **sslo_f5labs_explicit**. The topology summary screen will appear.

-  Click the edit icon (|pencil|) to the right of **Interception Rule**

   |topology-summary-IR-edit|

-  Select **/Common/f5labs-ntlm-ap** from the **Access Profile** drop down menu


.. image:: ../images/ntlm-access-profile.png
   :alt: Access Profile for NTLM Authentication


-  Click **Save & Next** at the bottom of the screen

|

-  The **Egress Settings** screen will load. Wait a moment for the yellow "Deploy" ribbon to appear. When it does, click the **Deploy** button (see example below).

   |egress-settings-deploy-ribbon|

-  Click **OK** to acknowledge the successful deployment.

.. |topology-summary-IR-edit| image:: ../images/topology-summary-IR-edit.png
   :alt: Edit Interception Rule from Topology Summary

.. |pencil| image:: ../images/pencil.png
   :width: 20px
   :height: 20px
   :alt: Pencil Icon

.. |egress-settings-deploy-ribbon| image:: ../images/egress-settings-deploy-ribbon.png
   :alt: Deploy Ribbon on Egress Settings