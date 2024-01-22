Defining a Service Chain
================================================================================

Create a Service Chain
--------------------------------------------------------------------------------

With the TAP inspection service created, you will create a service chain that contains this service.

.. note::
   Service chains and traffic policies are only deployed to a BIG-IP Next instance when associated to an application.

.. note::
   If continuing from the previous lab module, you should already an **Inline L3** and an **ICAP** inspection service. You can optionally add these to your new service chain.

#. Click **Service Chains** under **SSL Orchestrator** in the left menu.

#. Click the **Start Creating** button.

#. Enter ``my-service-chain-lab3`` in the **Name** field.

#. Enter ``service chain for lab 3`` in the **Description** field.

#. In the **Inspection Services** section, click the **Start Adding** button and
   select both of the previously created inspection services. Once applied, they
   can be re-ordered as required. Note that multiple service chains can also be
   created, as required.

#. Click the **Save** button to save the new service chain configuration.
