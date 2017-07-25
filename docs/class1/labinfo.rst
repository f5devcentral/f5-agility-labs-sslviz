SSL Orchestrator Lab Environment
================================

|image7|

- **BIG-IP Management IP**: 10.10.0.100         

- **Inline layer 2 service**:

  - Inward VLAN interface: ``1.2``
  
  - Outward VLAN interface: ``1.3``

- **Inline layer 3 service**:

  - Inward VLAN interface: ``1.4``

  - Outward VLAN interface: ``1.5``
                                            
- **Receive-only service**                    

  - MAC address: ``2c:c2:60:6e:cf:a2``

  - IP Address: ``10.90.0.5``
  
  - VLAN: ``ids-vlan``
  
  - Interface: ``1.6``

- **DLP service**                                   

  - IP Address: ``10.30.0.5:1344``
                                                  
- **ICAP Request/response URL**                     
                                                  
  - ``icap://${SERVER_IP}:${SERVER_PORT}/squidclamav``

  - Gateway IP Address: 10.40.0.1

.. |image7| image:: /_static/class1/image7.png
