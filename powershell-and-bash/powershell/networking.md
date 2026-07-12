# 5. Networking with PowerShell

---

# Learning Objectives

After completing this chapter, I should be able to:

- View network configuration
- Check IP addresses
- Identify DNS and Default Gateway
- Test internet connectivity
- Test whether a remote port is open
- Resolve domain names
- View network adapters
- Troubleshoot common networking issues using PowerShell

---

# Why is Networking Important?

Almost every IT Support job involves troubleshooting network problems.

Examples include:

- No Internet access
- Cannot access company servers
- VPN not connecting
- DNS resolution failures
- Slow network performance
- Printer not reachable
- File shares inaccessible

PowerShell provides built-in tools to diagnose these issues quickly.

---

# Check Network Configuration

## Command

```powershell
Get-NetIPConfiguration
```

## What it does

Displays the current network configuration, including:

- Computer Name
- Network Adapter
- IPv4 Address
- IPv6 Address
- Default Gateway
- DNS Servers

---

## Example Output

```
Ethernet

IPv4 Address : 192.168.1.100

Default Gateway : 192.168.1.1

DNS Server : 8.8.8.8
```

---

💡 Pro Tip

This cmdlet provides the same type of information as:

```cmd
ipconfig /all
```

but in a cleaner PowerShell format.

---

🧪 Try It Yourself

Run:

```powershell
Get-NetIPConfiguration
```

Can you identify:

- Your IPv4 Address?
- Your Default Gateway?
- Your DNS Server?

---

# View Network Adapters

## Command

```powershell
Get-NetAdapter
```

## What it does

Lists all physical and virtual network adapters.

Example:

```
Ethernet

Wi-Fi

Bluetooth Network Connection

Hyper-V Virtual Ethernet Adapter
```

---

## Why is this useful?

Sometimes the network adapter is disabled.

Instead of opening Device Manager, PowerShell can quickly show its status.

---

# Check Adapter Status

```powershell
Get-NetAdapter | Select Name, Status
```

---

# Test Internet Connectivity

## Command

```powershell
Test-Connection google.com
```

This is PowerShell's version of:

```cmd
ping google.com
```

---

## Send Only Four Requests

```powershell
Test-Connection google.com -Count 4
```

---

## Example Output

```
Source

Destination

Latency

Status
```

---

💡 Pro Tip

If `Test-Connection` fails:

Ask yourself:

- Is the adapter connected?
- Does the computer have an IP address?
- Is DNS working?
- Is the Default Gateway reachable?

---

# Resolve DNS

## Command

```powershell
Resolve-DnsName google.com
```

## What it does

Converts a domain name into an IP address.

Example

```
google.com

↓

142.250.xxx.xxx
```

---

## Why is this useful?

If DNS fails:

Users may say:

> "The internet isn't working."

But actually:

The internet works.

Only DNS is broken.

---

🧪 Try It Yourself

Run

```powershell
Resolve-DnsName github.com
```

Did PowerShell return an IP address?

---

# Test Whether a Port is Open

## Command

```powershell
Test-NetConnection google.com -Port 443
```

---

## Why is this useful?

Suppose a user says:

> "I can't access our company's website."

Instead of guessing:

Test whether HTTPS (Port 443) is reachable.

---

Example Output

```
TcpTestSucceeded : True
```

If False:

The service may be offline.

A firewall may be blocking traffic.

The port may not be open.

---

# View Routing Table

## Command

```powershell
Get-NetRoute
```

---

## What is a Route?

A route tells Windows:

> "Where should I send this network traffic?"

Every computer has a routing table.

---

# View DNS Client Cache

## Command

```powershell
Get-DnsClientCache
```

---

## Clear DNS Cache

```powershell
Clear-DnsClientCache
```

---

## Why?

Sometimes websites fail because Windows remembers an old DNS record.

Clearing the cache forces Windows to request fresh DNS information.

---

# Restart a Network Adapter

Disable

```powershell
Disable-NetAdapter -Name "Wi-Fi"
```

Enable

```powershell
Enable-NetAdapter -Name "Wi-Fi"
```

⚠️ Administrator privileges are required.

---

# Real IT Support Scenario

## Ticket

A user reports:

> "I can connect to Wi-Fi but websites won't load."

---

### Step 1

Check IP Configuration

```powershell
Get-NetIPConfiguration
```

---

### Step 2

Test Internet

```powershell
Test-Connection 8.8.8.8
```

---

### Step 3

Test DNS

```powershell
Resolve-DnsName google.com
```

---

### Step 4

Check HTTPS Connectivity

```powershell
Test-NetConnection google.com -Port 443
```

---

### Step 5

Clear DNS Cache

```powershell
Clear-DnsClientCache
```

---

# Mini Lab

A user reports:

- Wi-Fi connected
- No websites open
- Microsoft Teams is offline

Using only PowerShell:

1. Check IP configuration.

2. Verify adapter status.

3. Test Internet connectivity.

4. Test DNS.

5. Test HTTPS.

6. Clear DNS cache if necessary.

Think about which commands you would run before looking below.

---

## Possible Solution

```powershell
Get-NetIPConfiguration

Get-NetAdapter

Test-Connection google.com

Resolve-DnsName google.com

Test-NetConnection google.com -Port 443

Clear-DnsClientCache
```

---

# Common Beginner Mistakes

❌ Assuming "No Internet" always means the ISP is down.

❌ Forgetting to verify DNS.

❌ Restarting the computer before collecting information.

❌ Ignoring the status of the network adapter.

---

# Best Practices

✔ Start with IP configuration.

✔ Verify adapter status.

✔ Test connectivity before making changes.

✔ Document the commands you use.

✔ Always verify that the issue is resolved before closing the ticket.

---

# Quick Revision

✅ `Get-NetIPConfiguration` displays IP settings.

✅ `Get-NetAdapter` shows network adapters.

✅ `Test-Connection` checks connectivity.

✅ `Resolve-DnsName` resolves domain names.

✅ `Test-NetConnection` tests specific ports.

✅ `Get-NetRoute` displays the routing table.

✅ `Clear-DnsClientCache` clears cached DNS records.

---

# Interview Questions

1. What information does `Get-NetIPConfiguration` provide?

2. What is the difference between `Test-Connection` and `Test-NetConnection`?

3. Why would you use `Resolve-DnsName`?

4. What is the purpose of a Default Gateway?

5. Why would you clear the DNS cache?

6. A user says, "I can connect to Wi-Fi but no websites load." Walk through your troubleshooting process using PowerShell.
