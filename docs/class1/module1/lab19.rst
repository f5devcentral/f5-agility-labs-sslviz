.. role:: red
.. role:: bred

Associate new services to service chains (optional - time permitting)
=========================================================================

In this section, you will associate the newly created services to service chains.

- Return to SSL Orchestrator Guided Configuration.

- Select the :red:`demoL3` topology.

- In the configuration summary, find the row labeled :red:`Service Chain` and click on the pencil at the far right.

- Click on the :red:`ssloSC_all_services` service chain.

- Add all of the newly created services in the :red:`Services Available` column to the :red:`Selected Service Chain Order` column.

- Click :red:`Save`.

- Click :red:`OK` on the :red:`Continue Save?` confirmation.

- Check :red:`Add` to add a new service chain.

- Enter a name such as :red:`L2_services`.

.. note:: Guided configuration automatically adds a prefix to object names.  The complete name in this instance will be :red:`ssloSC_L2_services`.

- Move the :red:`FireEye` and :red:`TAP services` from the :red:`Services Available` column to the :red:`Selected Service Chain Order` column.

- Click :red:`Save`.

.. image:: ../images/module1-21.png
   :scale: 50 %
   :align: center

The **Service Chains** have now been configured.

- Pause for a few seconds and the yellow banner shown below will appear at the very top of the :red:`Interception Rule` settings.

.. image:: ../images/module1-22.png
   :scale: 50 %
   :align: center

- Click :red:`Deploy`.

In the next section, you will test the newly created TAP service.