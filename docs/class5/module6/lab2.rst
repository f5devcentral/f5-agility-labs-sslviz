Accessing the API Client
================================================================================


Log into the Client Remote Desktop
--------------------------------------------------------------------------------

#. From within the UDF interface, navigate to the **Ubuntu-Server** instance and find the **WEBRDP** access link. Clicking this link opens a new browser tab.

#. Type in the username 'user' and password 'user' to access the Ubuntu client desktop within this browser window. You will be presented with a standard Ubuntu instance running an XFCE desktop environment.


Thunder Client Setup
--------------------------------------------------------------------------------

**Thunder Client** is an API client that runs as a **Visual Studio Code (vscode)** extension. It has a similar look and feel to the **Postman** tool, but does not require an account to use collections and environments. This is for student lab demonstration only. If you choose to use **Postman** in other environments, the Thunder Client can convert its collections and environments to **Postman** format.


#. Open the **Documents** folder (**/home/student/Documents**) and then click on the **API** subfolder. 

   You should see the following contents:

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

   The cURL scripts are provided as an alternative to the GUI-based **Thunder Client** tool.

#. To set up the **Thunder Client** extension, first launch the **Visual Studio Code** application from the command bar.

#. Within **vscode** , click on the **Thunder Client** icon in the left side bar.

#. In the **Thunder Client** left menu, click on the **Collections** tab. You should see a pre-loaded Collection: **sslo-api-collection-v1**.

#. Expand this collection to reveal three subfolders - **Basic App Deployment, SSLO Deployment, and Miscellaneous**.

#. For this lab, you will only use the contents of the **SSLO Deployment** folder. Click on it to expand it.


The **Thunder Client** vscode extension is now configured for the remaining steps of the lab.
