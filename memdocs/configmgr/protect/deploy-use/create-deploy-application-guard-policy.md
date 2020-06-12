---
title: Verwalten von Application Guard-Richtlinien
titleSuffix: Configuration Manager
description: Informationen zum Erstellen und Bereitstellen einer Microsoft Defender Application Guard-Richtlinie
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1189f8c89215bc228c533a88f38f5ae59b6855ee
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84454935"
---
# <a name="create-and-deploy-microsoft-defender-application-guard-policy"></a>Erstellen und Bereitstellen einer Microsoft Defender Application Guard-Richtlinie

*Gilt für: Configuration Manager (Current Branch)*
<!-- 1351960 -->  
Sie können [Microsoft Defender Application Guard (Application Guard)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)-Richtlinien erstellen und bereitstellen, indem Sie den Configuration Manager-Endpunktschutz verwenden. Diese Richtlinien dienen zum Schutz Ihrer Benutzer, indem nicht vertrauenswürdige Websites in einem sicheren isolierten Container geöffnet werden, auf den andere Teile des Betriebssystems keinen Zugriff haben.

## <a name="prerequisites"></a>Voraussetzungen

Wenn Sie eine Microsoft Defender Application Guard-Richtlinie erstellen möchten, müssen Sie das Windows 10 Fall Creators Update (1709) verwenden. Die Windows 10-Geräte, auf denen Sie die Richtlinie bereitstellen, müssen mit einer [Netzwerkisolationsrichtlinie](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard#network-isolation-settings) konfiguriert werden. Weitere Informationen finden Sie in der [Übersicht über Microsoft Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Erstellen einer Richtlinie und Durchsuchen der verfügbaren Einstellungen

1. Wählen Sie in der Configuration Manager-Konsole **Assets und Konformität** aus.
2. Wählen Sie im Arbeitsbereich **Assets und Konformität** nacheinander **Übersicht** > **Endpoint Protection** > **Windows Defender Application Guard** aus.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Windows Defender Application Guard-Richtlinie erstellen**.
4. Sie können die verfügbaren Einstellungen mithilfe des [Referenzartikels](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard) durchsuchen und konfigurieren. Mit Configuration Manager können Sie bestimmte Richtlinieneinstellungen festlegen:
   - [Einstellungen für die Hostinginteraktion](#bkmk_HIS)
   - [Anwendungsverhalten](#bkmk_ABS)
   - [Dateiverwaltung](#bkmk_FM)
5. Geben Sie auf der Seite **Netzwerkdefinition** die Unternehmensidentität an, und definieren Sie die Grenze Ihres Unternehmensnetzwerks.

    > [!NOTE]
    > PCs unter Windows 10 speichern nur eine Netzwerkisolationsliste auf dem Client. Sie können zwei verschiedene Arten von Netzwerkisolationslisten erstellen und diese auf dem Client bereitstellen:
    >
    >  - eine aus Windows Information Protection
    >  - eine aus Microsoft Defender Application Guard
    >
    > Wenn Sie beide Richtlinien bereitstellen, müssen diese Netzwerkisolationlisten übereinstimmen. Wenn Sie Listen bereitstellen, die nicht mit dem gleichen Client übereinstimmen, schlägt die Bereitstellung fehl. Weitere Informationen finden Sie in der [Dokumentation zu Windows Information Protection](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Schließen Sie den Assistenten ab, und stellen Sie die Richtlinie auf Windows 10-Geräten bereit, die Version 1709 verwenden.

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a> Einstellungen für die Hostinginteraktion

Mit diesen werden Interaktionen zwischen Hostgeräten und dem Application Guard-Container konfiguriert. Vor Version 1802 von Configuration Manager befanden sich die Einstellungen für das Anwendungsverhalten und die Hostinginteraktion auf der Registerkarte **Einstellungen**.

- **Zwischenablage:** Vor Version 1802 von Configuration Manager befand sich diese Einstellung unter „Einstellungen“.
  - Zulässiger Inhaltstyp:
    - Text
    - Bilder
- **Druckausgabe läuft:**
  - Drucken in XPS aktivieren
  - Drucken in PDF aktivieren
  - Drucken auf lokalen Netzwerkdruckern aktivieren
  - Enable printing to network printers (Drucken auf Netzwerkdruckern aktivieren)
- **Grafiken:** (ab Configuration Manager Version 1802)
  - Virtual graphics processor access (Zugriff auf virtuellen Grafikprozessor)
- **Dateien:** (ab Configuration Manager Version 1802)
  - Save downloaded files to host (Heruntergeladene Dateien auf Host speichern)

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a> Einstellungen für Anwendungsverhalten

Mit diesen wird das Anwendungsverhalten innerhalb der Application Guard-Sitzung konfiguriert. Vor Version 1802 von Configuration Manager befanden sich die Einstellungen für das Anwendungsverhalten und die Hostinginteraktion auf der Registerkarte **Einstellungen**.

- **Inhalt:**
  - Laden unternehmensfremder Inhalte wie z.B. Drittanbieter-Plug-Ins zulassen
- **Andere:**
  - Vom Benutzer generierte Browserdaten beibehalten
  - Sicherheitsereignisse in der isolierten Application Guard-Sitzung überwachen

### <a name="file-management"></a><a name="bkmk_FM"></a> Dateiverwaltung
<!--3555858-->
Ab Configuration Manager Version 1906 gibt es eine Richtlinieneinstellung, die es Benutzern ermöglicht, Dateien zu vertrauen, die normalerweise im Application Guard geöffnet werden. Nach erfolgreicher Durchführung werden die Dateien auf dem Hostgerät und nicht in Application Guard geöffnet. Weitere Informationen zu den Application Guard-Richtlinien finden Sie unter [Konfigurieren der Richtlinieneinstellungen für Microsoft Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard).

- **Benutzern das Vertrauen in Dateien ermöglichen, die in Windows Defender Application Guard geöffnet werden**: Ermöglichen Sie dem Benutzer, Dateien als vertrauenswürdig zu markieren. Wenn eine Datei vertrauenswürdig ist, wird Sie nicht in Application Guard, sondern auf dem Host geöffnet. Gilt für Clients mit Windows 10, Version 1809 oder höher.
  - **Prohibited** (Nicht zulässig): Erlauben Sie Benutzern nicht, Dateien als vertrauenswürdig zu markieren (Standard).
  - **File checked by antivirus** (Datei von Antivirusprogramm geprüft): Erlauben Sie Benutzern, Dateien nach einer Virenprüfung als vertrauenswürdig zu markieren.
  - **All files** (Alle Dateien): Erlauben Sie Benutzern, alle Dateien als vertrauenswürdig zu markieren.

Wenn Sie die Dateiverwaltung aktivieren, werden möglicherweise Fehler angezeigt, die in der Datei „DCMReporting.log“ des Clients protokolliert werden. Die folgenden Fehler wirken sich in der Regel nicht auf die Funktionalität aus: <!--4619457-->

- Auf kompatiblen Geräten:
  - FileTrustCriteria_condition nicht gefunden
- Auf nicht kompatiblen Geräten:
  - FileTrustCriteria_condition nicht gefunden
  - FileTrustCriteria_condition nicht in der Zuordnung gefunden
  - FileTrustCriteria_condition nicht im Hash gefunden

Um die Einstellungen von Application Guard zu bearbeiten, erweitern Sie **Endpoint Protection** im Arbeitsbereich **Bestand und Kompatibilität**, und klicken Sie dann auf den Knoten **Windows Defender Application Guard**. Klicken Sie mit der rechten Maustaste auf die Richtlinie, die Sie bearbeiten möchten, und wählen Sie dann **Eigenschaften** aus.

## <a name="known-issues"></a>Bekannte Probleme

Bei Geräten unter Windows 10 Version 2004 werden Fehler bei der Konformitätsberichterstattung für Kriterien für die Vertrauenswürdigkeit von Dateien für Microsoft Defender Application Guard angezeigt. Dieses Problem tritt auf, da einige Unterklassen aus der WMI-Klasse `MDM_WindowsDefenderApplicationGuard_Settings01` in Windows 10 Version 2004 entfernt wurden. Alle anderen Microsoft Defender Application Guard-Einstellungen sind noch gültig, es treten nur Fehler bei den Kriterien für die Vertrauenswürdigkeit von Dateien auf. Aktuell gibt es keine Problemumgehungen für diesen Fehler. <!--7099444,5946790-->

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen über Microsoft Defender Application Guard finden Sie in folgenden Artikeln:
 - [Übersicht über Microsoft Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)
- [Häufig gestellte Fragen zu Microsoft Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/faq-md-app-guard)
