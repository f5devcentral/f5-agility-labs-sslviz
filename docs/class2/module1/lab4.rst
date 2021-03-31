.. role:: red
.. role:: bred

Create a new "Cisco Firepower" Service Chain
================================================================================

You now need to create a new Service Chain containing only the Cisco Firepower TAP service.

-  On the **Service Chain List** screen click the **Add** button to create a new Service Chain

-  On the **Service Chain Properties** screen enter the following values:

   -  **Name -** enter ``CiscoFP_TAP`` as the service chain name

   -  **Description -** enter ``Cisco Firepower TAP only`` as the description.

   -  **Services -** select the Cisco Firepower service (**ssloS_CiscoFP**) under **Services Available** and click on the right arrow to move it to the **Selected Service Chain Order** side.

-  Click the **Save** button


.. image:: ../images/ciscofp-4.png
   :alt: Cisco Firepower Service Configuration

|

-  You will return to the **Service Chain List** where you should see three Service Chains.

   .. image:: ../images/new-service-chain-list.png
      :alt: Updated Service Chain List

-  Click the **Save & Next** button

-  Click the **Deploy** button. This action will take a moment. Verify that the deployment was successful with no errors.

-  When successfully deployed, the following pop-up should appear:

   .. image:: ../images/successful_deploy.png
      :alt: Successful Deployment

-  Click the **OK** button to return to the SSL Orchestrator Configuration screen.

