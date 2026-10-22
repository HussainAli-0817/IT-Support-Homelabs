# Ticketing System Setup

This project is from my help desk homelab. I set up osTicket locally, added help topics for common requests, and submitted 12 test requests through the customer portal. I used example customers and common help desk requests.

The goal was to practice the ticket lifecycle from both sides: the requester submitting an issue and the support agent handling the follow-up.

The password-reset, account-unlock, and file-access tickets connect to my Active Directory lab work. The other requests show how I document the next step when a requester, approver, or security team still needs to act.

## Tool Used

| Tool | Purpose |
| --- | --- |
| [osTicket 1.18.4](https://osticket.com/) | Local help desk ticketing system |
| [Mailpit](https://mailpit.axllent.org/) | Local mailbox for checking ticket replies |

## What I Practiced

- Submitted example requests through the customer portal and opened them in the agent view.
- Set priority, assigned tickets, and added internal notes.
- Sent short replies to the requester and checked that they arrived in Mailpit.
- Used ticket status to show completed work or who needs to act next.

## Tickets

The first two examples show completed account work tied to my AD lab. The other requests show follow-up while the requester, an approver, or Security still has a next step.

| Ticket | Issue | Current status |
| --- | --- | --- |
| [#451725](tickets/01-password-reset.md) | I can't log in to my computer | Closed |
| [#418085](tickets/02-account-unlock.md) | My account says it's locked out | Closed |
| [#115202](tickets/03-slow-computer.md) | My computer is really slow after I sign in | Waiting for User |
| [#351099](tickets/04-network-issue.md) | I can't open the company intranet | Waiting for User |
| [#198184](tickets/05-printer-issue.md) | My document is stuck in the print queue | Waiting for User |
| [#327797](tickets/06-file-access.md) | I need access to the team folder | Waiting for User |
| [#667554](tickets/07-software-request.md) | Can I get a diagramming app installed? | Waiting for Approval |
| [#437926](tickets/08-email-issue.md) | New emails show on the web but not in my email app | Waiting for User |
| [#721945](tickets/09-vpn-issue.md) | My VPN stopped working after I changed my password | Waiting for User |
| [#161600](tickets/10-new-hire.md) | Set up a standard account for a new starter | Waiting for Approval |
| [#608037](tickets/11-leaver-request.md) | Remove access for a departing employee | Open |
| [#162475](tickets/12-suspicious-email.md) | I received an email asking me to sign in | Waiting for Security |

## Evidence

| Step | Screenshot or writeup |
| --- | --- |
| osTicket installed and running | [System settings](assets/00-setup/01-system-settings.png) |
| Help topics created | [Help topics](assets/00-setup/02-help-topics.png) |
| Twelve test requests submitted | [Customer portal queue](assets/00-setup/00-all-requests.png) |
| Completed account request | [Password reset](tickets/01-password-reset.md) |
| Windows client network check | [Network ticket](tickets/04-network-issue.md#evidence) |
| AD group checked for the file-access request | [DC01 membership check](tickets/06-file-access.md#evidence) |
| Approval and security follow-up examples | [Software request](tickets/07-software-request.md) · [Suspicious email](tickets/12-suspicious-email.md) |

Each ticket page has a short screenshot trail showing the request, assignment, notes, reply, and test email. The two completed account tickets also show validation and their final status.

## What I Learned

- The customer portal and agent view show different sides of the same request.
- Internal notes and customer replies have different purposes.
- A short update should make the next step clear to the requester.
- Some requests need approval or security review before support can finish them.
