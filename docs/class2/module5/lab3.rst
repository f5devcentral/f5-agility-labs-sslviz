.. role:: red
.. role:: bred

Lab 5.3: Practice creating Security Policies
--------------------------------------------

The following are a few examples of security policy use cases:

- Create a new security policy that matches source addresses in the outbound
  desktop client’s subnet, intercepts SSL, and sends to a service chain. All
  other traffic is bypassed with no service chain.

  .. image:: ../images/image27.png

- Add a rule to the above security policy that matches a specific URL category,
  bypasses SSL and sends to a service chain. Move this rule to the top of the
  list.

  .. image:: ../images/image28.png

- Add a new rule to the above security policy that matches a specific
  destination IP and blocks this traffic. Move this rule below the URL category
  rule, but above the client network rule.

  .. image:: ../images/image29.png

- Click Deploy, then navigate to the **Security Policies** tab in the SSL
  Orchestrator UI. For the newly-created security policy, click the link under
  the **Per Request Policies** header. This will open a new tab to the visual
  per-request policy.

  .. image:: ../images/image30.png

  Notice that the visual policy elements are nested in accordance with the
  ordered set of rules,

  - If the URL category is “Financial Data and Services” (urlf\_bypass), bypass
    SSL and send to a service chain.

  - Otherwise, if the destination IP is 93.184.216.34/32 (host\_block), reject
    the traffic.

  - Otherwise, if the client IP matches 10.0.0.0/8 (client\_network), send to a
    service chain (SSL interception implied).

  - Otherwise, bypass SSL and do not send to a service chain.

  .. note:: The **L7 Protocol Lookup** and **URL Match** options must assume
     that incoming traffic is either unencrypted or decrypted, therefore any
     rules that use these, and any rules after these cannot select to intercept
     or bypass the SSL.

  Apply the new rule to an existing outbound topology and test that:

  a) financial sites are bypassed.
  b) https://www.example.com is blocked.
  c) and all other client traffic flows through the defined service chain.
  
  View the APM log to follow the policy logic:

  tail -f /var/log/apm \|grep “Following rule”
