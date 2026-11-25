# Active Directory Administration and Ticketing

Hands-on practice of Active Directory administration and ticket handling in a home lab, using simulated support tickets.

## About

Fictional employees submit tickets in Spiceworks, and I work each one the way an IT support person would: ask questions if the request is unclear, make the change in Active Directory, check that it worked, and close the ticket. Tickets cover everyday tasks such as accounts, groups, permissions, lockouts, and domain joins. Each one is written up in this repo.

All changes are made through the GUI (Active Directory Users and Computers and other Windows Server tools).

The users and requests are fictional and I write the tickets myself, so steps like phoning a manager to confirm someone's identity are scripted.

## Home lab at a glance

Built in VirtualBox. Domain: `kerneltech.internal`

| Machine | Role | OS |
|---|---|---|
| DC-01 | Domain controller (AD DS), DNS server, DHCP server, RAS/NAT | Windows Server 2022 |
| WKSTN-001 | Domain-joined client | Windows 10 |
| WKSTN-002 | Domain-joined client | Windows 11 |

## Contents

- [environment.md](environment.md): lab diagram, how the domain was built, proof it works, OU and group layout, fictional users, tools