.. role:: red
.. role:: bred

Lab 3.2: Add DNS and Logging settings
-------------------------------------

Minimally an explicit proxy requires DNS settings. To enable this for the L3
Explicit topology, in the SSLO UI click System Settings.

- **DNS Query Resolution** - select :red:`Local Forwarding Nameserver`.

- **Local Forwarding Nameserver(s)** - enter :red:`10.30.0.1`.

- **[Optional] Logging Level** - select the logging level most appropriate for
  the deployment. Keep in mind, however, that DEBUG logging produces an
  enormous amount of local Syslog traffic and is not recommended when
  processing production traffic flows.

- Click :red:`Deploy` to commit the changes.
