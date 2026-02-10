Additional Labs
================================================================================

If you have completed the labs included in the main AppWorld Labs event and are looking for more exercises to practice your skills, here are some additional labs you can try on your own:

Lab 1: SaaS Tenant Isolation
----------------------------

In this lab, you will the existing L3 Outbound Topology that was created in previous module with a policy that implements **SaaS Tenant Isolation** for managing tenant isolation (aka. restrictions) for several SaaS applications in a corporate environment. Tenant isolation is a way for corporate entities to control access to non-corporate SaaS endpoints, typically to defend against misuse and sensitive data exfiltration. For example, an enterprise user may have Office365 accounts from multiple organizations. Tenant isolation prevents that user from copying data from their company Sharepoint to an Office365 endpoint in another organization. This service extension enhances the SSL Orchestrator built-in Office365 Tenant Restrictions service.

|

Lab 2: Advanced Blocking Pages
------------------------------

In this lab, you will the existing L3 Outbound Topology that was created in previous module with a policy that implements **Advanced Blocking Pages**. This is a F5 SSL Orchestrator service extension function for managing these pages and can either be deployed as a static blocking page at the end of a blocking traffic policy, orwith iRule logic to dynamically inject blocking page content.

|

.. toctree::
   :caption: CONTENTS
   :maxdepth: 1
   :glob:

  module*/module*