<p align="center">


<h2>Video Demonstration</h2>

- ### [YouTube: Day 32 Lab: IPv6 Configuration Pt. 2](https://www.youtube.com/watch?v=xkq7FN9KP7o)

<h2>Environments and Technologies Used</h2>

- Jeremy's IT Lab Youtube Channel
- Cisco Packet Tracer
  

  
<h2>Operating Systems Used </h2>

- Cisco IOS


<h2>Step-by-Step</h2>

<b>🔹 Step 1 — Configure IPv6 with EUI-64 on R1 & R2</b>

✅ On R1

Check MAC address:

ENABLE

SHOW INTERFACES G0/1

Enable IPv6 routing:

CONF T

IPV6 UNICAST-ROUTING

Configure IPv6 using EUI-64:

INTERFACE G0/1

IPV6 ADDRESS 2001:DB8::/64 EUI-64

Verify:

DO SHOW IPV6 INTERFACE BRIEF

✅ On R2

Check MAC address:

ENABLE

SHOW INTERFACES G0/1

Enable IPv6 routing:

CONF T

IPV6 UNICAST-ROUTING

Configure IPv6 using EUI-64:

INTERFACE G0/1

IPV6 ADDRESS 2001:DB8:0:1::/64 EUI-64

Verify:

DO SHOW IPV6 INTERFACE BRIEF

<b>🔹 Step 2 — Configure IPv6 on PCs</b>

🖥️ PC1

IPv6 Address: 2001:DB8::2/64

Default Gateway: (R1 G0/1 IPv6 address from EUI-64)

🖥️ PC2

IPv6 Address: 2001:DB8:0:1::2/64

Default Gateway: (R2 G0/1 IPv6 address from EUI-64)

<b>🔹 Step 3 — Enable IPv6 on Interfaces (Link-Local Only)</b>

✅ On R1

INTERFACE G0/0

IPV6 ENABLE

✅ On R2

INTERFACE G0/0

IPV6 ENABLE

🔍 Verify:

DO SHOW IPV6 INTERFACE BRIEF

✔️ You should see:

Link-local addresses (FE80::)

Automatically generated from MAC (EUI-64)

<b>🔹 Step 4 — Configure IPv6 Static Routes</b>

📌 Key Rule:

When using a link-local next-hop, you MUST specify:

Exit interface AND

Next-hop address

✅ On R1 (route to PC2 network)

CONF T

IPV6 ROUTE 2001:DB8:0:1::/64 G0/0 <R2_LINK_LOCAL>

✅ On R2 (route to PC1 network)

CONF T

IPV6 ROUTE 2001:DB8::/64 G0/0 <R1_LINK_LOCAL>

<b>🔹 Step 5 — Test Connectivity</b>

🖥️ From PC1:

PING 2001:DB8:0:1::2

✔️ Should succeed
