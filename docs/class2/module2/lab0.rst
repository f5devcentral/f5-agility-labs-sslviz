Overview of SSL Orchestrator logging
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In SSL Orchestrator (v6 and above) log settings are defined per-topology. In environments where multiple topologies are deployed, this can help to streamline troubleshooting by limiting debug logging to the affected topology. Multiple logging options are available:

-  **Per-Request Policy** – logs events related to security policy processing. When set to Debug, this log facility produces an enormous amount of traffic, so it is recommended to only set this to Debug for troubleshooting. Otherwise the most appropriate setting is Error, which will only log error conditions.

-  **FTP** – specifically logs error conditions for the built-in FTP listener when FTP is selected among the additional protocols in the Interception Rule configuration. The most appropriate setting is Error, which will only log error conditions.

-  **IMAP** – specifically logs error conditions for the built-in IMAP listener when IMAP is selected among the additional protocols in the Interception Rule configuration. The most appropriate setting is Error, which will only log error conditions.

-  **POP3** – specifically logs error conditions for the built-in POP3 listener when POP3 is selected among the additional protocols in the Interception Rule configuration. The most appropriate setting is Error, which will only log error conditions.

-  **SMTP** – specifically logs error conditions for the built-in SMTP listener when SMTP is selected among the additional protocols in the Interception Rule configuration. The most appropriate setting is Error, which will only log error conditions.

-  **SSL Orchestrator Generic** – logs events related to generic SSLO processing, such as a summary of how a connection/flow was handled. If Per-Request Policy logging is set to Error, and SSL Orchestrator Generic is set to Information, only the connection/flow summary will be logged. If connection/flow summary logging is not required the most appropriate setting is Error, which will only log error conditions.

For the vast majority of troubleshooting cases the logging data from Per-Request Policy and SSL Orchestrator Generic (set to Debug and Information, respectively) are the most relevant. For ongoing connection summary logging to a system such as a SIEM, the SSL Orchestrator Generic log (set to Information) is usually the most relevant.