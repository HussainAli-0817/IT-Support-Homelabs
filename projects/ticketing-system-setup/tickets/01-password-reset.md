# Password Reset

**Ticket:** #451725 | **Priority:** Normal

## Ticket note

Issue: I forgot my password and can't sign in to my computer.

Checked: Reviewed the account status and lockout state in AD. The account was not disabled.

Action: Reset the password and required a password change at next login.

Validation: Confirmed the user signed in to the domain client after changing the temporary password.

Customer reply: Your password has been reset. Please use the sign-in instructions provided separately and change your password at the next login. Don't send passwords in the ticket.

Close note: Password reset completed and login confirmed.

## Evidence

| Step | Screenshot |
| --- | --- |
| Request filled in through the customer portal | [01-portal-request.png](../assets/01-password-reset/01-portal-request.png) |
| Request submitted | [02-request-created.png](../assets/01-password-reset/02-request-created.png) |
| Ticket assigned to me | [04-ticket-assigned.png](../assets/01-password-reset/04-ticket-assigned.png) |
| Work note saved | [06-work-note.png](../assets/01-password-reset/06-work-note.png) |
| Customer reply posted | [07-customer-reply.png](../assets/01-password-reset/07-customer-reply.png) |
| Final status saved | [08-final-status.png](../assets/01-password-reset/08-final-status.png) |
| Test email received in Mailpit | [09-test-email-received.png](../assets/01-password-reset/09-test-email-received.png) |
| AD account before the reset | [Account review](../../ad-support-workflows/assets/password-reset-first-login-validation/01-ada-account-before-reset.png) |
| AD account after the reset | [Account update](../../ad-support-workflows/assets/password-reset-first-login-validation/03-ada-account-after-reset.png) |
| Sign-in after the reset | [Client sign-in](../../ad-support-workflows/assets/password-reset-first-login-validation/04-ada-login-after-password-reset.png) |
| Account after sign-in | [Post-login check](../../ad-support-workflows/assets/password-reset-first-login-validation/05-ada-account-after-successful-login.png) |

## Status

Closed after sign-in was confirmed.
