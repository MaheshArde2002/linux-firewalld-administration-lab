# Firewalld Administration Commands Cheat Sheet

This document contains the important firewalld, systemd, and network troubleshooting commands used in the Linux Firewalld Administration Lab.

---

## 1. Firewalld Service Management

### Check firewalld status

    systemctl status firewalld.service

### Start firewalld

    systemctl start firewalld.service

### Enable firewalld at system boot

    systemctl enable firewalld.service

### Restart firewalld

    systemctl restart firewalld.service

### Stop firewalld

    systemctl stop firewalld.service

### Disable firewalld at system boot

    systemctl disable firewalld.service

---

## 2. Firewalld Zone Management

### List all available zones

    firewall-cmd --get-zones

### Check the default zone

    firewall-cmd --get-default-zone

### Check active zones

    firewall-cmd --get-active-zones

### Display complete configuration of the default zone

    firewall-cmd --list-all

### Display configuration of the public zone

    firewall-cmd --zone=public --list-all

### List services in a specific zone

    firewall-cmd --zone=public --list-services

---

## 3. Service Management

### List currently allowed services

    firewall-cmd --list-services

### Add HTTP service temporarily

    firewall-cmd --add-service=http

### Add HTTP service permanently

    firewall-cmd --permanent --add-service=http

### Remove HTTP service permanently

    firewall-cmd --permanent --remove-service=http

### Add SSH service permanently

    firewall-cmd --permanent --add-service=ssh

### Remove SSH service permanently

    firewall-cmd --permanent --remove-service=ssh

### Remove RPC-Bind service permanently

    firewall-cmd --permanent --remove-service=rpc-bind

---

## 4. Port Management

### List currently allowed ports

    firewall-cmd --list-ports

### Add a port temporarily

    firewall-cmd --add-port=3306/tcp

### Add MySQL port permanently

    firewall-cmd --permanent --add-port=3306/tcp

### Remove MySQL port permanently

    firewall-cmd --permanent --remove-port=3306/tcp

### Add HTTP port directly

    firewall-cmd --permanent --add-port=80/tcp

### Remove HTTP port

    firewall-cmd --permanent --remove-port=80/tcp

---

## 5. Reload Firewalld

After making permanent configuration changes, reload firewalld.

    firewall-cmd --reload

Verify the configuration:

    firewall-cmd --list-all

---

## 6. Runtime vs Permanent Configuration

### Runtime configuration

A runtime rule affects the currently running firewall.

Example:

    firewall-cmd --add-port=3306/tcp

This rule is active immediately but is not saved permanently.

### Permanent configuration

A permanent rule is saved to the firewall configuration.

Example:

    firewall-cmd --permanent --add-port=3306/tcp

Reload firewalld to apply the permanent configuration:

    firewall-cmd --reload

### Check runtime configuration

    firewall-cmd --list-all

### Check permanent configuration

    firewall-cmd --permanent --list-all

---

## 7. Rich Rules

Rich rules allow more specific firewall conditions such as source IP addresses, services, ports, protocols, and actions.

### Add SSH drop rule for a specific IP

    firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.0.113" service name="ssh" drop'

### Reload firewalld

    firewall-cmd --reload

### List rich rules

    firewall-cmd --zone=public --list-rich-rules

### Remove the SSH rich rule

    firewall-cmd --permanent --zone=public --remove-rich-rule='rule family="ipv4" source address="192.168.0.113" service name="ssh" drop'

### Reload after removing the rule

    firewall-cmd --reload

---

## 8. Rich Rule Components

Example:

    firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.0.113" service name="ssh" drop'

### family="ipv4"

Specifies that the rule applies to IPv4 traffic.

### source address="192.168.0.113"

Specifies the source IP address.

### service name="ssh"

Specifies that the rule applies to SSH traffic.

### drop

Silently drops matching packets.

---

## 9. Network Troubleshooting

### Display IP addresses

    ip addr

### Display routing table

    ip r l

### Test network connectivity

    ping 192.168.0.105

### Test SSH connectivity

    ssh 192.168.0.105

### Check listening TCP ports

    ss -lntp

### Check whether port 3306 is listening

    ss -lntp | grep 3306

### Check whether SSH is listening

    ss -lntp | grep :22

---

## 10. SSH Connectivity Test

### Client

    192.168.0.113

### Server

    192.168.0.105

### Test connectivity

    ping 192.168.0.105

### Test SSH

    ssh 192.168.0.105

