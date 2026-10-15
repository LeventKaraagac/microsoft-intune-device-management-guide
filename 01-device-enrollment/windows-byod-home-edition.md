# Enrolling a Windows 11 Home Device

Many small companies have staff using Windows 11 **Home** laptops. Home can be enrolled in Intune, but it can't be fully Entra-joined and it doesn't support BitLocker or Defender for Endpoint onboarding, so compliance on it is limited. This page shows how to enroll a Home device and what to expect afterwards.

## What works and what doesn't

| Feature | Windows 11 Home | Windows 11 Pro and above |
|---|---|---|
| Intune MDM enrollment | Yes | Yes |
| Join the device to Microsoft Entra | **No** (only "Access work or school") | Yes |
| BitLocker | **No** | Yes |
| Defender for Endpoint managed onboarding and device risk score | **No** | Yes |

**The honest conclusion:** a Home device enrolls, but you can only check a limited set of signals. If you need strong compliance (disk encryption reporting, risk score), plan an upgrade to Pro, Business or Enterprise. The [compliance policy page](../02-compliance-policies/windows-home-edition-limited.md) explains how to build a policy that doesn't mark Home devices non-compliant for settings they can't support.

## What you need

- An Intune license for the user
- Automatic MDM enrollment turned on in Intune (step 2 below)
- The [Entra device settings](README.md#before-you-enroll-anything-entra-device-settings) saved

## 1. Connect the device to the work account

On the Windows 11 Home device:

1. Open **Settings > Accounts > Access work or school**.
2. Select **Connect**. The option **Join this device to Microsoft Entra ID** is not available on Home, which is expected.
3. Enter the work credentials and complete MFA if prompted.
4. Confirm the account now appears under **Access work or school** as connected.

<br>
<img src="https://i.imgur.com/lkfS1xN.png" alt="Windows 11 Settings Access work or school page showing the work account connected"/>
<br>

## 2. Turn on automatic MDM enrollment

**Where:** Intune admin center > Devices > Device onboarding > Enrollment > Windows > **Enrollment options > Automatic Enrollment**

In the wizard, set the **MDM user scope** to **Some** (a group) or **All**, so the user is covered.

<br>
<img src="https://i.imgur.com/jc5bxOF.png" alt="Intune Windows Automatic Enrollment settings with the MDM user scope set"/>
<br>

## 3. Trigger the enrollment

Install **Company Portal** from the Microsoft Store on the device, and sign in with the same work account. This triggers and confirms the actual Intune MDM enrollment.

<br>
<img src="https://i.imgur.com/4K31v0P.png" alt="Company Portal app on Windows signed in with the work account"/>
<br>

## 4. Confirm it worked

**Where:** Intune admin center > Devices > All devices

The laptop should now appear, with **MDM** showing as enrolled (not "None").

<br>
<img src="https://i.imgur.com/WvSGrwp.png" alt="Intune All devices page showing the Windows 11 Home laptop with MDM enrolled"/>
<br>

> **What to expect.** Because the device is Windows Home, BitLocker and full compliance checks aren't available, however you enroll. The device will show as enrolled but limited to the basic signals Home can report, such as OS version where available.

## Next

Build the [Windows compliance policy for Home](../02-compliance-policies/windows-home-edition-limited.md).

## Checklist

- [ ] Work account connected under Access work or school
- [ ] Automatic enrollment turned on with the right user scope
- [ ] Company Portal installed and signed in
- [ ] Device shows MDM enrolled in Intune
- [ ] Limits of Windows Home understood and documented
