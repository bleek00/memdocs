---
title: Windows Autopilot user-driven Microsoft Entra join - Step 6 of 8 - Create and assign a user-driven Microsoft Entra join Autopilot profile
description: How to - Windows Autopilot user-driven Microsoft Entra join - Step 6 of 8 - Create and assign a user-driven Microsoft Entra join Autopilot profile.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# User-driven Microsoft Entra join: Create and assign user-driven Microsoft Entra join Autopilot profile

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)

> [!div class="checklist"]
>
> - **Step 6: Create and assign Autopilot profile**

- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Deploy the device](azure-ad-join-deploy-device.md)

For an overview of the Windows Autopilot user-driven Microsoft Entra join workflow, see [Windows Autopilot user-driven Microsoft Entra join overview](azure-ad-join-workflow.md#workflow).

## Create and assign user-driven Microsoft Entra join Autopilot profile

The Autopilot profile specifies how the device is configured during Windows Setup and what is shown during the out-of-box experience (OOBE).

When an admin creates an Autopilot profile for the user-driven scenario, devices with this Autopilot profile are associated with the user enrolling the device. User credentials are required to enroll the device.

The difference between an Autopilot user-driven Microsoft Entra join and an Autopilot Microsoft Entra hybrid join is that the user-driven Microsoft Entra join scenario only joins Microsoft Entra ID during Autopilot. The Microsoft Entra hybrid join scenario joins both an on-premises domain and Microsoft Entra ID during Autopilot.

> [!TIP]
>
> For Configuration Manager admins, the Autopilot profile is similar to some of the configuration that takes place during a task sequence via an `unattend.xml` file. The `unattend.xml` file is configured during the **Apply Windows Settings** and **Apply Network Settings** steps. Note however that Autopilot doesn't use `unattend.xml` files.

To create a user-driven Microsoft Entra join Autopilot profile, follow these steps:

[!INCLUDE [Autopilot profiles before steps](../includes/autopilot-profile-steps-before.md)]

8. In the **Out-of-box experience (OOBE)** page:

      - For **Deployment mode**, select **User-driven**.

      - For **Join to Microsoft Entra ID as**, select **Microsoft Entra joined**.

      - For **Microsoft Software License Terms**, select **Hide** to skip the EULA page.

      - For **Privacy settings**, select **Hide** to skip the privacy settings.

      - For **Hide change account options**, select **Hide**.

      - For **User account type**, select the desired account type for the user. The options are either **Administrator** or **Standard** user. If **Administrator** is chosen, the user is added to the local Administrator group for the device.

      - For **Allow pre-provisioned deployment**, select **No**.

        > [!NOTE]
        >
        > For the Windows Autopilot for pre-provisioned deployment Microsoft Entra join scenario, see [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra join in Intune](../pre-provisioning/azure-ad-join-workflow.md)

      - For **Language (Region)**, select **Operating system default** to use the default language for the operating system being configured. If another language is desired, select the desired language from the drop-down list.

      - For **Automatically configure keyboard**, select **Yes** to skip the keyboard selection page.

      - For **Apply device name template**, select **No**. Alternatively, **Yes** can be chosen to apply a device name template. Be aware of the following if the name template is selected to **Yes**:

        - Names must be 15 characters or less, and can have letters, numbers, and hyphens.
        - Names can't be all numbers.
        - Use the [%SERIAL% macro](/windows/client-management/mdm/accounts-csp) to add a hardware-specific serial number.
        - Use the [%RAND:x% macro](/windows/client-management/mdm/accounts-csp) to add a random string of numbers, where x equals the number of digits to add.

      > [!NOTE]
      >
      > The above settings are selected to minimize needed user interaction during device setup. However, some of the settings that are hidden can instead be shown as desired. For example, some regions might require that **Privacy settings** always be shown.

      > [!NOTE]
      >
      > If the language/region and keyboard screens are set to hidden, they might still be displayed if there's no network connectivity at the start of the Autopilot deployment. The settings to hide these screens are defined in the Autopilot profile. However, if there's no network connectivity, the Autopilot profile with the settings hasn't downloaded yet which results in the screens being displayed. Once network connectivity is established, the Autopilot profile is downloaded and any additional screen settings should work as expected.

[!INCLUDE [Autopilot profiles after steps](../includes/autopilot-profile-steps-after.md)]

## Verify device has an Autopilot profile assigned to it

[!INCLUDE [How to verify a device has an Autopilot profile assigned to it in Intune](../includes/verify-autopilot-profile-assignment.md)]

## Next step: Assign Autopilot device to a user (optional)

> [!div class="nextstepaction"]
> [Step 7: Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)

If a user isn't being assigned to the device, then skip to **[Step 8: Deploy the device](azure-ad-join-deploy-device.md)**.

> [!div class="nextstepaction"]
> [Step 8: Deploy the device](azure-ad-join-deploy-device.md)

## Related content

[!INCLUDE [More information Autopilot profile](../includes/more-info-autopilot-profile.md)]
