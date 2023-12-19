Explore CM API to Automate a Deployment
==============================================================================

Automation support adds an exciting new perspective to the F5 BIG-IP SSL
Orchestrator not previously available in BIG-IP “Classic”, and there are
two main drivers for programmability:

-  **Configuration**: Where API is used instead of a UI to deploy the
   general configuration of the product. While this is typically less
   important in data center appliance use cases, it is highly desirable
   in cloud and other “orchestrated” deployments, where you might need
   to programmatically spin up entire security and application
   architectures quickly. For example, deploying applications
   “on-demand” through a multi-cloud networking (MCN) workflow,
   generally requires programmability.

-  **Policy Manipulation**: The SSL Orchestrator policy represents a
   “tunable” control surface to address changing traffic behaviors and
   various events. Administrators can programmatically adjust the
   policy, either directly, or potentially use an AI/ML engine to inform
   policy actions.

This lab explores some basic programmability aspects of the SSL
Orchestrator, both to control configuration, and to manipulate the
policy. The following instructions assume basic connectivity to the lab
environment, and administrative access to the lab's network and virtual
machine configurations. Also, for this lab we will use the **Thunder Client** Visual
Studio Code extension to execute API requests to the F5 BIG-IP Central Manager.


Log into the Client Remote Desktop
--------------------------------------------------------------------------------

#. From within the UDF interface, navigate to the **Ubuntu-Server** instance and find the **WEBRDP** access link. Clicking this link opens a new browser tab.

#. Type in the username 'user' and password 'user' to access the Ubuntu client desktop within this browser window.

   You'll be presented with a standard Ubuntu instance running an XFCE desktop environment.
   In the user's Documents folder **/home/student/Documents**, an **API** subfolder exists with the following contents:

   - cURL scripts to create a basic BIG-IP Next application through CM (api-cURL-scripts-basic-application.txt)

   - Thunder Client API collection (thunder-collection_sslo-collection-v1.json)

   - Thunder Client API environment  (thunder-environment_sslo_environment.json)

   **Thunder Client** is a Postman alternative that runs as a Visual Studio Code extension. It has a similar look and feel to Postman but does not require a login to use collections and environments. This for student lab demonstration only. If you choose to use Postman in other environments, the Thunder Client can convert its collections and
   environments to Postman format.

   The cURL scripts are provided as an alternative to the GUI tool, but for this lab we will focus on using the API GUI.

   To access this visual API utility:

#. Launch the **Visual Studio Code** application from the command bar.

#. Within Visual Studio Code, click on the Thunder Client icon in the left side bar

#. In the Thunder Client left menu, click on the **Collections** tab.

#. Beneath this will be a pre-loaded collection: **sslo-api-collection-v1**. Expand this collection to view three subfolders - Basic App Deployment, SSLO Deployment, and Miscellaneous.

#. For this lab, we will focus on the contents of the SSLO Deployment folder, so expand this one.


You are now staged and ready to go for the remainder of the lab.


Log into Central Manager UI
--------------------------------------------------------------------------------

The next step is to log into the BIG-IP Central Manager UI. In a purely
programmatic sense this is not expressly required, but we will use it in
this lab to provide visual cues to successful API deployment. You will
be able to see and interact with the applications created from the API.

#. From within the UDF interface, navigate to the **BIG-IP-Next-CM** instance and find the **GUI** access link.

#. Clicking this link opens a new browser tab to the CM logon screen.

#. Provide the credentials to log in.

#. On the Home screen, click the **Manage Applications** button.

We will come back to the CM UI later. Let's now move on to API actions in the next step.



Login to Central Manager via API Request
--------------------------------------------------------------------------------

#. API requests to CM require a Bearer authorization token. To get that token you first need to make an initial login POST request to CM with your CM username and password.

   .. code-block:: text

      POST
      Content-Type: application/json
      {
      "username": "{{CM username}",
      "password": "{{CM password}"
      }

   This request returns an **access_token** that you will use for
   subsequent requests. This token will expire after a few moments, so it
   may be necessary to re-login and get a new bearer token occasionally.


Create an SSL Orchestrator Inspection Service
--------------------------------------------------------------------------------

The first true step in your adventure into SSL Orchestrator automation
is to create inspection services. These are the set of external security
devices that will receive decrypted traffic. Inspection services are
applied to service chains, service chains are applied to security
policies, and security policies are applied to applications.

#. TBD


Create an SSL Orchestrator Service Chain
--------------------------------------------------------------------------------

With one or more inspection services created, it's now time to create a
service chain that will define an ordered set of these for use in a
security policy.

#. TBD


Create an SSL Orchestrator Security Policy
--------------------------------------------------------------------------------

Let us now create an SSL Orchestrator security policy. This is the set
of traffic condition rules that will control TLS decryption and bypass
decisions, and dynamic service chaining to the inspection services.

#. TBD


Create an Application and Assign Security Policy
--------------------------------------------------------------------------------

The last API step is to apply the security policy to an application.

#. TBD


Review the Application in CM and Test Traffic Flow
--------------------------------------------------------------------------------

Finally, with all of the SSL Orchestrator and application objects
created via API, let's now review these in the Central Manager UI.
Again, not expressly required in a purely programmatic environment, but
useful here to see your creations. We'll also use this opportunity to
pass some traffic to the application and view the decrypted payloads
flowing across an inspection service.

#. TBD


Modify the Security Policy and Test Traffic Flow
--------------------------------------------------------------------------------

The bulk of our adventure so far has been in configuration, which is
mostly useful in cloud and other “orchestrated” deployments where
programmability is key. But now that traffic is flowing and SSL
Orchestrator is doing its job, you might need to “tune” the security
policy to adjust for different traffic demands. In this step we'll use
the security policy API to make real time updates to the active policy
and observe the changes in policy behavior.

#. TBD


Delete the Application, Policy, Service Chain, and Inspection Service
--------------------------------------------------------------------------------

As a final, and optional step in our API journey, we'll now tear
everything down.

#. TBD





|

.. attention::
   This is the end of the lab module.
