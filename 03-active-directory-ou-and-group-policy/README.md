# Active Directory Organizational Units and Group Policy

**Ankita Srivastava | Windows Server Administration Lab**

## Objective

Organize Active Directory users and computers into OUs and configure basic Group Policy settings.

## Lab environment

| Component | Configuration |
| --- | --- |
| Domain | `ankita.com` |
| DC | Domain controller with AD DS and DNS |
| PC | Domain-joined client computer |
| Accounts | `dcadmin` on DC; `user1` on PC |

## 1. OU structure

OUs organize users, computers, groups, and child OUs. They support delegated administration and targeted Group Policy.

My lab structure separates users and computers:

| Location | Object |
| --- | --- |
| `ankita.com / IT Department / IT Users` | `user1` |
| `ankita.com / IT Department / IT Computers` | `PC` |

OU designs can follow departments, locations, functions, or a combination.

| Feature | OU | Security group |
| --- | --- | --- |
| Purpose | Organization, delegation, and policy scope | Permissions and access |
| Contains child OUs | Yes | No |
| Direct GPO link | Yes | No |
| GPO security filtering | Not a security principal | Supported |

The default **Users** and **Computers** locations are containers, not OUs. GPOs cannot be linked directly to them, but domain-level policies can still apply to their objects.

## 2. Create and populate OUs

1. Open **Active Directory Users and Computers** with `dsa.msc`.
2. Right-click the domain, then select **New > Organizational Unit**.
3. Create **IT Department** and enable **Protect container from accidental deletion**.
4. Create **IT Users** and **IT Computers** beneath it.
5. Right-click `user1`, select **Move**, and choose **IT Users**.
6. Move the `PC` computer object into **IT Computers**.

GPOs linked to the destination OU or inherited from its parents can apply, subject to policy scope and filtering.

## 3. Pre-stage a computer

Pre-staging creates the computer account in its intended OU before domain join.

1. Obtain the exact computer name.
2. In `dsa.msc`, right-click **IT Computers**.
3. Select **New > Computer** and enter that name.
4. Join the client using an account authorized to reuse the pre-created computer account.

Matching the name is required; domain-join permissions and account-reuse security checks must also permit the join. Without pre-staging or an explicitly selected OU, new computer accounts normally enter the **Computers** container.

## 4. Create and link a GPO

1. Open **Group Policy Management** with `gpmc.msc`.
2. Right-click **IT Department**.
3. Select **Create a GPO in this domain, and Link it here**.
4. Enter a descriptive name.
5. Right-click the GPO and select **Edit**.

GPOs can be linked to sites, domains, and OUs. Parent OU links normally apply to child OUs through inheritance; filtering and inheritance settings can change applicability.

## 5. Control Panel restriction

Configure:

**User Configuration > Policies > Administrative Templates > Control Panel > Prohibit access to Control Panel and PC settings**

Set it to **Enabled** and link the GPO to **IT Department**. The user setting applies to `user1` in **IT Users**; it does not apply to the `PC` object merely because the computer is under the same parent OU.

Refresh policies on the client:

```cmd
gpupdate /force
```

After the user policy applies, Control Panel and Windows Settings access is restricted.

## 6. Removable storage restriction

Configure:

**Computer Configuration > Policies > Administrative Templates > System > Removable Storage Access > All Removable Storage classes: Deny all access**

Set it to **Enabled** and link the GPO to the OU containing `PC`, or its parent. This computer setting restricts removable storage access for users of that computer.

| Setting | Target | Expected behavior |
| --- | --- | --- |
| Control Panel restriction | `user1` | Follows the user under normal user-policy processing |
| Removable storage restriction | `PC` | Applies on that computer regardless of the signed-in user |

An HR user on `PC` receives the computer restriction but only receives the Control Panel restriction if that user's account is also in its scope. Physical USB testing requires a suitable physical client; Azure VMs do not provide direct local USB attachment.

## 7. User and computer policy processing

| Policy section | Normal scope | Processing |
| --- | --- | --- |
| User Configuration | User account location | User logon and background refresh |
| Computer Configuration | Computer account location | Startup and background refresh |

Normal background refresh is approximately **90 minutes plus a random offset of up to 30 minutes**. Domain controllers normally refresh every **5 minutes**. Some settings require logoff or restart.

User policies normally follow the user; computer policies stay with the computer. Loopback processing can change how user policies are selected.

Settings may exist under User Configuration, Computer Configuration, or both. Conflict behavior depends on the specific setting; computer settings do not universally override user settings.

The normal processing order is **Local, Site, Domain, OU (LSDOU)**. Later settings normally take precedence where they conflict, subject to enforcement and other processing rules.

## 8. Security filtering

Security groups can restrict who applies a linked GPO.

For a Control Panel policy limited to **IT Staff**:

1. Add the intended users to the **IT Staff** security group.
2. Keep the GPO linked to **IT Department**.
3. Grant **IT Staff** the **Read** and **Apply Group Policy** permissions.
4. Remove broader **Apply Group Policy** permission if the policy must target only that group.
5. Retain **Read** permission for the client computers, for example through **Domain Computers** or read-only **Authenticated Users** delegation.

A GPO is linked to an OU, site, or domain; the security group filters its application.

## 9. Test and protect changes

Test new GPOs in a **Test** OU with test users and computers before wider deployment. Document the change and follow the organization's approval and maintenance process.

Accidental-deletion protection helps prevent deletion of the protected OU. It does not individually protect every child object.

To intentionally delete a protected OU:

1. In `dsa.msc`, select **View > Advanced Features**.
2. Open the OU's **Properties > Object** tab.
3. Clear **Protect object from accidental deletion**.
4. Apply the change, then delete the intended OU after checking its contents.

## Key takeaways

- OUs organize objects and define policy scope.
- Security groups manage access and GPO filtering.
- Default containers cannot receive direct GPO links.
- Pre-staging requires matching names and appropriate join permissions.
- Separate users and computers for clearer policy targeting.
- Test policies before wider deployment.
