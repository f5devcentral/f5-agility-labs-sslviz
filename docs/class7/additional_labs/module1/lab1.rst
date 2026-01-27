SaaS Tenant Isolation Scenario
==============================

|

Challenge
---------

Your company has a growing number of SaaS applications that are used for daily productivity, (Office 365, Webex, Zoom, Youtube, Github, etc.) and your CISO is concerned about the risk of misuse and data exfiltration. You are challenged with finding a solution to reduce this risk by implementing a strategy to develop controls to isolate and restrict access to only approved portions of permitted SaaS applications.

|

Solution
--------

The **F5 SSL Orchestrator Service Extension** for **SaaS Tenant Isolation** can help meet this challenge. When a user attempts to connect to a SaaS Application, the **tenant isolation** inspection would be applied to the traffic flow. This action would be based on header inspection, removal, and injection that can be set for specific SaaS applications to allow access only to approved tenants within.  

Applications that can be restricted by SaaS Tenant Isolation:

* Office365 Tenant Restrictions v1
* Office365 Tenant Restrictions v2
* Webex
* Google GCloud
* Dropbox
* Youtube
* Slack
* Zoom
* Github
* ChatGPT