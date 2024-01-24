BIG-IP Next Instance Onboarding
==============================================================================

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


#. Since no BIG-IP Next instances have been added yet, click the
   **Start Adding Instances** button.

#. In the **Add Instance** panel, enter ``10.1.1.7`` as the IP address of the BIG-IP Next instance to add.

#. Click the **Connect** button.

   .. image:: ./images/add-bigip-1.png

#. In the login panel, enter ``admin`` in the **Username** field and enter ``Welcome123!`` in the **Password** field.

#. Click the **Next** button to continue.

   .. image:: ./images/add-bigip-2.png

#. In the **Management Credentials**, you will need to enter a new password for the **admin-cm** user. Enter ``Welcome123!`` in the **Password** and **Confirm Password** fields, then click the **Add Instance** button.

   .. image:: ./images/add-bigip-3.png

#. At the **Start Central Management on this instance?** prompt, click on the **Add** button.

#. At the **Continue Connecting?** prompt, click on the **Accept** button.

#. Once the instance has been added, you should see the new instance in the BIG-IP list.

   .. image:: ./images/add-bigip-4.png

#. Click the BIG-IP instance name link under the **Name** column to open the **Properties** panel.

   .. image:: ./images/add-bigip-5.png


#. Click the **License** button at the bottom of the left column of this
   panel. 

   .. attention::
      This BIG-IP Next instance already has an activated license, so there is no need to activate it here.

#. Click the **Cancel & Exit** button to close this panel.



   .. image:: ./images/add-bigip-6.png

