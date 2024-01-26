Defining a Traffic Policy
================================================================================

The SSL Orchestrator traffic policy enables policy-based traffic steering to the inspection services. The policy defines traffic conditions, and each condition defines a set of actions to take on matching flow.

A traffic policy is a combination of multiple rulesets, each with same or similar traffic conditions, but different potential actions.

   - The Traffic Rules ruleset controls blocking, TLS decrypt decisions, and steering to inspection services.
   - The Traffic Rules ruleset contains a single, immovable **All Traffic** condition that applies to all traffic flows that do not match any other (higher) condition. Its default and adjustable behavior is to Allow traffic and decrypt.
   - The Logging Rules ruleset controls logging behavior. 



Create an SSL Orchestrator Traffic Policy
--------------------------------------------------------------------------------

You will now create a traffic policy with a TLS decryption bypass rule for a specific hostname. The default rule will decrypt all other traffic.

#. In the **SSL Orchestrator** menu, click on **Policies**.

#. Click the **Start Creating** button.

   - Enter ``my-sslo-policy-lab2`` in the **Name** field and an optional description
   - Enter ``Traffic policy for lab 2`` in the **Description** field (optional).
   - Ensure the **Type** is set to **Inbound Application**. 

   .. image:: ./images/policy-1.png


#. Click the **Next** button to continue.


Create a Traffic Condition Rule - TLS Decryption Bypass
--------------------------------------------------------------------------------

A traffic condition rule is generally made up of three parts, depending on the type of condition - the condition type (ex. IP Protocol), expression (ex. equals), and evaluation (what is being tested).

#. Click the **+ Create** button to create a new traffic condition.

   .. image:: ./images/policy-2.png

#. Enter ``rule1`` as the name for this condition, and an optional description.

#. Click **Save & Continue**.

#. In **Conditions and Actions**, click the **Start Creating** button.

#. Create a TLS bypass rule for **test.f5labs.com** by selecting:

   - Type: **Server Name (TLS ClientHello)**
   - Expression: **Equals**
   - Evaluation: ``test.f5labs.com``

#. To complete this condition, define the set of actions to take:

   - Flow Action: **Allow**
   - SSL Action: **Bypass**
   - Service Chain: **my-service-chain-lab2**

   .. image:: ./images/policy-3.png

#. Click the **Save** button.


Edit Traffic Condition Rule - All Traffic (Default)
--------------------------------------------------------------------------------

#. Now, you want to ensure that all other traffic flows through a service chain (none selected by default). Click the **All Traffic** rule to modify it.

#. Click on **Conditions and Actions**

#. Select the **my-service-chain-lab2** service chain.

   .. image:: ./images/policy-4.png

#. Click the **Save** button to close the **Traffic Rules** panel.


Create a Logging Rule - Log all TCP traffic
--------------------------------------------------------------------------------

#. In the **Logging Rules** section, click the **Start Creating** button.

#. Enter ``all-logging`` in the **Name** field, and optional description.

#. Click **Save & Continue**.

#. In **Conditions and Actions**, click the **Start Creating** button.

#. Configure a rule to log all TCP traffic.

   - Type: **IP Protocol**
   - Expression: **Equals**
   - Evaluation: **TCP**

#. Click the **Save** button.

   .. image:: ./images/policy-5.png


#. Click the **Save and Continue** button to close the **Logging Rules** panel.

   .. image:: ./images/policy-6.png


Finish the Traffic Policy
--------------------------------------------------------------------------------

The traffic policy is now complete with respect to this lab module, but other traffic and logging rules can also be applied (as required). 

#. Click **Save & Finish**. The traffic policy is now saved to CM and will be deployed to a BIG-IP instance when it is associated with an application.

   .. image:: ./images/policy-7.png

