# GPO Detective

An interactive Windows Group Policy troubleshooting simulation by Ankita Srivastava, built with AI assistance.

[Play GPO Detective](https://sankitatech.github.io/windows-server-labs/interactive-labs/gpo-detective/)

## How to play

1. Open a case from the incident queue.
2. Inspect the three evidence views: policy results, GPMC scope, and the target or policy settings.
3. Choose a targeted repair. An incorrect choice explains why it does not address the evidence.
4. Run the simulated `gpupdate /force`, generate the correct user or computer `gpresult` report, and test the actual setting or behavior.
5. Close the case, read the explanation, and follow the link to the related hands-on lab.

Hints are optional. Cases track unsuccessful fix attempts and hint use. Progress stays in the current page session; reloading or selecting Restart all cases clears it. Cases can be played in any order.

## Cases

| Case | Fault | Main concept |
| --- | --- | --- |
| The missing firewall policy | Configured GPO has no link | GPO existence versus deployment scope |
| The user outside the OU | HR user is in a different OU | User versus computer policy scope |
| Read is not enough | Approved computer group lacks Apply Group Policy | Effective GPO permissions |
| Linked, but switched off | Existing GPO link is disabled | Link status versus Enforced |
| The disabled user settings | GPO User Configuration half is disabled | GPO status versus individual setting state |

## Simulation boundaries

All tickets, outputs, configuration changes, and verification results in the game are fictional, condensed teaching examples. They are inspired by the firewall and Registry Editor lab topics in this repository, rather than presented as records of five incidents actually encountered. Additional OUs and groups are scenario fixtures.

The game runs entirely in the browser. It does not execute commands, query Active Directory, connect to a server, or change a real Windows configuration. It does not reproduce every possible policy interaction, replication delay, restart or sign-out requirement, network-profile issue, or permission edge case. In a real environment, verify the affected identity, intended scope, effective settings, and any processing requirements.

For these cases, each scenario explicitly provides enough evidence for one targeted repair. Domain connectivity is assumed healthy unless evidence states otherwise. The security-filtering case assumes the computer's group membership is already effective. The user-policy cases preserve the computer Read permissions required for user GPO retrieval. The Registry Editor policy restricts `regedit.exe`; it does not prevent every possible registry modification.

## Run locally

Download `index.html` and open it in a modern browser. No dependencies, API keys, backend, or installation are needed. All controls work with keyboard navigation and activation.

## Hosting

The playable link requires GitHub Pages to publish the `main` branch from `/(root)` in `windows-server-labs`. Enable this under repository Settings → Pages → Build and deployment → Deploy from a branch. The HTML stays in `interactive-labs/gpo-detective/index.html`.

## Related hands-on labs

- [Windows Defender Firewall with Group Policy](../../05-group-policy/windows-defender-firewall/README.md)
- [Block Registry Editor with Group Policy](../../05-group-policy/registry-block/README.md)
- [Group Policy fundamentals](../../05-group-policy/fundamentals/README.md)

## Technical references

- [Microsoft: Applying Group Policy troubleshooting guidance](https://learn.microsoft.com/en-us/troubleshoot/windows-server/group-policy/applying-group-policy-troubleshooting-guidance)
- [Microsoft: Group Policy scope](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-scope)
- [Microsoft: Group Policy processing](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-processing)
- [Microsoft: User GPOs and computer Read permissions](https://learn.microsoft.com/en-us/troubleshoot/windows-server/group-policy/cannot-apply-user-gpo-when-computer-objects-dont-have-read-permissions)

## Project context

Created as an AI-assisted study tool for Ankita Srivastava's Windows administration portfolio. The code and simulated case content were generated with AI assistance and connected to the repository's existing lab topics. This is a learning simulation, not evidence of administering a production environment or an official Microsoft training product.
