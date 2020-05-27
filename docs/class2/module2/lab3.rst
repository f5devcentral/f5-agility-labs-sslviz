Local Traffic logging
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

While not the primary log destination for SSL Orchestrator some pertinent information may be logged to the Local Traffic log (/var/log/ltm). Log messages concerning pool and pool member availability (i.e. security service availability) and SSL/TLS handshake errors will appear in this log file and may help you ascertain why a particular connection (or multiple connections) are failing.

An example of an SSL handshake failure can be seen in the example below:

.. code-block:: shell-session

   May  4 14:05:35 sslo1 warning tmm2[11526]: 01260013:4: SSL Handshake failed for TCP 10.1.10.50:61863 -> 93.184.216.34:443

While not overly descriptive on its own, this message indicates that either the client-side (client to SSLO) or server-side (SSLO to server) SSL/TLS handshake was unsuccessful. This can be due to a number of reasons, such as a handshake timeout or negotiation failure. To troubleshoot this further, an administrator may refer to `K15292: Troubleshooting SSL/TLS handshake failures <https://support.f5.com/csp/article/K15292>`_ for next steps.