# 🌐 Remote Access to Cisco Switch Using Telnet

### 🖥️ Cisco Packet Tracer | Switching Technologies | Remote Device Management

---

## 📌 Project Overview

This project demonstrates how to configure **remote access to a Cisco switch using Telnet** with Cisco Packet Tracer.

The main objective is to remotely manage a Cisco switch from an **Admin PC** without directly connecting a console cable to the switch.

In this lab, the switch is configured with a **management IP address**, hostname, domain name, local username and password, VTY lines, and Telnet access.

---

## 🎯 Project Objectives

The main objectives of this project were to:

* 🔹 Understand remote device management
* 🔹 Configure IP addressing on network devices
* 🔹 Configure a management IP address on a switch
* 🔹 Configure a default gateway on the switch
* 🔹 Configure hostname and domain name
* 🔹 Create a local username and password
* 🔹 Configure VTY lines
* 🔹 Enable local authentication
* 🔹 Allow Telnet as a remote access protocol
* 🔹 Test connectivity using `ping`
* 🔹 Remotely access the switch from an Admin PC
* 🔹 Verify the remote login and privileged EXEC access

---

## 🧠 Remote Access Methods

Cisco devices can be managed remotely or locally using different methods.

### 🔌 1. Console Access

A console cable can be directly connected between the PC and the switch.

```text
PC
 │
 │ Console Cable
 │
 ▼
Cisco Switch
```

This method requires **physical access** to the device.

### 🌐 2. Remote Access

With remote access, an administrator can manage the switch over the network.

In this project:

```text
Admin PC
    │
    │ Network
    ▼
 Router
    │
    │ Network
    ▼
Cisco Switch
```

The focus of this lab is **Telnet-based remote access**.

> ⚠️ Telnet sends communication, including credentials, without encryption. For production environments, **SSH is strongly preferred**.

---

# 🗺️ Network Topology

The topology contains:

* 💻 Admin PC
* 💻 Additional host PC
* 🌐 Router
* 🖧 Cisco Switch
* 🔗 Network connections between the devices

### 🌐 IP Addressing Plan

| Device   | Interface | IP Address         | Purpose           |
| -------- | --------- | ------------------ | ----------------- |
| Router   | G0/0      | `192.168.1.1/24`   | Gateway           |
| Router   | G0/1      | `192.168.2.1/24`   | Gateway           |
| Admin PC | NIC       | `192.168.2.10/24`  | Remote Management |
| Host PC  | NIC       | `192.168.1.10/24`  | Network Host      |
| Switch   | VLAN 1    | `192.168.2.254/24` | Management IP     |

---

# ⚙️ Configuration Steps

## 1️⃣ Build the Network Topology

Created the required network topology in Cisco Packet Tracer.

The main objective is to remotely manage the switch from the Admin PC through the network.

---

## 2️⃣ Configure IP Addresses

Configured IP addresses on the router and end devices according to the network design.

### Router G0/0

```bash
interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
```

### Router G0/1

```bash
interface gigabitEthernet 0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
```

The appropriate default gateway was configured on the end devices.

---

## 3️⃣ Configure the Switch Management IP

A management IP address was configured on **VLAN 1**.

```bash
enable
configure terminal

interface vlan 1
ip address 192.168.2.254 255.255.255.0
no shutdown
exit
```

### 🌐 Configure Default Gateway

Since the switch needs to communicate with devices outside its local network, a default gateway was configured:

```bash
ip default-gateway 192.168.2.1
```

---

## 4️⃣ Configure Hostname, Domain Name & Credentials

A hostname was configured to identify the switch.

```bash
hostname S1
```

A domain name was configured:

```bash
ip domain-name cisco.com
```

A local username and password were created:

```bash
username admin password Cisco
```

These credentials are used for local authentication during Telnet login.

---

## 5️⃣ Configure VTY Lines for Telnet

The VTY lines were configured to allow remote management sessions.

```bash
line vty 0 15
login local
transport input telnet
```

### 🔍 Configuration Explanation

#### `line vty 0 15`

Provides access to the virtual terminal lines used for remote connections.

#### `login local`

Tells the switch to authenticate users using the locally configured username and password.

#### `transport input telnet`

Allows Telnet connections to the VTY lines.

---

## 6️⃣ Test Connectivity from Admin PC

Before attempting Telnet access, connectivity to the switch management IP was tested.

```bash
ping 192.168.2.254
```

### ✅ Expected Result

The Admin PC should successfully reach the switch management IP.

```text
Admin PC
   │
   │ ping
   ▼
192.168.2.254
Switch Management IP
```

Successful ping confirms basic IP connectivity between the Admin PC and the switch.

---

## 7️⃣ Connect to the Switch Using Telnet

From the Admin PC, the switch was accessed using the Telnet command.

```bash
telnet 192.168.2.254
```

The switch then requested the configured local credentials:

```text
Username: admin
Password: Cisco
```

