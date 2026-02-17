# Spanning-Tree-STP-

In the world of Layer 2 networking, loops are the enemy. Without a mechanism to manage them, "Broadcast Storms" would consume all available bandwidth, crashing your network in seconds.

What is Spanning Tree Protocol?
STP is a Layer 2 network protocol (defined in IEEE 802.1D) that ensures a loop-free topology. It works by logically "blocking" redundant paths while keeping them on standby. If a primary link fails, STP automatically "unblocks" a backup path to keep data flowing.

Why do we use it?
Redundancy without Chaos: It allows for multiple physical paths between switches for high availability.

Prevents Broadcast Storms: Stops frames from looping endlessly around the network.

MAC Table Stability: Prevents "MAC flapping," where a switch gets confused about which port a device is actually on.

The Evolution: Types and Standards
Not all STP is created equal. Over the years, the protocol has evolved to become faster and more efficient:
<img width="1493" height="313" alt="image" src="https://github.com/user-attachments/assets/4d39c1b1-6af6-44c3-9ffc-73bfb37bd630" />

To identify the Root Bridge, Root Ports, and Designated Ports, Spanning Tree Protocol (STP) follows a specific hierarchy of rules. Think of it as an election where the "lowest" value always wins.

Here is the step-by-step logic used by the 802.1D standard:

1. How to Identify the Root Bridge (The "Election")
There is only one Root Bridge per network (or per VLAN). The switch with the lowest Bridge ID (BID) becomes the Root Bridge.

The Bridge ID consists of two parts:

Bridge Priority: (Default is 32768).

MAC Address: Used as a tie-breaker if priorities are equal.

The Rule:

Lowest Bridge Priority wins.

If priorities are a tie, the Lowest MAC Address wins.

2. How to Identify the Root Switch
Actually, the Root Switch is just another name for the Root Bridge. Once a switch wins the election based on the BID rules above, it is designated as the Root Switch/Bridge. All other switches are considered Non-Root Bridges.

3. How to Identify Root Ports (RP)
Every Non-Root Bridge must select exactly one Root Port. This is the port that provides the "cheapest" (fastest) path back to the Root Bridge.

The Decision Criteria (in order):

Lowest Root Path Cost: The sum of the bandwidth costs of the links to the Root (e.g., 10Gbps=2, 1Gbps=4, 100Mbps=19).
<img width="983" height="708" alt="image" src="https://github.com/user-attachments/assets/7c67c7b5-9864-4540-a2c0-5d201bd752b3" />

Lowest Neighbor Bridge ID: If costs are equal, the switch chooses the port connected to the neighbor with the lowest BID.

Lowest Neighbor Port Priority: (Default is 128).

Lowest Neighbor Port ID: The final tie-breaker (e.g., Fa0/1 wins over Fa0/2).

4. How to Identify Designated Ports (DP)
A Designated Port is the port on a network segment (the cable between two switches) that is allowed to forward traffic toward the Root Bridge.

The Rules:

All ports on the Root Bridge are Designated Ports (and they are always in Forwarding mode).

On a segment between two Non-Root switches, the switch with the lowest Root Path Cost gets the Designated Port.

If costs are tied, the switch with the lowest Bridge ID gets the Designated Port.

5. How to Identify Non-Designated Ports (Block/Alt)
A Non-Designated Port (also called a Blocking or Alternate port) is any port that is not a Root Port or a Designated Port. STP puts these into a "Blocking" state to break the loop.

Now we will do the lab

<img width="1529" height="1070" alt="Screenshot 2026-02-16 213400" src="https://github.com/user-attachments/assets/ee0879d0-5779-40a2-b621-ce59d2b28f1e" />

here down i have label the topology 
<img width="1516" height="1057" alt="Screenshot 2026-02-16 221005" src="https://github.com/user-attachments/assets/2ada646f-be63-4d62-9bd1-a14b29fafdea" />

the switch bridge is switch 3 bec it has the lowest Bridge Priority when compare to the other switches we will conform by looking at the spanning tree on the CLI 

<img width="2186" height="1367" alt="Screenshot 2026-02-16 220007" src="https://github.com/user-attachments/assets/ffe8d2b7-d90b-4c29-a760-e19e3e642071" />
now we will check all the switches spanning -tree on the CLI
<img width="1620" height="639" alt="Screenshot 2026-02-16 220901" src="https://github.com/user-attachments/assets/d74bf446-9aa2-4a56-a889-5f8277dde98b" />
<img width="1299" height="852" alt="Screenshot 2026-02-16 220822" src="https://github.com/user-attachments/assets/b614a2f2-6e49-49d7-bd9d-87aa0060e3ae" />


<img width="1314" height="752" alt="Screenshot 2026-02-16 220743" src="https://github.com/user-attachments/assets/430ecfd6-6b9f-470e-a5f1-a5f6fdcd60d3" />

