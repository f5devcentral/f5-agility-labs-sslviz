Appendix - Demo Scripts
=======================

Lab 1 demo script
-----------------

**Configuration review and prerequisites**

1. Optionally define DNS, NTP and gateway route

2. Click Next

**Topology Properties**

1. Name - some name

2. Protocol: Any

3. IP Family: IPv4

4. Topology: L3 Outbound

5. Click Save & Next

**SSL Configuration**

1. Create a New SSL Profile

2. Client-side SSL (Cipher Type): Cipher String

3. Client-side SSL (Cipher String): DEFAULT

4. Client-side SSL (Certificate Key Chain): default.crt and default.key

5. Client-side SSL (CA Certificate Key Chain): subca.f5demolabs.com

6. Server-side SSL (Cipher Type): Cipher String

7. Server-side SSL (Cipher String): DEFAULT

8. Server-side SSL (Trusted Certificate Authority): ca-bundle.crt

9. Click Save & Next

**Service List**

1. **Inline Layer 2 service**

a. Name: some name (ex. FireEye)

b. Network Configuration

- Ratio: 1

- From BIGIP VLAN: Create New, name (ex. FireEye_in), int 1.6

- To BIGIP VLAN: Create New, name (ex. FireEye_out), int 1.7

- Click Done

c. Service Action Down: Ignore

d. Enable Port Remap: Enable, 8080

3. Click Save

2. **Inline layer 3 service**

a. Name: some name (ex. IPS)

b. IP Family: IPv4

c. Auto Manage: Enabled

d. To Service Configuration

- To Service: 198.19.64.7/25

- VLAN: Create New, name (ex. IPS_in), interface 1.3, tag 50

e. Service Action Down: Ignore

f. L3 Devices: 198.19.64.64

g. From Service Configuration

- From Service: 198.19.64.245/25

- VLAN: Create New, name (ex. IP_out), interface 1.3, tag 60

h. Enable Port Remap: Enabled, 8181

i. Manage SNAT Settings: None

j. Click Save

3. **Inline HTTP service**

a. Name: some name (ex. Proxy)

b. IP Family: IPv4

c. Auto Manage: Enabled

d. Proxy Type: Explicit

e. To Service Configuration

- To Service: 198.19.96.7/25

- VLAN: Create New, name (ex. Proxy_in), interface 1.3, tag 110

f. Service Action Down: Ignore

g. HTTP Proxy Devices: 198.19.96.66, Port 3128

h. From Service Configuration

- From Service: 198.19.96.245/25

- VLAN: Create New, name (ex. Proxy_out), interface 1.3, tag 120

i. Manage SNAT Settings: None

j . Authentication Offload: Disabled

k. Click Save

4. **ICAP Service**

a. name: some name (ex. DLP)

b. IP Family: IPv4

c. ICAP Devices: 10.70.0.10, Port 1344

d. Request URI Path: /squidclamav

e. Response URI Path: /squidclamav

f. Preview Max Length(bytes): 524288

g. Service Action Down: Ignore

h. Click Save

5. **TAP Service**

a. Some Name (ex. TAP)

b. Mac Address: 12:12:12:12:12:12

c. VLAN: Create New, name (ex. TAP_in)

d. Interface: 1.4

e. Service Action Down: Ignore

f. Click Save

6. Click Save & Next

**Service Chain List**

1. Add

a. Name: some name (ex. my-service-chain)

b. Services: all of the services

c. Click Save

2. Add

a. name: some name (ex. my-sub-service-chain)

b. Services: L2 and TAP services

c. Click Save

3. Click Save & Next

**Security Policy**

1. Add a new rule

a. Name: some name (ex. urlf_bypass)

b. Conditions

- Category Lookup (All)

- SNI Category: Financial Data and Services, Health and Medicine

c. Action: Allow

d. SSL Forward Proxy Action: bypass

e. Service Chain: L2/TAP service chain

f. Click OK

2. Modify the All rule

a. Service Chain: all services chain

b. Click OK

3. Click Save & Next

**Interception Rule**

a. Select Outbound Rule Type: Default

b. Ingress Network (VLANs): client-side

c. L7 Interception Rules: apply FTP and email protocols as required

d. Click Save & Next

**Egress Setting**

a. Manage SNAT Settings: Auto Map

b. Gateways: New, ratio 1, 10.30.0.1

**Summary**

a. Review configuration

b. Click Deploy

Lab 2 demo script
-----------------

**Configuration review and prerequisites**

1. Optionally define DNS, NTP and gateway route

2. Click Next

**Topology Properties**

1. Name: some name (ex. sslo-inbound-1)

2. Protocol: TCP

3. IP Family: IPv4

4. Topology: L3 Inbound

5. Click Save & Next

**SSL Configuration**

1. Show Advanced Setting

2. Client-side SSL (Cipher Type): Cipher String

3. Client-side SSL (Cipher String): DEFAULT

4. Client-side SSL (Certificate Key Chain): default.crt and default.key

5. Server-side SSL (Cipher Type): Cipher String

6. Server-side SSL (Cipher String): DEFAULT

7. Server-side SSL (Trusted Certificate Authority): ca-bundle.crt

8. Advanced (Expire Certificate Control): Ignore

9. Advanced (Untrusted Certificate Authority): Ignore

10. Click Save & Next

**Services List**

1. Click Save & Next

**Service Chain List**

1. Click Save & Next

**Security Policy**

1. Remove Pinners_Rule

2. Edit All Traffic rule and add L2/TAP service chain

3. Click Save & Next

**Interception Rule**

1. Gateway-mode

a. Hide Advanced Setting

b. Source Address: 0.0.0.0/0

c. Destination Address/Mask: 0.0.0.0/0

d. Port: 443

e. VLANs: outbound

2. Targeted-mode

a. Show Advanced Setting

b. Source Address: 0.0.0.0/0

c. Destination Address: 10.30.0.200

d. Port: 443

e. VLANs: outbound

f. Pool: webserver-pool

3. Click Save & Next

**Egress Settings**

1. Manage SNAT Settings: Auto Map

2. Gateways: Default Route

**Summary**

1. Review configuration

2. Click Deploy

Lab 3 demo script
-----------------

**Configuration review and prerequisites**

1. Optionally define DNS, NTP and gateway route

2. Click Next

**Topology Properties**

1. Name: some name (ex. sslo-explicit)

2. Protocol: TCP

3. IP Family: IPv4

4. Topology: L3 Explicit Proxy

5. Click Save & Next

**SSL Configuration**

1. SSL Profile: Use Existing, existing outbound SSL settings

2. Click Save & Next

**Services List**

1. Click Save & Next

**Service Chain List**

1. Click Save & Next

**Security Policy**

1. Type: Use Existing, existing outbound security policy

2. Click Save & Next

**Interception Rule**

1. IPV4 Address: 10.20.0.150

2. Port: 3128

3. VLANs: client-net

4. Click Save & Next

**Egress Settings**

1. Manage SNAT Settings: Auto Map

2. Gateways: Existing Gateway Pool, -ex-pool-4 pool

**Summary**

1. Review configuration

2. Click Deploy

**System Settings**

1. DNS Query Resolution: Local Forwarding Nameserver

2. Local Forwarding Nameserver(s): 10.1.20.1

3. Click Deploy
