# Fix the Domain Join

An interactive Active Directory troubleshooting game by Ankita Srivastava, built with AI assistance.

[Play Fix the Domain Join](https://sankitatech.github.io/windows-server-labs/interactive-labs/fix-the-domain-join/)

## How to play

1. Select a provisioning case.
2. Read the three evidence views and identify the fault.
3. Choose a targeted repair. Incorrect choices explain why they do not address the cause.
4. Check prerequisites, retry the domain join, restart the simulated workstation, and verify domain membership and the secure channel.
5. Read the explanation and explore the related Windows Server lab.

Hints are optional. Cases track unsuccessful repair attempts and hint use, and can be played in any order. Progress resets when you reload the page or select Restart all cases.

## Cases

| Case | Fault | Practice |
| --- | --- | --- |
| The internet works. The domain does not. | Client queries public DNS instead of the approved AD DNS server | SRV records and DNS client configuration |
| The disconnected workstation | Local Ethernet adapter is disabled | Local connectivity before remote service changes |
| One letter, a different domain | Join target contains a spelling mistake | Compare requested and configured domain names |
| Found the domain. Denied the join. | Authenticated account lacks computer creation rights | Authorization and existing delegated provisioning rights |
| The clock is ahead | Explicit Kerberos clock-skew failure in this scenario | Actual UTC offset and trusted time configuration |

## Simulation

This browser game uses fictional incidents and condensed teaching outputs inspired by this repository's Windows administration topics. It does not run Windows commands or connect to Active Directory, and it never requests passwords. The LAB-PC machines and provisioning roles are scenario fixtures.

The domain is `ankita.com`, with an internal DNS/DC address of `10.0.1.4`. These values are displayed as lab examples; the game makes no network requests to them. All workstations in the cases use Windows 11 Pro. They begin in WORKGROUP and use an elevated local provisioning session.

Each case isolates one fault and explicitly supplies the other relevant prerequisites. The permissions case uses a new computer object, a machine account quota of zero, and an already approved delegated operator. It does not model existing-account reuse or all domain-join hardening requirements. The clock case specifically models an authentication path that reports Kerberos clock skew; not every domain-join failure has that cause. The supplied time comparison is in UTC.

The successful path includes a simulated restart, a `Get-CimInstance Win32_ComputerSystem` membership check, and `Test-ComputerSecureChannel`. Real troubleshooting also requires appropriate logging, service-port connectivity, account and OU checks, and environment-specific validation.

## Run locally

Download `index.html` and open it in a modern browser. No dependencies, installation, backend, or API keys are required. Use Tab and Enter/Space to operate the controls with a keyboard.

## Related labs

- [Windows Server VM and networking](../../01-azure-windows-server-vm/README.md)
- [Active Directory domain controller](../../02-active-directory-domain-controller/README.md)
- [Active Directory OUs](../../03-active-directory-ou-and-group-policy/README.md)
- [Play GPO Detective](https://sankitatech.github.io/windows-server-labs/interactive-labs/gpo-detective/)

## References

- [Microsoft: Active Directory domain join troubleshooting](https://learn.microsoft.com/en-us/troubleshoot/windows-server/active-directory/active-directory-domain-join-troubleshooting-guidance)
- [Microsoft: DNS client settings](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/best-practices-for-dns-client-settings)
- [Microsoft: Active Directory domain join permissions](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/active-directory-domain-join-permissions)
- [Microsoft: Kerberos authentication troubleshooting](https://learn.microsoft.com/en-us/troubleshoot/windows-server/windows-security/kerberos-authentication-troubleshooting-guidance)
- [Microsoft: Join a computer to a domain](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/join-computer-to-domain)

Built with AI assistance as a personal Windows administration study tool.
