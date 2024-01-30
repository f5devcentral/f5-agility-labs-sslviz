Accessing the REST API Client
================================================================================

In this lab, you will need to log into the **Client VM desktop** to launch **VS Code** and access the **Thunder Client** extension. Then, you will send REST API requests to the **F5 BIG-IP Central Manager** in order to create and deploy an SSL Orchestrator configuration (with an HTTPS application).

|thunder-client| is a lightweight REST API client for testing APIs. It has a similar look and feel to the **Postman** REST API tool, but implemented as a |vscode| extension. If you choose to use **Postman** outside of the F5 UDF lab environment, the **Thunder Client** can convert its collections and environments to **Postman** format.

.. |vscode| raw:: html

   <a href="https://code.visualstudio.com/" target="_blank"><b>Visual Studio Code (VS Code)</b></a>

.. |thunder-client| raw:: html

   <a href="https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client" target="_blank"><b>Thunder Client</b></a>


Log into the Client Remote Desktop
--------------------------------------------------------------------------------

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


   .. caution::
      **VS Code** might display a notification (bottom-right corner) that a newer version is available for download. Do **NOT** install the update because it might break this lab. Just ignore the notification pop-up and it will close automatically.


#. In **VS Code** , click on the **Thunder Client** icon in the left side bar to see the extension's interface.

   .. image:: ./images/vscode-4.png


About Thunder Client Environment Variables
--------------------------------------------------------------------------------

**Environment** variables provide shortcuts by substituting stored values into API requests when they are sent. Several variables are provided in the included SSL Orchestrator **Environment** file.

#. To view these Environment values, click on the **Env** tab in the Thunder Client top menu bar (under the **New Request** button), and then click on **sslo-environment**.

   .. image:: ./images/thunder-env.png


The list will contain both user-defined variable with static values, and variables whose values are captured/updated dynamically when certain API requests (from the SSL Orchestrator Collection) are sent.

The **{{CM}}** static variable contains the management IP address of the BIG-IP CM. All of the API calls in the Collection use this variable in the request URL.

The dynamic variables in the Collection are referenced by subsequent API requests that depend on data returned from a previous API request. For example, the **{{authToken}}** variable is updated by the **CM Login** API request and then used in the access token header of other API requests.



About Thunder Client API Collections
--------------------------------------------------------------------------------

#. Click on the **Collections** tab in the Thunber Client top menu bar, and then click on the pre-loaded collection called **sslo-api-collection-v1** to expand it.

#. There are several folders within this collection. Click on the **Create SSLO Deployment** folder to expand it.

   .. image:: ./images/vscode-5.png

   These are all of the API requests that need to be sent to the BIG-IP CM API in order create an **Inbound Application Mode** deployment.


The **Thunder Client** VS Code extension is now configured for the remaining steps of the lab.


Additional Files (For Reference)
--------------------------------------------------------------------------------

The **API** folder (**/home/student/Documents/API**) on the **Client VM** contains the **Thunder Client** SSL Orchestrator API Collection and related Environment files.

   .. list-table::
      :header-rows: 1
      :widths: auto

      * - **Filename**
        - **Description**
      * - thunder-environment_sslo_environment.json
        - Thunder Client API environment
      * - thunder-collection_sslo-collection-v1.json
        - Thunder Client API collection 

