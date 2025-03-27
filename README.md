# MyNetworkNotes

# Building A Simple Home/Office Network with Packet-Tracer

# 1. Add Devices in this hierarchy to the Workspace

-- PC1
-- Switch0
-- RouterPT0
-- RouterPT1
-- Switch1
-- PC2 (Laptop)

-- Note PC1 and PC2 are end devices, while the routers and switches are network devices

# 2. Assign Name and Configure both Router Device (Router0 and Router1)
-- go to the router
-- enter the CLI
-- while booting up click ctrl + c to abort booting to enter rommon mode 
-- while in rommon mode go to the physical mode of the router to restart the router  
-- click 'no' in the system configuration dialog and click enter to get started where you will automatically enter the "USER EXEC MODE"
 
-- `enable or en` to go to the "PRIVILEEGED EXEC MODE"
-- `disable` to go back to the "USER EXEC MODE"
-- from the PRIVILEEGED EXEC MODE enter `show clock` to see the time and date 
-- `show history` to see all the list of commands
-- `show ip interface` to see all the interface running or enter `show ip interface brief` for a shorter description of all the running interfaces 
-- `configure terminal` to go to the "GLOBAL CONFIGURATION MODE"

-- The global configuration should look like this `Router(config)#`. Now assign a hostname with this command `hostname <AnyNameForHost>`

-- Secure Privileged EXEC Mode --
-- `enable secret <yourpassword>`

-- Secure User EXEC Mode (Console Access) --
-- `line console 0`
-- `password <yourpassword>`
-- `login`

-- Secure Remote SSH Access
-- `line vty 0 4`
-- `password <yourpassword>`
-- `login`
-- `transport input ssh`

-- Encrypt All Plaintext Passwords
-- `service password encryption` or `service password-encryption`

-- Provide Legal Notification (Banner Message)
-- `banner motd # <Unauthorized Access Prohibited> #`

-- Save the Configuration
-- `copy running-config startup-config`

-- Activate Interfaces and Assign IP addresses for both Router0 and Router1
RouterPT uses the FastEthernet Interface and it's configuration is beginner friendly

# For Router0
-- `interface FastEthernet1/0`
-- `ip address 192.168.2.1 255.255.255.252`
-- `no shutdown`
-- `exit`

# For Router1
-- `interface FastEthernet1/0`
-- `ip address 192.168.2.2 255.255.255.252`
-- `no shutdown`
-- `exit`

# 3. Properly connect all the devices

[PC0] ---- [Switch0] ---- [Router0] ---- [Router1] ---- [Switch1] ---- [PC1]

-- select the automatic cable to connect all devices except both Routers
-- use the cross-over cable to connect both routers 


# Subnetting  IPv4 Networks

# *IPv4 addressing*

IPv4 addresses are 32-bit logical address - Consists of a network portion and a host portion

*Characteristics Of IPv4*

-- Length will vary depending on the size of the network.

-- A network is a range of addresses

-- All devices on the same network have The same network portion (network ID) but a different host portion (host ID)

*Important Addresses to Determine In an IPv4 Network Range*

- Network Address (first address in the range): This is used to identify the network itself

- Broadcast Address (last address in the range) :- This is used to send a message on all devices in the network at once.

- First usable host (address after the network address)

- Last usable host (address before the broadcast address)

# *Binary Anding Process*

A binary Anding process is used to find the network address of a host.
By performing a bitwise AND operation between an IP address and its subnet mask, network devices can identify the network portion of the IP address.   
This is essential for routers to make forwarding decisions and for devices to determine if they are on the same network.

For Example,

Given the host Ipv4 address and Subnet mask 192.168.2.34/24

Using ANDing process find the network address of the host.

/24 subnet mask equals 255.255.255.0

![ANDing Process](https://github.com/user-attachments/assets/e7d6e7e8-43db-4922-8964-d5568e199357)

Thus, the network address in binary format is 11000000.10101000.00000010.00000000
Converting the Network Address back to decimal will be 192.168.2.0 /24

