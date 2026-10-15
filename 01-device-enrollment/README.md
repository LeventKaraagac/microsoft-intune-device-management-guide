# 01 - Device Enrollment
**Last edited:** 14/10/2026

Enrollment is how a device becomes known to Intune. Until a device is enrolled, you can't check its compliance or apply policy to it, and Conditional Access can't tell it apart from any other device.

This section covers the enrollment path for each platform. The right path depends on the platform and on who owns the device.

## Pick the path for each device

| Device | Ownership | Enrollment path | Guide |
|---|---|---|---|
| Linux (Ubuntu) | Company | Microsoft Intune app for Linux | [Linux (Ubuntu)](linux-ubuntu-corporate.md) |
| iPhone / iPad | Company, without Apple Business Manager | Company Portal, then mark the device as corporate-owned | [iOS corporate (non-ABM)](ios-corporate-non-abm.md) |
| iPhone / iPad | Personal (BYOD) | Company Portal | [iOS BYOD](ios-byod.md) |
| Windows 11 Home | Personal or company | Access work or school, plus automatic MDM enrollment | [Windows Home](windows-byod-home-edition.md) |

> **Check the edition first.** Windows Home can enroll in Intune, but it can't be Entra-joined and doesn't support BitLocker. That limits what compliance can check. See the Windows guide for the details.

## Before you enroll anything: Entra device settings

These tenant-wide settings decide who can register or join devices, and what happens when they do. Set them first.

**Where:** Entra ID > Devices > Manage > Device settings

| Setting | Recommendation | Why |
|---|---|---|
| **Users may join devices to Microsoft Entra** | **All** for a small company. Use **Selected** as you grow | Unrestricted joining is convenient but becomes a risk at scale |
| **Require multifactor authentication to register or join devices** | **Yes** | A stolen password alone shouldn't be enough to add a device |
| **Maximum number of devices per user** | **20** (Microsoft's recommended default) | Limits clutter and abuse |
| **Global administrator role is added as local administrator on the device during Microsoft Entra join** | **No** | Stops one compromised cloud account from becoming local admin on every company device |
| **Registering user is added as local administrator on the device during Microsoft Entra join** | **None** or **Selected** where you can. Use **All** only if you have a reason | Local admin rights let a user change security settings on their own device |

<br>
<img src="https://i.imgur.com/KSaCsol.png" alt="Entra ID Device settings page showing the settings for who can join devices, MFA to register or join, maximum devices per user and local administrator options"/>
<br>

Save the settings, then start enrolling devices.

> **Licensing:** Intune needs a license assigned to each user. For example, Microsoft 365 Business Premium includes Intune Plan 1. Check **Microsoft 365 admin center > Users > Licenses and apps** before you start.

## Check what's already enrolled

Before you add devices, see what the tenant already has. If this is your first time enrolling devices, the Devices section will be empty like in the picture below.

**Where:** Intune admin center > Devices > All devices

<br>
<img src="https://i.imgur.com/rsf5BdU.png" alt="Intune admin center All devices page before any device is enrolled"/>
<br>

Also check **Devices > Manage devices > Configuration** and **Compliance**, to see whether policies already exist. Don't build over them without knowing what they do.

## Next

After enrollment, build a [compliance policy](../02-compliance-policies/) for each platform so the devices have something to be measured against.

## Checklist

- [ ] Intune licenses assigned
- [ ] Entra device settings reviewed and saved
- [ ] Existing devices and policies checked
- [ ] Enrollment path chosen for each device
