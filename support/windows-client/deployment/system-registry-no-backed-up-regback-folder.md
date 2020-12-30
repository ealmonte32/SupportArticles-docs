---
title: The system registry is no longer backed up to the RegBack folder starting in Windows 10 version 1803
description: Starting in Windows 10, version 1803, Windows no longer automatically backs up the system registry to the RegBack folder. System restore points include registry information.
ms.date: 12/07/2020
author: Deland-Han
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-client
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Servicing
ms.technology: Deployment
---
# The system registry is no longer backed up to the RegBack folder starting in Windows 10 version 1803

This article discusses a by-design behavior where Windows no longer automatically backs up the system registry to the RegBack folder starting in Windows 10, version 1803.

_Original product version:_ &nbsp; Windows 10 - all editions  
_Original KB number:_ &nbsp; 4509719

## Summary

Starting in Windows 10, version 1803, Windows no longer automatically backs up the system registry to the RegBack folder. If you browse to the \\Windows\\System32\\config\\RegBack folder in Windows Explorer, you will still see each registry hive, but each file is 0 kb in size.

:::image type="content" source="./media/system-registry-no-backed-up-regback-folder/regisrtry-hive-0-kb.png" alt-text="Screenshot of 0kb-registry hive file.":::

## More information

This change is by design, and is intended to help reduce the overall disk footprint size of Windows. To recover a system with a corrupt registry hive, Microsoft recommends that you use a system restore point.

If you have to use the legacy backup behavior, you can re-enable it by configuring the following registry entry, and then restarting the computer:

- Path: `HKLM\System\CurrentControlSet\Control\Session Manager\Configuration Manager\EnablePeriodicBackup`
- Type: REG_DWORD
- Value: 1

Windows backs up the registry to the RegBack folder when the computer restarts, and creates a RegIdleBackup task to manage subsequent backups. Windows stores the task information in the Scheduled Task Library, in the Microsoft\\Windows\\Registry folder. The task has the following properties:

:::image type="content" source="./media/system-registry-no-backed-up-regback-folder/properties-of-regIdlebackup-task.png" alt-text="Screenshot of RegIdleBackup task properties.":::