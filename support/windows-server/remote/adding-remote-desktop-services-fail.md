---
title: Adding Remote Desktop Services role fails
description: Helps solve an issue where adding Remote Desktop Services role fails when Firewall Service is stopped.
ms.date: 09/08/2020
author: delhan
ms.author: Delead-Han
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Administration
ms.technology: RDS
---
# Adding Remote Desktop Services role may fail when Firewall Service is stopped in Windows Server 2012

This article provides help to solve an issue where adding Remote Desktop Services role fails when Firewall Service is stopped.

_Original product version:_ &nbsp; Windows Server 2012 R2  
_Original KB number:_ &nbsp; 2802436

## Symptoms

On a computer that is running Windows Server 2012, when you try to install the Remote Desktop Services role, using the "Add Roles and Features" Wizard, the installation may fail. Additionally, during the installation process you may receive one of the following error messages:

Unable to open remote connections on the RD Connection Broker server

The post installation configuration did not complete.

> [!NOTE]
> After a reboot the RDS Server may work. If it does not, the following powershell commands will complete the failed action:

$tss = Get-WmiObject -namespace root\cimv2\terminalservices -class Win32_TerminalServiceSetting
 $tss.SetAllowTSConnections(1,0)

## Cause

During the post installation configuration, the wizard attempts to enable necessary firewall exceptions for the RDS Role. When the firewall service is stopped, this operation fails and is reported with the above error.

## Resolution

It is not recommended to run without a Firewall. If you have certain requirements to do so, enable the Firewall Service at least during installation of this Role.