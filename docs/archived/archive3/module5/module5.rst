Module 5 - Manage the SSLO Security Policy
==========================================

SSL Orchestrator provides a rich, interactive, rules-based security policy
through the Guided Configuration.

.. image:: ../images/image25.png

The security policy itself is a front-end to an access per-request engine that
converts the rules into visual elements in this policy. Also note that the
order of rules affects the order of events in the visual policy. Rules are read
top-to-bottom and converted into corresponding visual agents nesting from left
to right.

.. image:: ../images/image26.png

While security policy rules work well for most traffic processing scenarios, it
may be necessary to go beyond their capabilities and manipulate the visual
per-request policy directly.

.. important:: Keep in mind, however, that the rules engine converts rules to
   visual elements in one direction only. It cannot convert visual elements
   back to rules, therefore once the visual per-request policy has been
   manipulated, the Guided Configuration security policies user interface will
   no longer be available.

This lab will explore some of the different options for manipulating SSLO
security policies.

.. toctree::
   :maxdepth: 1
   :glob:

   lab*
