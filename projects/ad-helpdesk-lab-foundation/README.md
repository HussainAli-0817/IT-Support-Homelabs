# Active Directory Help Desk Lab Foundation

This project is my fresh Active Directory help desk lab build. I set up a Windows Server domain controller, joined a Windows 10 client to the domain, created a basic OU structure, created test users, and practiced adding a user to a security group.

The goal was to build a clean lab that I can use for future help desk projects like password resets, account unlocks, onboarding, offboarding, file share permissions, and group access tickets.

## Lab Setup

| Machine | Purpose | IP Address |
| --- | --- | --- |
| `DC01` | Windows Server 2022 domain controller | `192.168.10.10` |
| `WIN10-CLIENT01` | Windows 10 domain client | `192.168.10.20` |

Domain:

`homelab.local`

## What I Built

- Created two VirtualBox VMs: `DC01` and `WIN10-CLIENT01`.
- Set both VMs on the same internal VirtualBox network.
- Configured static IP addresses.
- Tested network connectivity both ways with `ping`.
- Installed Active Directory Domain Services on `DC01`.
- Promoted `DC01` to a domain controller for `homelab.local`.
- Opened Active Directory Users and Computers and confirmed the domain.
- Created a `HomeLab` OU.
- Created OUs for `Users`, `Computers`, `Groups`, and `Disabled Users`.
- Created test users `Ada Lovelace` and `Grace Hopper`.
- Joined `WIN10-CLIENT01` to the domain.
- Logged into `WIN10-CLIENT01` as `homelab\ada.lovelace`.
- Created a test security group and added Ada to it.

## Evidence

| Step | Screenshot |
| --- | --- |
| `DC01` running in VirtualBox | [01-dc01-running.png](assets/01-dc01-running.png) |
| `WIN10-CLIENT01` running in VirtualBox | [02-win10-client-running.png](assets/02-win10-client-running.png) |
| `DC01` static IP set | [03-dc01-static-ip.png](assets/03-dc01-static-ip.png) |
| `WIN10-CLIENT01` static IP set | [04-win10-static-ip.png](assets/04-win10-static-ip.png) |
| Windows 10 client pinging `DC01` | [05-win10-ping-dc01.png](assets/05-win10-ping-dc01.png) |
| `DC01` pinging Windows 10 client | [06-dc01-ping-win10.png](assets/06-dc01-ping-win10.png) |
| `DC01` promoted to domain controller | [07-dc01-domain-controller.png](assets/07-dc01-domain-controller.png) |
| ADUC opened with `homelab.local` | [08-aduc-open.png](assets/08-aduc-open.png) |
| `HomeLab` OU structure | [09-ou-structure.png](assets/09-ou-structure.png) |
| Test users created | [10-test-users-created.png](assets/10-test-users-created.png) |
| Windows 10 client joined to domain | [11-win10-domain-joined.png](assets/11-win10-domain-joined.png) |
| Computer object visible in ADUC | [12-win10-computer-object-aduc.png](assets/12-win10-computer-object-aduc.png) |
| Ada logged into the domain client | [13-ada-domain-login.png](assets/13-ada-domain-login.png) |
| Ada group membership checked in PowerShell | [14-ada-ad-group-membership.png](assets/14-ada-ad-group-membership.png) |
| Ada shown in the group members tab | [15-group-members-tab.png](assets/15-group-members-tab.png) |

## Troubleshooting I Ran Into

I ran into a few issues while building the lab:

- `DC01` first showed an APIPA address before the static IP applied correctly.
- I accidentally typed the wrong network range on the Windows 10 client once.
- The VMs needed a power cycle after changing the VirtualBox internal network.
- Ping worked one way at first, but Windows Firewall blocked ping from `DC01` to the client.
- I fixed the ping issue by enabling the File and Printer Sharing firewall rules.

That troubleshooting was useful because it felt closer to real help desk work: check the IP, check DNS, test connectivity, check firewall, and verify again.

## What I Learned

This lab helped me understand the foundation behind many Active Directory help desk tasks. Before I can practice password resets, account unlocks, group access, or onboarding, I need a working domain, a domain controller, a joined client, test users, and test groups.

This is the base lab I will use for the next projects.

