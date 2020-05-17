---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie Microsoft Defender Advanced Threat Protection verwalten und überwachen können. Mit diesem neuen Dienst können Unternehmen auf komplexe Angriffe reagieren.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801aee9665e567ce1a983fba294f1e58f58eee04
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406662"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*Gilt für: Configuration Manager (Current Branch)*

Endpoint Protection kann Ihnen dabei helfen, [Microsoft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection), ehemals Windows Defender ATP, zu verwalten und zu überwachen. Microsoft Defender ATP unterstützt Unternehmen dabei, komplexe Angriffe auf ihre Netzwerke zu entdecken, zu untersuchen, und darauf zu reagieren. Configuration Manager-Richtlinien können Sie beim Onboarding und der Überwachung von Windows 10-Clients unterstützen.

Microsoft Defender ATP ist ein Dienst im [Windows Defender Security Center](https://securitycenter.windows.com). Durch Hinzufügen und Bereitstellen einer Client-Onboardingkonfigurationsdatei kann Configuration Manager den Bereitstellungsstatus und die Microsoft Defender ATP-Agent-Integrität überwachen. Microsoft Defender ATP wird auf PCs unterstützt, auf denen der Konfigurations-Manager-Client ausgeführt wird oder die [von Microsoft Intune verwaltet](https://docs.microsoft.com/intune/protect/advanced-threat-protection) werden.

## <a name="prerequisites"></a>Voraussetzungen

- Abonnement für den Microsoft Defender Advanced Threat Protection-Onlinedienst  
- Clientcomputer, auf denen der Konfigurations-Manager-Client ausgeführt wird
- Clients, die ein Betriebssystem verwenden, das im Abschnitt [Unterstützte Clientbetriebssysteme](#bkmk_os) aufgeführt ist.

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a> Unterstützte Clientbetriebssysteme
Je nach der Version von Configuration Manager, die ausgeführt wird, ist ein Onboarding der folgenden Clientbetriebssysteme möglich:

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager, Version 1910 und früher

- Clientcomputer unter Windows 10, Version 1607 und höher

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager, Version 2002 und höher
<!--5229962-->
Ab der Version 2002 von Configuration Manager können Sie die folgenden Betriebssysteme einbinden:

- Windows 8.1
- Windows 10, Version 1607 oder höher
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, Version 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>Erstellen einer Konfigurationsdatei für das Onboarding

1. Wechseln Sie zum [Microsoft Defender ATP-Onlinedienst](https://securitycenter.windows.com/), und melden Sie sich an.
1. Wählen Sie unter **Einstellungen** die Option **Computerverwaltung** aus, und klicken Sie dann auf **Onboarding**.
1. Wählen Sie in der Liste die Betriebssysteme aus, für die Sie das Onboarding durchführen möchten.
   - Wenn Sie ein Onboarding von Windows 10, Windows Server 1803 und Windows Server 2019 durchführen:
      1. Wählen Sie **Configuration Manager (Current Branch) Version 1606** aus, und klicken Sie auf **Paket herunterladen**.
      1. Laden Sie die komprimierte Archiv-Datei (ZIP-Datei) herunter, und extrahieren Sie die Inhalte.
   - Beim Onboarding eines anderen Windows-Betriebssystems:
      1. Wählen Sie die Betriebssysteme für das Onboarding aus der Liste aus, die im Microsoft Defender ATP-Onlinedienst angezeigt wird.
      1. Kopieren Sie die Werte für den **Arbeitsbereichsschlüssel** und die **Arbeitsbereichs-ID** aus dem Abschnitt **Verbindung konfigurieren**, sobald der Prozess abgeschlossen ist.

> [!IMPORTANT]
> - Die Microsoft Defender ATP-Konfigurationsdatei enthält vertrauliche Informationen, die gesichert werden sollten.

## <a name="onboard-devices"></a>Integrieren von Geräten

1. Wechseln Sie in der Configuration Manager-Konsole zu **Assets und Konformität** > **Endpoint Protection** > **Windows Defender ATP-Richtlinien**, und klicken Sie auf **Windows Defender ATP-Richtlinie erstellen**. Dann wird der Assistent für Microsoft Defender ATP-Richtlinien geöffnet.  
1. Geben Sie den **Namen** und die **Beschreibung** für die Microsoft Defender ATP-Richtlinie ein, und wählen Sie **Onboarding** aus.
1. **Wechseln** Sie zu der Konfigurationsdatei, die vom Microsoft Defender ATP-Clouddienstmandanten Ihrer Organisation bereitgestellt wurde.
   - Geben Sie für Windows 8.1 oder Windows Server 2012 R2 und 2016 den **Arbeitsbereichsschlüssel** und die **Arbeitsbereichs-ID** an.
   - Bei der Configuration Manager-Version 2002 benötigen Sie den **Arbeitsbereichsschlüssel** und die **Arbeitsbereichs-ID** auch, wenn Sie nur Geräte mit Windows Server 2019 und Windows Server 1803 oder höher integrieren. Sie erhalten diese Werte, indem Sie im [Microsoft Defender ATP-Onlinedienst](https://securitycenter.windows.com/) auf **Einstellungen** > **Onboarding** > **Windows 7 und 8.1** klicken. <!--7054188-->
1. Geben Sie die Dateibeispiele an, die von verwalteten Geräten gesammelt und für Analysezwecke freigegeben werden.  

   - **Keine**

   - **Alle Dateitypen**  
1. Überprüfen Sie die Zusammenfassung, und schließen Sie den Assistenten ab.  

Klicken Sie auf **Bereitstellen**, um die Microsoft Defender ATP-Richtlinie für die Clients bereitzustellen.

## <a name="monitor"></a>Überwachen

1. Navigieren Sie in der Configuration Manager-Konsole zu **Überwachung** > **Sicherheit**, und klicken Sie dann auf **Windows Defender ATP**.  

1. Überprüfen Sie das Microsoft Defender Advanced Threat Protection-Dashboard.  

    - **Windows Defender Agent Deployment Status** (Bereitstellungsstatus des Windows Defender-Agents): Anzahl und Prozentsatz der geeigneten verwalteten Clientcomputer mit integrierter und aktivierter Microsoft Defender ATP-Richtlinie  

    - **Integrität von Windows Defender ATP-Agent**: Prozentsatz von Computerclients, die den Status ihres Microsoft Defender-ATP-Agents melden  

        - **Integriert** – Funktioniert ordnungsgemäß  

        - **Inaktiv** – In dem Zeitraum wurden keine Daten an den Dienst gesendet  

        - **Agent-Status** – Der Systemdienst für den Agent in Windows wird nicht ausgeführt.  

        - **Nicht integriert** – Die Richtlinie wurde angewendet, aber der Agent hat die Richtlinienintegration nicht gemeldet.  

## <a name="create-an-offboarding-configuration-file"></a>Erstellen einer Konfigurationsdatei für das Offboarding  

1. Melden Sie sich beim [Microsoft Defender ATP-Onlinedienst](https://securitycenter.windows.com/) an.

1. Wählen Sie unter **Einstellungen** die Option **Computerverwaltung** aus, und klicken Sie dann auf **Onboarding**.  

1. Wählen Sie **Configuration Manager (Current Branch) Version 1606** aus, und klicken Sie auf **Endpoint offboarding** (Endpunktoffboarding).  

1. Laden Sie die komprimierte Archiv-Datei (ZIP-Datei) herunter, und extrahieren Sie die Inhalte. Offboardingdateien sind 30 Tage lang gültig.

1. Wechseln Sie in der Configuration Manager-Konsole zu **Assets und Konformität** > **Endpoint Protection** > **Windows Defender ATP-Richtlinien**, und klicken Sie auf **Windows Defender ATP-Richtlinie erstellen**. Dann wird der Assistent für Microsoft Defender ATP-Richtlinien geöffnet.  

1. Geben Sie den **Namen** und die **Beschreibung** für die Microsoft Defender ATP-Richtlinie ein, und wählen Sie **Offboarding** aus.

1. **Wechseln** Sie zu der Konfigurationsdatei, die vom Microsoft Defender ATP-Clouddienstmandanten Ihrer Organisation bereitgestellt wurde.

1. Überprüfen Sie die Zusammenfassung, und schließen Sie den Assistenten ab.  

Klicken Sie auf **Bereitstellen**, um die Microsoft Defender ATP-Richtlinie für die Clients bereitzustellen.  

> [!IMPORTANT]
> Die Microsoft Defender ATP-Konfigurationsdateien enthalten vertrauliche Informationen, die gesichert werden sollten.

## <a name="next-steps"></a>Nächste Schritte

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Beheben von Onboardingproblemen mit Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
