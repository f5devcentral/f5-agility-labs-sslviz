.. role:: red
.. role:: bred

.. image:: ../images/image13.png

Lab 1.8: Security Policy
------------------------

Security policies are the set of rules that govern how traffic is processed in
SSLO. The "actions" a rule can take include:

- Whether or not to allow the traffic

- Whether or not to decrypt the traffic

- Which service chain (if any) to pass the traffic through

The SSLO Guided Configuration presents an intuitive rule-based, drag-and-drop
user interface for the definition of security policies.

.. image:: ../images/image14.png

In the background, SSLO maintains these security policies as visual
per-request policies. If traffic processing is required that exceeds the
capabilities of the rule-based user interface, the underlying per-request
policy can be managed directly.

.. note:: That once the per-request policy is manipulated, the rules-based
   interface can no longer be used.

For the lab, create an additional rule to bypass SSL for "Financial Data and
Services" and "Health and Medicine" URL categories.

- Click Add to create a new rule.

  - **Name** – provide a unique name for the rule (ex. "urlf\_bypass").

  - **Conditions**

    - **Category Lookup (All)** – add Financial Data and Services and Health
      and Medicine.

      The Category Lookup (All) condition provides categorization for TLS
      SNI, HTTP Connect and HTTP Host information.

  - **Action** – select Allow.

  - **SSL Forward Proxy Action** – select Bypass.

  - **Service Chain** – select the L2/TAP service chain.

  - Click OK.

    .. image:: ../images/image15.png

  Notice in the list of rules that the **All Traffic** rule intercepts but
  does not send traffic to a service chain. For the lab, edit this rule to
  send all intercepted traffic to a service chain.

  - Click the pencil icon to edit this rule.

  - Service Chain – select the service chain containing all of the services.

  - Click OK.

  .. image:: ../images/image16.png

  - Click Save & Next.
