.. role:: red
.. role:: bred

Verify authentication is currently disabled
================================================================================

-  Start a TMUI session on **SSL Orchestrator** and log in if prompted (*Components > SSL Orchestrator > ACCESS > TMUI*)

      `Link to user credentials (if needed) <../labinfo.html>`_

-  From the Main menu on the left, select **Access > Overview > Active Sessions**. The following screen should appear. You should see an **Active Session Count** of **0** and that there are no sessions listed in the table.

.. image:: ../images/active-sessions-none.png
   :alt: Active Sessions (None)

.. important::

   For this lab exercise, you will be using the :bred:`WINDOWS CLIENT` machine instead of the Ubuntu18.04 Client machine
   that you used in the other lab exercises.


-  Start an RDP session to the **Windows Client** (*Systems > Windows Client > ACCESS > RDP*)

.. image:: ../images/windows-client-rdp.png
   :alt: Windows Client RDP Access

- Open the RDP file to connect.

- At the authentication prompt, click on **More choices** to show additional logon options. Then click on **Use a different account**.

.. image:: ../images/windows-logon-1.png
   :alt: RDP Client Logon - Use a different account

-  Login in as user: ``F5LABS\mike`` with password: ``agility``

.. image:: ../images/windows-logon-2.png
   :alt: Windows Logon - domain\user and password

-  Accept any connection/security prompts.

.. note::
   Please be patient. The Windows machines are running with limited resources, so may be slow at times.


-  Using Chrome, browse to ``https:\\www.f5.com``.

.. note::
   Chrome is already configured to use 10.1.10.150 as its Internet access proxy.


-  Refresh the previously shown TMUI screen. You should still see an **Active Session Count** of **0**.

