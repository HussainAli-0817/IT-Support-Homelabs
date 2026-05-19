# Password Reset And First Login Validation

This project is from my Active Directory help desk lab. I practiced a basic password reset workflow for a domain user and documented the before and after steps.

The goal was to treat it like a simple help desk ticket: check the account, reset the password, require the user to change it at next logon, and confirm the user can sign in.

## Lab User

User:

`Ada Lovelace`

Username:

`ada.lovelace@homelab.local`

Client used for testing:

`WIN10-CLIENT01`

## What I Practiced

- Opening a user account in Active Directory Users and Computers.
- Checking the user's account tab before making changes.
- Confirming the account was not locked before resetting the password.
- Resetting a user's password.
- Requiring password change at next logon.
- Logging into the domain client as the user.
- Confirming the user could sign in after changing the temporary password.
- Checking the account again after the successful login.

## Evidence

| Step | Screenshot |
| --- | --- |
| Ada account before reset | [01-ada-account-before-reset.png](assets/01-ada-account-before-reset.png) |
| Password reset window | [02-ada-password-reset-window.png](assets/02-ada-password-reset-window.png) |
| Account set to require password change | [03-ada-account-after-reset.png](assets/03-ada-account-after-reset.png) |
| Ada logged into `WIN10-CLIENT01` after password change | [04-ada-login-after-password-reset.png](assets/04-ada-login-after-password-reset.png) |
| Account after successful login | [05-ada-account-after-successful-login.png](assets/05-ada-account-after-successful-login.png) |

## Ticket Note

**Scenario:** Ada Lovelace needed a password reset in the homelab domain.

**What I checked:**

- Opened the user account in Active Directory Users and Computers.
- Confirmed the account was not locked.
- Confirmed the username was `ada.lovelace@homelab.local`.

**Action taken:**

- Reset Ada's password in Active Directory.
- Checked "User must change password at next logon."
- Had Ada sign in from `WIN10-CLIENT01`.
- Changed the temporary password during login.

**Validation:**

- Confirmed Ada could log in to the domain client.
- Ran `whoami` and confirmed the session was `homelab\ada.lovelace`.
- Checked Ada's account again and confirmed "User must change password at next logon" was no longer checked.

**Closure note:**

Password reset completed for Ada Lovelace. User was required to change the temporary password at next logon and successfully signed in to the Windows 10 domain client.

## What I Learned

This helped me practice the normal help desk flow for a password reset: check the account first, make the change, have the user test login, and verify the final account state.

I also learned that a password reset is not the same thing as an account unlock. The reset window showed Ada's account was already unlocked, so this project focuses on password reset and login validation only. I will handle a real lockout/unlock scenario separately when I build that workflow.
