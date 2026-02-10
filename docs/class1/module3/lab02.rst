Review Pre-configured Settings
========================================================================================

For this lab exercise, you will leverage the pre-configured settings as described below.


.. attention::

   There are no additional hands-on configuration steps that you need to perform before proceeding to the next section.


-  **CA certificate and private key**

   In order to terminate and re-encrypt outbound SSL traffic, the SSL Forward Proxy must re-issue (forge) remote server certificates that the internal client trusts. In order to perform this re-issuance process, the BIG-IP must possess a Certificate Authority (CA) certificate and associated private key. The client must also trust this CA certificate.

   A CA certificate and private key has been pre-loaded and stored in the  **subrsa.f5labs.com** object. The client machine also has a copy of the CA certificate in its trusted CAs store.

   |

-  **Client-side VLAN and self-IP**

   This VLAN and self-IP connects the client to the BIG-IP. In this lab, that is the **10.1.10.0/24** subnet and interface **1.1** on the BIG-IP.

   |

-  **Internet outbound VLAN and self-IP**

   This VLAN and self-IP connects the BIG-IP to the outbound Internet router. In this lab
   that is the **10.1.60.0/24** subnet and interface **1.6** on the BIG-IP.

   |

-  **Default Internet route for outbound traffic**

   The Guided Configuration wizard provides the option to leverage a defined gateway pool or use the system default route to reach Internet destinations.
   A system default route has been pre-configured and will be used in this lab module.
