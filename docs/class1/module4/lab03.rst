Test the Configuration
================================================================================


Connect to the Wireshark Service
--------------------------------------------------------------------------------

#. From the **Deployment** tab in the UDF console, select **ACCESS > WIRESHARK TAP** for the **Ubuntu-Server** resource (*Components > Ubuntu-Server > ACCESS > WIRESHARK TAP*).

   .. note::
      This resource connects to a containerized version of Wireshark.

   A new tab will open showing the **Wireshark** web interface.


#. Double-click on the **eth1** interface to start capturing traffic. **Do NOT select the eth0** interface because that is used for remote access to the web interface.

   .. image:: ./images/ws-1.png
      :align: center

   |

#. In the Wireshark filter bar, enter ``tcp.port == 443 and http`` so that only relevant traffic is displayed.

   .. image:: ./images/ws-2.png
      :align: center

   |


Display Decrypted Traffic
--------------------------------------------------------------------------------

#. Switch to your **Ubuntu-Client** tab and connect to https://www.f5.com again with the **Firefox** browser.

#. Verify that the certificate was issued by the **f5labs.com** CA certificate.

   .. image:: ./images/client-decrypt-1.png
      :align: center

   |

#. Switch to your **WIRESHARK TAP** tab and review the traffic.

   You should see some cleartext HTML in the packet capture (with Protocol **HTTP**, but **Dst Port: 443**). This was decrypted by SSL Orchestrator and sent to the **wireshark TAP** Service for inspection and visualized in the Wireshark web interface.

   .. image:: ./images/ws-3.png
      :align: center

   |



Verify the Bypass Rule
--------------------------------------------------------------------------------

#. Before performing your next test, change the Wireshark filter to ``tcp.port == 443`` in order to see both encrypted and decrypted traffic.

#. Click on the **restart** button to clear the capture log. Do not save the capture.

   .. image:: ./images/ws-4.png
      :align: center

   |

#. Switch to your **Ubuntu-Client** tab and connect to https://www.bankofamerica.com with the **Firefox** browser.

#. Verify that the certificate was issued by the **Digicert** using a trusted public CA certificate.


   .. note::
      SSL Orchestrator did not forge a certificate for the remote server because the web site name matched the **Financial Data and Services** URL category that was selected in the **urlf_bypass** Security Policy rule.


   .. image:: ./images/client-bypass-1.png
      :align: center

   |

#. Switch to your **WIRESHARK TAP** tab and review the traffic.

   Find the **Client Hello** packet that contains and **SNI** value with a **bankofamerica.com** domain name. All related packets are identified as **TLS** (encrypted) traffic. You will still see decrypted traffic for other URLs (3rd party domains) that do not match the **urlf_bypass** rule.

   .. image:: ./images/ws-5.png
      :align: center

   |

