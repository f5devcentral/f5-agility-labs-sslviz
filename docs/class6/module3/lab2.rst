Deploy a Basic L3 Outbound Proxy Topology
================================================================================

In this section, you will create a basic SSL Orchestrator **Topology** to verify that outbound client traffic is being intercepted before enabling the **user coaching** function.

|

Create Topology
--------------------------------------------------------------------------------

#. In the **SSL Orchestrator UI**, click on the **Topologies** tab.

   .. image:: ./images/l3outbound.png
      :align: left


#. Click on the **Add** button to start creating a new Topology.

#. Scroll to the bottom of the **Configuration** introduction page and click on the **Next** button to start creating a new Topology.

#. Enter ``l3_outbound`` as the topology name.

#. Select the **L3 Outbound** topology type.

   .. image:: ./images/l3outbound-create.png
      :align: left

#. Scroll down to the bottom of the page and click on the **Save & Next** button to proceed to the next step in the configuration workflow.

|

Create SSL Configuration
--------------------------------------------------------------------------------

On the **SSL Configurations** page, create the **Client-side SSL** profile for the L3 outbound (transparent) forward proxy.


#. In the **Name** field, leave the default value as ``l3_outbound``.

#. In the **CA Certificate Key Chain** section, leave the default settings as is (default certificate and key).

   |

   .. important::

      Since this is an outbound forward proxy deployment, the SSL Orchestrator will be using a subordinate CA certificate and private key to sign the re-issued ('forged') certificates delivered to clients for outbound traffic. This is configured in the **CA Certificate Key Chains** section, **not** the **Certificate Key Chains** section.

   |

   .. note::

      When using subordinate CA certificates, both the subordinate and root CA certificates must be imported into the client's browser certificate store. The Ubuntu-Client machine in the lab environment trusts has these already installed.

   |

#. In the **CA Certificate Key Chain** section, click on the **Edit** (pencil) icon.

#. In the **Certificate** drop-down list, select **subrsa.f5labs.com** to replace the default value.

#. In the **Key** drop-down list, select **subrsa.f5labs.com** to replace the default value.

#. Click on the **Done** button to apply the config change.

   .. image:: ./images/l3outbound-ssl.png
      :align: left


#. Leave the default **Server-side SSL** settings.

#. Click on the **Save & Next** button to proceed to the next step in the configuration workflow.

|

User Authentication
--------------------------------------------------------------------------------

No user authentication will be enabled at this time.

#. Click on the **Save & Next** button to proceed to the next step in the configuration workflow.

|

Create Services
--------------------------------------------------------------------------------

There are 3 Inspection Services. The **ssloS_FEYE** and **ssloS_F5_AWAF** services were created in the previous lab module. Recall that the **ssloS_F5_UC** service was created by the **SSLO User Coaching** script.

   .. image:: ./images/l3outbound-services.png
      :align: left

No additional services need to be created at this time.

#. Scroll down to the bottom of the page and click on the **Save & Next** button to proceed to the next step in the configuration workflow.

|

Create Service Chains
--------------------------------------------------------------------------------

There are 2 Service Chains: **ssloSC_service_chain_1** and **ssloSC_service_chain_2**. These were created in the previous lab module.

   .. image:: ./images/l3outbound-chain.png
      :align: left

No additional Service Chains need to be created at this time.

#. Scroll down to the bottom of the page and click on the **Save & Next** button to proceed to the next step in the configuration workflow.

|

Create Security Policy
--------------------------------------------------------------------------------

The **Security Policy** contains 2 default rules: **Pinners_Rule** and **All Traffic**.

   .. image:: ./images/l3outbound-policy-1.png
      :align: left

#. Click on the **Edit** (pencil) icon for the **All Traffic** rule.

#. Set **Service Chain** to **ssloSC_service_chain_2**. Recall that this Service Chain contains the **ssloS_FEYE** and **ssloS_F5_AWAF** services.

   .. image:: ./images/l3outbound-policy-2.png
      :align: left

#. Click on the **OK** button to exit edit mode.


   Your **Security Policy** rules should now look like the following:

   .. image:: ./images/l3outbound-policy-3.png
      :align: left


#. Click on the **Save & Next** button to continue.

|

Create Interception Rule
--------------------------------------------------------------------------------

The **Interception Rule** determines which traffic to process. For an L3 Outbound topology, you will accept traffic for all destinations and ports.

#. Leave the default **Destination Address/mask** value as ``0.0.0.0%0/0``.

#. Leave the default **Port** as ``0``.

#. In the **Ingress Network** section, select the **client-vlan** VLAN.

   .. image:: ./images/l3outbound-int-1.png
      :align: left


#. Leave the default values for the remaining sections:

   - **Protocol Settings**
   - **Security Policy Settings**
   - **Authentication**
   - **L7 Interception Rules**

   |

   .. image:: ./images/l3outbound-int-2.png
      :align: left


#. Click on the **Save & Next** button to continue.

|

Create Egress Settings
--------------------------------------------------------------------------------

You will use SNAT all egress traffic and use the default route as a gateway.

#. In the **Manage SNAT Settings** drop-down list, select **Auto Map**.

#. Leave the default **Gateways** setting.

   .. image:: ./images/l3outbound-egress.png
      :align: left

#. Click on the **Save & Next** button to continue.

|

Create Log Settings
--------------------------------------------------------------------------------

#. Leave the default log settings.

   .. image:: ./images/l3outbound-log.png
      :align: left


#. Click on the **Save & Next** button to continue.

|

Deploy Topology
--------------------------------------------------------------------------------

#. Click on the **Deploy** button to create the new topology configuration.

   .. image:: ./images/l3outbound-deploy-1.png
      :align: left

#. When the deployment has completed, click on the **OK** button to close the dialog box and return to the **Topologies** list.

   .. image:: ./images/l3outbound-deploy-2.png
      :align: left

