SSL Orchestrator Generic logging
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The logs produced by the SSL Orchestrator Generic facility provide a summary of details during multiple stages of the client/server connection. The Information level of severity provides a single log message per-connection, summarizing connection properties, whether it was decrypted, and which Service Chain it was sent through. The Debug level of severity produces information at multiple stages while the connection is established and .

An example of the logging that is produced by the SSL Orchestrator Generic facility can be seen below. In this example the severity was set to Debug, which includes log messages of all levels of severity, including Information:

.. code-block:: shell-session

   tcpdump -lnni ssloN_IPS_in.app/ssloN_IPS_in

   May  5 12:11:49 sslo1 debug tmm[11503]: 01c4ffff:7: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit_accessProfile:Common:2cd3ff97: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit-in-t-4 CLIENT_ACCEPTED TCP from 10.1.10.50_64258 to
    93.184.216.34_443 L7 guess=https

   May  5 12:11:49 sslo1 debug tmm[11503]: 01c4ffff:7: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit_accessProfile:Common:2cd3ff97: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit-in-t-4 SERVER_CONNECTED 10.1.10.50_64258 to 93.184.216.34_443 
    SNAT 10.1.20.100_46108

   May  5 12:11:49 sslo1 debug tmm[11503]: 01c4ffff:7: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit_accessProfile:Common:2cd3ff97: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit-in-t-4 CLIENTSSL_CLIENTHELLO client spoke TLSv1.2 Client Hello 
    517 bytes, SNI='www.example.com', L7 guess=https, pre-HS

   May  5 12:11:49 sslo1 debug tmm[11503]: 01c4ffff:7: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit_accessProfile:Common:2cd3ff97: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit-in-t-4 CLIENTSSL_HANDSHAKE 
    www.example.com-TLSv1.2-ECDHE-RSA-AES128-GCM-SHA256-128

   May  5 12:11:49 sslo1 debug tmm[11503]: 01c4ffff:7: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit_accessProfile:Common:2cd3ff97: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit-in-t-4 CLIENTSSL_DATA client spoke first within TLS 348 bytes, 
    inner-protocol http, L7 guess=https, post-HS
    
   May  5 12:11:49 sslo1 info tmm[11503]: 01c40000:6: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit_accessProfile:Common:2cd3ff97: /Common/sslo_f5labs_explicit.app
    /sslo_f5labs_explicit-in-t-4 Traffic summary - tcp 10.1.10.50:64258 -> 93.184.216.34:443 
    clientSSL: TLSv1.2 ECDHE-RSA-AES128-GCM-SHA256 serverSSL: TLSv1.2 ECDHE-RSA-AES128-GCM-SHA256 
    L7 https (www.example.com) decryption-status: decrypted duration: 87 msec service-path: 
    ssloSC_All_Services client-bytes-in: 1543 client-bytes-out: 4242 server-bytes-in: 5947 
    server-bytes-out: 1251


.. NOTE:: To minimize impact on the BIG-IP system, F5 recommends that Debug logging only be enabled when advised by F5 Technical Support, and for as short a time as possible to collect the necessary diagnostic data.