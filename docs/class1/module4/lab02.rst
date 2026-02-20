Edit the Existing Topology
================================================================================

#. If not already there, navigate to the **SSL Orchestrator > Configuration** page. The previously deployed Topology will be listed (named **sslo_l3_outbound**).

   .. image:: ./images/topology-1.png
      :align: center

   |

#. Click on the Topology name to edit it using the **Guided Configuration** UI.


Create a TAP Service
--------------------------------------------------------------------------------

Now, you will create a TAP service for a Wireshark instance.


#. To edit the **Services**, click on the **Service** icon at the top (or click on the *pencil* icon to the right of the **Service** menu item).

   .. image:: ./images/topology-2.png
      :align: center

   |

#. Click on the **Add Service** button to create a new Service.

   .. image:: ./images/service-tap-1.png
      :align: center

   |

   The **Services List** page is used to define security services that SSL Orchestrator can steer traffic to. To simplify the service configuration, common product integration templates are provided in a service catalog which is separated into 6 service types:

      - Inline L2
      - Inline L3
      - Inline HTTP
      - ICAP
      - TAP
      - F5

   The service catalog also provides "generic" security service options. Depending on your computer's screen resolution, it may be necessary to scroll down to see additional services.

#. Click on the **TAP** tab to view the available templates.

#. Select the **Generic TAP** service from the catalog and click the **Add** button (or simply double-click on the **Generic TAP** service).

   .. image:: ./images/service-tap-2.png
      :align: center

   |


#. Enter ``wireshark`` in the **Name** field.

#. Enter ``12:12:12:12:12:13`` in the **MAC Address** field. This tap service is directly connected to a BIG-IP interface, so the MAC address does not matter and can be arbitrarily defined. For a tap service that is not directly connected to the BIG-IP (but still on the same switch VLAN), enter the device's real MAC address.

#. Click on the **Create New** radio button under **VLAN** and enter ``wstap_in`` as the **Name**.

#. Select **Interface** **1.3**.

#. Enter ``1001`` in the VLAN **Tag** field.

   .. image:: ./images/service-tap-3.png
      :align: center

   |

#. The **Enable Port Remap** option allows SSL Orchestrator to remap the port of HTTPS traffic flowing to this service. For this lab, leave the option disabled (unchecked).

#. Click on the **Save** button to return to the **Services** list.

   .. image:: ./images/service-tap-4.png
      :align: center

   |


#. Click on the **Save & Next** button to continue.


Create a Service Chain
--------------------------------------------------------------------------------

You will now add the Wireshark **TAP** service to a **Service Chain**.

#. Click on the **Add** button to create a new **Service Chain**.

   .. image:: ./images/sc-1.png
      :align: center

   |

#. Enter ``tap_only`` in the **Name** field.

#. Double-click on the **ssloS_wireshark** service to move it from the **Services Available** column to the **Selected Service Chain Order** column.

   .. image:: ./images/sc-2.png
      :align: center

   |

#. Click on the **Save** button to return to the list of **Service Chains**.

   |

   .. attention::
      |

      A yellow "pending changes" notification banner will appear below the **Guided Configuration** workflow path.

      .. image:: ./images/pending-changes.png
         :align: center

      **DO NOT click** on the Deploy button at this time.

      |

   .. image:: ./images/sc-3.png
      :align: center

   |

#. Click on the **Save & Next** button to continue.



Edit the Security Policy
--------------------------------------------------------------------------------

You must associate the **tap_only** **Service Chain** with **Security Policy** rules in order to send traffic to Wireshark.


#. Click on the **Edit** (pencil) icon for the **All Traffic** rule.

   .. image:: ./images/sp-1.png
      :align: center

   |


#. Set **Service Chain** to **tap_only**. Recall that this Service Chain contains the **wireshark TAP** Service.

   .. image:: ./images/sp-2.png
      :align: center

   |

#. Click on the **OK** button to continue.


   Your **Security Policy** rules should now look like the following:

   .. image:: ./images/sp-3.png
      :align: center

   |


#. Click on the **Add** button to create a new rule. This rule will be used to bypass decryption for web sites categorized as **Financial Data and Services** or **Health and Medicine**.

#. Enter ``url_bypass`` in the **Name** field.

#. Select **Category Lookup (All)** from the **Conditions** drop-down list and then add the **Financial Data and Services** and **Health and Medicine** URL categories. Start typing the category name to narrow the list.

   .. note::
      The **Category Lookup (All)** condition provides categorization for TLS SNI, HTTP Connect and HTTP Host information.

   |

#. Select **ssloSC_tap_only** from the **Service Chain** drop-down list.


   .. image:: ./images/sp-4.png
      :align: center

   |

#. Click on the **OK** button to return to the **Security Policy** list.


   .. image:: ./images/sp-5.png
      :align: center

   |

#. Click on the **Save & Next** button to continue.


#. In a few moments, a yellow notification banner will appear below the **Guided Configuration** workflow path. Click on the **Deploy** button to apply the changes.


   .. image:: ./images/sp-6.png
      :align: center

   |

#. Click on the **OK** button when the deployment has completed and you will return to the **Topologies** list. Note that the Wireshark **TAP** service is now represented in the SSL Orchestrator configuration diagram.

   .. image:: ./images/topology-tap.png
      :align: center

   |