### Expected result before applying the rich rule

SSH connection should be successful if the SSH service is running and port 22 is allowed.

### Expected result after applying the drop rule

    ssh: connect to host 192.168.0.105 port 22: Connection timed out

---

## 11. Useful Verification Commands

### Show all allowed services

    firewall-cmd --list-services

### Show all allowed ports

    firewall-cmd --list-ports

### Show complete firewall configuration

    firewall-cmd --list-all

### Show public zone configuration

    firewall-cmd --zone=public --list-all

### Show rich rules

    firewall-cmd --zone=public --list-rich-rules

### Show permanent configuration

    firewall-cmd --permanent --list-all

### Check firewalld service status

    systemctl status firewalld

---

## 12. Common Firewall Troubleshooting Sequence

When a network service is not reachable, check the following:

### Step 1: Check IP address

    ip addr

### Step 2: Check routing

    ip r l

### Step 3: Test basic connectivity

    ping 192.168.0.105

### Step 4: Check whether the service is listening

    ss -lntp

### Step 5: Check firewalld status

    systemctl status firewalld

### Step 6: Check allowed services

    firewall-cmd --list-services

### Step 7: Check allowed ports

    firewall-cmd --list-ports

### Step 8: Check rich rules

    firewall-cmd --list-rich-rules

### Step 9: Test the application connection

    ssh 192.168.0.105

---

## 13. Commands Used in This Lab

### Firewalld service

    systemctl status firewalld.service
    systemctl start firewalld.service
    systemctl enable firewalld.service

### Zone inspection

    firewall-cmd --get-zones
    firewall-cmd --get-default-zone
    firewall-cmd --get-active-zones
    firewall-cmd --list-all

### Zone services

    firewall-cmd --zone=public --list-services
    firewall-cmd --zone=dmz --list-services
    firewall-cmd --zone=drop --list-services
    firewall-cmd --zone=block --list-services
    firewall-cmd --zone=home --list-services
    firewall-cmd --zone=libvirt --list-services
    firewall-cmd --zone=trusted --list-services
    firewall-cmd --zone=work --list-services
    firewall-cmd --zone=external --list-services

### Services and ports

    firewall-cmd --list-services
    firewall-cmd --list-ports

### HTTP

    firewall-cmd --permanent --add-service=http
    firewall-cmd --reload

### MySQL

    firewall-cmd --permanent --add-port=3306/tcp
    firewall-cmd --reload

### RPC-Bind removal

    firewall-cmd --permanent --remove-service=rpc-bind
    firewall-cmd --reload

### SSH connectivity

    ip r l
    ping 192.168.0.105
    ssh 192.168.0.105

### SSH rich rule

    firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.0.113" service name="ssh" drop'

    firewall-cmd --reload

    firewall-cmd --zone=public --list-rich-rules

### Verify restriction

    ssh 192.168.0.105

Expected:

    ssh: connect to host 192.168.0.105 port 22: Connection timed out

---

## 14. Quick Reference

| Task | Command |
|---|---|
| Check firewalld | `systemctl status firewalld` |
| Start firewalld | `systemctl start firewalld` |
| Enable at boot | `systemctl enable firewalld` |
| List zones | `firewall-cmd --get-zones` |
| Default zone | `firewall-cmd --get-default-zone` |
| Active zones | `firewall-cmd --get-active-zones` |
| Show configuration | `firewall-cmd --list-all` |
| List services | `firewall-cmd --list-services` |
| List ports | `firewall-cmd --list-ports` |
| Add HTTP | `firewall-cmd --permanent --add-service=http` |
| Add MySQL port | `firewall-cmd --permanent --add-port=3306/tcp` |
| Remove RPC-Bind | `firewall-cmd --permanent --remove-service=rpc-bind` |
| Reload firewall | `firewall-cmd --reload` |
| List rich rules | `firewall-cmd --list-rich-rules` |
| Check IP | `ip addr` |
| Check route | `ip r l` |
| Test connectivity | `ping 192.168.0.105` |
| Test SSH | `ssh 192.168.0.105` |
| Check listening ports | `ss -lntp` |

---

## Lab Summary

This cheat sheet covers the commands used to practice:

- Firewalld service management
- Firewall zones
- Firewall services
- Firewall ports
- Permanent configuration
- Runtime configuration
- Rich rules
- Source IP filtering
- SSH connectivity testing
- Network troubleshooting
- Firewall rule verification