After successful authentication, remote access to the switch was established.

---

## 8️⃣ Enter Privileged EXEC Mode

After logging into the switch remotely, privileged EXEC mode was accessed using:

```bash
enable
```

The configured enable password was then entered.

Example configuration:

```bash
enable password Cisco
```

After successful authentication, the administrator could access privileged configuration commands remotely.

---

# 🔍 Verification

The following tests were performed to verify the configuration.

### 🧪 Test 1 — Ping the Switch

```bash
ping 192.168.2.254
```

✅ Confirmed IP connectivity between the Admin PC and the switch.

### 🧪 Test 2 — Telnet Access

```bash
telnet 192.168.2.254
```

✅ Confirmed successful remote login.

### 🧪 Test 3 — Local Authentication

```text
Username: admin
Password: Cisco
```

✅ Confirmed that the switch was using the local user database.

### 🧪 Test 4 — Privileged EXEC Access

```bash
enable
```

✅ Confirmed access to privileged EXEC mode after entering the enable password.

---

# 🔑 Important Cisco IOS Commands

### 🌐 Management IP

```bash
interface vlan 1
ip address 192.168.2.254 255.255.255.0
no shutdown
```

### 🚪 Default Gateway

```bash
ip default-gateway 192.168.2.1
```

### 🏷️ Hostname

```bash
hostname S1
```

### 🌍 Domain Name

```bash
ip domain-name cisco.com
```

### 👤 Local User

```bash
username admin password Cisco
```

### 🔐 VTY Configuration

```bash
line vty 0 15
login local
transport input telnet
```

### 🔑 Enable Password

```bash
enable password Cisco
```

### 🧪 Connectivity Test

```bash
ping 192.168.2.254
```

### 🌐 Telnet Connection

```bash
telnet 192.168.2.254
```

---

# 🧪 Final Results

The configuration was successfully completed and verified.

| Test                             | Result       |
| -------------------------------- | ------------ |
| 🌐 Management IP configured      | ✅ Successful |
| 🚪 Default gateway configured    | ✅ Successful |
| 🏷️ Hostname configured          | ✅ Successful |
| 🌍 Domain name configured        | ✅ Successful |
| 👤 Local user configured         | ✅ Successful |
| 🔐 VTY authentication configured | ✅ Successful |
| 🌐 Telnet enabled                | ✅ Successful |
| 📡 Ping to switch                | ✅ Successful |
| 💻 Remote Telnet login           | ✅ Successful |
| 🔑 Privileged EXEC access        | ✅ Successful |

---

# 🧠 Key Concepts Learned

Through this hands-on project, I practiced:

* 🌐 IP Addressing
* 🖧 Switch Management IP
* 🚪 Default Gateway Configuration
* 🏷️ Hostname Configuration
* 🌍 Domain Name Configuration
* 👤 Local User Authentication
* 🔐 VTY Line Configuration
* 📡 Telnet Remote Access
* 🧪 Ping Testing
* 🔍 Network Connectivity Verification
* 🛠️ Basic Cisco IOS Troubleshooting
* 💻 Remote Device Management

---

# 🔐 Security Note

Telnet is useful for learning and lab environments, but it is **not recommended for production networks** because Telnet does not encrypt the communication between the administrator and the network device.

For secure remote management, **SSH (Secure Shell)** should be used.

### Telnet

```text
❌ Unencrypted
❌ Credentials can be exposed
```

### SSH

```text
✅ Encrypted
✅ More secure
✅ Recommended for production
```

The next logical lab after this project is:

**🔐 Configuring Secure Remote Access Using SSH**

---

# 🛠️ Technologies & Tools

| Category              | Technology                |
| --------------------- | ------------------------- |
| 🖥️ Network Simulator | Cisco Packet Tracer       |
| 🌐 Networking         | Cisco Routing & Switching |
| 📡 Remote Access      | Telnet                    |
| 🔐 Authentication     | Local User Database       |
| 💻 CLI                | Cisco IOS                 |
| 🧪 Testing            | Ping & Telnet             |

---

# 🚀 Future Improvements

This lab can be extended by implementing:

* 🔐 SSH Remote Access
* 👤 Secure User Authentication
* 🔑 Secret Password Configuration
* 🛡️ Password Encryption
* 🔒 Login Security
* ⏱️ Session Timeout
* 🚨 Login Blocking / Security Controls
* 🔥 Access Control Lists
* 📡 Secure Network Management

---

## 👨‍💻 Project Information

**📚 Learning Area:** Switching Technologies
**🎯 Focus:** Remote Access & Device Management
**🖥️ Platform:** Cisco Packet Tracer
**📡 Protocol:** Telnet
**🔰 Level:** Beginner / Entry-Level Network Engineering
**🧪 Project Type:** Hands-on Networking Lab

---

⭐ **This project is part of my hands-on networking practice focused on developing practical Cisco IOS, network management, remote access, and troubleshooting skills.**
