.. role:: red
.. role:: bred

Web Application Firewall-as-a-Service (WAFaaS)
================================================================================

In this lab, you will learn how to leverage an Existing Application inbound topology deployed with WAFaaS service to protect a vulnerable web application. You will see how the OWASP Juice Shop application is vulnerable to SQL injection attacks and provide protection with SSL Orchestrator and F5 Advanced WAF.


.. note::
   This methodology is documented in the following DevCentral Article:
   `WAFaaS with SSL Orchestrator <https://community.f5.com/t5/technical-articles/wafaas-with-ssl-orchestrator/ta-p/285752>`_.
   
   It leverages a pre-configured Advanced WAF policy to protect the vulnerable web application.

   This lab features the OWASP Juice Shop; a modern and sophisticated insecure web application designed to demonstrate common security vulnerabilities that can easily be exploited by anyone on the internet that can access your application. 
   `OWASP Juice Shop <https://owasp.org/www-project-juice-shop/>`_.

.. toctree::
   :maxdepth: 1
   :glob:

   scenario*
   lab*