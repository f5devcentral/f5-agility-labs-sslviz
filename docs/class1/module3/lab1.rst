Lab 3.1: Reviewing the Policies
-------------------------------

Task 1 - View the Per-Request Policies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Login to the BIG-IP with Firefox

#. Navigate to :menuselection:`SSL Orchestrator --> Policies --> Access Per-Request Policies`

   |image57|

#. Click the plus sign next to :guilabel:`Show all` for the `ssloP_outbound_ssl` row

#. Select the `ssloP_outbound_ssl_prpTcp` Per-Request policy

   |image58|

#. Review the general flow from categorization through Intercept policy to Service Chain

   |image59|

#. Expand the :guilabel:`Macro: Categorization` macro by clicking on
   :guilabel:`Categorization` in the boxed area or the plus symbol in
   the macro section.

   |image60|

#. Explore the :guilabel:`SSL Check` advanced Action Properties

   |image61|
   |image62|

#. Expand the :guilabel:`SSL Intercept Policy` macro. Notice that the
   `Not Intercepted` and `Intercepted` terminal endings differ based
   on the category and setting interception.

   |image63|

#. Explore the :guilabel:`Category Branching` Action Property

   |image64|

#. Expand the macros :guilabel:`Service Chain Intercepted` and
   :guilabel:`Service Chain Not Intercepted`

   |image65|

#. Explore the Action Properties in the Service Chains and notice the
   :guilabel:`Connector Profiles`

   |image66|

Task 2 - Modify the Intercept Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Expand the macro :guilabel:`SSL Intercept Policy` and click the
   :guilabel:`Intercepted` terminal ending

   |image67|

#. Select the :guilabel:`Not Intercepted` radio button, then
   :guilabel:`Save`

   |image68|

   .. NOTE::
      Notice that now all traffic is bypassed and therefore **not**
      decrypted

      |image69|

#. Repeat the test from `Lab 1.8 <../module1/lab8.html>`_ and notice that traffic
   is not decrypted. Notice that this had the impact of all traffic bypassing
   inspection zone.

#. Undo the change by setting the terminal ending back to :guilabel:`Intercepted`
   and repeat test.

Task 3 - Modify Service Chain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Expand the macro named :guilabel:`Service Chain Not Intercepted` and
   remove the :guilabel:`HTTP Service` node by selecting the :guilabel:`X` in the
   corner. The :guilabel:`X` will turn red when you hover over it.

   |image70|

#. Click the :guilabel:`Delete` button in the Item delete confirmation
   dialogue box

   |image71|

#. View your results

   |image72|

#. Add the :guilabel:`HTTP Service` node back by selecting the plus key
   between :guilabel:`TAP` and :guilabel:`L3` services

   |image73|

#. Select the :guilabel:`Traffic Management` tab, then the
   :guilabel:`Service Connect` item and click :guilabel:`Add Item`

   |image74|

#. Change the :guilabel:`Name` to `HTTP Service`, choose the HTTP
   Service item from the :guilabel:`Connector Profile` drop down menu
   named `/Common/ssloS_HTTP_server.app/ssloS_HTTP_service-t-connector`
   and then click :guilabel:`Save` at the bottom

   |image75|

.. |image57| image:: /_static/image52.png
   :width: 6.50000in
   :height: 1.43472in
.. |image58| image:: /_static/image53.png
   :width: 6.50000in
   :height: 1.64097in
.. |image59| image:: /_static/image54.png
   :width: 6.50000in
   :height: 2.56806in
.. |image60| image:: /_static/image54.png
   :width: 6.50000in
   :height: 2.56806in
.. |image61| image:: /_static/image55.png
   :width: 6.50000in
   :height: 1.48056in
.. |image62| image:: /_static/image56.png
   :width: 6.50000in
   :height: 5.24375in
.. |image63| image:: /_static/image57.png
   :width: 6.50000in
   :height: 3.73611in
.. |image64| image:: /_static/image58.png
   :width: 6.50000in
   :height: 4.60625in
.. |image65| image:: /_static/image59.png
   :width: 6.50000in
   :height: 4.38333in
.. |image66| image:: /_static/image60.png
   :width: 6.50000in
   :height: 5.72500in
.. |image67| image:: /_static/image61.png
   :width: 6.50000in
   :height: 1.32639in
.. |image68| image:: /_static/image62.png
   :width: 4.54167in
   :height: 5.73958in
.. |image69| image:: /_static/image63.png
   :width: 6.50000in
   :height: 1.25625in
.. |image70| image:: /_static/image64.png
   :width: 6.50000in
   :height: 0.81528in
.. |image71| image:: /_static/image65.png
   :width: 5.47917in
   :height: 2.32292in
.. |image72| image:: /_static/image66.png
   :width: 6.50000in
   :height: 1.17153in
.. |image73| image:: /_static/image66.png
   :width: 6.50000in
   :height: 1.17153in
.. |image74| image:: /_static/image67.png
   :width: 6.50000in
   :height: 5.74375in
.. |image75| image:: /_static/image68.png
   :width: 6.50000in
   :height: 7.42986in

