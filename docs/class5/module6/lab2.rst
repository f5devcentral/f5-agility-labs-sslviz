Setting up the API Client
================================================================================

|thunder-client| is a lightweight Rest API client for testing APIs. It has a similar look and feel to the **Postman** tools, but implemented as a |vscode| extension. If you choose to use **Postman** in other environments, the **Thunder Client** can convert its collections and environments to **Postman** format.

.. |vscode| raw:: html

   <a href="https://code.visualstudio.com/" target="_blank">Visual Studio Code (VS Code)</a>

.. |thunder-client| raw:: html

   <a href="https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client" target="_blank"><b>Thunder Client</b></a>


Log into the Client Remote Desktop
--------------------------------------------------------------------------------

In this lab, you will need to log into the **Client VM desktop** to launch **VS Code** and the **Thunder Client** to send API requests to the **F5 BIG-IP Central Manager**.

#. In the UDF **Deployment** tab, find the **Ubuntu-Server** resource.

#. Under **Ubuntu-Server**, click on **ACCESS** to see the list of available access methods.

#. Click on **WebRDP** to open a new browser tab that connects to the Client desktop GUI.

   .. image:: ./images/vscode-1.png

#. Enter the username (``user``) and password (``user``) to login.

   .. image:: ./images/vscode-2.png

This is a basic Ubuntu Linux VM instance running an XFCE desktop environment.


Access Thunder Client Extension
--------------------------------------------------------------------------------

You will now set up the **Thunder Client** extension in **VS Code**.

#. Click on the **VS Code** application shortcut in the command bar (bottom of the screen).

   .. image:: ./images/vscode-3.png


#. In **VS Code** , click on the **Thunder Client** icon in the left side bar to see the extension's interface.

   .. image:: ./images/vscode-4.png


About Thunder Client Environment Variables
--------------------------------------------------------------------------------

Environment variables provide shortcuts by substituting stored values into API requests when they are sent. All of the API calls in the SSL Collection will minimally include a **{{CM}}** variable value. Several variables are provided in the included SSLO Environment file.

#. To view these Environment values, click on the **Env** tab in the Thunder Client top menu bar (under the **New Request** button), and then click on **sslo-environment**. The list will contain both user-defined variables, and variables captured dynamically from API responses.

   .. image:: ./images/thunder-env.png


About Thunder Client API Collections
--------------------------------------------------------------------------------

#. Click on the **Collections** tab in the Thunber Client top menu bar. You will see a pre-loaded collection called **sslo-api-collection-v1**.

#. There are several folders within this collection. Click on the **Create SSLO Deployment** collection to expand it.

   .. image:: ./images/vscode-5.png


The **Thunder Client** vscode extension is now configured for the remaining steps of the lab.


Additional Files (For Reference)
--------------------------------------------------------------------------------

The **API** folder (**/home/student/Documents/API**) contains the **Thunder Client** SSL Orchestrator API collection and related environment variables files. cURL scripts are also provided as a command-line alternative to the GUI-based **Thunder Client** tool. 

   .. list-table::
      :header-rows: 1
      :widths: auto

      * - **Filename**
        - **Description**
      * - thunder-environment_sslo_environment.json
        - Thunder Client API environment
      * - thunder-collection_sslo-collection-v1.json
        - Thunder Client API collection 
      * - api-curl-scripts-basic-application.txt
        - cURL scripts to create a basic BIG-IP Next application through CM

   |

   .. image:: ./images/vscode-6.png

