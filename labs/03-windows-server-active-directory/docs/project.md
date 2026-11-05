# Windows Server and Active Directory

Hyper-V on `UDOPC`. Two guests: `DC01` (Windows Server 2025) and `WKSTN01` (Windows 11). Domain `udokaudodigwe.com`. Work below is in the order it was built, 22–24 Jul 2026.

## 1. Domain controller

`DC01` is a generation-2 VM, 2048 MB, 8 virtual processors, Secure Boot, DVD `26100` (Windows Server 2025). It was renamed to `DC01` while still in `WORKGROUP`.

![DC01 running in Hyper-V](../evidence/01-domain-controller/01-hyperv-dc01.png)

![Server Manager: computer name DC01, workgroup](../evidence/01-domain-controller/02-dc01-workgroup.png)

A second NIC was added. One adapter is on **External 1 Virtual Switch**, the other on **Private 1 Virtual Switch**. Inside the guest they are named `External` and `Private`.

![Both virtual switches on DC01](../evidence/01-domain-controller/03-second-nic.png)

![Adapters renamed Private and External](../evidence/01-domain-controller/04-nics-renamed.png)

Private IPv4 is static: `172.16.0.1/16`, DNS `172.16.0.1`. External stays on DHCP (`10.0.0.132`, gateway `10.0.0.1`). Time zone is Eastern (UTC−05:00), region Canada. The Private firewall profile was turned off before promotion. After promotion, Server Manager shows the Domain profile on.

![Private static address](../evidence/01-domain-controller/05-private-static-ip.png)

![Firewall profiles and time zone](../evidence/01-domain-controller/06-firewall-and-timezone.png)

## 2. Active Directory

AD DS was installed and `DC01` was promoted. Server Manager shows domain `udokaudodigwe.com`, roles AD DS and DNS, and Windows Server 2025 Standard Evaluation. `gpresult` records it as the primary domain controller, OS `10.0.26100`, in `OU=Domain Controllers`.

![DC01 in udokaudodigwe.com](../evidence/01-domain-controller/07-ad-ds.png)

## 3. DHCP

DHCP on `dc01.udokaudodigwe.com`. Scope `172.16.0.0/24`, name starting “Private Net”, state Active, range `172.16.0.100`–`172.16.0.200`, lease 8 days.

![DHCP address pool](../evidence/01-domain-controller/08-dhcp-scope.png)

## 4. WDS

