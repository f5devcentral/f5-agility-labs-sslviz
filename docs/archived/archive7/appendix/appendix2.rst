Appendix 2 - About the Consolidated Services Architecture
================================================================================

The consolidated architecture vastly reduces the resources used in the
UDF environment by consolidating the security services onto a single
Ubuntu server instance using Docker. The project is detailed
here:
https://github.com/kevingstewart/sslo-consolidated-services/tree/main/udf.

**Layer 3**, **HTTP**, **ICAP** security services, plus **web** and **Juiceshop** servers
are created as Docker containers via a Docker Compose file. The **layer 2**
and **TAP** services are hosted directly on the Ubuntu host with dedicated
interfaces. To verify that the container services are running, SSH to
the Ubuntu server instance and issue the following command:

.. code-block:: bash

   docker ps


There should be several services running, including:

-  **SSL Orchestrator security services**

   -  ICAP service: deepdiver/icap-clamav-service

   -  Layer 3 service: nsherron/suricata

   -  HTTP service: sameersbn/squid:3.5.27-2

-  **Web application** (for inbound testing)

   -  Apache web application: httpd:2.4

-  **Guacamole** (for web-based RDP (Remote Desktop Protocol) access to the client
   workstation)

   -  guacamole/guacamole

   -  guacamole/guacd

   -  postgres:13.4-buster

-  **OWASP Juice Shop** (for web vulnerability testing)

   -  nginx:alpine

   -  bkimminich/juice-shop

If this is not the case, or there are other issues, it may be easiest to
delete and recreate the entire Docker Compose environment to return to a
pristine deployment:

.. code-block:: bash

   cd /home/ubuntu/build/sslo-consolidated-services-main/udf
   ./security-service-rebuild-next.sh

This script will destroy all containers and images, then re-download the
images and rebuild new containers.

Should you need to log into any of the Docker container services directly:

- ICAP service (Clamav): ``docker exec -it icap /bin/bash``

- HTTP service (explicit proxy): ``docker exec -it explicit-proxy /bin/bash``

- Layer 3 service (Suricata): ``docker exec -it layer3 /bin/bash``

- Web server (Apache): ``docker exec -it apache /bin/bash``

- Juice Shop: ``docker exec -it nginx /bin/sh``

