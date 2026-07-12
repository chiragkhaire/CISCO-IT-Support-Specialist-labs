# Windows Troubleshooting Guide

## Useful Commands

```cmd
ipconfig
ping
tracert
nslookup
hostname
whoami
systeminfo
tasklist
taskkill
netstat
sfc /scannow
DISM /Online /Cleanup-Image /RestoreHealth
chkdsk
gpupdate /force
shutdown /r /t 0
```

---

## Slow Computer

Possible causes

- Too many startup apps
- Low RAM
- Full storage
- Malware
- Windows updates

Checklist

- Check Task Manager
- Disable startup programs
- Free disk space
- Run Windows Update
- Scan for malware

---

## No Internet

Check

- Ethernet/Wi-Fi
- IP address
- DNS
- Gateway
- Router

Commands

```cmd
ipconfig
ping 8.8.8.8
ping google.com
ipconfig /flushdns
ipconfig /release
ipconfig /renew
```

---

## Blue Screen (BSOD)

Possible causes

- Faulty drivers
- Bad RAM
- Corrupted Windows files
- Hardware failure

Tools

- Event Viewer
- Windows Memory Diagnostic
- SFC
- DISM