WDS is installed on `DC01.udokaudodigwe.com`. Image group **Windows 10** has two online x64 install images, OS `10.0.19041`, added 23 Jul 2026. The exports identify the boot image as Windows 10 Setup (`boot.wim`) and one install image as Windows 10 Pro N (`install-(2).wim` on `\\DC01.udokaudodigwe.com\REMINST\Images\Windows 10\`).

![WDS install images](../evidence/01-domain-controller/09-wds.png)

## 5. Workstation

`Wkstn01` was created 23 Jul 2026, generation 2, 4096 MB, 8 processors, TPM and Secure Boot. Disk `C:\VHDs\Wkstn01.vhdx`. DVD `Win11_25H2_English_x64_v2.iso`. NIC stayed on **External 1 Virtual Switch**. Firmware boots from the hard drive.

![Wkstn01 in Hyper-V](../evidence/02-workstation/01-vm-created.png)

![Windows 11 ISO on the DVD drive](../evidence/02-workstation/02-windows-11-iso.png)

![Boot from hard drive, external NIC](../evidence/02-workstation/03-boot-and-external-nic.png)

Windows 11 setup ran on that VM. The finished desktop is Windows 11.

![Windows 11 setup](../evidence/02-workstation/04-installing-windows-11.png)

![Windows 11 desktop](../evidence/02-workstation/05-windows-11-desktop.png)

The workstation did not take a lease from the `172.16.0.0` scope. It remained on the external network: `10.0.0.134/24`, gateway `10.0.0.1`, DHCP server `10.0.0.1`. DNS was set to DC01 at `10.0.0.132`. The adapter was renamed `External`. The PC was renamed `Wkstn01`. Time zone Eastern, region Canada. `gpresult` later shows OS `10.0.26200`.

![Address 10.0.0.134 on the external network](../evidence/02-workstation/06-ipconfig.png)

![DNS server 10.0.0.132](../evidence/02-workstation/07-dns-dc01.png)

![Computer name Wkstn01](../evidence/02-workstation/08-renamed.png)

![Eastern time](../evidence/02-workstation/09-timezone.png)

![NIC renamed External](../evidence/02-workstation/10-nic-external.png)

## 6. Domain join

`WKSTN01` joined `udokaudodigwe.com`. Full name `Wkstn01.udokaudodigwe.com`. It first appeared in the Computers container, then was moved to the Marketing OU.

![Joined domain, computer object in Computers](../evidence/02-workstation/11-domain-join.png)

## 7. Accounts and Group Policy

Marketing OU holds user **Udoka Udodigwe** (`udoka.udodigwe`), security group **Marketing**, and computer **WKSTN01**.

![Marketing OU](../evidence/03-accounts-and-policy/01-marketing-ou.png)

![WKSTN01 in the Marketing OU](../evidence/03-accounts-and-policy/02-computer-in-marketing.png)

GPO **Marketing Lockdown** is linked to `udokaudodigwe.com/Marketing` (link enabled, not enforced, security filtering Authenticated Users). User setting **Prohibit access to Control Panel and PC settings** is Enabled. On WKSTN01 that produces “This operation has been cancelled due to restrictions in effect on this computer.”

The workstation `gpresult` was taken as `Administrator`, whose account is in `CN=Users`, so that report lists only Default Domain Policy. The restriction dialog is the check for a user the Marketing link applies to.

![Marketing Lockdown linked](../evidence/03-accounts-and-policy/03-gpo-linked.png)

![Prohibit Control Panel enabled](../evidence/03-accounts-and-policy/04-prohibit-control-panel.png)

![Link path and security filtering](../evidence/03-accounts-and-policy/05-gpo-scope.png)

![Control Panel blocked on WKSTN01](../evidence/03-accounts-and-policy/06-restriction-on-wkstn01.png)

Default Domain Policy password settings, also in the DC01 `gpresult`:

| Setting | Value |
| --- | --- |
| Enforce password history | 24 remembered |
| Maximum password age | 30 days |
| Minimum password age | 1 day |
| Minimum password length | 10 characters |
| Complexity | Enabled |
| Reversible encryption | Disabled |

![Password policy](../evidence/03-accounts-and-policy/07-password-policy.png)

## 8. Share and local admin

`C:\UdokaShare` is shared as `UdokaShare`. `udoka.udodigwe` has Full Control on the share and Full control on the NTFS ACL. The same account is a member of local Administrators, with `Administrator`, the local user `udokaudodigwe`, and `UDOKAUDODIGWE\Domain Admins`.

![Share permissions](../evidence/04-share-remote-recovery/01-share-permissions.png)

![NTFS permissions](../evidence/04-share-remote-recovery/02-ntfs-permissions.png)

![Local Administrators](../evidence/04-share-remote-recovery/03-local-administrators.png)

WKSTN01 optional features added: RSAT IPAM Client, Volume Activation Tools, Storage Replica PowerShell, and WSUS Tools. DC01 already had DNS Server Tools and DHCP Server Tools installed.

![RSAT on WKSTN01, role tools on DC01](../evidence/04-share-remote-recovery/04-rsat.png)

## 9. WinRM and firewall

On WKSTN01 the External adapter’s profile is `DomainAuthenticated`. `Enable-PSRemoting -Force` started WinRM and enabled the firewall exception. From DC01, `Resolve-DnsName Wkstn01` returns an A record, `Test-WSMan Wkstn01` answers, and `Enter-PSSession` lands as `udokaudodigwe\administrator`.

![WinRM enabled](../evidence/04-share-remote-recovery/05-winrm-enabled.png)

![Remote session from DC01](../evidence/04-share-remote-recovery/06-winrm-from-dc01.png)

Inbound rule **DOOM** is enabled: allow TCP 666.

![DOOM inbound rule](../evidence/04-share-remote-recovery/07-doom-firewall-rule.png)

## 10. Files and recovery

`C:\UdokaShare\SecretData.txt` is in the share. `cipher` on that folder reports that new files there are not encrypted. System Protection is on for `C:`, max 5% (4.96 GB). A restore point was created 24 Jul 2026 12:45 AM. The same session wrote `file9.txt`–`file18.txt` and packed them into `UdokaWkstn01.zip`.

![Export commands and cipher check](../evidence/04-share-remote-recovery/08-export-commands.png)

![SecretData.txt in UdokaShare](../evidence/04-share-remote-recovery/09-secretdata.png)

![System Protection on C:](../evidence/04-share-remote-recovery/10-system-protection.png)

![Restore point created](../evidence/04-share-remote-recovery/11-restore-point.png)

## Exports

| DC01 | What it confirms |
| --- | --- |
| [file1-gpresult.txt](../evidence/exports/dc01/file1-gpresult.txt) | Primary DC, domain, password policy |
| [file2-timezone.txt](../evidence/exports/dc01/file2-timezone.txt) | Eastern time |
| [file3-firewall-profiles.txt](../evidence/exports/dc01/file3-firewall-profiles.txt) | Domain profile on, Private profile off |
| [file4-ip-configuration.txt](../evidence/exports/dc01/file4-ip-configuration.txt) | Private `172.16.0.1`, External `10.0.0.132` |
| [file5-dhcp-scope.txt](../evidence/exports/dc01/file5-dhcp-scope.txt) | Scope `172.16.0.100`–`200`, 8 days |
| [file6-wds-boot-image.txt](../evidence/exports/dc01/file6-wds-boot-image.txt) | `boot.wim`, Windows 10 Setup |
| [file7-wds-install-image.txt](../evidence/exports/dc01/file7-wds-install-image.txt) | Windows 10 Pro N install image |
| [file8-ous.txt](../evidence/exports/dc01/file8-ous.txt) | OUs Domain Controllers and Marketing |

| WKSTN01 | What it confirms |
| --- | --- |
| [file9-gpresult.txt](../evidence/exports/wkstn01/file9-gpresult.txt) | Member workstation in Marketing, OS `10.0.26200` |
| [file10-timezone.txt](../evidence/exports/wkstn01/file10-timezone.txt) | Eastern time |
| [file11-ip-configuration.txt](../evidence/exports/wkstn01/file11-ip-configuration.txt) | `10.0.0.134`, DNS `10.0.0.132` |
| [file12-installed-products.txt](../evidence/exports/wkstn01/file12-installed-products.txt) | Empty `Win32_Product` query |
| [file13-share.txt](../evidence/exports/wkstn01/file13-share.txt) | Share `UdokaShare` |
| [file14-ntfs-acl.txt](../evidence/exports/wkstn01/file14-ntfs-acl.txt) | NTFS ACL |
| [file15-restore-point.txt](../evidence/exports/wkstn01/file15-restore-point.txt) | Restore point |
| [file16-firewall-rules.txt](../evidence/exports/wkstn01/file16-firewall-rules.txt) | Full rule list, including DOOM |
| [file17-winrm.txt](../evidence/exports/wkstn01/file17-winrm.txt) | WinRM identity |
| [file18-cipher.txt](../evidence/exports/wkstn01/file18-cipher.txt) | Folder is not encrypting new files |
