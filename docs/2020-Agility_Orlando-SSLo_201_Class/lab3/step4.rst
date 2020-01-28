Step 4: Verify that user information is being identified on the F5 SSL Orchestrator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  From the main menu select ***Access->Overview->Active Sessions***

-  On the ***AD server and Testing Client*** open up the Firefox browser
   and navigate through to any website

-  Notice that the user is now being prompted for credentials in
   Firefox. This is because Firefox needs to be told on which sites to
   automatically provide NTLM credentials

   -  In the address bar of the Firefox browser type in *about:config*

   -  Type in *ntlm* in the search box on the top of the browser. Modify
      the *network.automatic-ntlm-auth.allow-non-fqdn* and
      *network.automatic-ntlm.trusted-uris* such that the screen looks
      like below

|image37|

-  In the ***AD server & Testing Client*** machine browser, browse
   through a few websites. You should now be able to browse without
   supplying credentials.

-  On the F5 device navigate to the ***Access->Overview->Active
   Sessions*** menu item from the main menu

-  You should be presented with session information and the username

|image38|

-  Click on *View* for the session – there is a lot of information that
   is displayed that is obtained from active directory. This confirms
   that the user has been authenticated and has been successfully looked
   up in Active Directory.

|image39|


.. |image37| image:: ../media/image036.png
   :width: 7.05556in
   :height: 2.46111in
.. |image38| image:: ../media/image037.png
   :width: 7.05556in
   :height: 2.49722in
.. |image39| image:: ../media/image038.png
   :width: 7.05556in
   :height: 8.12986in
