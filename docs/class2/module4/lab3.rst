.. role:: red
.. role:: bred

Lab 4.3: Attach the SSLO objects to an existing LTM application
---------------------------------------------------------------

The Existing Application topology workflow produces a single SSLO per-request
policy. To attach this to the LTM virtual server, edit the virtual server
properties.

- **Access Policy (Access Profile**): attach the single
  "ssloDefault\_accessProfile".

- **Access Policy (Per-Request Policy)**: attach the existing application
  per-request policy.
