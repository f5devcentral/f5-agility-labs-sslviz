SSL Orchestrator Initial Setup
========================================================================================

Let's first get logged into the BIG-IP SSL Orchestrator system.

#. In the **UDF Console**, navigate to the **Deployment** tab.

#. Select **ACCESS > TMUI** for the **BIG-IP SSL Orchestrator** resource (*Components > BIG-IP SSL Orchestrator > ACCESS > TMUI*).

#. A new tab will open and present the **BIG-IP** login screen. Log in as ``admin`` with password ``admin``.

   .. image:: images/initial-0.png
      :align: center


#. In the left-hand menu, click on **SSL Orchestrator** to see the available options.


#. Click on the **Configuration** menu item. 

   .. image:: ./images/initial-1.png
      :align: center

   |

   The **SSL Orchestrator Guided Configuration** UI will initialize.

   .. image:: ./images/initial-2.png
      :align: center

   |

   When loading completes, you will see the initial setup screen.

   .. image:: ./images/initial-3.png
      :align: center


#. Review the **Required Configuration** section (to the right of the **Configuration Options** section). You will see that system-level **DNS** and **Route** settings have already been configured, but **NTP** is unconfigured.

   .. image:: ./images/initial-4.png
      :align: center


#. Click on the **Click to configure** link beside **NTP**. This will open a new browser tab referencing the **System > Configuration > Device - NTP** configuration settings.

#. Enter ``0.pool.ntp.org`` in the **Address** field and click on the **Add** button. 

#. Repeat this step with ``1.pool.ntp.org`` and ``2.pool.ntp.org``.

#. Click on the **Update** button to apply the settings.

   .. image:: ./images/initial-5.png
      :align: center

#. Close the **NTP** tab to return to the main SSL Orchestrator tab. You should now see that all of the requirements have been satisfied.

   .. image:: ./images/initial-6.png
      :align: center


   |

   .. note::
      The SSL Orchestrator **Guided Configuration** UI also provides an opportunity to define topology-specific DNS and Route settings later in the workflow.


#. The **Configuration Options** section contains some basic overview information about various deployment Topologies that are supported. Click on the **left** or **right** navigation buttons to cycle through the options and read about the topology characteristics.

#. Scroll to the bottom of the page and click on the **Next** button to start creating a topology.
