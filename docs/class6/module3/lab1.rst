User Coaching Scenario
================================================================================

**Challenge**

You CISO is concerned about the increasing use of public generative AI applications by employees because of the 
risk of exposing confidential or proprietary company data. You are challenged with finding a solution to reduce this risk
by presenting a warning message containing your corporate **AI Usage Policy**, recommended actions, and then requiring user
acceptance before being allowed access to the web site.

|

**Solution**

SSL Orchestrator has the ability to manipulate the application flow based on a security policy rule match. When
a user attempts to connect to a web site that matches the **AI** URL category. The **AI Usage Policy** would be
presented and the user would be required to click on an *Acknowledgement* button before being allowed to continue.
Custom logging could also be enabled to track *risky site* usage for future deny/allow listing.

