---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie Microsoft Defender Advanced Threat Protection verwalten und überwachen können. Mit diesem neuen Dienst können Unternehmen auf komplexe Angriffe reagieren.
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cbf7dd3e35db8d2020e96e2511017e43863f724e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613461"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*Gilt für: Configuration Manager (Current Branch)*

Endpoint Protection kann Ihnen dabei helfen, [Microsoft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection), ehemals Windows Defender ATP, zu verwalten und zu überwachen. Microsoft Defender ATP unterstützt Unternehmen dabei, komplexe Angriffe auf ihre Netzwerke zu entdecken, zu untersuchen, und darauf zu reagieren. Configuration Manager-Richtlinien können Sie beim Onboarding und der Überwachung von Windows 10-Clients unterstützen.

Microsoft Defender ATP ist ein Dienst im [Microsoft Defender Security Center](https://securitycenter.windows.com). Durch Hinzufügen und Bereitstellen einer Client-Onboardingkonfigurationsdatei kann Configuration Manager den Bereitstellungsstatus und die Microsoft Defender ATP-Agent-Integrität überwachen. Microsoft Defender ATP wird auf PCs unterstützt, auf denen der Konfigurations-Manager-Client ausgeführt wird oder die [von Microsoft Intune verwaltet](https://docs.microsoft.com/intune/protect/advanced-threat-protection) werden.

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
- Windows Server 2016, Version 1803 oder höher
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>Onboarding von ATP mit Configuration Manager

Für unterschiedliche Betriebssysteme gibt es unterschiedliche Voraussetzungen für das Onboarding in ATP. Windows 8.1 und andere Geräte mit älteren Betriebssystemen benötigen für das Onboarding den **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID**. Geräte mit neueren Versionen, z. B. mit Windows Server 1803, benötigen die Onboardingkonfigurationsdatei. Configuration Manager installiert bei Bedarf zudem Microsoft Monitoring Agent (MMA) auf den Geräten, für die ein Onboarding durchgeführt wurde, aktualisiert den Agent jedoch nicht automatisch.

Zu den neueren Betriebssystemen zählen:
- Windows 10, Version 1607 und höher
- Windows Server 2016, Version 1803 oder höher
- Windows Server 2019

Zu den älteren Betriebssystemen zählen:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, Version 1709 und früher

Wenn Sie mit Configuration Manager in ATP ein Onboarding für Geräte durchführen, wird die ATP-Richtlinie in einer oder mehreren Zielsammlungen bereitgestellt. Manchmal enthält die Zielsammlung Geräte, auf denen eine beliebige Anzahl der unterstützten Betriebssysteme ausgeführt wird. Die Anweisungen für das Onboarding dieser Geräte variieren abhängig davon, ob Sie eine Sammlung mit Geräten verwenden, deren Betriebssysteme neuer, älter oder beides sind.

- Wenn die Zielsammlung Geräte mit neueren und älteren Betriebssystemen enthält, sollten Sie die Anweisungen unter [Onboarding von Geräten mit unterstützten Betriebssystemen (empfohlen)](#bkmk_any_os) befolgen.
- Wenn Ihre Sammlung nur neuere Geräte enthält, können Sie die [Anweisungen für das Onboarding neuerer Geräte](#bkmk_uplevel) befolgen.
- Wenn Ihre Sammlung nur ältere Geräte enthält, können Sie die [Anweisungen für das Onboarding älterer Geräte](#bkmk_downlevel) befolgen.

> [!Warning]
> - Wenn Ihre Zielsammlung neuere Geräte enthält und Sie die Anweisungen für ältere Geräte befolgen, erfolgt für die neueren Geräte kein Onboarding.
> - Wenn Ihre Zielsammlung ältere Geräte enthält und Sie die Anweisungen für neuere Geräte befolgen, erfolgt für die älteren Geräte kein Onboarding.

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a> Onboarding von Geräten mit unterstützten Betriebssystemen (empfohlen)
 Sie können mit jedem [unterstützten Betriebssystem](#bkmk_os) ein Onboarding für Geräte in ATP durchführen, indem Sie die Konfigurationsdatei, den **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID** in Configuration Manager bereitstellen.

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>Abrufen der Konfigurationsdatei, der Arbeitsbereich-ID und des Arbeitsbereichschlüssels

1. Wechseln Sie zum [Microsoft Defender ATP-Onlinedienst](https://securitycenter.windows.com/), und melden Sie sich an.
1. Klicken Sie auf **Einstellungen**, und wählen Sie dann **Onboarding** unter **Geräteverwaltung** aus.
1. Wählen Sie das Betriebssystem **Windows 10** aus.
1. Wählen Sie die Bereitstellungsmethode **Microsoft Endpoint Configuration Manager current branch and later** (Microsoft Endpoint Configuration Manager Current Branch und höher) aus.
1. Klicken Sie auf **Paket herunterladen**.
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="Download der Onboardingkonfigurationsdatei" lightbox="media/5229962-onboarding-configuration.png":::
1. Laden Sie die komprimierte Archiv-Datei (ZIP-Datei) herunter, und extrahieren Sie die Inhalte.
1. Klicken Sie auf **Einstellungen**, und wählen Sie dann **Onboarding** unter **Geräteverwaltung** aus.
1. Wählen Sie aus der Liste der Betriebssysteme **Windows 7 SP1 und 8.1** oder **Windows Server 2008 R2 SP1, 2012 R2 und 2016** aus.
   - Der **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID** bleiben unabhängig von Ihrer Auswahl gleich.
1. Kopieren Sie die Werte für den **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID** aus dem Abschnitt **Verbindung konfigurieren**.

   > [!IMPORTANT]
   > Die Microsoft Defender ATP-Konfigurationsdatei enthält vertrauliche Informationen, die gesichert werden sollten.


### <a name="onboard-the-devices"></a>Onboarding der Geräte

1. Navigieren Sie in der Configuration Manager-Konsole zu **Assets und Konformität** > **Endpoint Protection** > **Microsoft Defender ATP-Richtlinien**.
1. Klicken Sie auf **Microsoft Defender ATP-Richtlinie erstellen**, um den Assistenten für Microsoft Defender ATP-Richtlinien zu öffnen. 
1. Geben Sie den **Namen** und die **Beschreibung** für die Microsoft Defender ATP-Richtlinie ein, und wählen Sie **Onboarding** aus.
1. **Navigieren** Sie zur Konfigurationsdatei, die Sie aus der heruntergeladenen ZIP-Datei extrahiert haben.
1. Geben Sie den **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID** an, und klicken Sie auf **Weiter**.

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Assistent zum Erstellen von Microsoft Defender ATP-Richtlinien" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. Geben Sie die Dateibeispiele an, die von verwalteten Geräten gesammelt und für Analysezwecke freigegeben werden.  
   - **Keine**
   - **Alle Dateitypen**  
1. Überprüfen Sie die Zusammenfassung, und schließen Sie den Assistenten ab.  
1. Klicken Sie mit der rechten Maustaste auf die erstellte Richtlinie, und klicken Sie dann auf **Bereitstellen**, um die Microsoft Defender ATP-Richtlinie den Clients zuzuordnen.

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a> Onboarding von Geräten mit neueren Betriebssystemen in ATP

Bei neueren Clients muss das Onboarding in ATP mithilfe der Onboardingkonfigurationsdatei erfolgen. Zu den neueren Betriebssystemen zählen:
- Windows 10, Version 1607 und höher 
- Windows Server 2016, Version 1803 und höher
- Windows Server 2019

Wenn die Zielsammlung Geräte mit neueren und älteren Betriebssystemen enthält oder Sie nicht sicher sind, sollten Sie die Anweisungen zum [Onboarding von Geräten mit unterstützten Betriebssystemen (empfohlen)](#bkmk_any_os) befolgen.

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>Abrufen einer Onboardingkonfigurationsdatei für neuere Geräte

1. Wechseln Sie zum [Microsoft Defender ATP-Onlinedienst](https://securitycenter.windows.com/), und melden Sie sich an.
1. Klicken Sie auf **Einstellungen**, und wählen Sie dann **Onboarding** unter **Geräteverwaltung** aus.
1. Wählen Sie das Betriebssystem **Windows 10** aus.
1. Wählen Sie die Bereitstellungsmethode **Microsoft Endpoint Configuration Manager current branch and later** (Microsoft Endpoint Configuration Manager Current Branch und höher) aus.
1. Klicken Sie auf **Paket herunterladen**.
1. Laden Sie die komprimierte Archiv-Datei (ZIP-Datei) herunter, und extrahieren Sie die Inhalte.

> [!IMPORTANT]
> Die Microsoft Defender ATP-Konfigurationsdatei enthält vertrauliche Informationen, die gesichert werden sollten.


### <a name="onboard-the-up-level-devices"></a>Onboarding der neueren Geräte

1. Navigieren Sie in der Configuration Manager-Konsole zu **Assets und Konformität** > **Endpoint Protection** > **Microsoft Defender ATP-Richtlinien**, und klicken Sie auf **Microsoft Defender ATP-Richtlinie erstellen**. Dann wird der Assistent für Microsoft Defender ATP-Richtlinien geöffnet.  
1. Geben Sie den **Namen** und die **Beschreibung** für die Microsoft Defender ATP-Richtlinie ein, und wählen Sie **Onboarding** aus.
1. **Navigieren** Sie zur Konfigurationsdatei, die Sie aus der heruntergeladenen ZIP-Datei extrahiert haben.
   > [!Note]
   > Bei Configuration Manager 2002 benötigen Sie den **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID** auch dann, wenn Sie nur für neuere Geräte ein Onboarding durchführen. Sie erhalten diese Werte, indem Sie im [Microsoft Defender ATP-Onlinedienst](https://securitycenter.windows.com/) auf **Einstellungen** > **Onboarding** > **Windows 7 und 8.1** klicken. <!--7054188-->
1. Geben Sie die Dateibeispiele an, die von verwalteten Geräten gesammelt und für Analysezwecke freigegeben werden.  
   - **Keine**
   - **Alle Dateitypen**  
1. Überprüfen Sie die Zusammenfassung, und schließen Sie den Assistenten ab.  
1. Klicken Sie mit der rechten Maustaste auf die erstellte Richtlinie, und klicken Sie dann auf **Bereitstellen**, um die Microsoft Defender ATP-Richtlinie den Clients zuzuordnen.

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a> Onboarding von Geräten mit älteren Betriebssystemen in ATP

Bei älteren Clients sind der **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID** für das Onboarding in ATP erforderlich. Zu den älteren Betriebssystemen zählen:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, Version 1709 und früher

Wenn die Zielsammlung Geräte mit neueren und älteren Betriebssystemen enthält oder Sie nicht sicher sind, sollten Sie die Anweisungen zum [Onboarding von Geräten mit unterstützten Betriebssystemen (empfohlen)](#bkmk_any_os) befolgen.

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>Abrufen der Arbeitsbereich-ID und des Arbeitsbereichschlüssels für ältere Geräte

1. Wechseln Sie zum [Microsoft Defender ATP-Onlinedienst](https://securitycenter.windows.com/), und melden Sie sich an.
1. Klicken Sie auf **Einstellungen**, und wählen Sie dann **Onboarding** unter **Geräteverwaltung** aus.
1. Wählen Sie aus der Liste der Betriebssysteme **Windows 7 SP1 und 8.1** oder **Windows Server 2008 R2 SP1, 2012 R2 und 2016** aus.
   - Der **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID** bleiben unabhängig von Ihrer Auswahl gleich.
1. Kopieren Sie die Werte für den **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID** aus dem Abschnitt **Verbindung konfigurieren**.

### <a name="onboard-the-down-level-devices"></a>Onboarding der älteren Geräte

1. Navigieren Sie in der Configuration Manager-Konsole zu **Assets und Konformität** > **Endpoint Protection** > **Microsoft Defender ATP-Richtlinien**, und klicken Sie auf **Microsoft Defender ATP-Richtlinie erstellen**. Dann wird der Assistent für Microsoft Defender ATP-Richtlinien geöffnet.  
1. Geben Sie den **Namen** und die **Beschreibung** für die Microsoft Defender ATP-Richtlinie ein, und wählen Sie **Onboarding** aus.
1. Geben Sie den **Arbeitsbereichschlüssel** und die **Arbeitsbereich-ID** an.
   > [!Note]
   > - Bei Configuration Manager 2002 benötigen Sie die Konfigurationsdatei auch dann, wenn Sie nur für ältere Geräte ein Onboarding durchführen. Diese Werte finden Sie im [Microsoft Defender ATP-Onlinedienst](https://securitycenter.windows.com/) unter **Einstellungen** > **Onboarding** > **Windows 10**. <!--7054188--> 
   > - Die Microsoft Defender ATP-Konfigurationsdatei enthält vertrauliche Informationen, die gesichert werden sollten.
1. Geben Sie die Dateibeispiele an, die von verwalteten Geräten gesammelt und für Analysezwecke freigegeben werden.  
   - **Keine**
   - **Alle Dateitypen**  
1. Überprüfen Sie die Zusammenfassung, und schließen Sie den Assistenten ab.  
1. Klicken Sie mit der rechten Maustaste auf die erstellte Richtlinie, und klicken Sie dann auf **Bereitstellen**, um die Microsoft Defender ATP-Richtlinie den Clients zuzuordnen.


## <a name="monitor"></a>Überwachen

1. Navigieren Sie in der Configuration Manager-Konsole zu **Überwachung** > **Sicherheit**, und klicken Sie dann auf **Microsoft Defender ATP**.  

1. Überprüfen Sie das Microsoft Defender Advanced Threat Protection-Dashboard.  

    - **Onboardingstatus des Microsoft Defender ATP-Agents**: Anzahl und Prozentsatz der geeigneten verwalteten Clientcomputer mit integrierter und aktivierter Microsoft Defender ATP-Richtlinie  

    - **Integrität des Microsoft Defender ATP-Agents**: Prozentsatz von Computerclients, die den Status ihres Microsoft Defender-ATP-Agents melden  

        - **Integriert** – Funktioniert ordnungsgemäß  

        - **Inaktiv** – In dem Zeitraum wurden keine Daten an den Dienst gesendet  

        - **Agent-Status** – Der Systemdienst für den Agent in Windows wird nicht ausgeführt.  

        - **Nicht integriert** – Die Richtlinie wurde angewendet, aber der Agent hat die Richtlinienintegration nicht gemeldet.  

## <a name="create-an-offboarding-configuration-file"></a>Erstellen einer Konfigurationsdatei für das Offboarding  

1. Melden Sie sich beim [Microsoft Defender ATP-Onlinedienst](https://securitycenter.windows.com/) an.
1. Klicken Sie auf **Einstellungen**, und wählen Sie dann **Offboarding** unter **Geräteverwaltung** aus.
1. Wählen Sie **Windows 10** als Betriebssystem und **Microsoft Endpoint Configuration Manager current branch and later** (Microsoft Endpoint Configuration Manager Current Branch und höher) als Bereitstellungsmethode aus.
   - Mit der Option **Windows 10** wird sichergestellt, dass für alle Geräte in der Sammlung ein Offboarding durchgeführt und MMA bei Bedarf deinstalliert wird.
1. Laden Sie die komprimierte Archiv-Datei (ZIP-Datei) herunter, und extrahieren Sie die Inhalte. Offboardingdateien sind 30 Tage lang gültig.

1. Navigieren Sie in der Configuration Manager-Konsole zu **Assets und Konformität** > **Endpoint Protection** > **Microsoft Defender ATP-Richtlinien**, und klicken Sie auf **Microsoft Defender ATP-Richtlinie erstellen**. Dann wird der Assistent für Microsoft Defender ATP-Richtlinien geöffnet.  

1. Geben Sie den **Namen** und die **Beschreibung** für die Microsoft Defender ATP-Richtlinie ein, und wählen Sie **Offboarding** aus.

1. **Navigieren** Sie zur Konfigurationsdatei, die Sie aus der heruntergeladenen ZIP-Datei extrahiert haben.

1. Überprüfen Sie die Zusammenfassung, und schließen Sie den Assistenten ab.  

Klicken Sie auf **Bereitstellen**, um die Microsoft Defender ATP-Richtlinie für die Clients bereitzustellen.  

> [!IMPORTANT]
> Die Microsoft Defender ATP-Konfigurationsdateien enthalten vertrauliche Informationen, die gesichert werden sollten.

## <a name="next-steps"></a>Nächste Schritte

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Beheben von Onboardingproblemen mit Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
