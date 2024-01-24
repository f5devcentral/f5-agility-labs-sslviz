Defining a Traffic Policy
================================================================================

Create an SSL Orchestrator Traffic Policy
--------------------------------------------------------------------------------

The SSL Orchestrator traffic policy enables policy-based traffic steering to the inspection services. The policy defines traffic conditions, and each condition defines a set of actions to take on matching flow.

#. In the **SSL Orchestrator** menu, click on **Policies**.

#. Click the **Start Creating** button.

   - Enter ``my-sslo-policy-lab2`` in the **Name** field and an optional description
   - Enter ``Traffic policy for lab 2`` in the **Description** field (optional).
   - Ensure the **Type** is set to **Inbound Application**. 

   .. image:: ./images/policy-1.png


#. Click the **Next** button to continue.

   .. note::

      The SSL Orchestrator traffic policy is a combination of multiple rulesets, each with same or similar traffic conditions, but different potential actions. The Traffic Rules ruleset controls blocking, TLS decrypt decisions, and steering to inspection services. The Logging Rules ruleset controls logging behavior. The Traffic Rules ruleset contains a single, immovable “All Traffic” condition that applies to all traffic flows that do not match any other (higher) condition. Its default and adjustable behavior is to Allow traffic and decrypt. Let us now make a few modifications to the Traffic Rules ruleset.


   .. image:: ./images/policy-2.png

#. Click the **+ Create** button to create a new traffic condition.

#. Enter ``rule1`` as the name for this condition, and an optional description

#. Click **Save & Continue**.

#. In **Conditions and Actions**, click the **Start Creating** button.

#. A traffic condition is generally made up of three parts, depending on the type of condition - the condition type (ex. IP Protocol), expression (ex. equals), and evaluation (what is being tested). For this simple demonstration, select the following:

   - Type: **Server Name (TLS ClientHello)**
   - Expression: **Equals**
   - Evaluation: ``test.f5labs.com``

#. To complete this condition, define the set of actions to take:

   - Flow Action: **Allow**
   - SSL Action: **Bypass**
   - Service Chain: **my-service-chain-lab2**

   .. image:: ./images/policy-3.png

#. Click the **Save** button.

#. Click the **All Traffic** condition to modify it

#. Click on **Conditions and Actions**

#. Select the **my-service-chain-lab2** service chain.

   .. image:: ./images/policy-4.png

#. Click the **Save** button to close the **Traffic Rules** panel.

#. Now, create a single **Logging Rules** condition to log all incoming traffic. In the **Logging Rules** section, click the **Start Creating** button.

#. Enter ``all-logging`` in the **Name** field, and optional description.

#. Click **Save & Continue**.

#. In **Conditions and Actions**, click the **Start Creating** button.

#. A traffic condition is generally made up of three parts, depending on the type of condition - the condition type (ex. IP Protocol), expression (equals), and evaluation (what is being tested). For this simple demonstration, you will configure a rule to log all TCP traffic.

   - Type: **IP Protocol**
   - Expression: **Equals**
   - Evaluation: **TCP**

   .. image:: ./images/policy-5.png

#. Click the **Save** button to close the **Logging Rules** panel.


   .. image:: ./images/policy-6.png


#. Click **Save & Finish**. The traffic policy is now saved to CM and will be deployed to a BIG-IP instance when it is associated with an application.

   .. image:: ./images/policy-7.png

