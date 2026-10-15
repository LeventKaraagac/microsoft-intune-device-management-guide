# Linux Compliance Policy (Ubuntu)
**Last updated:** 15.10.2026

Intune supports Linux devices for **compliance reporting and Conditional Access**. You can check a Linux machine against a compliance policy (distribution, disk encryption, password rules, or your own Bash checks) and use the result to gate access to Microsoft 365 web apps in Edge. Intune's Linux support doesn't cover the broader management you get on Windows. Endpoint protection for Linux, such as antivirus and EDR, comes from **Microsoft Defender for Endpoint**, which has its own guide: [Defender Threat Protection Guide](https://github.com/LeventKaraagac/microsoft-defender-threat-protection-guide).

## Before you start

- The device is [enrolled](../01-device-enrollment/linux-ubuntu-corporate.md).
- You have a dynamic device group for Linux devices, for example **SG-Devices-Linux**.
- **Disk encryption must be set up when the operating system is installed** (LUKS). You can't add it afterwards without reinstalling, so tell users before they set up a new machine.

## Create the policy

**Where:** Intune admin center > Devices > Manage devices > Compliance > Policies > Create policy

1. Choose **Linux** as the platform and select **Create**.
2. Name the policy, for example `Linux Compliance - Ubuntu`, and add a description.
3. On **Compliance settings**, set:

| Setting | Value |
|---|---|
| Allowed distributions | **Ubuntu**, with the versions you support (at the time of writing 24.04 and 26.04 LTS) |
| Require disk encryption | **Require** |
| Require password or passcode | **Require** |

<br>
<img src="https://i.imgur.com/iMFvZ1F.png" alt="Linux compliance policy settings showing the allowed distribution, disk encryption and password requirements"/>
<br>

4. On **Actions for noncompliance**, choose **Send email to end user** and select your [notification template](noncompliance-notifications.md).

<br>
<img src="https://i.imgur.com/o3wzZLk.png" alt="Actions for noncompliance tab for the Linux policy with the email action selected"/>
<br>

5. On **Assignments**, select the Linux device group, for example **SG-Devices-Linux**.
6. Select **Review + create**. The policy now appears in the table.

<br>
<img src="https://i.imgur.com/csqMj8n.png" alt="Compliance policies list showing the Linux compliance policy"/>
<br>

## Check your work

- The enrolled Linux device reports **Compliant**.
- If it reports **Not compliant**, open the device's compliance details to see which setting failed. A typical cause is a distribution version you haven't listed.

## Checklist

- [ ] Allowed distributions and versions set
- [ ] Disk encryption required and confirmed on the device
- [ ] Notification template chosen
- [ ] Assigned to the Linux device group
- [ ] Device reports Compliant
