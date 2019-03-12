.. role:: red
.. role:: bred

Lab 4.3: Attach the SSLO objects to an existing LTM application
---------------------------------------------------------------

The Existing Application topology workflow produces a single SSLO per-request
policy. To attach this to the LTM virtual server, edit the virtual server
previously created.

#. Go to Local Traffic --> Virtul Servers and select your virtual server.
   Modify the following properties:

   - **Access Policy (Access Profile**): attach the single
     ":red:`ssloDefault_accessProfile`".

   - **Access Policy (Per-Request Policy)**: attach the :red:`existing application
     per-request policy`.

#. Test your virtual servers with the attached SSLO policy.

   - RDP to the **Inbound** Windows client.
   - Browse to https://10.30.0.205 or if you added a host entry earlier
     https://www.f5loabs.com
