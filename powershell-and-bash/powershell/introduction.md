# 1. Introduction to PowerShell

---

# What is PowerShell?

PowerShell is Microsoft's command-line shell and scripting language used to manage Windows computers.

Think of it as a smarter and more powerful version of Command Prompt (CMD).

PowerShell can:

- Run commands
- Automate tasks
- Manage Windows
- Troubleshoot problems
- Control services
- Configure networks
- Create scripts

---

# Why Was PowerShell Created?

Before PowerShell, Windows administrators mostly used Command Prompt.

CMD is useful but limited.

PowerShell was introduced because administrators needed a better way to:

- Automate repetitive work
- Manage hundreds of computers
- Retrieve detailed system information
- Configure Windows using commands
- Write reusable scripts

---

# CMD vs PowerShell

| CMD | PowerShell |
|------|------------|
| Older command shell | Modern command shell |
| Works mostly with text | Works with objects |
| Limited scripting | Powerful scripting language |
| Basic administration | Advanced administration |
| Few built-in commands | Thousands of built-in cmdlets |

---

# What are Objects?

This is the biggest difference between CMD and PowerShell.

CMD passes plain text.

Example:

```
Running
```

PowerShell passes an object.

An object contains multiple pieces of information.

For example, a service object may contain:

- Name
- Status
- Display Name
- Start Type
- Description

Instead of getting only text, PowerShell gives structured data that can be filtered, sorted, and reused.

---

# What is a Cmdlet?

A Cmdlet (pronounced **command-let**) is a built-in PowerShell command.

Cmdlets follow a simple naming convention:

```
Verb-Noun
```

Examples:

```powershell
Get-Service
Get-Process
Get-Help
Get-Date
Set-Location
```

Notice that every command starts with a verb.

Examples of common verbs:

| Verb | Meaning |
|------|---------|
| Get | Retrieve information |
| Set | Change something |
| Start | Start a process |
| Stop | Stop a process |
| Restart | Restart something |
| Remove | Delete |
| New | Create |
| Test | Check something |

---

# Where Can You Open PowerShell?

You can launch PowerShell from:

- Start Menu
- Windows Terminal
- Run → powershell
- Windows Search
- Right-click Start Menu (depending on Windows version)

---

# Why IT Support Engineers Use PowerShell

PowerShell allows IT professionals to perform tasks much faster than using graphical menus.

Examples include:

- Viewing system information
- Checking running services
- Listing installed software
- Managing users
- Testing network connectivity
- Viewing event logs
- Diagnosing Windows issues

---

# Quick Revision

✅ PowerShell is Microsoft's command-line shell.

✅ It is used for administration and automation.

✅ PowerShell works with objects.

✅ Built-in commands are called Cmdlets.

✅ Cmdlets follow the Verb-Noun format.

---

# Interview Questions

### 1. What is PowerShell?

### 2. Why is PowerShell preferred over CMD?

### 3. What is a Cmdlet?

### 4. What is the Verb-Noun naming convention?

### 5. What is the biggest difference between CMD and PowerShell?
