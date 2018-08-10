Lab 1.7: Outbound Interception Rules
------------------------------------

Task 1 - Interception Rules
~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Login to the BIG-IP with Firefox

2. Navigate to :menuselection:`SSL Orchestrator --> Deployment --> Interception Rules` and click:

   |image29|

3. Click :guilabel:`Install Default Rules...`

   |image30|

4. Under :guilabel:`Proxy Settings`, configure these options:

   .. list-table::
      :widths: 50 50
      :header-rows: 1
      :stub-columns: 1


      * - **Property**
        - **Value**
      * - Proxy Scheme
        - Transparent and Explicit
      * - Proxy Server : Port
        - 10.20.0.150 : 3128

   |image31|

5. Under :menuselection:`Security --> SSL`, select :guilabel:`Create New`. This will redirect to a separate page for configuring SSL settings.

   |image32|

6. Name the configuration `ssloT_ob_ssl`

   |image33|

7. In the :guilabel:`Client` section, for :guilabel:`Certificate Key Chains`, select `default.crt` and `default.key`, and then click :guilabel:`Add`

   |image35|

8. Under :guilabel:`CA Certificate Key Chains`, select `subca.f5demolabs.com.cer` and `subca.f5demolabs.com.key`, and then click :guilabel:`Add`.

   |image36|

9. In the :guilabel:`Server` section, select `ca-bundle.crt` for :guilabel:`Trusted Certificate Authority`. Leave all other settings at the defaults. Click :guilabel:`Finished`.

   |image37|

#. The screen should have returned to the original :guilabel:`Install Default Rules` page. Under the :guilabel:`Security` section, from the :guilabel:`Per Request Policy` drop-down select :guilabel:`Create New`

   |image38|

#. Name the policy `ssloP_ob_pol`

   |image39|

#. Under :guilabel:`TCP Service Chain`, add and order the available services to both the :guilabel:`Intercept Chain` and :guilabel:`Non Intercept Chain`:

   |image40|

#. Repeat step (12) for :guilabel:`UDP Service Chain`

#. Click :guilabel:`Finish`.

#. Under :menuselection:`Ingress Network --> VLANs`, choose `/Common/client-net` from the :guilabel:`Available VLANs` and add to the :guilabel:`Selected` section.

   |image41|

#. Click :guilabel:`Finish`.

.. |image29| image:: /_static/image25.png
   :width: 6.29167in
   :height: 1.34722in
.. |image30| image:: /_static/image26.png
   :width: 6.50000in
   :height: 0.71111in
.. |image31| image:: /_static/image27.png
   :width: 6.50000in
   :height: 2.03125in
.. |image32| image:: /_static/image28.png
   :width: 5.86111in
   :height: 1.08333in
.. |image33| image:: /_static/image29.png
   :width: 6.50000in
   :height: 1.38750in
.. |image34| image:: /_static/image30.png
   :width: 5.72222in
   :height: 1.68056in
.. |image35| image:: /_static/image31.png
   :width: 6.50000in
   :height: 1.57153in
.. |image36| image:: /_static/image32.png
   :width: 6.50000in
   :height: 2.06667in
.. |image37| image:: /_static/image33.png
   :width: 6.50000in
   :height: 2.72292in
.. |image38| image:: /_static/image34.png
   :width: 6.50000in
   :height: 1.66528in
.. |image39| image:: /_static/image35.png
   :width: 6.37500in
   :height: 0.94444in
.. |image40| image:: /_static/image36.png
   :width: 6.50000in
   :height: 3.63472in
.. |image41| image:: /_static/image37.png
   :width: 6.50000in
   :height: 1.26528in

