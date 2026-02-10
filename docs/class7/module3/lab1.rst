Using SSLO with DNS-over-HTTPS Guardian
=======================================
|

Challenge
---------
Your company is adopting DNS-over-HTTPS (*DoH*) to protect users against DNS eavesdropping and tampering. At the same time, DoH blinds traditional network security tools and can let applications bypass enterprise DNS policies. The CISO has asked you to design a solution that restores visibility and control, and provides a method to block or allow DoH requests based on URL category. 

|

Solution
--------
The **F5 SSL Orchestrator Service Extension** **DoH Guardian** is a function for monitoring/managing DNS-over-HTTPS traffic flows and detecting potentially malicious DoH exfiltration over a L3 Outbound Proxy. This **Service Extension** is invoked at a detected (and *decrypted*) DNS-over-HTTPS request and has several options for logging, management, blocking, and anomaly detection. 

You will be enabling the capability to inspecting DoH requests and applying controls to block (blackhole or sinkhole) or allow based on the DoH request URL category.

