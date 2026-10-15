# Enrolling an Ubuntu Linux Device
**Last updated:** 15/10/2026

Intune supports Linux devices for **compliance reporting and Conditional Access**. It is not full device management: you can check a Linux machine against a compliance policy and use that result to gate access to Microsoft 365 web apps in the browser. You can't push apps or configuration to it the way you can with Windows.

## What you need

- A supported Linux distribution. At the time of writing that is **Ubuntu 24.04 and 26.04 LTS** and **RHEL 9 and 10**. Check [Microsoft's current list](https://learn.microsoft.com/en-us/intune/user-help/company-portal/intune-app-linux) before you start.
- **Microsoft Edge** for Linux. Conditional Access for Microsoft 365 web apps on Linux is enforced through Edge.
- The **Microsoft Intune app** for Linux.
- A user with an Intune license.
- The [Entra device settings](README.md#before-you-enroll-anything-entra-device-settings) saved.

## 1. Install Microsoft Edge

1. Go to [microsoft.com/edge](https://www.microsoft.com/edge) and choose **Download for Linux (.deb)**.
2. Open the downloaded package. It opens in the App Center. Confirm the installation and wait for it to finish.

<br>
<img src="https://i.imgur.com/90hh6Ij.png" alt="Ubuntu App Center installing the Microsoft Edge package"/>
<br>

## 2. Install the Microsoft Intune app

Microsoft's instructions are on the [Intune app for Linux page](https://learn.microsoft.com/en-us/intune/user-help/company-portal/intune-app-linux). At the time of writing, the app is installed with a script from a Microsoft GitHub repository (`microsoft/shell-intune-samples`, folder `Linux/Intune Installer`). Check the page for the current method, since this may change.

1. Install git if you don't have it:

```bash
sudo apt install git
```

2. Clone the repository:

```bash
git clone https://github.com/microsoft/shell-intune-samples.git
```

3. Move to the installer folder:

```bash
cd "shell-intune-samples/Linux/Intune Installer/"
```

4. Make the script executable and run it:

```bash
chmod +x installer.sh
sudo ./installer.sh --verbose
```

<br>
<img src="https://i.imgur.com/9HlbeBG.png" alt="Terminal input of the Intune installer script running with the verbose flag"/>
<br>

5. Refresh the session-level services, then **reboot** to be safe.

6. After the reboot, the **Microsoft Intune** app appears in your Apps.

<br>
<img src="https://i.imgur.com/2VodCuB.png" alt="Ubuntu Apps list showing the Microsoft Intune Portal app installed"/>
<br>

## 3. Register the device

1. Open the **Microsoft Intune** app and sign in with the work account.
2. Select **Register**.

<br>
<img src="https://i.imgur.com/oJSs4sx.png" alt="Microsoft Intune Portal app on Linux showing the Register screen after sign-in"/>
<br>

3. The agent checks the device's compliance status on the next screen.

<br>
<img src="https://i.imgur.com/yDx1ouV.png" alt="Microsoft Intune Portal app on Linux checking device compliance after registration"/>
<br>

## 4. Confirm it worked

- **Entra ID > Devices > All devices:** the device should appear as registered.
- **Intune admin center > Devices > All devices:** the device should appear and show a compliance state.

<br>
<img src="https://i.imgur.com/yYkwqjN.png" alt="Entra ID All devices page showing the Linux device registered"/>
<br>

<br>
<img src="https://i.imgur.com/MIjqT0G.png" alt="Intune admin center All devices page showing the Linux device managed by Intune with its compliance state"/>
<br>

## Troubleshooting: registration stalls at "Verify your identity"

A common failure looks like this: sign-in reaches a **Verify your identity** screen and then sits there with no error, no MFA prompt and no progress. Retrying, rebooting and clearing caches don't help.

**Check the local side first.** These rule out the machine:

- The `microsoft-identity-broker` and `intune-daemon` services are present. They're started on demand, so being idle is normal.
- The WebKitGTK dependency is installed.
- The Microsoft package repository and its signing key were set up by the installer.
- The Secret Service (`org.freedesktop.secrets`, provided by GNOME Keyring) is running and unlocked.

**Then check the sign-in logs.** The real cause is often not on the device. In **Entra ID > Monitoring & health > Sign-in logs**, open the failed sign-in and look at the **Conditional Access** tab and the error code.

A failure with:

- `conditionalAccessStatus`: **failure**
- `errorCode`: **50074** ("Strong authentication is required")

means a Conditional Access policy is asking for something the Linux client can't provide. This happens with a policy that requires **phishing-resistant MFA** for administrators: the Linux Intune client can't complete a passkey (FIDO2) challenge, so it can never meet that requirement.

**The quick fix:** Temporarily exclude the **Microsoft Intune** resource from that policy (**Target resources > Resources > Exclude**), register the device, then remove the exclusion.

> **Keep the exception small.** A broad exclusion on your main admin policy weakens it. A better pattern is a dedicated, narrowly scoped policy for the exception, and a note of when you added it and when you'll review it.

## Limits to know about

- Linux support covers **compliance checks and Conditional Access for browser access to Microsoft 365** (through Edge). It is not full device management.
- Disk encryption and password rules are checked by the compliance policy. See [Linux compliance policy](../02-compliance-policies/linux-ubuntu.md).

## Checklist

- [ ] Supported distribution confirmed
- [ ] Microsoft Edge installed
- [ ] Microsoft Intune app installed and the device rebooted
- [ ] Device registered
- [ ] Device visible in Entra ID and Intune
- [ ] Any Conditional Access exception documented and scoped narrowly
