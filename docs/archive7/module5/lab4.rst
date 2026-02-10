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

#. Click **+ Create** in the top right to add a new traffic policy.

#. In the **Create Policy** pane:

   - Enter ``my-sslo-policy-lab3`` in the **Name** field and an optional description
   - Enter ``Traffic policy for lab 3`` in the **Description** field (optional).
   - Set the **Type** to **Inbound Gateway**. 

   .. image:: ./images/policy-1.png


#. Click the **Next** button to continue to the **Rules** configuration.


Create a Traffic Condition Rule - TLS Decryption Bypass
--------------------------------------------------------------------------------

A **Traffic Rule** is generally made up of three parts, depending on the type of condition - the condition type (e.g., 'IP Protocol'), expression (e.g., 'equals'), and evaluation (what is being tested).

Now, you will create a TLS bypass rule for traffic destined for **gwapp3.f5labs.com**


#. Click the **+ Create** button to create a new traffic rule.

   .. image:: ./images/policy-2.png


#. In the **Rule Properties** section of the **Create Traffic Rule** panel:

   - Enter ``gwapp3`` in the **Name** field.
   - Enter ``TLS bypass for gwapp3.f5labs.com`` in the **Description** field.
   
#. Click on the **Save & Continue** button to continue to **Conditions and Actions**.

#. In the **Conditions** section, click the **Start Creating** button and create a conditional expression:

   - Select a condition type of **Server Name (TLS ClientHello)**.
   - Select an expression of **Equals**.
   - Enter an evaluation value of ``gwapp3.f5labs.com``.


#. Define the action to take when this conditional expression matches:

   .. hint::
      Scroll down if you not see the **Actions** section.

   - Set the **Flow Action** to **Allow**. This will allow the traffic to pass.
   - Set the **SSL Action** to **Bypass**. This will disable decryption of the traffic.
   - Set the **Service Chain** to **my-service-chain-lab3**. This will send the traffic through a specified Service Chain.

   .. image:: ./images/policy-3.png

#. Click the **Save** button.

You will now see 2 **Traffic Rules** (**gwapp3** and **All Traffic**).

   .. image:: ./images/policy-3b.png


Edit Traffic Condition Rule - All Traffic (Default)
--------------------------------------------------------------------------------

By default, the **All Traffic** rule does not have a Service Chain selected. Let's attach a Service Chain to ensure that traffic flows not matching other rules is sent through a service chain.

#. Click the **All Traffic** rule to modify it.

#. Click on **Conditions and Actions**.

#. Set the **Service Chain** to **my-service-chain-lab3**.

   .. image:: ./images/policy-4.png

#. Click the **Save** button to close the panel.


Create a Logging Rule - Log all TCP traffic
--------------------------------------------------------------------------------

#. Now, create a single **Logging Rules** condition to log all incoming traffic. In the **Logging Rules** ruleset, click the **Start Creating** button.

#. Enter ``all-logging`` in the **Name** field, and optional description.

#. Click **Save & Continue**.

#. In **Conditions and Actions**, click the **Start Creating** button.

#. Configure a rule to log all TCP traffic.

   - Type: **IP Protocol**
   - Expression: **Equals**
   - Evaluation: **TCP**

#. Click the **Save** button to close the **Logging Rules** panel.

   .. image:: ./images/policy-5.png


Finish the Traffic Policy
--------------------------------------------------------------------------------

#. Click the **Save and Finish** button.

   .. image:: ./images/policy-6.png


The traffic policy is now saved to the BIG-IP Central Manager. In the next section, you will deploy it to a BIG-IP instance by associating it with an application.

   .. image:: ./images/policy-7.png



.. note::
   The traffic policy is now complete with respect to this lab module, but other traffic and logging rules can also be applied (as required). 

