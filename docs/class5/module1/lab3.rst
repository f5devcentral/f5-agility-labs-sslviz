What's new in SSL Orchestrator?
==============================================================================

BIG-IP Next SSL Orchestrator Features
------------------------------------------------------------------------------

The **BIG-IP Next SSL Orchestrator (BIG-IP Next 20.1)** release on BIG-IP Next provides the following features:

- **Inbound Application Mode**: SSL Orchestrator security policy can natively attach to a standard BIG-IP Next application workflow.

- **Inbound Gateway Mode**: SSL Orchestrator provides a separate gateway mode application workflow that enables an inbound (reverse proxy) routed traffic mode, where the destination is beyond the BIG-IP.

- **TAP Inspection Service Support**: TAP inspection services are passive, receive-only tools. Intrusion Detection Systems (IDS) are commonly deployed as a TAP and simply receive an out-of-band copy of the network packets.

- **ICAP Inspection Service Support**: An ICAP device is one that adheres to RFC 3507 specifications. ICAP itself is a payload encapsulation protocol and is often used to encapsulate payloads to various types of services, including DLP and malware detection products. In this case SSL Orchestrator is the ICAP client, encapsulating HTTP request and response payloads to an ICAP service.

- **Inline L3 Inspection Service Support**: An inline L3 device is an IP-based device that can route. It is “inline” in the sense that network traffic enters one (physical or logical) interface and routes out another. In this case, the SSL Orchestrator routes to it, and it routes back.

- **Inline HTTP Inspection Service Support**: an inline HTTP device is a subset of inline L3 devices, except that it is a proxy-type device. Proxy-type devices can be transparent or explicit, but the most important difference between HTTP and L3 devices is that HTTP devices, as a function of proxying, change the TCP flows. In particular, a proxy device will always minimally change the source port but may also change source and destination addresses.

- **Policy-based Traffic Steering and Dynamic Service Chaining**: The SSL Orchestrator Security Policy represents the set of rules that match traffic patterns and assign a set of actions, including:

  - Allow or reject traffic
  - Intercept (decrypt) or bypass decryption
  - Assign the traffic to a “service chain” of inspection devices

- **High Availability Support**: High availability is the ability to pair BIG-IP instances for greater availability and protection against unintended outages.

- **iRules Support**: BIG-IP Next carries forward the full extensibility of F5 iRules to provide programmatic access to the BIG-IP data plane. iRules present an unparalleled flexibility within the F5 BIG-IP full proxy architecture to tune and adjust traffic flows, and even application behavior, at wire speed.
