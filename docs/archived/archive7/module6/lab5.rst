Verify SSL Orchestrator Deployment Settings
================================================================================

In a purely programmatic sense, it is not required to log into the BIG-IP Central
Manager GUI. However, you will use it in in this lab to provide visual feedback
on successful API deployment.


Log into Central Manager (CM) GUI
--------------------------------------------------------------------------------

.. note::
   Skip this section if you are still logged into the BIG-IP CM GUI from the previous lab module.

#. Refer to section 3.1 of this Lab Guide to access and log into the BIG-IP CM GUI.

#. On the home screen, click the **Manage Applications** button.


Review the Application in BIG-IP CM
--------------------------------------------------------------------------------

#. Navigate to the BIG-IP CM Security workspace.

#. In the SSL Orchestrator left menu, click on **Inspection Services**.
#. Verify that the **my-sslo-tap** inspection service was created and review its configuration.

#. In the SSL Orchestrator left menu, click on **Service Chains**.
#. Verify that the **my-api-service-chain** Service Chain was created and review its configuration.
 
#. In the SSL Orchestrator left menu, click on **Policies**.
#. Verify that the **my-api-policy** Traffic Policy was created and review its configuration.

#. Navigate to the BIG-IP CM Applications workspace.

#. In the Applications left menu, observe the applications that you created from the previous lab modules.
#. Verify that the **my_app** application was created and review its configuration.

