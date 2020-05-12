Scenario
--------

To prevent large attachments from clogging up the email system, your company has enacted a new policy that restricts the size of email attachments from the previously generous 10MB to 500K or less. When this policy was enacted, employees were unable to send presentations or office documents to each other. This prevented collaboration.

To fix this problem, your company signed up for Dropbox to facilitate easy file transfers between employees. While this worked flawlessly prior to deploying SSL Orchestrator, employees are no longer able to access Dropbox using the native client after SSL Orchestrator has been deployed. They are however able to visit Dropbox and do their operations using a browser. However, the client provides certain functions that cannot be replicated by the browser and the native client also provides a richer and more convenient user experience.

You are tasked with fixing this such that both browser and native client have unhindered access. Your manager has empowered you to do what is necessary to get this working.

Lab Overview
------------

This lab will continue work from the previous lab. We will be reviewing the Pinned certificates category and see how to modify it to find a solution to the stated problem.