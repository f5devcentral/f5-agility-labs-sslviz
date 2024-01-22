Create Inbound Gateway Deployment
================================================================================


Create an Inbound Gateway Application with SSL Orchestrator Policy
--------------------------------------------------------------------------------

SSL Orchestrator inspection services, service chain, and traffic policy creation are now done, and it's time to apply this to a gateway application.

#. In the top left corner of the CM UI, click the workspace menu tool (9 dots) and click Applications. An application may already exist from the previous lab, but in any case either click the Start Adding Apps button (no existing applications), or the + Create button (existing applications).

#. In the Add Application drawer, enter a unique application name (ex. my-sslo-lab3-app) and select From Template. Click the Select Template button and then select the sslo-inbound-gateway-topology and click the Start Creating button. Optionally add a description and then click the Start Creating button.

#. In the Virtual Servers box, enter a unique name for your new application (ex. my_service). Set the Virtual Port to 443. 

#. In the Protocols & Profiles column, click the tool icon to open a new Protocols & Profiles drawer.

   - Enable (toggle) the Enable HTTPS (Client-Side TLS) option, then click the Add button. 

   - In the Add Client-Side TLS drawer, provide a name (ex. wildcard.f5labs.com), select the
     wildcard.f5labs.com RSA Certificate, then click the Save button.

   - Enable (toggle) the Enable Server-side TLS option.

   - Enable (toggle) Enable SNAT and Enable Auto SNAT.

#. Click the Save button in the Protocols & Profiles drawer.

#. In the Security Policies column, click the tool icon to open a new Security Profiles drawer. Enable (toggle) Use an SSL Orchestrator Policy, select your SSL Orchestrator traffic policy, then click Save.

#. Click the Review & Deploy button in the bottom right of the application drawer.

#. In the new Deploy drawer click the Start Adding button and select the BIG-IP Next instance. Click the + Add to List button.

#. In the Deploy drawer, now enter the Virtual Address (0.0.0.0/0) to listen for all incoming addresses.

#. In the Configure column, click the tool icon. Enable (toggle) Enable VLANs to listen on, select clientside, then click Save. No pool or pool members are required for a gateway mode deployment.

#. Click the Deploy Changes button to push the application definition to the BIG-IP Next instance.
