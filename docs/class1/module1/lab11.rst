.. role:: red
.. role:: bred

GC Log Settings
===============

.. image:: ../images/gc-path-8.png
   :align: center

Log settings are defined per-topology. In
environments where multiple topologies are deployed, this can help to
streamline troubleshooting by reducing debug logging to the affected
topology.

.. note:: There are no additional steps that need to be taken by the student before proceeding to the next section.  The information below is intended to provide additional context on Log Settings.


Multiple discreet logging options are available:

-  **Per-Request Policy** - provides log settings for security policy
   processing. In Debug mode, this log facility produces an enormous
   amount of traffic, so it is recommended to only set Debug mode for
   troubleshooting. Otherwise the most appropriate setting is :red:`Error`
   to log only error conditions.

-  **FTP** - specifically logs error conditions for the built-in FTP
   listener when FTP is selected among the additional protocols in
   the Interception Rule configuration. The most appropriate setting
   is :red:`Error` to log only error conditions.

-  **IMAP** - specifically logs error conditions for the built-in
   IMAP listener when IMAP is selected among the additional protocols
   in the Interception Rule configuration. The most appropriate
   setting is :red:`Error` to log only error conditions.

-  **POP3** - specifically logs error conditions for the built-in
   POP3 listener when POP3 is selected among the additional protocols
   in the Interception Rule configuration. The most appropriate
   setting is :red:`Error` to log only error conditions.

-  **SMTP** - specifically logs error conditions for the built-in
   SMTP listener when SMTP is selected among the additional protocols
   in the Interception Rule configuration. The most appropriate
   setting is :red:`Error` to log only error conditions.

-  **SSL Orchestrator Generic** - provides log settings for generic
   SSLO processing. If Per-Request Policy logging is set to Error,
   and SSL Orchestrator Generic is set to Information, only the SSLO
   packet summary will be logged. Otherwise the most appropriate
   setting is :red:`Error` to log only error conditions.


.. image:: ../images/module1-14.png

For further details about the options available on this screen, click here.


The **Log Settings** have now been configured.

-  Click :red:`Save & Next` to continue to the next stage.
