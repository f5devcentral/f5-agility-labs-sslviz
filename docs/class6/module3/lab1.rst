User Coaching Scenario
================================================================================

**Challenge**

Your CISO is concerned about the increasing use of public generative AI applications by employees because of the 
risk of exposing confidential or proprietary company data. You are challenged with finding a solution to reduce this risk
by presenting a warning message containing your corporate **AI Usage Policy**, recommended actions, and then requiring user
acceptance before being allowed access to the web site.

|

**Solution**

The functionality of SSL Orchestrator can be extended using a mechanism called **service extensions**. This capability allows user-defined code to implement application logic and manipulate decrypted traffic flows.

The **service extension** for **user coaching** can help meet this challenge. When a user attempts to connect to a web site that matches the **AI** URL category. The **AI Usage Policy** would be presented  and the user would be required to click on an *acknowledgement* button before being allowed to continue. Custom logging could also be enabled to track *risky site* usage for future allow/deny-listing, or even record a usage reason (as provided by the user).

