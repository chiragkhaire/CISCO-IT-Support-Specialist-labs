# 7. Windows Event Logs

---

# Learning Objectives

After completing this chapter, I should be able to:

- Understand Windows Event Logs
- Understand Event Viewer
- Identify different log types
- Understand Event Levels
- Search Windows logs using PowerShell
- Filter logs efficiently
- Troubleshoot common Windows issues using event logs

---

# What are Event Logs?

Every important activity inside Windows is recorded in a log.

Think of it as a security camera for your operating system.

Whenever Windows starts...

Whenever a program crashes...

Whenever a user logs in...

Whenever a service fails...

Windows records an event.

These records help IT Support engineers understand **what happened, when it happened, and why it happened.**

---

# Why are Event Logs Important?

Suppose a user says:

> "My computer suddenly restarted."

Simply asking questions may not reveal the cause.

Instead, check the event logs.

Windows may tell you:

- Unexpected Shutdown
- Power Failure
- Driver Crash
- Blue Screen
- Disk Error
- Windows Update Failure

---

# Where are Event Logs Stored?

You can view them using:

**Event Viewer**

Open:

```
Start → Event Viewer
```

or

```
Run

eventvwr.msc
```

PowerShell can access the same logs without opening Event Viewer.

---

# Types of Windows Logs

| Log | Purpose |
|------|----------|
| Application | Application events |
| Security | Login, authentication and security events |
| System | Windows components, drivers and services |
| Setup | Windows installation events |
| Forwarded Events | Events collected from other computers |

---

# Event Levels

Every event has a severity level.

| Level | Meaning |
|--------|----------|
| Information | Normal operation |
| Warning | Something may become a problem |
| Error | Something failed |
| Critical | Serious failure requiring immediate attention |

---

# View Available Logs

## Command

```powershell
Get-EventLog -List
```

---

## What does it do?

Lists all classic Windows Event Logs.

Example:

```
Application

System

Security
```

---

🧪 Try It Yourself

Run:

```powershell
Get-EventLog -List
```

How many logs are available on your computer?

---

# View Recent System Events

## Command

```powershell
Get-EventLog System -Newest 20
```

---

## What does it do?

Displays the newest 20 events from the System log.

---

# View Recent Application Events

```powershell
Get-EventLog Application -Newest 20
```

---

# View Error Events Only

```powershell
Get-EventLog System |
Where-Object EntryType -eq Error
```

---

## Why is this useful?

Instead of scrolling through hundreds of entries, display only actual errors.

---

# View Warning Events

```powershell
Get-EventLog System |
Where-Object EntryType -eq Warning
```

---

# Search for a Specific Event

Example

```powershell
Get-EventLog System |
Where-Object Source -like "*Disk*"
```

Useful for locating storage-related problems.

---

# Search by Event ID

Every Windows event has a unique Event ID.

Example:

```powershell
Get-EventLog System |
Where-Object EventID -eq 6008
```

---

## Common Event IDs

| Event ID | Meaning |
|-----------|----------|
| 41 | Unexpected Shutdown (Kernel-Power) |
| 6005 | Event Log Service Started |
| 6006 | Event Log Service Stopped |
| 6008 | Unexpected Shutdown |
| 1074 | Planned Restart or Shutdown |

---

💡 Pro Tip

Do not memorize Event IDs.

Instead, learn how to search for them.

Microsoft's documentation explains each Event ID in detail.

---

# Modern Event Logs

PowerShell also provides a newer command:

```powershell
Get-WinEvent
```

Unlike `Get-EventLog`, it supports newer Windows event logs and offers better filtering.

Example:

```powershell
Get-WinEvent -LogName System -MaxEvents 20
```

---

# Why Use Get-WinEvent?

Advantages:

- Faster
- Supports modern event logs
- Better filtering
- Recommended for newer versions of Windows

---

# Real IT Support Scenario 1

## Ticket

> "The computer restarted overnight."

### Investigation

Check recent system events.

```powershell
Get-WinEvent -LogName System -MaxEvents 50
```

Look for:

- Event ID 41
- Event ID 6008

These may indicate an unexpected shutdown.

---

# Real IT Support Scenario 2

## Ticket

> "An application keeps crashing."

### Investigation

Check the Application log.

```powershell
Get-WinEvent -LogName Application -MaxEvents 50
```

Look for:

- Error
- Warning

Identify the application name and event details.

---

# Real IT Support Scenario 3

## Ticket

> "Windows Update failed."

Check:

```powershell
Get-WinEvent -LogName Setup -MaxEvents 30
```

Review recent setup-related events for update failures.

---

# Mini Lab

A user reports:

- Computer restarted unexpectedly.
- Microsoft Word crashed.
- Windows Update failed yesterday.

Using only PowerShell:

1. View the newest System events.
2. Search for unexpected shutdown events.
3. View recent Application events.
4. View recent Setup events.
5. Identify any Error or Critical entries.

Think about which commands you would use before checking below.

---

## Possible Solution

```powershell
Get-WinEvent -LogName System -MaxEvents 50

Get-EventLog System |
Where-Object EventID -eq 6008

Get-WinEvent -LogName Application -MaxEvents 50

Get-WinEvent -LogName Setup -MaxEvents 50
```

---

# Common Beginner Mistakes

❌ Ignoring Event Logs completely.

❌ Looking only at the newest event.

❌ Assuming every Warning indicates a serious issue.

❌ Restarting the computer without collecting evidence.

---

# Best Practices

✔ Review Event Logs before making major changes.

✔ Record important Event IDs in your troubleshooting notes.

✔ Correlate events with the time the issue occurred.

✔ Use `Get-WinEvent` for modern Windows systems.

---

# Quick Revision

✅ Windows records important system activities in Event Logs.

✅ Event Viewer displays these logs graphically.

✅ `Get-EventLog` accesses classic logs.

✅ `Get-WinEvent` is the recommended modern cmdlet.

✅ Event IDs help identify specific problems.

✅ Event Levels indicate the severity of an event.

---

# Interview Questions

1. What are Windows Event Logs?

2. Why are Event Logs useful for IT Support?

3. What is the difference between `Get-EventLog` and `Get-WinEvent`?

4. What information does Event ID 6008 indicate?

5. Which Windows log would you check if Microsoft Word keeps crashing?

6. A user reports an unexpected restart. How would you investigate using PowerShell?
