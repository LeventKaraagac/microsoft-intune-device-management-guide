# Enrolling a Company-Owned iPhone or iPad (without Apple Business Manager)
**Last updated:** 15.10.2026

The cleanest way to manage a company-owned iPhone devices is through Apple Business Manager (ABM), which enrolls the device automatically during setup and puts it in supervised mode. Not every small company has ABM ready, though. This page covers the path without it: enroll through the Company Portal app, then mark the device as corporate-owned in Intune.

Without ABM enrollment, the devices are enrolled but classified as non-supervised.

## What you get, and what you don't

| Capability | Company Portal enrollment, marked corporate | Full ABM / supervised |
|---|---|---|
| Compliance policy evaluation | Yes | Yes |
| Full remote wipe | Yes | Yes |
| Corporate ownership reporting | Yes | Yes |
| Supervised-only restrictions (for example, blocking the App Store entirely or a system-wide AirDrop block) | **No** | Yes |
| Zero-touch Setup Assistant enrollment | **No** (manual Company Portal install) | Yes |

Marking a device "corporate" in Intune is a **label**. It does not make the device supervised. If you need supervised-only restrictions, plan for ABM and automated enrollment, which generally happens when a device is first set up.

## What you need

- An Intune license for the user
- An **Apple MDM push certificate** in Intune. Without it, Apple enrollment isn't available
- An Apple ID to create that certificate (see the advice below)
- The [Entra device settings](README.md#before-you-enroll-anything-entra-device-settings) saved
- If you plan to use ABM later, sign up for Apple Business Manager early. It can take time to be verified

## 1. Set up the Apple MDM push certificate

Intune needs this certificate to manage Apple devices.

**Where:** Intune admin center > Devices > Device onboarding > Enrollment > **Apple** tab

If the certificate isn't set up, the enrollment options are unavailable until it is.

<br>
<img src="https://i.imgur.com/aLajo4c.png" alt="Intune Enrollment page Apple tab showing that the Apple MDM Push Certificate is required before enrollment options are available"/>
<br>

1. Select **Apple MDM Push Certificate**.
2. In the wizard, tick **I agree** to grant Microsoft permission to send user and device information to Apple.
3. Download the **Intune certificate signing request (CSR)** to your computer.
4. Go to [identity.apple.com](https://identity.apple.com/), sign in, and upload the CSR to create the push certificate. Download the certificate it gives you.
5. Return to Intune, upload the Apple certificate, and enter the **Apple ID** you used to create it. Select **Upload**.

<br>
<img src="https://i.imgur.com/EuAD7G6.png" alt="Intune Apple MDM Push Certificate page showing the certificate with an Active status"/>
<br>

The certificate should now show as **Active**, and the Apple enrollment options become available.

> **Use a company Apple ID.** The certificate is tied to the Apple ID that created it. It expires after one year, and **you must renew it with the same Apple ID**. Put a reminder in your calendar well before the expiry date.

<br>
<img src="https://i.imgur.com/QDwskPD.png" alt="Apple enrollment options when the MDM Push Certificate is set up"/>


**Note:** As this guide showcases non-ABM deployment, the steps below refers to that.

## 2. Install the Company Portal on the device

1. On the iPhone, install **Company Portal** from the App Store and sign in with the work account.
2. Follow the setup steps in the app.

<br>
<img src="https://i.imgur.com/4B7csZE.png" alt="Company Portal app on iPhone showing the company access setup steps"/>
<br>

3. **Review the privacy information** shown by the app.

<br>
<img src="https://i.imgur.com/hXDisiL.png" alt="Company Portal privacy information screen on iPhone"/>
<br>

4. **Download and install the management profile** when prompted, and allow it in iOS Settings.

<br>
<img src="https://i.imgur.com/KmIFpi6.png" alt="iPhone prompt to download and install the management profile for company access"/>
<br>

## 3. Confirm the device appears

**Where:** Intune admin center > Devices > Apple mobile devices

The device should now be listed.

<br>
<img src="https://i.imgur.com/IzDkKFx.png" alt="Intune Apple mobile devices list showing the newly enrolled iPhone"/>
<br>

## 4. Mark the device as corporate-owned

A device enrolled this way defaults to **Personal** ownership. Change it:

1. In **Devices > Apple mobile devices**, select the device.
2. Open the **Properties** tab and choose **Edit** next to the basic properties.

<br>
<img src="https://i.imgur.com/peFwWSZ.png" alt="Device Properties tab in Intune with the Edit option for basic properties"/>
<br>

3. Set **Ownership** to **Corporate** and save.

<br>
<img src="https://i.imgur.com/idkwGU2.png" alt="Device ownership setting changed to Corporate in Intune"/>
<br>

The device is now enrolled as company-owned. Remember it is **not supervised**.

> **Why it matters:** Ownership drives which policies apply. Dynamic device groups use it to separate corporate and personal devices (see [02 - groups](../../microsoft-entra-id-security-guide/tree/main/02-user-group-and-role-structure/)), and compliance policies can be different for each.

## Next

Build the [iOS compliance policy](../02-compliance-policies/) for corporate devices.

## Checklist

- [ ] Apple MDM push certificate created with a company Apple ID and showing Active
- [ ] Renewal reminder set
- [ ] Company Portal installed and management profile accepted
- [ ] Device visible under Apple mobile devices
- [ ] Ownership set to Corporate
- [ ] Limits of non-supervised enrollment understood
