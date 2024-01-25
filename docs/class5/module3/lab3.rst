Testing the Application Deployment
==============================================================================

Congratulations! You have now deployed a simple HTTPS application on BIG-IP Next. The next step is to test your application from a client environment and verify that everything is working properly.

Accesing the Client VM
--------------------------------------------------------------------------------

The UDF lab environment provides an Ubuntu Linux VM instance (**Ubuntu-Client**) with access to an interactive shell for command line testing, as well as a GUI desktop to run web browsers and other tools.

In the UDF Deployment tab, find the Client VM resource. The application tests performed in the next section will require you to execute commands from the Linux shell. The shell session can be accessed via either a **Web Shell** or a **terminal shell** within a **WebRDP** desktop GUI session.

If you want to use the Client desktop GUI option, click on the **WebRDP** access method under the **Ubuntu-Server** resource. This opens a new browser tab providing a view of the client desktop GUI. Enter the username (``user``) and password (``user``) to login. From the client desktop, you can launch a Linux **Terminal** window to issue shell commands.

For this lab module, we recommend using the **Web Shell** access method.

#. Under the **Ubuntu-Client** resource, click on the **Web Shell** access option. This will open a console shell window to the Client VM (in a separate browser tab).


Test Access to the HTTPS Application
--------------------------------------------------------------------------------

You will now test the HTTPS application by sending a command line **cURL** request to the BIG-IP Virtual Server. 

#. In the **Client VM shell** (or a Terminal shell running on the Client VM desktop), enter the following command:

   .. code-block:: bash

      curl -vk https://10.1.10.20

   The output of this command will contain the full HTML payload of the web page.


#. To see just the headers and TLS handshake output, add the **I** flag:

   .. code-block:: bash

      curl -vkI https://10.1.10.20


#. Look for the **Server certificate** section. You should see that the **subject** field's **Common Name (CN)** attribute is **\*.f5labs.com**. This confirms that the site is being presented from the BIG-IP deployed application.

   .. image:: ./images/add-app-12.png

|

.. attention::
   This is the end of the lab module.