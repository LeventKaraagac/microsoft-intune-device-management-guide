# Non-Compliance Notifications
**Last updated:** 15.10.2026

When a device falls out of compliance, the user should hear about it and know what to fix. A notification template defines the email they receive. Create it **before** you build your compliance policies, because the policies refer to it.

**Where:** Intune admin center > Devices > Manage devices > Compliance > **Notifications** > Create notification

## Steps

1. Select **Create notification** and give it a clear name on the **Basics** tab, for example `Device out of compliance`.

<br>
<img src="https://i.imgur.com/jjHNr8k.png" alt="Create notification Basics tab with a descriptive name entered"/>
<br>

2. Leave the header and footer settings on their defaults.
3. Under **Notification message template**, select **Add** and write the message. Say what happened and what the user should do (for example, "set a passcode" or "update iOS"). Add a contact for help.

<br>
<img src="https://i.imgur.com/CgB3MJ6.png" alt="Notification message template with a subject and message body for non-compliant devices"/>
<br>

<br>
<img src="https://i.imgur.com/Ss7u0ON.png" alt="Notification message template with a subject and message body for non-compliant devices"/>
<br>



4. Select **Review + create**. The template now appears in the Notifications list.

<br>
<img src="https://i.imgur.com/NBTROqk.png" alt="Notifications list showing the new notification template"/>
<br>

## Use it in a policy

In each compliance policy, open **Actions for noncompliance**, add **Send email to end user**, and choose this template.

## Tips for a good message

- Keep it short and specific. Say which requirement failed and how to fix it.
- Don't blame the user. People rarely turn off protections on purpose.
- Say how long they have before they lose access, if a Conditional Access policy depends on compliance.

## Checklist

- [ ] Template created
- [ ] Message tells the user what to do
- [ ] Template selected in each compliance policy
- [ ] A test notification received
