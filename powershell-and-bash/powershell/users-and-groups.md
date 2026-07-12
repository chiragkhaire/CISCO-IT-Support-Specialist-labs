# 8. Users & Groups

---

# Learning Objectives

After completing this chapter, I should be able to:

- Understand user accounts
- Understand local groups
- Differentiate between Local Users and Domain Users
- View users and groups using PowerShell
- Understand permissions
- Create, disable and remove local users
- Add users to groups
- Apply these concepts in real IT Support scenarios

---

# What is a User Account?

A **User Account** allows a person or service to sign in to a computer and access resources.

Every user account has its own:

- Username
- Password
- Permissions
- Profile
- Settings

Without a user account, Windows cannot determine who is using the computer.

---

# Types of User Accounts

## Local User

A Local User exists only on one computer.

Example

```
PC-01

Users

- Chirag
- Administrator
- Guest
```

If another computer exists on the network, these accounts do **not** automatically exist there.

---

## Domain User

A Domain User is managed by **Active Directory (AD)**.

Instead of creating users on every computer, the administrator creates the account once on the Domain Controller.

Example

```
Company Domain

CHIRAG.KHAIRE

↓

Can sign in to

PC-01

PC-02

Laptop-15

Finance-PC

HR-PC
```

This is one of the biggest advantages of Active Directory.

---

# Local Users vs Domain Users

| Local User | Domain User |
|------------|-------------|
| Exists on one computer | Exists in Active Directory |
| Managed locally | Managed by Domain Controller |
| Cannot log into other computers by default | Can log into multiple domain-joined computers |
| Suitable for home PCs | Suitable for organizations |

---

# What is a Group?

A **Group** is a collection of users.

Instead of assigning permissions to every user individually, administrators assign permissions to a group.

Example

```
Accounting Group

↓

Alice

Bob

Charlie
```

Grant permission to the group once, and all members receive that permission.

---

# Why Use Groups?

Imagine a company with 500 employees.

Without groups:

- Assign permissions 500 times.

With groups:

- Assign permissions once.

This saves time and reduces mistakes.

---

# Common Local Groups

| Group | Purpose |
|--------|----------|
| Administrators | Full control over the computer |
| Users | Standard user permissions |
| Guests | Temporary limited access |
| Backup Operators | Backup and restore files |
| Remote Desktop Users | Allowed to connect using Remote Desktop |

---

# View Local Users

## Command

```powershell
Get-LocalUser
```

## What it does

Displays all local user accounts.

Example

```
Administrator

Guest

Chirag
```

---

🧪 Try It Yourself

Run

```powershell
Get-LocalUser
```

Can you identify:

- Administrator
- Guest
- Your own account

---

# View Local Groups

```powershell
Get-LocalGroup
```

Displays every local security group on the computer.

---

# View Members of a Group

Example

```powershell
Get-LocalGroupMember Administrators
```

This displays every member of the Administrators group.

---

# Create a New Local User

```powershell
$password = Read-Host "Enter Password" -AsSecureString

New-LocalUser `
-Name "TestUser" `
-Password $password `
-FullName "Test User"
```

Administrator privileges are required.

---

# Disable a User Account

```powershell
Disable-LocalUser TestUser
```

Useful when an employee leaves temporarily or an account should no longer be used.

---

# Enable a User Account

```powershell
Enable-LocalUser TestUser
```

Re-enables a previously disabled account.

---

# Remove a User

```powershell
Remove-LocalUser TestUser
```

⚠️ Be careful.

Deleting a user account may remove access to files and settings associated with that account.

---

# Add a User to a Group

Example

```powershell
Add-LocalGroupMember `
-Group Administrators `
-Member TestUser
```

This grants TestUser Administrator privileges.

---

⚠️ Security Warning

Only add trusted users to the **Administrators** group.

Administrator accounts have full control over the system.

Follow the **Principle of Least Privilege**:

Give users only the permissions they need to perform their job.

---

# Remove a User from a Group

```powershell
Remove-LocalGroupMember `
-Group Administrators `
-Member TestUser
```

---

# Check the Current User

```powershell
whoami
```

Useful when troubleshooting permission-related issues.

---

# Real IT Support Scenario 1

## Ticket

> "The new employee starts today."

Tasks

- Create user account
- Assign password
- Add to the Users group
- Verify login

---

# Real IT Support Scenario 2

## Ticket

> "A former employee has left the company."

Tasks

- Disable account
- Remove unnecessary group memberships
- Document actions
- Delete account later according to company policy

---

# Real IT Support Scenario 3

## Ticket

> "A user cannot install software."

Investigation

Check whether the user belongs to the Administrators group.

```powershell
Get-LocalGroupMember Administrators
```

If not, determine whether administrative access is actually required before making changes.

---

# Mini Lab

A new employee joins the company.

Using only PowerShell:

1. View existing local users.
2. View existing local groups.
3. Create a new local user.
4. Add the user to a group.
5. Verify group membership.
6. Disable the account.
7. Re-enable the account.
8. Remove the account.

Think about the commands before looking below.

---

## Possible Solution

```powershell
Get-LocalUser

Get-LocalGroup

New-LocalUser

Add-LocalGroupMember

Get-LocalGroupMember Administrators

Disable-LocalUser

Enable-LocalUser

Remove-LocalUser
```

---

# Common Beginner Mistakes

❌ Giving every user Administrator rights.

❌ Deleting accounts instead of disabling them first.

❌ Forgetting to verify group membership.

❌ Ignoring the Principle of Least Privilege.

---

# Best Practices

✔ Follow the Principle of Least Privilege.

✔ Use groups instead of assigning permissions to individual users whenever possible.

✔ Disable accounts before deleting them.

✔ Document all account-related changes.

✔ Verify permissions after making changes.

---

# Quick Revision

✅ A User Account identifies a person or service.

✅ Local Users exist on one computer.

✅ Domain Users are managed by Active Directory.

✅ Groups simplify permission management.

✅ `Get-LocalUser` lists local users.

✅ `Get-LocalGroup` lists local groups.

✅ `Get-LocalGroupMember` displays group membership.

✅ Follow the Principle of Least Privilege.

---

# Interview Questions

1. What is the difference between a Local User and a Domain User?

2. Why do organizations use Groups?

3. What is the Principle of Least Privilege?

4. Which command lists all local users?

5. Which command displays members of the Administrators group?

6. Why should an account be disabled before being deleted?

7. A user cannot install software. How would you determine whether the issue is related to permissions?

8. What is the advantage of Active Directory over local user management?
