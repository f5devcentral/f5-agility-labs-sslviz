Lab 1.1: Deployment Settings
---------------------------------

Task 1 - Create Outbound SSLO Deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this lab, we will explore the settings required to deploy Outbound
SSLO. First, we will cover the :guilabel:`General Properties` of the deployment. We
will then configure the :guilabel:`Egress`, :guilabel:`DNS`, and :guilabel:`Logging` settings.

.. NOTE::
    This guide may require you to Copy/Paste information from the
    guide to your jumphost. To make this easier you can open a
    copy of the guide by using the **Lab Guide** bookmark in Firefox.

1. Open Firefox and navigate to the following bookmark: :guilabel:`f5 BIG-IP`.
   Bypass any SSL errors that appear and ensure you see the
   login screen for each bookmark:

   |image3|

.. WARNING::
  
    We are using a self-signed certificate in this lab. In your
    environment you must make sure that you use certificates issued by
    your certificate authority for both production and lab equipment.
    Not doing so would make it possible for an attacker to do a
    man-in-the-middle attack and allow him the ability to steal
    passwords and tokens.

2. Authenticate to the interface using the default credentials as
   defined in the lab topology.
   

3. Navigate to :menuselection:`SSL Orchestrator --> Deployment --> Deployment Settings` and
   click:

   |image4|

4. In :guilabel:`General Properties` change the :guilabel:`Deployment Name` to `sslo_agility_lab`

   |image5|

5. In the :guilabel:`Egress Configuration` section set the following:

   a. :guilabel:`Manage SNAT Settings` --> `Auto Map`
   b. :guilabel:`Gateways` --> `Specific gateways`
   c. Add IPv4 gateway address `10.30.0.1`

   |image6|

6. Leave the :guilabel:`DNS` settings at their defaults.

7. Change :guilabel:`Logging level` --> `Debug`

   |image7|

   .. NOTE::
       The :guilabel:`Debug` log level should not be used in production unless recommended by f5
       Support.

This completes the :guilabel:`Deployment Settings` setup. When your
screen looks like the following, click :guilabel:`Finished`:


|image8|


.. NOTE:: 
    The :guilabel:`Strict Updates` option protects against accidental changes to an application
    service's configuration. The :guilabel:`Strict Updates` setting is `checked` by default.

    Unless you have a specific reason to turn off strict updates, F5
    recommends that you leave the setting enabled.


.. |image3| image:: /_static/image3.png
   :width: 5.52778in
   :height: 1.01389in
.. |image4| image:: /_static/image4.png
   :width: 3.69444in
   :height: 2.95833in
.. |image5| image:: /_static/image5.png
   :width: 4.00000in
   :height: 1.69608in
.. |image6| image:: /_static/image6.png
   :width: 4.83333in
   :height: 1.23209in
.. |image7| image:: /_static/image7.png
   :width: 2.75000in
   :height: 0.51684in
.. |image8| image:: /_static/image8.png
   :width: 4.59705in
   :height: 5.61111in

