Defining a Service Chain
================================================================================

.. note::
   Service chains and traffic policies are only deployed to a BIG-IP Next instance when associated to an application.


Create a Service Chain
--------------------------------------------------------------------------------

With the **ICAP** inspection service created, you will create a new service chain that contains that service, along with the **Inline L3** service that was created in the previous module.


#. In the **SSL Orchestrator** menu, click on **Service Chains**.

#. Click **+ Create** in the top right to add a new **Service Chain**.

   .. image:: ./images/gwm-sc-1.png

#. In the **Create Service Chain** panel:

   - Enter ``my-service-chain-lab3`` in the **Name** field.
   - Enter ``L3 and ICAP service chain`` in the **Description** field (optional).


#. In the **Inspection Services** section, click the **Start Adding** button.

#. Select the both of the previously created inspection services and then click **Add to List**. 

   .. hint::
      Scroll down if you don't see both services.

   .. image:: ./images/gwm-sc-2.png


#. Click the **Save** button to save the service chain configuration.

   .. image:: ./images/gwm-sc-3.png

   .. note::
      If needed, the ordering of the **Inspection Services** can be changed by selecting the checkbox beside a service, and then clicking on the **up-arrow** or **down-arrow** buttons.


The new service chain will appear in the list.

   .. image:: ./images/gwm-sc-4.png
