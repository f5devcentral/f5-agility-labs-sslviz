.. role:: red
.. role:: bred

Appendix - Demo Scripts
=======================

Lab 1 demo script
-----------------

**Configuration review and prerequisites**

#. Optionally define DNS, NTP and gateway route
#. Click :red:`Next`

**Topology Properties**

#. Name - some name
#. Protocol: :red:`Any`
#. IP Family: :red:`IPv4`
#. Topology: :red:`L3 Outbound`
#. Click :red:`Save & Next`

**SSL Configuration**

#. :red:`Create a New` SSL Profile
#. Client-side SSL (Cipher Type): :red:`Cipher String`
#. Client-side SSL (Cipher String): :red:`DEFAULT`
#. Client-side SSL (Certificate Key Chain): :red:`default.crt and default.key`
#. Client-side SSL (CA Certificate Key Chain): :red:`subca.f5demolabs.com`
#. Server-side SSL (Cipher Type): :red:`Cipher String`
#. Server-side SSL (Cipher String): :red:`DEFAULT`
#. Server-side SSL (Trusted Certificate Authority): :red:`ca-bundle.crt`
#. Click :red:`Save & Next`

**Service List**

1. Inline Layer 2 service

   a. Name: some name (ex. :red:`FireEye`)
   #. Network Configuration

      - Ratio: :red:`1`
      - From BIGIP VLAN: Create New, name (ex. FireEye_in), :red:`int 1.6`
      - To BIGIP VLAN: Create New, name (ex. FireEye_out), :red:`int 1.7`
      - Click :red:`Done`

   #. Service Action Down: :red:`Ignore`
   #. Enable Port Remap: Enable, :red:`8080`
   #. Click :red:`Save`

#. Inline layer 3 service

   a. Name: some name (ex. :red:`IPS`)
   #. IP Family: :red:`IPv4`
   #. Auto Manage: :red:`Enabled`
   #. To Service Configuration

      - To Service: :red:`198.19.64.7/25`
      - VLAN: Create New, name (ex. IPS_in), :red:`interface 1.3, tag 50`

   #. Service Action Down: :red:`Ignore`
   #. L3 Devices: :red:`198.19.64.64`
   #. From Service Configuration

      - From Service: :red:`198.19.64.245/25`
      - VLAN: Create New, name (ex. IP_out), :red:`interface 1.3, tag 60`

   #. Enable Port Remap: Enabled, :red:`8181`
   #. Manage SNAT Settings: :red:`None`
   #. Click: :red:`Save`

#. Inline HTTP service

   a. Name: some name (ex. :red:`Proxy`)
   #. IP Family: :red:`IPv4`
   #. Auto Manage: :red:`Enabled`
   #. Proxy Type: :red:`Explicit`
   #. To Service Configuration

      - To Service: :red:`198.19.96.7/25`
      - VLAN: Create New, name (ex. Proxy_in), :red:`interface 1.3, tag 110`

   #. Service Action Down: :red:`Ignore`
   #. HTTP Proxy Devices: :red:`198.19.96.66, Port 3128`
   #. From Service Configuration

      - From Service: :red:`198.19.96.245/25`
      - VLAN: Create New, name (ex. Proxy_out), :red:`interface 1.3, tag 120`

   #. Manage SNAT Settings: :red:`None`
   #. Authentication Offload: :red:`Disabled`
   #. Click :red:`Save`

#. ICAP Service

   a. name: some name (ex. :red:`DLP`)
   #. IP Family: :red:`IPv4`
   #. ICAP Devices: :red:`10.70.0.10, Port 1344`
   #. Request URI Path: :red:`/squidclamav`
   #. Response URI Path: :red:`/squidclamav`
   #. Preview Max Length(bytes): :red:`524288`
   #. Service Action Down: :red:`Ignore`
   #. Click :red:`Save`

#. TAP Service

   a. Some Name (ex. :red:`TAP`)
   #. Mac Address: :red:`12:12:12:12:12:12`
   #. VLAN: Create New, name (ex. :red:`TAP_in`)
   #. Interface: :red:`1.4`
   #. Service Action Down: :red:`Ignore`
   #. Click :red:`Save`
   
#. Click :red:`Save & Next`

**Service Chain List**

#. Add

   a. Name: some name (ex. :red:`my-service-chain`)
   #. Services: :red:`all of the services`
   #. Click :red:`Save`

#. Add

   a. name: some name (ex. :red:`my-sub-service-chain`)
   #. Services: :red:`L2 and TAP services`
   #. Click :red:`Save`

#. Click :red:`Save & Next`

**Security Policy**

