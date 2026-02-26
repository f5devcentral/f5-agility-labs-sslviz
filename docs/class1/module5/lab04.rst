Edit the Security Policy
================================================================================

Modify Default Rule
--------------------------------------------------------------------------------

You must associate the new **malware_scan** **Service Chain** with a **Security Policy** rule to send traffic to the **Services** in the **Service Chain**.


#. Click on the **Security Policies** tab to view the policies list.

#. Click on the **l3_outbound** policy to edit it.

   .. image:: ./images/policy2-1.png
      :align: center

   |

#. Click on the **Edit** (pencil) icon for the **All Traffic** rule.

   .. image:: ./images/policy2-2.png
      :align: center

   |

#. Edit the **All Traffic** rule and select the **malware_scan** **Service Chain**.

   .. image:: ./images/policy2-3.png
      :align: center

   |

#. Click on the **OK** button to accept the changes.

#. Scroll down to the bottom and click on the **Deploy** button.

#. When prompted for confirmation, click on **Deploy** again.

   .. image:: ./images/policy2-4.png
      :align: center

   |

#. When the deployment completes, click on the **OK** button to return to the **SSL Orchestrator > Configuration** page.

   .. image:: ./images/policy2-5.png
      :align: center

