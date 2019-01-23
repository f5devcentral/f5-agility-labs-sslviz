.. role:: red
.. role:: bred

Lab 5.1: Review and edit the existing policy
--------------------------------------------

In the SSLO dashboard view, navigate to the Security Policies tab and click on
a :red:`security policy (Name)`. The Guided Configuration will present the
rules engine previously seen as part of the topology workflow. New rules can be
added, and existing rules edited. Notice also that the "All Traffic" rule is
anchored to the security policy and cannot be moved or removed. This is the
default action rule for the policy, similar to a default deny rule in a
firewall policy. By default, it Intercepts (decrypts) traffic, but does not
send traffic to any service chain. This can be edited to Intercept, bypass or
block (reject), and to send traffic to a service chain.

Additional rules can use **AND** (Match All) or **OR** (Match Any) logic to
create complex decisions. Review the **Conditions** options to see the
possibilities.

To view the underlying :red:`visual security policy`, in the SSLO dashboard
view, navigate to the Security Policies tab and click on a security policy (Per
Request Policies). This will open a new tab with a view of the visual
per-request policy. By default, the security policy is locked and prevents any
changes to the visual per-request policy. To edit the visual policy, first
unlock the policy in the SSLO dashboard, Security Policies tab.

Keep in mind, however, that the rules engine converts rules to visual elements
in one direction only. It cannot convert visual elements back to rules,
therefore once the visual per-request policy has been manipulated, the Guided
Configuration security policies user interface will no longer be available.
