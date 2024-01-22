Testing the SSL Orchestrator Deployment
================================================================================


Review the Application in CM and Test Traffic Flow
--------------------------------------------------------------------------------

Finally, with all of the SSL Orchestrator and application objects
created via API, you will now review these in the Central Manager UI.
While not expressly required in a purely programmatic environment, it is
useful here to see your deployed configuration. 

You will also use this opportunity to pass some traffic to the application and view the decrypted payloads flowing across an inspection service.


#. In the CM UI, navigate to the Security workspace, and under the SSL Orchestrator left menu,
   observe the Inspection Services, Service Chains, and Policies that have been created across all
   of the previous labs.

#. In the CM UI, navigate to the Applications workspace, and under the Applications left 
   menu, observe the applications that have been create across all of the previous labs.

#. Test access to all of the applications created in the labs.

   #. **Lab 1** created an application listening on https://10.1.10.20. 

   #. **Lab 2** created an application listening on https://10.1.10.21.

   #. **Lab 3** created a gateway path to three services running behind the BIG-IP, addressable as:

      - https://gwapp1.f5labs.com
      - https://gwapp2.f5labs.com
      - https://gwapp3.f5labs.com

   #. **Lab 4** created an application listening on https://10.1.10.22. 

#. From the **Client VM desktop**, access to all of the above URLs using cURL (command line) 
   or a web browser.

#. Observe decrypted traffic to the TAP inspection device by initiating a tcpdump packet
   capture directly from the server VM host: The TAP interface is **ens7** directly on
   the host server VM:

   .. code-block:: text

      tcpdump -lnni ens7


#. Add the **-Xs0** flag to the capture command to view the unencrypted payload:

   .. code-block:: text

      tcpdump -lnni ens7 -Xs0



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

#. Edit the original policy contents as required and POST it back to CM, specifying the **policy id** {{policy-id}} in the API URL:

#. Update the SSL Orchestrator policy - Inbound App:

   .. code-block:: text

      POST https://{{CM}}/api/v1/spaces/default/security/policies/{{policy-id}}

   The updated policy is now stored on CM and needs to be pushed to each BIG-IP Next instance that references it. 

#. Deploy the updated policy to the BIG-IP Next instance:

   .. code-block:: text

      POST https://{{CM}}/api/v1/spaces/default/security/ssl-orchestrator-policies/{{policy-id}}/deploy

The above will push the updated policy to the BIG-IP Next instances.

