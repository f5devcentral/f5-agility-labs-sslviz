Define Traffic Policy
================================================================================


Create an SSL Orchestrator Traffic Policy
--------------------------------------------------------------------------------

The SSL Orchestrator traffic policy enabled policy-based traffic steering to the inspection services. The policy defines traffic conditions, and each condition defines a set of actions to take on matching flow.

#. Click Policies under SSL Orchestrator in the left menu.

#. Click the Start Creating button.

#. Provide a name (ex. my-sslo-policy-lab3), an optional description, and then ensure the Type is set to Inbound Gateway. Click the Next button to continue.

The SSL Orchestrator traffic policy is a combination of multiple rulesets, each with same or similar traffic conditions, but different potential actions. The Traffic Rules ruleset controls blocking, TLS decrypt decisions, and steering to inspection services. The Logging Rules ruleset controls logging behavior. The Traffic Rules ruleset contains a single, immovable “All Traffic” condition that applies to all traffic flows that do not match any other (higher) condition. Its default and adjustable behavior is to Allow traffic and decrypt. Let us now make a few modifications to the Traffic Rules ruleset.

#. Click the + Create button to create a new traffic condition.

#. Provide a name for this condition (ex. rule1) and optional description, then click Save & Continue.

#. In Conditions and Actions, click the Start Creating button.

#. A traffic condition is generally made up of three parts, depending on the type of condition - the condition type (ex. IP Protocol), expression (ex. equals), and evaluation (what is being tested). For this simple demonstration, select the following:

   - Type: Server Name (TLS ClientHello)
   - Expression: Equals
   - Evaluation: gwapp3.f5labs.com

#. To complete this condition, define the set of actions to take:

   - Flow Action: Allow
   - SSL Action: Bypass
   - Service Chain: select your service chain

#. Click the Save button.

#. Click to modify the All Traffic condition and assign a service chain.

#. Let us now create a single Logging Rules condition to log all incoming traffic. In the Logging Rules ruleset, click the Start Creating button.

#. Provide a name for this condition (ex. all-logging) and optional description, then click Save & Continue.

#. In Conditions and Actions, click the Start Creating button.

#. Again, a traffic condition is generally made up of three parts, depending on the type of condition - the condition type (ex. IP Protocol), expression (equals), and evaluation (what is being tested). For this simple demonstration, and to log ALL traffic, select the following:

   - Type: IP Protocol
   - Expression: Equals
   - Evaluation: TCP

#. Click the Save button.

#. The traffic policy is now complete for the sake of this lab, but other traffic and logging rules can also be applied, as required. When done, click Save & Finish. The traffic policy is now saved to CM and will be deployed to a BIG-IP instance when it is associated with an application.



|

.. attention::
   This is the end of the lab module.
