.. role:: red

Verify that user information is being identified on the F5 SSL Orchestrator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  On the **Windows 10 Desktop** open up the Firefox browser and browse to a few websites

-  On SSL Orchestrator select **Access > Overview > Active Sessions** from the Main menu on the left

-  You should now see an active session similar to the example below.

   |active-sessions-mike|

.. TIP:: Click the **Refresh Session Table** button if the table is empty

-  Click on the **View** link to the left of the username you are logged in with to see more attributes associated with that user's access session, including attributes retrieved from Active Directory, such as: memberOf, sAMAccountName, and userPrincipalName.

   |session-variables-mike|

.. |active-sessions-mike| image:: ../images/active-sessions-mike.png
   :width: 706px
   :height: 332px
   :alt: Active Sessions
.. |session-variables-mike| image:: ../images/session-variables-mike.png
   :width: 1042px
   :height: 705px
   :alt: Mike's Session Variables