#. Add a new rule

   a. Name: some name (ex. :red:`urlf_bypass`)
   b. Conditions

      - Category Lookup :red:`(All)`
      - SNI Category: :red:`Financial Data and Services, Health and Medicine`

   c. Action: :red:`Allow`
   d. SSL Forward Proxy Action: :red:`bypass`
   e. Service Chain: :red:`L2/TAP service chain`
   f. Click :red:`OK`

#. Modify the All rule

   a. Service Chain: :red:`all services chain`
   #. Click :red:`OK`

#. Click :red:`Save & Next`

**Interception Rule**

#. Select Outbound Rule Type: :red:`Default`
#. Ingress Network (VLANs): :red:`client-side`
#. L7 Interception Rules: :red:`Apply FTP and email protocols as required.`
#. Click :red:`Save & Next`

**Egress Setting**

#. Manage SNAT Settings: :red:`Auto Map`
#. Gateways: :red:`New, ratio 1, 10.30.0.1`

**Summary**

#. Review configuration
#. Click :red:`Deploy`

Lab 2 demo script
-----------------

**Configuration review and prerequisites**

#. Optionally define DNS, NTP and gateway route
#. Click :red:`Next`

**Topology Properties**

#. Name: some name (ex. :red:`sslo-inbound-1`)
#. Protocol: :red:`TCP`
#. IP Family: :red:`IPv4`
#. Topology: :red:`L3 Inbound`
#. Click :red:`Save & Next`

**SSL Configuration**

#. :red:`Show Advanced Setting`
#. Client-side SSL (Cipher Type): :red:`Cipher String`
#. Client-side SSL (Cipher String): :red:`DEFAULT`
#. Client-side SSL (Certificate Key Chain): :red:`default.crt and default.key`
#. Server-side SSL (Cipher Type): :red:`Cipher String`
#. Server-side SSL (Cipher String): :red:`DEFAULT`
#. Server-side SSL (Trusted Certificate Authority): :red:`ca-bundle.crt`
#. Advanced (Expire Certificate Control): :red:`Ignore`
#. Advanced (Untrusted Certificate Authority): :red:`Ignore`
#. Click :red:`Save & Next`

**Services List**

#. Click :red:`Save & Next`

**Service Chain List**

#. Click :red:`Save & Next`

**Security Policy**

#. Remove :red:`Pinners_Rule`
#. Edit All Traffic rule and add :red:`L2/TAP service chain`
#. Click :red:`Save & Next`

**Interception Rule**

#. Gateway-mode

   a. :red:`Hide Advanced Setting`
   #. Source Address: :red:`0.0.0.0/0`
   #. Destination Address/Mask: :red:`0.0.0.0/0`
   #. Port: :red:`443`
   #. VLANs: :red:`outbound`

#. Targeted-mode

   a. :red:`Show Advanced Setting`
   #. Source Address: :red:`0.0.0.0/0`
   #. Destination Address: :red:`10.30.0.200`
   #. Port: :red:`443`
   #. VLANs: :red:`outbound`
   #. Pool: :red:`webserver-pool`

#. Click :red:`Save & Next`

**Egress Settings**

#. Manage SNAT Settings: :red:`Auto Map`
#. Gateways: :red:`Default Route`

**Summary**

#. Review configuration
#. Click :red:`Deploy`

Lab 3 demo script
-----------------

**Configuration review and prerequisites**

#. Optionally define DNS, NTP and gateway route
#. Click :red:`Next`

**Topology Properties**

#. Name: some name (ex. :red:`sslo-explicit`)
#. Protocol: :red:`TCP`
#. IP Family: :red:`IPv4`
#. Topology: :red:`L3 Explicit Proxy`
#. Click :red:`Save & Next`

**SSL Configuration**

#. SSL Profile: :red:`Use Existing, existing outbound SSL settings`
#. Click :red:`Save & Next`

**Services List**

#. Click :red:`Save & Next`

**Service Chain List**

#. Click :red:`Save & Next`

**Security Policy**

#. Type: :red:`Use Existing, existing outbound security policy`
#. Click :red:`Save & Next`

**Interception Rule**

#. IPV4 Address: :red:`10.20.0.150`
#. Port: :red:`3128`
#. VLANs: :red:`client-net`
#. Click :red:`Save & Next`

**Egress Settings**

#. Manage SNAT Settings: :red:`Auto Map`
#. Gateways: :red:`Existing Gateway Pool, -ex-pool-4 pool`

**Summary**

#. Review configuration
#. Click :red:`Deploy`

**System Settings**

#. DNS Query Resolution: :red:`Local Forwarding Nameserver`
#. Local Forwarding Nameserver(s): :red:`10.1.20.1`
#. Click :red:`Deploy`
