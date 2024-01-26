Defining a Service Chain
================================================================================

.. note::
   Service chains and traffic policies are only deployed to a BIG-IP Next instance when associated to an application.


Create a Service Chain
--------------------------------------------------------------------------------

With the ICAP inspection service created, you will create a new service chain that contains this inspection service. If continuing from the previous lab module, you should also be able to add the **Inline L3** service.


#. In the **SSL Orchestrator** menu, click on **Service Chains**.

#. Click the **+ Create** in the top right to open the **Create Service Chain** panel.

   - Enter ``my-service-chain-lab3`` in the **Name** field.

   - Enter ``L3 and ICAP service chain`` in the **Description** field (optional).


   .. image:: ./images/service-chain-1.png


#. In the **Inspection Services** section, click the **Start Adding** button.

#. Select the both of the previously created inspection services and then click **Add to List**. Once applied, they can be re-ordered as needed.

   .. image:: ./images/service-chain-2.png


#. Click the **Save** button to save the service chain configuration.

   .. image:: ./images/service-chain-3.png


.. todo:: add screenshots
