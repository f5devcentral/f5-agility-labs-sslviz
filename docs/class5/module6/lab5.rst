Testing the API-based Deployment
================================================================================

With all of the SSL Orchestrator and application objects
created via API, you will now review these in the BIG-IP Central Manager UI.
While not expressly required in a purely programmatic environment, it is
useful here to see your deployed configuration. 

You will also send some traffic to the applications and view the decrypted payloads flowing across inspection services.


Review the Application in BIG-IP CM
--------------------------------------------------------------------------------

#. In the BIG-IP CM GUI, navigate to the Security workspace.

#. In the SSL Orchestrator left menu, click on **Inspection Services**.
#. Verify that the **my-sslo-tap** inspection service was created and review its configuration.

#. In the SSL Orchestrator left menu, click on **Service Chains**.
#. Verify that the **my-api-service-chain** Service Chain was created and review its configuration.
 
#. In the SSL Orchestrator left menu, click on **Policies**.
#. Verify that the **my-api-policy** Traffic Policy was created and review its configuration.

#. In the BIG-IP CM GUI, navigate to the Applications workspace.
#. In the Applications left menu, observe the applications that have been create across all of the previous labs.


Test Access to the HTTPS Application
--------------------------------------------------------------------------------

You will now test the HTTPS application by sending a command line **cURL** request to the BIG-IP Virtual Server. 


#. In the **Client VM shell** (or a shell running in the Client VM desktop), enter the following command:

   .. code-block:: text

      curl -vk https://10.1.10.22

   You should see HTML payload of the web page returned.


#. Under the **Ubuntu-Server** resource of the UDF Deployment tab, click on Access -> **Web Shell**. This will open a console shell window to the Server VM (in a separate browser tab).

#. Observe decrypted traffic to the TAP inspection device by initiating a tcpdump packet
   capture: The **TAP** interface is **ens7** directly on the host server VM:

   .. code-block:: text

      tcpdump -lnni ens7 -Xs0

#. In the **Client VM shell** (or a shell running in the Client VM desktop), send another cURL request:

   .. code-block:: text

      curl -vk https://10.1.10.22

   You should see decrypted traffic in the tcpdump packet capture (in the Server VM shell).


Modify the Security Policy and Test Traffic Flow
--------------------------------------------------------------------------------

The bulk of our adventure so far has been in configuration, which is
mostly useful in cloud and other **orchestrated** deployments where
programmability is key. But now that traffic is flowing and SSL
Orchestrator is doing its job, you might need to **tune** the security
policy to adjust for different traffic demands. 

In this section, you will use the security policy API to make real time updates 
to the active policy and observe the changes in policy behavior. Not surprisingly, modifying an existing deployed policy is fairly straightforward. First get the **id** {{policy-id}} value of all of the defined SSL Orchestrator policies. You will be referencing the target policy by its **id** in the next two API calls.

#. Get the SSL Orchestrator policies:

   .. code-block:: text

      GET https://{{CM}}/api/v1/spaces/default/security/policies?select=name,id

#. Record the **id** value of your intended policy. 

#. Edit the original policy contents as required and POST it back to the BIG-IP CM API, specifying the **policy id** {{policy-id}} in the API URL:

#. Update the SSL Orchestrator policy - Inbound App:

   .. code-block:: text

      POST https://{{CM}}/api/v1/spaces/default/security/policies/{{policy-id}}

   The updated policy is now stored on BIG-IP CM and needs to be pushed to each BIG-IP Next instance that references it. 

#. Deploy the updated policy to the BIG-IP Next instance:

   .. code-block:: text

      POST https://{{CM}}/api/v1/spaces/default/security/ssl-orchestrator-policies/{{policy-id}}/deploy

   The above will push the updated policy to the BIG-IP Next instances.

