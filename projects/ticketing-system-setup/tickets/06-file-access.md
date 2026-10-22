# File Access

**Ticket:** #327797 | **Priority:** Low

## Ticket note

Issue: I need access to the team folder for my work.

Checked: ADUC on DC01 shows Grace Hopper in `Domain Users` and `GG_Helpdesk_Test_Access`.

Action: Added Grace Hopper to the approved test-access group.

Validation: Group membership is visible in ADUC and the earlier PowerShell check. Folder access still needs confirmation from the client after sign-in.

Customer reply: The approved group change is complete. Please refresh your sign-in session and let support know if you still can't open the folder.

## Evidence

| Step | Screenshot |
| --- | --- |
| Request filled in through the customer portal | [01-portal-request.png](../assets/06-file-access/01-portal-request.png) |
| Request submitted | [02-request-created.png](../assets/06-file-access/02-request-created.png) |
| Ticket assigned to me | [04-ticket-assigned.png](../assets/06-file-access/04-ticket-assigned.png) |
| Work note saved | [06-work-note.png](../assets/06-file-access/06-work-note.png) |
| Customer reply posted | [07-customer-reply.png](../assets/06-file-access/07-customer-reply.png) |
| Test email received in Mailpit | [09-test-email-received.png](../assets/06-file-access/09-test-email-received.png) |
| Group membership before access | [ADUC review](../../ad-support-workflows/assets/group-access-request/01-grace-before-group-access.png) |
| Group membership after access | [ADUC update](../../ad-support-workflows/assets/group-access-request/02-grace-after-group-access.png) |
| Group membership verified | [PowerShell check](../../ad-support-workflows/assets/group-access-request/03-powershell-group-validation.png) |
| Grace's current group membership on DC01 | [ADUC screenshot](../assets/06-file-access/10-dc01-grace-ad-membership.jpg) |

## Status

Waiting for User. The requester needs to confirm folder access after signing in again.
