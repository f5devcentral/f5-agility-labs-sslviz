Environment Setup
================================================================================

In order to ensure the proper execution of the Ansible Playbooks within this module, it is important to have a properly configured environment. This environment is provided through the **Ubuntu-Client** WebRDP session. This client is running VScode and will be the tool used to execute the Ansible Playbooks.

|

Access the Ubuntu-Client WebRDP Session and open VScode
-------------------------------------------------------------

#. From the UDF **Deployment** tab, access the WebRDP session for the **Ubuntu-Client** resource. This will open a new browser tab with a GUI session. Login with **user** / **user**.

   .. image:: images/udf-ubuntu-webrdp-1.png
      :align: left

#. After logging in, open the VScode application from the bottom panel taskbar. This should auto display the README file for the the Ansible Playbooks that are stored on the desktop.

   .. image:: images/ubuntu-client-vscode-1.png
      :align: left
|

Initialize the Ansible Environment
----------------------------------

#. In the terminal pane of VScode, ensure you are in the proper working directory for the Ansible Playbooks:

   .. code-block:: text

      cd ~/Desktop/Ansible-Playbooks

#. Run the source command to initialize the Ansible environment and set the necessary environment variables:

   .. code-block:: text

      source ansible_venv/bin/activate

   .. code-block:: text

      export BIGHOST='10.1.1.6'

   .. code-block:: text

      export BIGUSER='admin'   




Setup environment.  

Destroy current SSLO environment?
--If destroy, setup up new L3 Outbound Transparent Proxy Topology.