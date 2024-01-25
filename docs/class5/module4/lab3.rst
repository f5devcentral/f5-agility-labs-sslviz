Defining a Service Chain
================================================================================

.. note::
   Service chains and traffic policies are only deployed to a BIG-IP Next instance when associated to an application.


Create a Service Chain
--------------------------------------------------------------------------------

With the **Inline L3** inspection service created, you will now create a service chain that contains the service.


#. In the **SSL Orchestrator** menu, click on **Service Chains**.

#. Click the **Start Creating** button to open the **Create Service Chain** panel.

   - Enter ``my-service-chain-lab2`` in the **Name** field

   - Enter ``sc-ngfw-only`` in the **Description** field (optional).


   .. image:: ./images/service-chain-1.png

#. In the **Inspection Services** section, click the **Start Adding** button.

#. Select the previously created inspection service and click **Add to List**.

   .. image:: ./images/service-chain-2.png


#. Click the **Save** button to save the service chain configuration.

   .. image:: ./images/service-chain-3.png

