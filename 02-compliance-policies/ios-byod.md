# iOS Compliance Policy: Personal Devices (BYOD)
**Last updated:** 15.10.2026

Personal phones should have a **lighter** policy than company ones. The device belongs to the person, and asking for too much will make people refuse to enrol. The aim is to protect company data with the least intrusion on the owner.

## What is deliberately lighter than the corporate policy

| Setting | Corporate | BYOD | Reason |
|---|---|---|---|
| Device Threat Level and machine risk score | Required | Not configured | Requiring a security agent on a personal phone is too invasive |
| Password type | Alphanumeric | Numeric | Easier for people to live with on their own phone |
| Inactivity before screen lock | 10 minutes | 5 minutes | |
| Password expiration, reuse limits | Reuse limit set | Not configured | Less friction |
| Minimum OS version | Set | **Same as corporate** | Keep the version baseline the same, whoever owns the device |

## Before you start

- Devices are [enrolled](../01-device-enrollment/ios-byod.md) as **Personal**.
- You have a dynamic device group for personal iOS devices, for example **SG-Devices-iOS-BYOD**.
- Pair this with an [app protection policy](../03-app-protection-policies/) to protect work data in apps.

## Create the policy

**Where:** Intune admin center > Devices > Manage devices > Compliance > Policies > Create policy

1. Choose **iOS/iPadOS** and select **Create**.
2. Name the policy, for example `iOS Compliance - BYOD`, and add a description.

<br>
<img src="https://i.imgur.com/trxGyyI.png" alt="Create compliance policy page with the iOS/iPadOS platform selected for the BYOD policy"/>
<br>

3. On **Compliance settings**, use these values.

### Device Health

| Setting | Value |
|---|---|
| Jailbroken devices | **Block** |
| Device Threat Level | Not configured |

### Device Properties: operating system version

| Setting | Value |
|---|---|
| Minimum OS version | Same as your corporate policy |
| Maximum OS version, build versions | Not configured |

### Microsoft Defender for Endpoint

| Setting | Value |
|---|---|
| Machine risk score | Not configured |

### System Security: Password (all enrollment types)

| Setting | Value |
|---|---|
| Require a password to unlock mobile devices | **Require** |

### System Security: Password (device enrollment and automated device enrollment)

| Setting | Value |
|---|---|
| Simple passwords | **Block** |
| Minimum password length | **6** |
| Required password type | **Numeric** |
| Number of non-alphanumeric characters | Not configured |
| Maximum minutes after screen lock before password is required | **Immediately** |
| Maximum minutes of inactivity until screen locks | **5** |
| Password expiration, previous passwords | Not configured |

### Device Security

| Setting | Value |
|---|---|
| Restricted apps | Not configured |

<br>
<img src="https://i.imgur.com/fOsRvHc.png" alt="iOS BYOD compliance policy settings showing the lighter Device Health and System Security password options"/>
<br>

<br>
<img src="https://i.imgur.com/QYC8nLM.png" alt="iOS BYOD compliance policy settings showing the lighter Device Health and System Security password options"/>
<br>

<br>
<img src="blob:https://imgur.com/0a5c66b4-8316-458f-a882-5d6bdfbde3c9" alt="iOS BYOD compliance policy settings showing the lighter Device Health and System Security password options"/>
<br>

4. On **Actions for noncompliance**, add **Send push notification to end user** and **Send email to end user**.

<br>
<img src="https://i.imgur.com/dY0tqER.png" alt="Actions for noncompliance tab for the BYOD policy with push notification and email actions selected"/>
<br>

5. On **Assignments**, select **SG-Devices-iOS-BYOD**.

<br>
<img src="https://i.imgur.com/lSt6Prt.png" alt="Assignments tab with the personal iOS devices group selected"/>
<br>

6. Select **Review + create**.

## Check your work

- A personal iPhone reports **Compliant**.
- Test non-compliance on a spare device (for example, remove the passcode) and confirm the user is notified.

## Checklist

- [ ] Lighter settings chosen on purpose and explained to users
- [ ] OS baseline matches the corporate policy
- [ ] Notification template chosen
- [ ] Assigned to the BYOD group
- [ ] Tested
