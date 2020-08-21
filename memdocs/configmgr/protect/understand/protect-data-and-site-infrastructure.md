---
title: Schützen der Daten und Standortinfrastruktur
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Ressourcen Ihrer Organisation mit Configuration Manager vor Risiken oder böswilligen Angriffen schützen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2a73fff7fd2eb5d630d6047a7da6f131188f06c5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693487"
---
# <a name="protect-data-and-site-infrastructure"></a>Schützen der Daten und Standortinfrastruktur

*Gilt für: Configuration Manager (Current Branch)*

Sie möchten, dass Ihre Benutzer sicher auf die Ressourcen Ihrer Organisation zugreifen können. Schützen Sie sowohl Ihre Infrastruktur als auch Ihre Daten vor der Offenlegung oder böswilligen Angriffen. Verwenden Sie Configuration Manager, um den Zugriff zu aktivieren und die Ressourcen Ihres Unternehmens zu schützen.  

- Mit [Endpoint Protection](../deploy-use/endpoint-protection.md) können Sie die folgenden Microsoft Defender-Richtlinien für Clientcomputer verwalten:

  - Microsoft Defender-Antischadsoftware
  - Microsoft Defender Firewall
  - Microsoft Defender Advanced Threat Protection
  - Microsoft Defender Exploit Guard
  - Microsoft Defender Application Guard
  - Microsoft Defender Application Control

  > [!TIP]
  > Stellen Sie die [**Endpoint Protection**-Workload](../../comanage/workloads.md#endpoint-protection) auf Intune um, damit Sie Endpoint Protection auf gemeinsam verwalteten Windows 10-Geräten mit dem Clouddienst von Microsoft Endpoint Manager verwalten können. Weitere Informationen finden Sie unter [Endpoint Protection für Microsoft Intune](/intune/endpoint-protection-windows-10).

- Schützen Sie Daten, die auf lokalen Windows-Clients mit BitLocker-Laufwerkverschlüsselung (BitLocker Drive Encryption, BDE) gespeichert sind. Configuration Manager bietet eine vollständige BitLocker-Lebenszyklusverwaltung, die die Verwendung von Microsoft BitLocker-Verwaltung und -Überwachung (Microsoft BitLocker Administration and Monitoring, MBAM) ersetzen kann. Weitere Informationen finden Sie unter [Planen der BitLocker-Verwaltung](../plan-design/bitlocker-management.md).

- Aktivieren Sie anstelle von herkömmlichen Kennwörtern mithilfe von Windows Hello for Business alternative Anmeldemethoden auf Windows 10-Geräten. Weitere Informationen finden Sie unter [Configure Windows Hello for Business settings (So konfigurieren Sie Windows Hello for Business-Einstellungen)](../deploy-use/windows-hello-for-business-settings.md).

- Minimieren Sie den Aufwand Ihrer Benutzer zum Herstellen einer Verbindung mit Ressourcen, indem Sie VPN-Verbindungen mithilfe von VPN-Profilen aktivieren. Weitere Informationen finden Sie unter [VPN-Profile](../deploy-use/vpn-profiles.md).  

- WLAN-Profile stellen eine Reihe von Tools und Ressourcen bereit, die Sie bei der Verwaltung von Einstellungen für drahtlose Netzwerke auf Geräten in Ihrer Organisation unterstützen. Durch Bereitstellen dieser Einstellungen erleichtern Sie den Endbenutzern das Herstellen einer Verbindung mit Drahtlosnetzwerken. Weitere Informationen finden Sie unter [Erstellen von WLAN-Profilen](../deploy-use/create-wifi-profiles.md).  

- Stellen Sie Geräten die Zertifikate bereit, die Benutzer zum Herstellen einer Verbindung mit Ressourcen benötigen. Weitere Informationen finden Sie unter [Zertifikatprofile](../deploy-use/introduction-to-certificate-profiles.md).