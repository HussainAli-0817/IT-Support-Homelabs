# Active Directory Support Workflows

This project is from my Active Directory help desk homelab. I practiced common AD support tasks that a help desk or junior admin might handle: password reset, account unlock, group access, and account status changes.

The goal was to check the account first, make the correct change, validate the result, and document the ticket clearly.

## Lab Used

| System | Purpose |
| --- | --- |
| `DC01` | Windows Server 2022 domain controller |
| `WIN10-CLIENT01` | Windows 10 domain client |
| `homelab.local` | Test domain |

## Workflows Completed

| Workflow | What I practiced |
| --- | --- |
| Password reset + first login validation | Reset a user password, required password change at next logon, and confirmed successful login |
| Account lockout + unlock | Set a lockout policy, triggered a lockout, confirmed it in ADUC, unlocked the account, and validated login |
| Group access request | Checked group membership, added a user to a security group, and verified membership with PowerShell |
| Disable + re-enable account | Disabled a test account, verified status with PowerShell, and restored the account |

## Workflow 1: Password Reset + First Login Validation

**What I practiced**

- Checked Ada Lovelace's account before making changes.
- Reset the password in Active Directory Users and Computers.
- Required password change at next logon.
- Confirmed the user could sign in after changing the temporary password.

**Evidence**

| Step | Screenshot |
| --- | --- |
| Account before reset | [01-ada-account-before-reset.png](assets/password-reset-first-login-validation/01-ada-account-before-reset.png) |
| Password reset window | [02-ada-password-reset-window.png](assets/password-reset-first-login-validation/02-ada-password-reset-window.png) |
| Account set to require password change | [03-ada-account-after-reset.png](assets/password-reset-first-login-validation/03-ada-account-after-reset.png) |
| Login after password change | [04-ada-login-after-password-reset.png](assets/password-reset-first-login-validation/04-ada-login-after-password-reset.png) |
| Account after successful login | [05-ada-account-after-successful-login.png](assets/password-reset-first-login-validation/05-ada-account-after-successful-login.png) |

**Ticket note**

Issue: Ada Lovelace needed a password reset in the homelab domain.

Checked: Reviewed the account in ADUC and confirmed the account was not locked.

Action: Reset the password and required the user to change it at next logon.

Validation: User successfully signed in to `WIN10-CLIENT01` after changing the temporary password.

Close note: Password reset completed and login confirmed.

Escalation if repeated or unresolved: If login still failed, I would check account lockout, disabled status, username format, DNS/domain connectivity, and password policy requirements.

## Workflow 2: Account Lockout + Unlock

**What I practiced**

- Set a basic domain account lockout policy.
- Triggered a lockout with failed sign-in attempts.
- Confirmed the locked state in ADUC.
- Unlocked the account without resetting the password.
- Validated the user could sign in after the unlock.

**Evidence**

| Step | Screenshot |
| --- | --- |
| Lockout policy set | [01-account-lockout-policy.png](assets/account-lockout-unlock/01-account-lockout-policy.png) |
| Client locked-out message | [02-client-locked-out-message.png](assets/account-lockout-unlock/02-client-locked-out-message.png) |
| Account locked in ADUC | [03-aduc-account-locked.png](assets/account-lockout-unlock/03-aduc-account-locked.png) |
| Account unlocked in ADUC | [04-aduc-account-unlocked.png](assets/account-lockout-unlock/04-aduc-account-unlocked.png) |
| Login validation after unlock | [05-login-validation-after-unlock.png](assets/account-lockout-unlock/05-login-validation-after-unlock.png) |

**Ticket note**

Issue: User could not sign in because the account was locked out.

Checked: Confirmed the lockout policy, verified the client error message, and confirmed the account was locked in ADUC.

Action: Unlocked the account in ADUC. No password reset was performed.

Validation: User successfully signed in after the unlock.

Close note: Account unlocked and login confirmed.

Escalation if repeated or unresolved: If the account keeps locking, I would check for old saved credentials, mapped drives, services, scheduled tasks, or another device using an old password.

## Workflow 3: Group Access Request

**What I practiced**

- Checked Grace Hopper's current group membership.
- Added Grace to `GG_Helpdesk_Test_Access`.
- Verified the change in ADUC.
- Confirmed group membership with PowerShell.

**PowerShell validation**

```powershell
Get-ADPrincipalGroupMembership grace.hopper | Select-Object Name
```

**Evidence**

| Step | Screenshot |
| --- | --- |
| Before group access | [01-grace-before-group-access.png](assets/group-access-request/01-grace-before-group-access.png) |
| After group access | [02-grace-after-group-access.png](assets/group-access-request/02-grace-after-group-access.png) |
| PowerShell validation | [03-powershell-group-validation.png](assets/group-access-request/03-powershell-group-validation.png) |

**Ticket note**

Issue: Grace Hopper needed access to the simulated Help Desk resource.

Checked: Reviewed Grace's AD group membership and confirmed she only had `Domain Users` before the change.

Action: Added Grace to `GG_Helpdesk_Test_Access` in ADUC after simulated approval.

Validation: Confirmed the group appeared in ADUC and verified membership with PowerShell.

Close note: Access group was added and membership was confirmed.

Escalation if repeated or unresolved: If access still failed, I would check whether the resource permissions are tied to the correct group and have the user sign out/in to refresh access.

## Workflow 4: Disable + Re-enable Account

**What I practiced**

- Checked that Grace Hopper's account was enabled before testing.
- Disabled the account in ADUC.
- Verified the disabled state with PowerShell.
- Re-enabled the account and confirmed the status changed back.

**PowerShell validation**

```powershell
Get-ADUser grace.hopper -Properties Enabled | Select-Object Name,SamAccountName,Enabled
```

**Evidence**

| Step | Screenshot |
| --- | --- |
| Account enabled before test | [01-grace-account-enabled-before.png](assets/disable-reenable-account/01-grace-account-enabled-before.png) |
| Account disabled in ADUC | [02-grace-account-disabled-aduc.png](assets/disable-reenable-account/02-grace-account-disabled-aduc.png) |
| Login worked before disabling | [03-grace-login-works-before-disable.png](assets/disable-reenable-account/03-grace-login-works-before-disable.png) |
| PowerShell shows disabled | [04-powershell-account-disabled.png](assets/disable-reenable-account/04-powershell-account-disabled.png) |
| PowerShell shows enabled again | [05-powershell-account-enabled.png](assets/disable-reenable-account/05-powershell-account-enabled.png) |

**Ticket note**

Issue: Grace Hopper's AD account was temporarily disabled and then re-enabled in the homelab.

Checked: Confirmed the account was enabled before the test and verified Grace could sign in before disabling it.

Action: Disabled Grace's account in ADUC, verified the account status with PowerShell, then re-enabled the account.

Validation: PowerShell showed `Enabled` as `False` while disabled and `True` after re-enabling the account.

Close note: Account status was tested and restored. Grace Hopper's account is enabled again.

Escalation if repeated or unresolved: If a disabled account still appears able to sign in, I would check for cached credentials, existing sessions, domain controller connectivity, and whether the account change was fully applied.

## What I Learned

- A password reset is different from an account unlock.
- Group access should be checked before and after changes.
- PowerShell is useful for quick AD verification.
- ADUC changes need to be applied before validation.
- Account status testing can be affected by cached credentials or existing sessions.

## Still Building

This AD support project is still being expanded. The next workflows I plan to add are:

- basic AD account review
- computer object and OU move check
- basic AD PowerShell verification
- basic Group Policy support
