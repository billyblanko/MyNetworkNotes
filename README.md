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

![Image](https://github.com/user-attachments/assets/539c5c07-a9c3-4f0e-b7ec-9a3bbd4a61af)

Thus, the network address in binary format is 11000000.10101000.00000010.00000000
Converting the Network Address back to decimal will be 192.168.2.0 /24

# Subnetting With Magic Numbers

-- METHOD 1 

![Image](https://github.com/user-attachments/assets/490ffee1-1e02-4d7f-8e11-9e80a3571c26)

The number of borrowed network from your host determines the magic number value. For instance if you borrow 3 host bits from the host bit octets, The value is determined by; 2^(Remaining Number Of Host Bit Octets). 
Here is an example;
Using this subnet mask 255.255.255.240. 
STEP 1;
Convert the subnet mask to binary 
11111111.11111111.11111111.11110000

You achieve your Magic Number from your host octets
Host Octets= 11110000
where; 1's represents the borrowed network bits and 0's represents the host bits 
thus; we have 4 0's left 
therefore; 2^4 equals 16.

We just derived the magic number which is 16. 

-- METHOD 2
Using this subnet mask 255.255.255.240. 

The maximum subnet mask length is 255.255.255.256.

Convert the subnet mask to binary 
11111111.11111111.11111111.11110000

Focusing on the 0's subtract this host bits from the maximum length of a host octet (256)

256 - 240 = 16

Therefore your magic number is 16.

The Magic number helps you ascertain the specific number of addresses a subnet will increase in a network. 


# Subnetting An IPv4 Network 

 Create multiple subnets out of this IP address 192.168.0.0 /24

 1. For the first subnet is the LAN-A network you need a minimum of 50 hosts IP address.
 2. The second subnet is the LAN-B network, you need a minimum of 40 host IP address.
 3. You also need at least two additional unused subnet for future network expansion.
    Note: Variable length subnet mask will not be used. All of the device subnet masks should be the same length
4. Answer the following questions to help create a subnetting scheme that meets the stated network requirements
   a. How many host addresses are needed in the largest required subnets
   b. what is the minimum number of subnet required

The network you are tasked to subnet is 192.168.0.0 /24. 

The 192.168.0.0
11111111.11111111.00000000.00000000

/24 prefix length simply means the first 24 bits are all 1s 

Subnet Mask Value in Binary: 11111111.11111111.111111111.00000000
Subnet Mask Value in Decimal: 255.255.0

![Image](https://github.com/user-attachments/assets/0a07b568-931c-47d5-b468-6bc6508ae78f)

The first question states that LAN-A requires 50 hosts. This requirement falls under the /26 prefix 
The second question states that the LAN-B requires 40 hosts. This requirement falls under the same prefix length
The third qustion states that we need an additional two unused subnets for future expansion 
The fourth question: 
a. 62 usable host addresses are needed for the large network
b. the minimum number of subnets needed is 4

Now we can create a Subnetting Scheme for this table below 

![Image](https://github.com/user-attachments/assets/b26c9c29-8a76-4864-8a4f-d145fc9d8b76)

With this scheme we can achieve our network topology on packet tracer 

Completeing The Subnetting Scheme Table

Since the minimum number of subnets is 4

the first subnet is 192.168.0.0 /26 using the increment of the magic number `64` 4x. We will get;

192.168.0.0
192.168.0.64
192.168.0.128
192.168.0.192

In Details this is how structure looks like </br>
Subnet 1: 192.168.0.0/26
</br>
Network Address: 192.168.0.0 </br>
Broadcast Address: 192.168.0.63 </br>
First Usable Host: 192.168.0.1 </br>
Last Usable Host: 192.168.0.62

Subnet 2: 192.168.0.64/26
</br>
Network Address: 192.168.0.64 </br>
Broadcast Address: 192.168.0.127 </br>
First Usable Host: 192.168.0.65 </br>
Last Usable Host: 192.168.0.126

Subnet 3: 192.168.0.128/26 
</br>
Network Address: 192.168.0.128 </br> 
Broadcast Address: 192.168.0.191 </br>
First Usable Host: 192.168.0.129 </br>
Last Usable Host: 192.168.0.190

Subnet 4: 192.168.0.192/26
</br>
Network Address: 192.168.0.192 </br>
Broadcast Address: 192.168.0.255 </br>
First Usable Host: 192.168.0.193 </br>
Last Usable Host: 192.168.0.254

Complete IPv4 Addressing Scheme;

![Image](https://github.com/user-attachments/assets/135704d4-86ba-4fcd-80a1-fa76255f38b1)

Below is the IPv4 Subnetting Scheme Network Topology 

![Image](https://github.com/user-attachments/assets/39f4ffe5-c443-42b5-9b86-fd5d5fa1655d)
