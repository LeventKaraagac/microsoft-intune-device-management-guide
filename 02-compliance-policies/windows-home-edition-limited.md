# Windows Compliance Policy for Home Edition (Limited)

Windows 11 **Home** can enroll in Intune, but it reports fewer signals than Pro, Business or Enterprise. This page builds a policy for Home devices that checks what Home can actually report, and leaves the rest alone so healthy devices aren't flagged by mistake.

## Why a separate policy

Several checks don't work on Home:

- **BitLocker** isn't available on Home.
- **Defender for Endpoint device risk score** needs managed onboarding that Home doesn't support.
- **Encryption reporting:** Intune's encryption check only recognises BitLocker's reporting. Home may have **Device Encryption** turned on, but Intune can't see it, so a check would wrongly return **Not compliant**.

If you need those checks, plan an upgrade to Pro or above. Until then, build a limited policy and document the gap.

## Create the policy

**Where:** Intune admin center > Devices > Manage devices > Compliance > Policies > Create policy

1. Choose **Windows 10 and later** as the platform and select **Create**.
2. On the **Basics** tab, name the policy, for example `Windows Compliance - Home Edition (Limited)`, and add a description that says it is for Home-edition devices.

<br>
<img src="https://i.imgur.com/p5YGwi4.png" alt="Create compliance policy page with the Windows 10 and later platform selected"/>
<br>

3. On the **Compliance settings** tab, use the values below.

### Device Health

| Setting | Value |
|---|---|
| Require BitLocker | Not configured (not supported on Home) |
| Require Secure Boot to be enabled | **Require** |
| Require code integrity | Not configured |

### Device Properties

| Setting | Value |
|---|---|
| Minimum and maximum OS version | Not configured. Set a minimum once you decide which versions you support |
| Valid operating system builds | Not configured |

### System Security: Password

| Setting | Value |
|---|---|
| Require a password to unlock mobile devices | **Require** |
| Simple passwords | **Block** |
| Password type | **Alphanumeric** |
| Password complexity | Require digits, lowercase, uppercase and special characters |
| Minimum password length | **8** |
| Maximum minutes of inactivity before password is required | **60** |
| Password expiration (days) | Not configured. Current guidance advises against forced periodic changes. Set one only if a regulation requires it |
| Number of previous passwords to prevent reuse | **5** |

### Encryption

| Setting | Value |
|---|---|
| Require encryption of data storage on device | **Not configured.** Device Encryption can be enabled manually (it uses AES and the TPM), but Intune only recognises BitLocker's reporting, so this setting would produce a false Non-compliant result |

### Device Security

| Setting | Value |
|---|---|
| Firewall | **Require** |
| Trusted Platform Module (TPM) | **Require** |
| Antivirus | **Require** |
| Antispyware | **Require** |

### Microsoft Defender

| Setting | Value |
|---|---|
| Microsoft Defender Antimalware | **Require** |
| Antimalware security intelligence up to date | **Require** |
| Real-time protection | **Require** |
| Antimalware minimum version | Not configured |

### Microsoft Defender for Endpoint

| Setting | Value |
|---|---|
| Require the device to be at or under the machine risk score | **Not configured.** A risk score needs Defender for Endpoint managed onboarding, which Home doesn't support. Closing this gap means upgrading to Pro, Business or Enterprise |

<br>
<img src="https://i.imgur.com/YoVcWUs.png" alt="Windows compliance policy settings pages showing Device Health, System Security password and Device Security options"/>
<br>

<br>
<img src="https://i.imgur.com/ObMvdZp.png" alt="Windows compliance policy settings pages showing Device Health, System Security password and Device Security options"/>
<br>

4. On **Actions for noncompliance**, add **Send email to end user** and choose your [notification template](noncompliance-notifications.md).

<br>
<img src="https://i.imgur.com/1vyG133.png" alt="Actions for noncompliance tab with Send email to end user selected"/>
<br>

5. On **Assignments**, select the group for your Windows devices, for example **SG-Devices-Windows**.

<br>
<img src="https://i.imgur.com/ew71Rb6.png" alt="Assignments tab with the Windows devices group selected"/>
<br>

6. Select **Review + create**. The policy now appears in the Compliance policies list.

<br>
<img src="https://i.imgur.com/f00BPmf.png" alt="Compliance policies list showing the Windows compliance policy for Home edition"/>
<br>

## Check your work

- An enrolled Home device reports **Compliant** (not Not compliant because of encryption or risk score).
- Turn off the firewall on a test device and confirm it flips to **Not compliant**, then turn it back on.

## Checklist

- [ ] Unsupported checks left as Not configured, with the reasons documented
- [ ] Notification template chosen
- [ ] Assigned to the Windows device group
- [ ] Tested with a compliant and a non-compliant state
