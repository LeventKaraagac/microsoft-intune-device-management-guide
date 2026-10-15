# 03 - App Protection Policies
**Last updated:** 15.10.2026

Compliance policies protect the **device**. App protection policies protect the **company data inside specific apps**, whoever owns the device. They matter most for personal (BYOD) phones, where you don't want, and often shouldn't, manage the whole device.

## What this section will cover

### 1. What app protection policies are, and when to use them
- Device management vs app management: what each one controls
- Why app protection fits personal devices
- How it works alongside [compliance policies](../02-compliance-policies/) and Conditional Access, not instead of them

### 2. Choosing which apps to protect
- Which Microsoft apps support app protection (for example Outlook and Teams)
- Why a device with only protected apps is a cleaner, lower-friction setup for personal phones

### 3. Building an iOS app protection policy
- **Data protection:** controlling copy and paste between company and personal apps, saving to personal locations, and backups
- **Access requirements:** requiring a PIN or biometrics to open protected apps, and how often to re-check
- **Conditional launch:** blocking access on jailbroken devices or old OS versions, and what happens when a device can't reach Intune for a while
- **Assignment:** targeting users or groups, and the apps the policy applies to

### 4. Testing the policy
- Confirming that company data can't be copied into an unmanaged app
- Confirming the PIN and conditional-launch rules work as intended
- Reviewing the app protection reports in Intune

### 5. Using app protection in Conditional Access
- Requiring a protected app for access to company data from personal phones
- Combining it with a compliance requirement for company-owned devices

## Before you start

You'll need:

- Intune licenses for your users
- Users signed in to the supported apps with their work accounts
- A clear idea of which devices are personal and which are company-owned. See [device enrollment](../01-device-enrollment/)

## Related sections

- [Device enrollment](../01-device-enrollment/): how personal and company devices get into Intune
- [Compliance policies](../02-compliance-policies/): checks for the device itself
