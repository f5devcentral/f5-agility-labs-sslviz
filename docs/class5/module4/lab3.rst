Defining a Service Chain
================================================================================

.. note::
   Service chains and traffic policies are only deployed to a BIG-IP Next instance when associated to an application.


Create a Service Chain
--------------------------------------------------------------------------------

With the **Inline L3** inspection service created, you will now create a service chain that contains the service.


#. In the **SSL Orchestrator** menu, click on **Service Chains**.

   .. image:: ./images/service-chain-1.png




#. Click the **Start Creating** button to open the **Create Service Chain** panel.

   - Enter ``my-service-chain-lab2`` in the **Name** field

   - Enter ``sc-ngfw-only`` in the **Description** field (optional).


#. In the **Inspection Services** section, click the **Start Adding** button.

   .. image:: ./images/service-chain-1.png


#. Select the previously created inspection service and click **Add to List**.

   .. image:: ./images/service-chain-2a.png


#. Click the **Save** button to save the service chain configuration and close the panel.

   .. image:: ./images/service-chain-2b.png


The new service chain will appear in the list.

   .. image:: ./images/service-chain-3.png
