.. role:: red
.. role:: bred

[Optional] Deleting everything...the hard way
---------------------------------------------

In the unlikely event that the above steps do not work, and some SSLO objects
remain and cannot be deleted, one of the following steps can be used:

- If the topology and interception rules are gone but other objects remain and
  will not uninstall in the SSL Orchestrator UI, in the BIG-IP UI navigate to
  iApps -> Application Services -> Applications LX. The remaining objects will
  all be here in states of deployed (green), undeployed (gray), and error
  (red). Delete any objects in an error state and toggle the other objects from
  deployed to undeployed and back until they enter an error state and can also
  be deleted.

- If the above fails, the following script can be used to automate destruction
  of SSLO objects.

  - Copy the script to the BIG-IP (ex. :red:`cleaner.sh`)

  - Chmod the script to give it execute privileges:
    
    .. code-block:: bash
    
       chmod +x cleaner.sh

  - Execute the script:
  
    .. code-block:: bash
    
       ./cleaner.sh

  - It will typically be necessary to execute the script several times to get
    through dependencies. It is completely done when the script returns
    quickly with no additional output. Validate that all SSLO objects are gone
    from the BIG-IP UI under the Local Traffic and Network sections.

  - Under the iApps menu, Application Services, Applications LX - un-deploy any
    remaining SSL orchestrator objects. If using any other Guided Configuration
    engine (ex. Access GC), ensure that only SSLO objects are deleted here.

  - Under the iApps menu, Templates, Templates LX - delete all of the SSL
    Orchestrator templates.

  - Under the iApps menu, Package management LX - delete the SSL Orchestrator
    package.

.. code-block:: bash

   #!/bin/bash
   user_pass='admin:admin'
    
   for svc in `curl -sk -X GET "https://localhost/mgmt/tm/sys/application/service" -u ${user_pass} | jq -r '.items[].fullPath' |sed 's/\/Common\///g' |grep ^sslo`; do
      tmsh modify sys application service ${svc} strict-updates disabled
      tmsh delete sys application service ${svc}
   done
    
   for block in `curl -sk -X GET 'https://localhost/mgmt/shared/iapp/blocks?$select=id,state,name&$filter=state%20eq%20%27*%27%20and%20state%20ne%20%27TEMPLATE%27' -u ${user_pass} | jq -r '.items[] | [.name, .id] |join(":")' |grep -E '^sslo|f5-ssl-orchestrator' | awk -F":" '{print $2}'`; do
      curl -sk -X PATCH "https://localhost/mgmt/shared/iapp/blocks/${block}" -d '{state:"UNBINDING"}' -u ${user_pass}
      curl -sk -X DELETE "https://localhost/mgmt/shared/iapp/blocks/${block}" -u ${user_pass}
   done

- If the above fails, manually clear the REST database from the command line:

  - Break any HA configuration

  - Issue the ':red:`clear-rest-storage [options]`' command, where the options
    are "-l" (lowercase L) to delete the restjavad log files as well as the
    stored state, and "-d" to reset the system configuration to default. This
    command will remove all SSL Orchestrator objects from the restnoded
    database. After issuing this command, follow with
    ':red:`bigstart restart restnoded`' and 
    ':red:`bigstart restart restjavad`', clear the browser cache, log out and
    back in.

  - Issue the ':red:`tmsh delete sys application service recursive`' command to
    also delete any remaining SSL Orchestrator application service objects.

  - Once all SSLO objects have been removed, also uninstall the SSLO RPM
    package under the iApps menu, Package management LX - delete the SSL
    Orchestrator package.

  - Rebuild HA and redeploy SSLO by navigating to the SSL Orchestrator
    configuration UI. On first visit it will automatically restore the on-box
    package.
