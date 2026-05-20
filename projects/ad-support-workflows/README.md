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
| Basic AD account review | Reviewed account status, group membership, and password metadata with ADUC and PowerShell |
| Computer object + OU move check | Moved a computer object to the lab OU and verified the new path with PowerShell |
| Basic AD PowerShell verification | Checked user status, group membership, and computer object DN with read-only PowerShell commands |
| Basic Group Policy support | Created a custom GPO, linked it to the lab OU, set a policy, and validated the effect on the client |

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

## Workflow 5: Basic AD Account Review

**What I practiced**

- Reviewed Grace Hopper's account identity fields in ADUC.
- Checked the account status and group membership.
- Verified account state and password metadata with PowerShell.

**Evidence**

| Step | Screenshot |
| --- | --- |
| ADUC account tab review | [01-aduc-account-tab-review.png](assets/basic-account-review/01-aduc-account-tab-review.png) |
| ADUC member-of review | [02-aduc-memberof-review.png](assets/basic-account-review/02-aduc-memberof-review.png) |
| PowerShell account review | [03-powershell-account-review.png](assets/basic-account-review/03-powershell-account-review.png) |

**Ticket note**

Issue: Performed a basic AD account review for Grace Hopper in the homelab.

Checked: Reviewed account identity fields, account status, and group membership in ADUC. Verified account state and password metadata with PowerShell.

Action: No account changes were made. This was a read-only validation check.

Validation: Confirmed account identity format, current enabled/lockout state, password last set value, and group membership output.

Close note: Basic AD account review completed and current account state documented.

Escalation if repeated or unresolved: If sign-in or access issues are reported later, I would re-check account status, group membership, OU placement, and policy application.

## Workflow 6: Computer Object + OU Move Check

**What I practiced**

- Found the `WIN10-CLIENT01` computer object in the default Computers container.
- Moved it to the lab `HomeLab > Computers` OU.
- Refreshed policy on the client with `gpupdate /force`.
- Verified the computer object path with PowerShell.

**Evidence**

| Step | Screenshot |
| --- | --- |
| Computer object before move | [01-computer-object-before-move.png](assets/computer-object-ou-move-check/01-computer-object-before-move.png) |
| Computer object after move | [02-computer-object-after-move.png](assets/computer-object-ou-move-check/02-computer-object-after-move.png) |
| PowerShell OU validation | [03-powershell-ou-validation.png](assets/computer-object-ou-move-check/03-powershell-ou-validation.png) |
| Policy refresh after move | [04-gpupdate-after-ou-move.png](assets/computer-object-ou-move-check/04-gpupdate-after-ou-move.png) |

**Ticket note**

Issue: `WIN10-CLIENT01` computer object needed to be moved from the default Computers container to the lab Computers OU.

Checked: Confirmed `WIN10-CLIENT01` was located under `homelab.local > Computers` before the change.

Action: Moved `WIN10-CLIENT01` to `homelab.local > HomeLab > Computers` in ADUC and refreshed policy on the client with `gpupdate /force`.

Validation: Confirmed the object appeared in `HomeLab > Computers` and was no longer in the default Computers container. Verified the OU path with PowerShell.

Close note: Computer object OU placement was corrected and validated.

Escalation if repeated or unresolved: If computer objects keep landing in the wrong location, I would review the join workflow, delegated rights, and any automation or policy affecting computer object placement.

## Workflow 7: Basic AD PowerShell Verification

**What I practiced**

- Checked account status with a read-only AD user query.
- Checked group membership with PowerShell.
- Verified the computer object path with PowerShell.

**PowerShell commands**

```powershell
Get-ADUser grace.hopper -Properties Enabled,LockedOut,PasswordLastSet | Select-Object Name,SamAccountName,Enabled,LockedOut,PasswordLastSet
Get-ADPrincipalGroupMembership grace.hopper | Select-Object Name
Get-ADComputer WIN10-CLIENT01 -Properties DistinguishedName | Select-Object Name,DistinguishedName
```

**Evidence**

| Step | Screenshot |
| --- | --- |
| User account status | [01-user-account-status.png](assets/basic-ad-powershell-verification/01-user-account-status.png) |
| User group membership | [02-user-group-membership.png](assets/basic-ad-powershell-verification/02-user-group-membership.png) |
| Computer object DN | [03-computer-object-dn.png](assets/basic-ad-powershell-verification/03-computer-object-dn.png) |

**Ticket note**

Issue: Performed a basic AD PowerShell verification check for Grace Hopper and `WIN10-CLIENT01`.

Checked: Reviewed user status, user group membership, and computer object path with PowerShell.

Action: No changes were made. This was a read-only verification check.

Validation: Confirmed Grace Hopper's account status, current group membership, and `WIN10-CLIENT01` computer object distinguished name in the lab OU.

Close note: Basic AD PowerShell verification completed and documented.

Escalation if repeated or unresolved: If account or computer object issues are reported later, I would re-check account status, group membership, OU placement, and policy application.

## Workflow 8: Basic Group Policy Support

**What I practiced**

- Reviewed the default domain policy scope.
- Created and linked a custom GPO to the `HomeLab` OU.
- Set a simple user restriction policy.
- Refreshed policy on the client and confirmed the restriction applied.

**Evidence**

| Step | Screenshot |
| --- | --- |
| Default domain policy scope | [01-default-domain-policy-scope.png](assets/basic-group-policy-support/01-default-domain-policy-scope.png) |
| Custom GPO scope | [02-custom-gpo-scope.png](assets/basic-group-policy-support/02-custom-gpo-scope.png) |
| Policy enabled | [03-gpo-control-panel-policy-enabled.png](assets/basic-group-policy-support/03-gpo-control-panel-policy-enabled.png) |
| Policy refresh on client | [04-gpupdate-after-gpo-enable.png](assets/basic-group-policy-support/04-gpupdate-after-gpo-enable.png) |
| Client restriction message | [05-control-panel-blocked.png](assets/basic-group-policy-support/05-control-panel-blocked.png) |

**Ticket note**

Issue: Set up and tested a basic Group Policy restriction in the lab.

Checked: Reviewed the default domain policy scope, created a custom GPO linked to the `HomeLab` OU, and verified the policy location and filters.

Action: Enabled a user policy to restrict access to Control Panel and PC settings, then refreshed policy on `WIN10-CLIENT01` with `gpupdate /force`.

Validation: Confirmed the policy update completed successfully and the client showed a restrictions message when Control Panel access was tested.

Close note: Basic GPO creation, linking, and client-side validation were completed successfully.

Escalation if repeated or unresolved: If the policy does not apply as expected, check the GPO link, security filtering, user logon session, and whether the client refreshed policy from the domain.

## What I Learned

- A password reset is different from an account unlock.
- Group access should be checked before and after changes.
- PowerShell is useful for quick AD verification.
- ADUC changes need to be applied before validation.
- Account status testing can be affected by cached credentials or existing sessions.
