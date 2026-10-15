# Enrolling a Personal iPhone or iPad (BYOD)
**Last updated:** 15.10.2026

When people use their own phones for work, the goal is to protect company data without taking over the person's device. This page covers enrolling personal iOS devices through the Company Portal app.

## What changes for a personal device

- **Ownership stays Personal.** Don't change it to Corporate, because the device is not company property.
- **Lighter requirements.** Personal devices should have a lighter compliance baseline than company ones. For example, you might not require a security agent on a personal phone, and might accept a simpler passcode. See the [BYOD compliance policy](../02-compliance-policies/).
- **Protect work data, not the whole device.** Pair enrollment with an [app protection policy](../03-app-protection-policies/), which encrypts and isolates company data in apps like Outlook and Teams without needing full device management.

**Be open with users about what you can see.** Before you enroll anyone's personal phone, read Microsoft's documentation on [what Intune can and can't see on personal devices](https://learn.microsoft.com/en-us/mem/intune/user-help/what-information-can-your-company-see-when-you-enroll-your-device-in-intune) and explain it to them. Trust is the main reason people will agree to this.

## What you need

- An Intune license for the user
- An **Apple MDM push certificate** in Intune. See [the corporate iOS page](ios-corporate-non-abm.md#1-set-up-the-apple-mdm-push-certificate) for how to create one
- The [Entra device settings](README.md#before-you-enroll-anything-entra-device-settings) saved if ABM deployment methods are used.

## Steps

1. On the user's iPhone, install **Company Portal** from the App Store and sign in with the work account.
2. Follow the setup steps in the app and review the **privacy information** it shows.

<br>
<img src="https://i.imgur.com/4B7csZE.png" alt="Company Portal privacy information screen on a personal iPhone"/>
<br>

3. **Download and install the management profile** when prompted, and allow it in iOS Settings.

<br>
<img src="https://i.imgur.com/KmIFpi6.png" alt="iPhone prompt to install the management profile during BYOD enrollment"/>
<br>

4. In the Intune admin center, go to **Devices > Apple mobile devices** and confirm the device is listed with ownership **Personal**.

<br>
<img src="https://i.imgur.com/IzDkKFx.png" alt="Intune Apple mobile devices list showing the personal iPhone with ownership set to Personal"/>
<br>

## Check your work

- The device appears under **Apple mobile devices** with ownership **Personal**.
- It is in the personal-device dynamic group (for example SG-Devices-iOS-BYOD). If it isn't, check the group rule. See the Entra guide's section on dynamic device groups.
- After you assign a compliance policy, the device reports a compliance state.

## Checklist

- [ ] User understands what the company can and can't see
- [ ] Company Portal installed and management profile accepted
- [ ] Device visible with ownership Personal
- [ ] Device in the BYOD dynamic group
- [ ] BYOD compliance policy and app protection policy assigned
