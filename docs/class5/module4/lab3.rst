Defining a Service Chain
================================================================================

With inspection services created, we will create a service chain that contains both of these in a specific order.

.. note::
   Service chains and traffic policies are only deployed to a BIG-IP Next instance when associated to an application.


Create a Service Chain
--------------------------------------------------------------------------------

#.	Click **Service Chains** under **SSL Orchestrator** in the left menu.

#.	Click the **Start Creating** button.

#.	Enter ``my-service-chain-lab2`` in the **Name** field

#. Enter ``sc-ngfw-only`` in the **Description** field (optional).

#.	In the **Inspection Services** section, click the **Start Adding** button.

#. Select the previously created inspection service.

.. note::
   Multiple service chains could be created here, but you will only create one for this lab module.

   |

#.	Click the **Save** button to save the service chain configuration.
