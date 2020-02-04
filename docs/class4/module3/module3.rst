Module 3 - Create an Explicit Forward Proxy SSLO
================================================

SSL Orchestrator creates discreet, non-overlapping interception rules
(listeners) based on the selected topology. For example, the explicit forward
proxy workflow minimally creates an explicit proxy listener and relying
transparent proxy listener attached to the explicit proxy tunnel. If a separate
transparent proxy workflow was created, the resulting listener would not
conflict with or overlap the existing transparent proxy listener. Therefore,
assuming a transparent forward proxy already exists from Module 1, the
following workflow will create a separate set of non-overlapping listeners to
satisfy an explicit forward proxy use case.

.. note:: This module consists of an abbreviated set of steps, as some of
   the objects created in Module 1 (SSL settings, services, service chains and
   security policies) are re\-usable here. If any of these objects have not
   been created, please review
   `Module 1 - Create a Transparent Forward Procy SSLO
   <../module1/module1.html>`_ for more detailed configuration instructions.

.. toctree::
   :maxdepth: 2
   :glob:

   lab*
