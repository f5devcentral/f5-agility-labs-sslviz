Step 1: Review the Security Objects and Access Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  From the main menu select ***Access->Authentication->NTLM->NTLM Auth
   Configuration*** and select *f5labs.com-NTLM-AAA* from the presented
   list (should be only one item in the list). The following screen
   should be presented.

|image30|

-  Machine Account Name is the name of the security object that is added
   to the domain as a Computer Account and Domain Controller FQDN List
   contains a list of the domain servers. In this lab environment we are
   using the Testing Client as the AD server as well.

-  From the main menu select ***Access->Profiles/Policies/Access
   Profiles (Per-Session Policies)***. The following screen will be
   presented.

   |image31|

-  Click on the ***Edit*** button next to the *f5labs-ntlm-ap* Access
   Profile Name. The following Access Policy should present itself.

|image32|

-  Close the newly opened tab

.. |image30| image:: ../media/image029.png
   :width: 6.87500in
   :height: 4.37500in
.. |image31| image:: ../media/image030.png
   :width: 7.05556in
   :height: 2.34097in
.. |image32| image:: ../media/image031.png
   :width: 6.37500in
   :height: 2.61458in
