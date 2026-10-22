# Network Issue

**Ticket:** #351099 | **Priority:** Normal

## Ticket note

Issue: I can't open the company intranet on my computer. A coworker on the same network can open it.

Triage: Check the connection, IP settings, gateway, and name lookup. Compare with a working computer before treating this as a wider outage.

Next step: Check the connection, IP settings, gateway, and internal name lookup. Compare DNS settings with a working computer. If the DNS setting is wrong, restore the approved setting and check the intranet again.

## VM check

On WIN10-CLIENT01, the network flyout showed `homelab.local` and “No Internet.” That confirms the visible network status only; I haven't confirmed whether an internal intranet page is reachable.

Customer reply: Please try the intranet again and let support know if any other internal pages fail to open. Include the error message if it still doesn't work.

## Evidence

| Step | Screenshot |
| --- | --- |
| Request filled in through the customer portal | [01-portal-request.png](../assets/04-network-issue/01-portal-request.png) |
| Request submitted | [02-request-created.png](../assets/04-network-issue/02-request-created.png) |
| Ticket assigned to me | [04-ticket-assigned.png](../assets/04-network-issue/04-ticket-assigned.png) |
| Work note saved | [06-work-note.png](../assets/04-network-issue/06-work-note.png) |
| Customer reply posted | [07-customer-reply.png](../assets/04-network-issue/07-customer-reply.png) |
| Test email received in Mailpit | [09-test-email-received.png](../assets/04-network-issue/09-test-email-received.png) |
| Current network status on WIN10-CLIENT01 | [Windows network panel](../assets/04-network-issue/10-win10-domain-network.jpg) |

## Status

Waiting for User. The requester needs to retry the intranet and report back.
