Appendix 1 - Office 365 URL Category Automation
================================================

Microsoft publishes a list of the FQDNs that are associated with Office 365 services. SSL Orchestrator can consume that list and use it in the traffic classification process supporting **Security Policy** rules.

This lab takes you through the process required to automate Office 365 URL category database updates on the F5 SSL Orchestrator.
You will:

- Download and install the automation script
- Verify that the custom URL category was created successfully
- Create a new **Security Policy** rule to bypass decryption for Office 365 traffic
- Verify that the rule is working

.. toctree::
   :maxdepth: 1
   :glob:

   scenario*
   lab*