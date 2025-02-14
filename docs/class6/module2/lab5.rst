Module Completion
================================================================================

Congratulations! You now have a more robust architecture by decoupling the SSL visibility/orchestration functions from the application delivery/LB functions. The Security team can now fully manage the SSL Orchestrator platform configuration and software lifecycle without impacting the application delivery platform implementation.


In this lab module, you completed the following tasks:

- Created an on-box F5 Advanced WAF policy using a violation rating-based template.
- Created an **Inbound Gateway** Topology deployment.
- Created an on-box F5 WAF Inspection Service.
- Create two service chains: (1) FireEye service only and (2) FireEye and F5 WAF services.
- Created Security Policy with rules for two backend application instances (jsapp1 and jsapp2).
- Created SSL profiles with unique client-side TLS certificates for each application to support SNI-based certificate association.
- Verified that SSL Orchestrator is handling traffic for both applications via per-application inspection rules by sending SQL injection attacks to both applications.


.. note::

   For more information about **F5 Advanced WAF** policy creation, please check out our comprehensive WAF labs on `Clouddocs <https://clouddocs.f5.com/training/community/waf/html/>`_.


.. note::
   
   This lab features the **OWASP Juice Shop**: a modern insecure web application designed to demonstrate common security vulnerabilities that can easily be exploited. Read more about it here:  `OWASP Juice Shop <https://owasp.org/www-project-juice-shop/>`_.


|

This is the end of this lab module.

