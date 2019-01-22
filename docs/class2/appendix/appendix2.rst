Appendix - Routing Considerations For Layer 3 Devices
=====================================================

SSL Orchestrator sends all traffic through an inline layer 3 or HTTP device in
the same direction – entering through the inbound interface. It is likely,
therefore, that the layer 3 device may not be able to correctly route both
outbound (forward proxy) and inbound (reverse proxy) traffic at the same time.
Please see the appendix, "Routing considerations for layer 3 devices" for more
details. For example, in a simple Linux-type environment there would be two
routes needed for SSLO:

- The default gateway to send traffic back to SSLO through the service’s
  outbound interface

- A static return route to allow client traffic to return through the service’s
  inbound interface

Example:

*Destination Gateway Genmask Flags Metric iFace*

*default 198.19.64.245 0.0.0.0 UG 0 eth2*

*10.1.10.0 198.19.64.7 255.255.255.0 UG o eth1*

In the above, configured for an outbound traffic flow, the default gateway is
on the outbound side interface (eth2), with a static route for 10.1.10.0/24
(client-sourced) traffic flowing back through the inbound interface (eth1). An
inbound flow, however, would require the opposite:

*Destination Gateway Genmask Flags Metric iFace*

*default 198.19.64.7 0.0.0.0 UG 0 eth1*

*10.1.10.0 198.19.64.245 255.255.255.0 UG o eth2*

There are generally a few options for handling inbound and outbound traffic
flows:

- Do not use the same layer 3 device for inbound and outbound flows – the
  simplest option, but not always possible in some environments.

- Create a policy route, if the device supports it, to create multiple
  gateways.

We will explore the second and second options below.

**Configuring a policy route on the layer 3 device**

If a service supports it, policy routing allows you to create multiple gateways
on a layer 3 (routed) device. In lieu of creating separate inbound and outbound
services, and service chains for a single L3 device, all traffic in this use
case still flows through the inbound side interface, but the policy route will
effectively steer traffic in the correct direction. Policy routing can be a
complex topic in and of itself, and each security product will have its own way
of configuring policy routing anyway, so it cannot be covered in total in this
guide. Please refer to product-specific documentation to learn more about your
policy routing options.

The following is an example script to enable a policy route on a generic Linux
device (most of which have iproute2 installed by default). In the script, it is
only necessary to modify the top eight variables, defining attributes of the
inbound and outbound networks. Once complete, chmod the script to make it
executable, test it, and then call it from a startup process like /etc/rc.local
or /etc/init.d/rc.local. If the script is successful, you should be able to
send inbound and outbound SSLO traffic flows through this device.

#!/bin/bash

## Inbound interface

inbound\_interface=eth1.10

inbound\_ip=198.19.64.65

inbound\_mask=25

inbound\_gw=198.19.64.7

## Outbound interface

outbound\_interface=eth1.20

outbound\_ip=198.19.64.130

outbound\_mask=25

outbound\_gw=198.19.64.245

### ---------------------------------------------- ###

### ---------------------------------------------- ###

## static table names

inbound\_table=av\_in

outbound\_table=av\_out

## function to get network from mask and IP

get\_network () {

IFS=. read -r io1 io2 io3 io4 <<< "$2"

set -- $(( 5 - ($1 / 8) )) 255 255 255 255 $(( (255 << (8 - ($1 % 8))) & 255 )) 0 0 0

[ $1 -gt 1 ] && shift $1 \|\| shift

NET\_ADDR="$((${io1} & ${1-0})).$((${io2} & ${2-0})).$((${io3} & ${3-0})).$((${io4} & ${4-0}))"

echo "$NET\_ADDR"

}

## stop if iproute2 isn not installed

if ! [ -d "/etc/iproute2/" ]; then

echo "iproute2 policy routing is not available on this system - exiting"

exit

fi

## create the ipproute2 tables

if ! grep -q ${inbound\_table} /etc/iproute2/rt\_tables; then

echo "200 ${inbound\_table}" >> /etc/iproute2/rt\_tables

fi

if ! grep -q ${outbound\_table} /etc/iproute2/rt\_tables; then

echo "201 ${outbound\_table}" >> /etc/iproute2/rt\_tables

fi

## get the inbound and outbound networks from function

inbound\_net=$(get\_network ${inbound\_mask} ${inbound\_ip})

outbound\_net=$(get\_network ${outbound\_mask} ${outbound\_ip})

## create policy routes

ip rule add iif ${inbound\_interface} table ${inbound\_table}

ip rule add iif ${outbound\_interface} table ${outbound\_table}

ip addr add ${inbound\_ip}/${inbound\_mask} brd + dev
${inbound\_interface}

ip addr add ${outbound\_ip}/${outbound\_mask} brd + dev
${outbound\_interface}

ip route add ${inbound\_net}/${inbound\_mask} dev ${inbound\_interface}
src ${inbound\_ip} table ${inbound\_table}

ip route add ${inbound\_net}/${inbound\_mask} dev ${inbound\_interface}
src ${inbound\_ip} table ${outbound\_table}

ip route add ${outbound\_net}/${outbound\_mask} dev
${outbound\_interface} src ${outbound\_ip} table ${inbound\_table}

ip route add ${outbound\_net}/${outbound\_mask} dev
${outbound\_interface} src ${outbound\_ip} table ${outbound\_table}

ip route add default via ${outbound\_gw} table ${inbound\_table}

ip route add default via ${inbound\_gw} table ${outbound\_table}
