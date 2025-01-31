---
# required metadata

title: Find the primary user of a Microsoft Intune device.
titleSuffix:
description: Find the primary user (or User Device Affinity) of an Intune device.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Find the primary user of an Intune device

Primary User, also known as User Device Affinity, is a property of each Intune device. 
An Intune device can have zero or one primary user assigned to it. When there's no Primary User assigned, the device is referred to as a "Shared Device".

## How to find a device's primary user

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. Choose **Devices** > choose a device.
3. On the **Overview** page, choose **See more** and you'll see the primary user listed.

## What is the primary user?
The primary user property is used to map a licensed Intune user to their devices in:
- The Company Portal app
- End-user website
- IT pro experiences, like troubleshooting pages in the Azure portal. These pages map user accounts to devices by using the primary user.    

### Company Portal app
The Company Portal app expects that the user account that signed in to the Company Portal is the primary user of that device. If another user has been assigned as the primary user, the Company Portal shows a warning:

“This device is already assigned to someone in your organization. Contact company support about becoming the primary device user. You can continue to use Company Portal but functionality will be limited.”

If an Intune device has no primary user assigned, then the Company Portal app detects it as a shared device. Shared devices are visually identifiable with a “shared” label appearing on the device tile. In this mode, the Company Portal can still be used to request and install available apps. However, self-service actions (reset/rename/retire) aren't available.  

To appear in the Company Portal on shared devices, available apps must be assigned to a user group. They'll be installed in the system context or user context, depending on how the app was configured by the IT administrator. For more information about app context, see [Installing apps on Windows 10 devices](apps-windows-10-app-deploy.md#installing-apps-on-windows-10-devices). Company Portal version 10.3.4651.0 or later is required to use this feature.


## Who is assigned as the primary user?
Intune automatically adds primary user to devices during or soon after enrollment. The enrollment method determines when the primary user is added to a device.

| Platform | Enrollment method | Primary user assigned | Primary user is assigned |
| ---- | ---- | ---- | ---- |
| Windows | Add work or school (user driven) | Enrolling user | During enrollment |   
| Windows | Modern App sign-in (user driven) | Enrolling user | During enrollment | 
| Windows | Enroll in MDM only (user driven) | Enrolling user | During enrollment | 
| Windows | Azure AD join (out of box experience) | Enrolling user | During enrollment | 
| Windows | Azure AD join (Autopilot out of box experience) | Enrolling user | During enrollment | 
| Windows | Enroll in MDM only | Enrolling user | During enrollment | 
| Windows | Hybrid AADJ + automatic enrollment GPO | First user to sign in | When first user signs in | 
| Windows | Co-management | First user to sign in | When first user signs in | 
| Windows | Azure AD join (bulk enrollment token) | None | Not applicable | 
| Windows | Azure AD join (Autopilot self-deploying mode) | None | Not applicable | 
| Cross-platform | User driven enrollment with Company Portal App | Enrolling user | During enrollment |
| Cross-platform | Device Enrollment Manager (DEM) | Enrolling DEM user | During enrollment |
| iOS, macOS | Apple Automated Device Enrollment (DEP with User Affinity | Enrolling user | During enrollment |
| iOS, macOS | Apple Automated Device Enrollment (DEP without User Affinity) | None | Not applicable |
| Android | Android Corporate-Owned, Dedicated devices | None | Not applicable |

## Primary user and Azure AD device owner
In some cases, the Intune primary user may be different from the Azure AD Device’s **Owner** property (viewable under **Devices** > **Azure AD Devices**). The Azure AD Device owner is added during a device’s registration into Azure Active Directory.

## Next steps
[Manage your Intune devices.](device-management.md)
