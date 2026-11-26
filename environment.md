# Lab Environment

This is an Active Directory home lab built in VirtualBox for hands-on practice of AD administration and ticketing. It uses the domain **kerneltech.internal**, based on a fictional company, Kernel Technologies.

![Lab structure](images/env-lab_structure.png)

## Tools and Software

| Tool / Software | Version / Edition |
|---|---|
| VirtualBox | 7.1.12 r169651 (Qt 6.5.3) |
| Windows Server 2022 | Standard Evaluation |
| Windows 10 | Pro |
| Windows 11 | Enterprise Evaluation |
| Ticketing tool | Spiceworks |

## Virtual Machines

| VM | OS | Role |
|---|---|---|
| DC-01 | Windows Server 2022 | Domain controller (AD DS), DNS server, DHCP server, RAS/NAT router |
| WKSTN-001 | Windows 10 Pro | Domain-joined client |
| WKSTN-002 | Windows 11 Enterprise Evaluation | Domain-joined client |

## Network Design

**DC-01 has two network adapters:**

| Adapter | Type | Configuration |
|---|---|---|
| Adapter 1 | NAT | Gets its address from VirtualBox automatically. Gives DC-01 internet access through the host and keeps the lab hidden from the home network. |
| Adapter 2 | Internal network (<internal network name>) | Static IP 172.18.0.10, subnet mask 255.255.255.0, DNS server 127.0.0.1 (loopback, because DC-01 runs the DNS server itself) |

**DHCP scope on DC-01:**

| Setting | Value |
|---|---|
| Range | 172.18.0.20 – 172.18.0.100 |
| Subnet mask | 255.255.255.0 |
| Gateway | 172.18.0.10 (DC-01) |
| DNS server | 172.18.0.10 (DC-01) |

**Workstations** (WKSTN-001, WKSTN-002) each have one internal adapter. They get their IP settings from the DHCP server on DC-01 and reach the internet through RAS/NAT on DC-01.

## OU Structure

```
kerneltech.internal
├── KernelTech
│   ├── IT
│   │   ├── Users
│   │   └── Computers
│   ├── HR
│   │   ├── Users
│   │   └── Computers
│   └── Sales
│       ├── Users
│       └── Computers
├── Groups
│   ├── Department Groups   (global)
│   └── Resource Groups     (domain local)
├── Admins
└── Disabled Users
```

## Users

All users are fictional.

| Name | Job title | Department |
|---|---|---|
| Vikram Malhotra | IT Manager | IT |
| Akash Yadav | Systems Administrator | IT |
| Neha Kapoor | Helpdesk Technician | IT |
| Arjun Nair | Helpdesk Technician | IT |
| Priya Sharma | HR Manager | HR |
| Anita Desai | HR Executive | HR |
| Karan Bhatia | HR Executive | HR |
| Sanjay Bhatia | Sales Manager | Sales |
| Meera Joshi | Sales Executive | Sales |
| Rahul Singh | Sales Executive | Sales |
| Divya Menon | Sales Executive | Sales |

**Admin account:** Akash Yadav (Admin), username adm-akash.yadav, in the Admins OU and a member of Domain Admins. Akash also has a normal account in IT/Users for daily work.

## Groups

Users are organised with global groups per department, and shared-folder access is controlled through domain local groups.

**Department groups** (Groups/Department Groups)

| Group | Scope | Description |
|---|---|---|
| GG_IT | Global | All IT department staff |
| GG_HR | Global | All HR department staff |
| GG_SALES | Global | All Sales department staff |
| GG_IT_HELPDESK | Global | Helpdesk technicians |

**Resource groups** (Groups/Resource Groups)

| Group | Scope | Description |
|---|---|---|
| DL_IT_SHARE | Domain Local | Access to the IT shared folder |
| DL_HR_SHARE | Domain Local | Access to the HR shared folder |
| DL_SALES_SHARE | Domain Local | Access to the Sales shared folder |

## File Shares

Three shared folders are hosted on DC-01. Each one gives Read permission to the matching domain local group.

| Share | Hosted on | Permission | Group |
|---|---|---|---|
| IT_SHARES | DC-01 | Read | DL_IT_SHARE |
| HR_SHARES | DC-01 | Read | DL_HR_SHARE |
| SALES_SHARES | DC-01 | Read | DL_SALES_SHARE |

## Screenshots

**DHCP address leases:** both workstations hold addresses from the 172.18.0.20–100 scope.

![DHCP address leases](images/env-dhcp_server.png)

**DNS Manager, forward lookup zone kerneltech.internal:** host records for the domain controller and both workstations.

![DNS Manager](images/env-dns_manager.png)

**Active Directory Users and Computers:** the OU structure.

![OU structure](images/env-ou_structure.png)




