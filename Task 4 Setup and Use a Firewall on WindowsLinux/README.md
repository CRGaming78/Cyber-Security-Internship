# Task 4: Setup and Use a Firewall on Linux (UFW)
---

## 1. Objective

The objective of this task was to configure and test basic firewall rules on a Linux system using UFW (Uncomplicated Firewall). The goal was to allow or block specific network traffic and document the process, thereby demonstrating a practical understanding of firewall management and network traffic filtering.

## 2. Tool Used

-   **Operating System:** `Kali Linux`
-   **Firewall Tool:** `UFW (Uncomplicated Firewall)`

## 3. Process and Documentation

Below are the steps taken to set up and test the firewall rules using UFW in the terminal.

### Step 1: Check Initial Firewall Status

First, I checked the status of UFW to see if it was active and to list any existing rules. It was initially inactive. I then enabled it, which is a crucial first step.

**Commands:**

```bash
sudo ufw status
sudo ufw enable
sudo ufw status verbose
```

**Screenshot 1: Initial Firewall Status**
This screenshot shows the output after enabling UFW and listing the default active rules.

<img src="/Task 4 Setup and Use a Firewall on WindowsLinux/Images/Image1.png">
 
---

### Step 2: Add a Rule to Block Port 23 (Telnet)

I added a rule to block all incoming traffic on TCP port 23. This is a standard security practice because Telnet is an insecure protocol.

**Command:**

```bash
sudo ufw deny 23/tcp
sudo ufw status
```

**Screenshot 2: Firewall with Block Rule Applied**
This screenshot shows the output of `sudo ufw status`, clearly listing the new `DENY` rule for port 23.

<img src="/Task 4 Setup and Use a Firewall on WindowsLinux/Images/Image2.png">

---

### Step 3: Test the Blocking Rule

To confirm the rule was working, I attempted to connect to port 23 on my own machine using the `telnet` client. The connection timed out, proving that the firewall was successfully blocking the traffic.

**Command:**

```bash
telnet localhost 23
```

**Screenshot 3: Testing the Telnet Block**
This screenshot shows the terminal after running the `telnet` command, demonstrating that the connection could not be established.

<img src="/Task 4 Setup and Use a Firewall on WindowsLinux/Images/Image3.png">

---

### Step 4: Add a Rule to Allow Port 22 (SSH)

To ensure remote access to the machine isn't cut off (a critical step for servers), I added a rule to explicitly allow incoming traffic on port 22 for SSH.

**Command:**

```bash
sudo ufw allow ssh
sudo ufw status
```

**Screenshot 4: Firewall with SSH Allow Rule**
This screenshot shows the updated rules list, which now includes an `ALLOW` rule for SSH (port 22).

<img src="/Task 4 Setup and Use a Firewall on WindowsLinux/Images/Image4.png">

---

### Step 5: Remove the Test Rule to Restore State

Finally, to clean up the configuration and restore the firewall to its standard operational state, I removed the temporary block rule for Telnet.

**Command:**

```bash
sudo ufw delete deny 23/tcp
sudo ufw status
```

**Screenshot 5: Final Firewall Status**
This screenshot shows the final state of the firewall after the Telnet block rule was successfully deleted.

<img src="/Task 4 Setup and Use a Firewall on WindowsLinux/Images/Image5.png">

---
