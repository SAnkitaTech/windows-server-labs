# Group Policy Preferences — Concise Summary

**Ankita Srivastava | Windows Server Study Notes**

## 1. Policies vs. Preferences

Group Policy Preferences (GPP) configure settings for users and computers.

| Policies | Preferences |
| --- | --- |
| Can enforce settings and restrict changes in the user interface | Set defaults without locking the setting |
| Example: enforced desktop wallpaper | Example: default printer |

Users may change a preference setting if they have permission. However, preferences normally reapply during Group Policy refresh and may overwrite those changes.

## 2. Apply Once or Reapply

The **Common** tab includes **Apply once and do not reapply**:

- **Unchecked:** the preference normally reapplies during policy refresh.
- **Checked:** the item applies once and is not reapplied during later refreshes.

Reapplying a preference is different from preventing the user from changing it.

## 3. Item-Level Targeting

Item-level targeting limits an individual preference item using conditions such as:

- Operating system
- IP address range
- MAC address
- User or computer security-group membership

## 4. Default Printer Example

A printer preference can target computers with IP addresses from **192.168.1.100 to 192.168.1.150**.

If a user changes the default printer, a later refresh may reset it unless **Apply once and do not reapply** is selected.

## Reference

[Microsoft Learn: Group Policy preferences](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-preferences)

---

Copyright © 2026 Ankita Srivastava.
