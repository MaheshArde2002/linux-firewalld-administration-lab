# Linux Firewalld Administration Lab

## Overview

This project is a hands-on Linux firewall administration lab using
firewalld.

The lab demonstrates how to manage the firewalld service, inspect
firewall zones, manage allowed services and ports, create permanent
firewall rules, remove unnecessary services, and configure advanced
rich rules.

The project also includes an SSH connectivity test before and after
applying an IP-based firewall restriction.

---

## Repository Name

`linux-firewalld-administration-lab`

---

## Lab Environment

- Operating System: CentOS / RHEL-based Linux
- Firewall: firewalld
- Server IP: `192.168.0.105`
- Client IP: `192.168.0.113`
- Firewall Zone: `public`
- Network Interface: `ens160`
- Protocol Tested: SSH
- SSH Port: `22/tcp`
- MySQL Port: `3306/tcp`
- HTTP Port: `80/tcp`

---

## Skills Demonstrated

- firewalld service management
- Linux firewall administration
- Firewall zones
- Active zone inspection
- Service-based firewall rules
- Port-based firewall rules
- Permanent firewall configuration
- Firewall configuration reload
- Service removal
- Rich rules
- Source IP-based traffic filtering
- SSH connectivity testing
- Basic network troubleshooting
- Firewall rule verification

---

# Project Structure

```text
linux-firewalld-administration-lab/
│
├── README.md
│
├── docs/
│   └── commands-cheatsheet.md
│
└── screenshots/
    ├── 01_firewalld_service_status_and_enable.png
    ├── 02_firewalld_zones_and_active_configuration.png
    ├── 03_firewalld_zones_and_services.png
    ├── 04_firewalld_list_services_and_ports.png
    ├── 05_firewalld_add_http_service_permanently.png
    ├── 06_firewalld_add_mysql_port_3306.png
    ├── 07_firewalld_remove_rpcbind_service.png
    ├── 08_ssh_connection_server_to_firewalld.png
    ├── 09_firewalld_add_rich_rule_ssh_drop.png
    └── 10_ssh_connection_timed_out.png