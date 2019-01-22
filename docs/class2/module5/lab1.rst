.. role:: red
.. role:: bred

Lab 5.1: Review and edit the existing security policy rules
-----------------------------------------------------------

In the SSLO dashboard view, navigate to the Security Policies tab and click on
a security policy (Name). The Guided Configuration will present the rules
engine previously seen as part of the topology workflow. New rules can be
added, and existing rules edited. Notice also that the "All Traffic" rule is
anchored to the security policy and cannot be moved or removed. This is the
default action rule for the policy, similar to a default deny rule in a
firewall policy. By default, it Intercepts (decrypts) traffic, but does not
send traffic to any service chain. This can be edited to Intercept, bypass or
block (reject), and to send traffic to a service chain.

Additional rules can use **AND** (Match All) or **OR** (Match Any) logic to
create complex decisions. Review the **Conditions** options to see the
possibilities.
