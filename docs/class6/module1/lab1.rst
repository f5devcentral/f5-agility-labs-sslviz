Accessing the Virtual Lab
================================================================================

If you are not familiar with the process for joining an F5 UDF-based training course, refer to:

- |join_link|
- |interface_link|

#. You should have received a course registration email that contains the **UDF Course link**. Click on the link and log into the UDF student portal.

   .. important::
      If MFA is not configured for your account, you will be asked to set it up before proceeding.


#. Click on the **JOIN** button to enter the lab session. You will see 3 tabs: **Overview**, **Documentation**, and **Deployment**. The **Overview** tab will be shown.

   .. image:: ./images/udf-overview.png
      :align: left


#. Click on the **Documentation** tab to view lab information and a link to the Lab Guide (this document).

   .. image:: ./images/udf-documentation.png
      :align: left


#. Click on the **DEPLOYMENT** tab to see all of your lab resources.

   .. image:: ./images/udf-deployment.png
      :align: left

   |

   .. note::

      It takes about 10 minutes for the lab resources to be provisioned and start up. Please wait until you see the green indicator beside all of the resources.

   |

   .. list-table::
      :header-rows: 1
      :widths: auto

      * - Virtual Machines
        - Access Methods Used In this Lab
      * - BIG-IP SSL Orchestrator
        - WEB SHELL - Browser-based SSH session

          TMUI - Browser-based GUI session
      * - Ubuntu-Server
        - WEB SHELL - Browser-based SSH session

          WEBRDP - Browser-based RDP to **Ubuntu-Client** Desktop
      * - Ubuntu-Client
        - WEB SHELL - Browser-based SSH session

   |

   To access a lab VM, click on the **ACCESS** link to view the remote access methods and then click on the desired option. Here is an example:

   .. image:: ./images/udf-access-1.png
      :align: left

|

 .. note::

    You will only need your local web browser to access the lab resources. Browser-based Remote Desktop access to the **Ubuntu-Client** is provided via the Guacamole service (**WEBRDP** access link) that runs on the **Ubuntu-Server** instance.

    .. image:: ./images/udf-access-2.png
       :align: left


.. |join_link| raw:: html

      <a href="https://help.udf.f5.com/en/articles/3832165-how-to-join-an-f5-training-course" target="_blank"> How to join an F5 training course </a>

.. |interface_link| raw:: html

      <a href="https://help.udf.f5.com/en/articles/3832340-f5-training-course-interface" target="_blank"> F5 Training Course Interface </a>

