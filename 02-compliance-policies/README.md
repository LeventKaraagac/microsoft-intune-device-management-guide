# 02 - Compliance Policies
**Last updated:** 15.10.2026

A compliance policy is a set of rules a device must meet, such as encryption on, a passcode set, and no jailbreak. Intune checks each enrolled device against its policy and marks it **Compliant** or **Not compliant**. Conditional Access can then use that result, for example by only allowing compliant devices to reach company data.

## What compliance policies do, and don't do

A compliance policy **checks** settings. It does **not change** them. If a device fails the policy, Intune can notify the user and flag the device, but it doesn't fix the setting. Pushing settings to devices is a separate job, done with configuration profiles.

## One policy per platform

Each platform reports different settings, so build a policy for each one:

| Policy | Platform | Guide |
|---|---|---|
| Windows (Home edition, limited) | Windows 10 and later | [Windows Home](windows-home-edition-limited.md) |
| Linux (Ubuntu) | Linux | [Linux (Ubuntu)](linux-ubuntu.md) |
| iOS corporate | iOS/iPadOS | [iOS corporate](ios-corporate.md) |
| iOS BYOD | iOS/iPadOS | [iOS BYOD](ios-byod.md) |

Set limits to what each platform can actually report. A policy that asks a device for something it can't provide will mark a healthy device as non-compliant.

## Before you build policies

1. **Enroll devices** first. See [01 - Device enrollment](../01-device-enrollment/).
2. **Create dynamic device groups** so each policy targets the right devices. See the Entra guide's [dynamic device groups](https://github.com/LeventKaraagac/microsoft-entra-id-security-guide/tree/main/02-user-group-and-role-structure).
3. **Create a notification template** so users are told when they fall out of compliance. See [non-compliance notifications](noncompliance-notifications.md). Do this before you build the policies, because they refer to it.

## Tenant-wide compliance setting

**Where:** Intune admin center > Devices > Manage devices > Compliance > **Compliance settings**

Set **Mark devices with no compliance policy assigned as** to **Not compliant**. Otherwise a device with no policy counts as compliant by default, which can let an unmanaged or forgotten device through a "require compliant device" rule.

<br>
<img src="https://i.imgur.com/oFisBBD.png" alt="Intune Compliance settings page with Mark devices with no compliance policy assigned as set to Not compliant"/>
<br>

## Where to create a policy

**Where:** Intune admin center > Devices > Manage devices > Compliance > Policies > **Create policy**

<br>
<img src="https://i.imgur.com/Gyck1H2.png" alt="Intune Compliance Policies page with the Create policy option"/>
<br>

## After you create the policies

Give Intune a little time to check each device. Then open the compliance overview report to see which devices are compliant, non-compliant or still being evaluated.


## Test them

| Check | How |
|---|---|
| Compliant device passes | Confirm each enrolled device reports **Compliant** |
| Non-compliance is detected | On a test device, turn off one required setting and confirm the device flips to **Not compliant** |
| Notification works | Confirm the user receives the message |
| Conditional Access uses it | Confirm a compliant device gets access and a non-compliant one doesn't |

## Checklist

- [ ] Devices enrolled and in the right groups
- [ ] Notification template created
- [ ] "No policy assigned" set to Not compliant
- [ ] One policy per platform built and assigned
- [ ] Each policy tested
