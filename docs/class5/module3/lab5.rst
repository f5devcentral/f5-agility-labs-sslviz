.. role:: raw-html(raw)
   :format: html

Configure and verify that the Squid Proxy can see user information (Optional Step)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


-   Logon to the Squid proxy server (please refer to Lab 1 -> Step 6)


-   Before making changes please verify that there is no user information
    in the squid logs by typing in the following command

        :raw-html:`<i><font color="red">tail -F /var/log/squid3/access.log*</font></i>`

-   In the screenshot below notice the **“-“** as shown - this is where
    the username should be displayed.

    |image40|


-   To display the username, config changes are needed in the squid
    proxy.  These configs have already been pre-staged for purposes of this
    lab and the necessary support files have already been created.



-   Type in the following commands to make the config changes and restart
    Squid proxy. Output similar to the screenshot below will be presented

        :raw-html:`<i><font color="red">cd /etc/squid3; cp -p squid.conf.after_auth squid.conf</font></i>`

        :raw-html:`<i><font color="red">service squid3 restart; service squid3 status</font></i>`

    |image41|

-   Watch the logs while browsing through a variety of websites in the
    browser in Testing Client by typing the following command  and notice
    that the username is now populated where there previously was a **“-“**.

        :raw-html:`<i><font color="red">tail -F /var/log/squid3/access.log</font></i>`

    |image42|

-   All done!  Thank you for participating and working through the labs.


.. |image40| image:: ../images/image039.png
   :width: 7.05556in
   :height: 2.39861in
.. |image41| image:: ../images/image040.png
   :width: 7.05556in
   :height: 1.09444in
.. |image42| image:: ../images/image041.png
   :width: 7.05556in
   :height: 2.96250in
