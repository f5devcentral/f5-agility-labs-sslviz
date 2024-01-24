Testing the Application Deployment
==============================================================================

Congratulations! You have just deployed a simple HTTPS application on
BIG-IP Next. The next step is to test your application from a client
environment. 


Log into the Client and Test Access to the HTTPS Application
--------------------------------------------------------------------------------

The UDF lab provides a unique client VM instance running a
version of Ubuntu Linux, access to an interactive shell for command line
testing, and a user desktop to run GUI browsers and other tools. Follow
these options to access *either* the client command line shell or desktop
GUI in the UDF lab:

-  **To access the Client VM shell**: In the UDF deployment window, find
   the Ubuntu **Client** instance and then find the **Web Shell** access
   option. This will open a console shell window to the client VM in a
   separate browser tab.

-  **To access the Client VM desktop**: In the UDF deployment window,
   find the Ubuntu **Server** instance and then find the **WebRDP** access
   option. This opens a new browser window to an instance of Guacamole
   running on the Ubuntu server with remote desktop access to the client
   desktop GUI. Enter the username (``user``) and password (``user``) to access
   the client desktop through the browser window.


The simplest test of the HTTPS application can be done with a command
line cURL request.

#. In the Client VM shell, or a shell running in the client desktop, enter the following command:

   .. code-block:: bash

      curl -vk https://10.1.10.20

   |

   The output of this command will contain the full payload of the webpage.


#. To see just the headers and TLS handshake output, add the **I** flag:

   .. code-block:: bash

      curl -vkI https://10.1.10.20

   |

#. Look for the **Server certificate** section. You should see that the **subject** field is **\*.f5labs.com**. This confirms that the site is being presented from the BIG-IP deployed application.

   .. image:: ./images/add-app-12.png

|

.. attention::
   This is the end of the lab module.