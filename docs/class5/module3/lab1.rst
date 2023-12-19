BIG-IP Next Instance Onboarding
==============================================================================

.. note::

   As there are far more comprehensive resources for describing the setup and configuration of BIG-IP Next and Central Manager, this guide seeks only to provide an abbreviated set of instructions for the sole purpose of standing up an SSL Orchestrator environment. Please see official BIG-IP Next documentation for complete information on the platform:

   https://clouddocs.f5.com/bigip-next/latest/


The following instructions assume basic connectivity to the lab
environment, and administrative access to the lab's network and virtual
machine configurations.


Instantiating a BIG-IP Next Instance
--------------------------------------------------------------------------------

Follow these steps to instantiate and activate a BIG-IP Next instance
through the Central Manager.

#. Log into Central Manager with username: ``admin`` and password: ``Welcome123!``.

   .. image:: ./images/bigip-login.png


#. On the Home screen, click the **Manage Instances** button.

   .. image:: ./images/bigip-home.png


#. Click the **Start Adding Instances** button to add a new BIG-IP Next
   instance.

#. In the new Add Instance drawer, type in the IP address of the BIG-IP
   Next instance (10.1.1.7) and click the **Connect** button.

#. In the following drawer, enter the Username and Password information,
   and then click the **Submit** button.

#. In the following drawer, under **Management Credentials**, enter a
   new admin-cm password (use 'Welcome123!' for consistency, then click
   the **Add Instance** button.

#. Once the instance has been added, click the BIG-IP instance name link
   under the **Name** column. This will open a new Properties drawer.

#. Click the **License** button at the bottom of the left column of this
   drawer, then click the **Activate License** button.

#. Click the **Next** button in the **Activate License** drawer.

#. Copy the contents of the JWT token into the JST window, then provide a unique name and
   click the **Activate** button.


