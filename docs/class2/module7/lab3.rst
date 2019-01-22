.. role:: red
.. role:: bred

Lab 7.3: Deleting everything
----------------------------

To completely remove the SSLO configuration and start from scratch:

- In the SSLO UI, click Delete Configurations and then click OK. This process
  will take some time as SSLO walks through all of the objects and dependencies
  to remove all configurations.

- Under the iApps menu, Application Services, Applications LX – un-deploy any
  remaining SSL orchestrator objects. If using any other Guided Configuration
  engine (ex. Access GC), ensure that only SSLO objects are deleted here.

- Under the iApps menu, Templates, Templates LX – delete all of the SSL
  Orchestrator templates.

- Under the iApps menu, Package management LX – delete the SSL Orchestrator
  package.

The next time the SSL Orchestrator configuration menu is accessed, SSLO will
automatically restore the on-box package.
