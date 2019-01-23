.. role:: red
.. role:: bred

Lab 4.3: Attach the SSLO objects to an existing LTM application
---------------------------------------------------------------

The Existing Application topology workflow produces a single SSLO per-request
policy. To attach this to the LTM virtual server, edit the virtual server
properties.

- **Access Policy (Access Profile**): attach the single
  ":red:`ssloDefault_accessProfile`".

- **Access Policy (Per-Request Policy)**: attach the :red:`existing application
  per-request policy`.
