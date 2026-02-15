Automating a new SWGaaS Deployment
================================================================================

Within this lab, we will be deploying a new Secure Web Gateway as a Service (SWGaaS) deployment using Ansible Playbooks to automate the configuration on BIG-IP SSL Orchestrator. 

We will accomplishing the following:
 - Review Ansible playbooks needed for this deployment
 - Deploying a new SWG Service using Ansible Playbooks
 - Modifying the existing Service Chain to include the new SWG Service
 - Testing the new SWG Service

|

What is a Secure Web Gateway?
-----------------------------

Secure Web Gateway (SWG) is a forward-proxy security solution that provides protection against web-based threats by enforcing corporate and regulatory policies for internet access. It acts as a barrier between users and the internet, inspecting and filtering web traffic to prevent access to malicious websites, block inappropriate content. SWG can be deployed within BIG-IP SSL Orchestrator and is commonly used to enhance security and control over outbound web traffic.


