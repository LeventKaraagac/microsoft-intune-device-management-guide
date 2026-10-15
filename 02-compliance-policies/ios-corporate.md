# iOS Compliance Policy: Corporate Devices
**Last updated:** 15.10.2026

Company-owned iPhones and iPads can carry a stricter policy than personal ones, because the company owns the device and can ask for more.

## Before you start

- Devices are [enrolled](../01-device-enrollment/ios-corporate-non-abm.md) and marked as **Corporate**.
- You have a dynamic device group for corporate iOS devices, for example **SG-Devices-iOS-Corporate**.
- The **device threat level** and **machine risk score** checks need **Microsoft Defender for Endpoint** connected to Intune, and the Defender app on the device. If you haven't set that up, leave those two settings as Not configured. See the [Defender guide](https://github.com/LeventKaraagac/microsoft-defender-threat-protection-guide).

## Create the policy

**Where:** Intune admin center > Devices > Manage devices > Compliance > Policies > Create policy

1. Choose **iOS/iPadOS** as the platform and select **Create**.
2. Name the policy, for example `iOS Compliance - Corporate`, and add a description.

<br>
<img src="https://i.imgur.com/a8YY3XY.png" alt="Create compliance policy page with the iOS/iPadOS platform selected"/>
<br>

3. On **Compliance settings**, use these values.

### Device Health

| Setting | Value |
|---|---|
| Jailbroken devices | **Block** |
| Require the device to be at or under the Device Threat Level | **Medium** (needs Defender for Endpoint) |

### Device Properties: operating system version

| Setting | Value |
|---|---|
| Minimum OS version | The oldest iOS version you're willing to support. Review it whenever Apple releases a major version |
| Maximum OS version, build versions | Not configured |

### Microsoft Defender for Endpoint

| Setting | Value |
|---|---|
| Require the device to be at or under the machine risk score | **Medium** (needs Defender for Endpoint) |

### System Security: Password (all enrollment types)

| Setting | Value |
|---|---|
| Require a password to unlock mobile devices | **Require** |

### System Security: Password (device enrollment and automated device enrollment)

| Setting | Value |
|---|---|
| Simple passwords | **Block** |
| Minimum password length | **6** |
| Required password type | **Alphanumeric** |
| Number of non-alphanumeric characters | **1** |
| Maximum minutes after screen lock before password is required | **Immediately** |
| Maximum minutes of inactivity until screen locks | **10** |
| Password expiration (days) | Not configured. Current guidance advises against forced periodic changes |
| Number of previous passwords to prevent reuse | **5** |

### Device Security

| Setting | Value |
|---|---|
| Restricted apps | Not configured |

<br>
<img src="https://i.imgur.com/IChv8ZO.png" alt="iOS compliance policy settings showing Device Health, Device Properties and System Security password options for corporate devices"/>
<br>

<br>
<img src="https://i.imgur.com/AStaHKc.png" alt="iOS compliance policy settings showing Device Health, Device Properties and System Security password options for corporate devices"/>
<br>

<br>
<img src="https://i.imgur.com/z8JvDQR.png" alt="iOS compliance policy settings showing Device Health, Device Properties and System Security password options for corporate devices"/>
<br>

<br>
<img src="https://i.imgur.com/S6TFZuB.png" alt="iOS compliance policy settings showing Device Health, Device Properties and System Security password options for corporate devices"/>
<br>

4. On **Actions for noncompliance**, add **Send push notification to end user** and **Send email to end user**.

<br>
<img src="https://i.imgur.com/k3HoFts.png" alt="Actions for noncompliance tab with push notification and email actions selected"/>
<br>

5. On **Assignments**, select **SG-Devices-iOS-Corporate**.

<br>
<img src="https://i.imgur.com/TN0NjNj.png" alt="Assignments tab with the corporate iOS devices group selected"/>
<br>

6. Select **Review + create**. The policy now appears in the policies list.

## Check your work

- The corporate iPhone reports **Compliant**.
- Test non-compliance on a spare device: for example, remove the passcode and confirm the device flips to **Not compliant** and the user is notified.

## Checklist

- [ ] Defender prerequisites met, or the Defender settings left Not configured
- [ ] Notification template chosen
- [ ] Assigned to the corporate iOS group
- [ ] Tested compliant and non-compliant states
