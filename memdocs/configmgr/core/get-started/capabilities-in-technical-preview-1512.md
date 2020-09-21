---
title: Funktionen in Technical Preview 1512
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1512 zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3e618a8a0db81ad870c5aeedc89b01ba6089a0f8
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607927"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Funktionen in der Technical Preview 1512 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1512 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.  

 Im Folgenden werden neue Funktionen aufgelistet, die Sie mit dieser Version ausprobieren können.  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a> Nachweis der Geräteintegrität  
 Ab Technical Preview 1512 können Administratoren den Status des Windows 10-Nachweises zur Geräteintegrität in der Configuration Manager-Konsole anzeigen.  Diese Funktion steht für Configuration Manager und Configuration Manager mit Microsoft Intune zur Verfügung. Mit dem Nachweis der Geräteintegrität kann der Administrator sicherstellen, dass Clientcomputer über vertrauenswürdige BIOS-, TPM- und Bootsoftwarekonfigurationen verfügen. Damit Sie den Nachweis der Geräteintegration unterstützen, müssen die Clientgeräte Windows 10 mit aktiviertem TPM 2 ausführen. Der Nachweis der Geräteintegrität zeigt die Anzahl der Geräte an, die jeweils für Folgendes aktiviert sind:  

-   Antischadsoftware-Frühstart  

-   BitLocker  

-   Sicherer Start  

-   Codeintegrität  

Die Konsole zeigt außerdem die wichtigsten fehlenden Einstellungen für den Integrationsnachweis mit der Anzahl der Geräte an.  

Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, klicken Sie auf den Knoten **Sicherheit** und anschließend auf **Integritätsnachweis**, um eine Vorschau des Nachweises der Geräteintegrität anzuzeigen.  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a> Überwachung in der Konsole hinsichtlich der Geschäftsbedingungen  
Ab Technical Preview 1512 können Sie beim Integrieren von Configuration Manager in Microsoft Intune die Configuration Manager-Konsole verwenden, um anzuzeigen, welche Benutzer die von der IT-Abteilung konfigurierten Geschäftsbedingungen akzeptiert haben und welche nicht.  

**So zeigen Sie eine Zusammenfassung an:**  

-   Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Bereitstellungen**, und wählen Sie die Bereitstellung der Geschäftsbedingungen aus, die Sie anzeigen möchten.  

**So zeigen Sie ausführliche Informationen an:**  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Kompatibilitätseinstellungen** > **Geschäftsbedingungen**, und wählen Sie dann die anzuzeigenden Geschäftsbedingungen aus.  

2.  Wählen Sie unten in der Konsole die Registerkarte **Bereitstellungen** und dann die Bereitstellung aus, und klicken Sie anschließend auf **Status anzeigen**.  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a> Verbesserungen an den Richtlinieneinstellungen für Endpoint Protection  
In der Technical Preview 1512 haben wir die folgenden neuen Einstellungen zur Endpoint Protection-Richtlinie für Antischadsoftware hinzugefügt:  

-   Echtzeitschutz: **Potenziell unerwünschte Programme beim Herunterladen und vor der Installation blockieren**  

    -   Potenziell unerwünschte Programme (Potential Unwanted Applications, PUA) stellen eine Klassifizierung der Bedrohung auf Basis des Ansehens und der forschungsorientierten Identifizierung dar. In den meisten Fällen handelt es sich um unerwünschte Programmbundler oder um ihre gebündelten Programme.  

    -   Die Einstellung für die Schutzrichtlinie ist standardmäßig aktiviert (auf „Ja“ festgelegt). Wenn sie aktiviert ist, blockiert diese Einstellung das Herunterladen und Installieren von potenziell unerwünschten Programmen. Sie können jedoch bestimmte Dateien oder Ordner auf die spezifischen Anforderungen Ihrer Umgebung ausschließen.  

-   Überprüfungseinstellungen: **Bei Ausführung einer vollständigen Überprüfung zugeordnete Netzlaufwerke überprüfen**  

    -   Diese Einstellung bietet dem Administrator eine höhere Genauigkeit, um bedarfsgesteuerte Überprüfungen von Netzwerkdateien ohne das Risiko zu gestatten, dass während einer vollständigen Überprüfung immer zugeordnete Netzlaufwerke überprüft werden.  

    -   Die Einstellung **Scannen von Netzwerkdateien** muss zunächst aktiviert werden („Ja“), damit diese Einstellung konfiguriert werden kann.  

    -   Standardmäßig ist diese Einstellung auf „Nein“ festgelegt und bedeutet somit, dass bei einer vollständigen Überprüfung nicht auf zugeordnete Netzlaufwerke zugegriffen wird.  

-   Einstellungen für automatische Übermittlung von Beispieldateien:  

     Die Engine für Antischadsoftware kann das Senden von Dateibeispielen an Microsoft anfordern, damit diese eingehender analysiert werden. Standardmäßig erfolgt immer eine Aufforderung, bevor diese Beispiele gesendet werden. Administratoren können jetzt die folgenden Einstellungen verwalten, um dieses Verhalten zu konfigurieren:  

    -   Erweitert: **Automatische Beispieldateiübermittlung aktivieren, um Microsoft bei der Erkennung von schädlichen Elementen zu unterstützen:**  Legen Sie diese Einstellung auf „Ja“ fest, um die automatische Beispieldateiübermittlung zu aktivieren. Standardmäßig ist diese Einstellung auf „Nein“ festgelegt. Somit ist die automatische Beispieldateiübermittlung deaktiviert, und Benutzer werden vor dem Senden von Beispielen entsprechend aufgefordert.   (Diese Einstellung wurde erstmals in System Center 2012 R2 Configuration Manager SP1 eingeführt.)  

    -   Erweitert: **Benutzern das Ändern der Einstellungen für die automatische Beispieldateiübermittlung erlauben:** Diese Einstellung bestimmt, ob ein Benutzer mit lokalen Administratorrechten auf einem Gerät die Einstellung für die automatische Übermittlung der Beispieldatei über die Clientbenutzeroberfläche ändern kann. Diese Einstellung ist standardmäßig auf „Nein“ festgelegt, d.h. die Einstellungen können nur in der Configuration Manager-Konsole geändert werden, und lokale Administratoren auf einem Gerät können diese Konfiguration nicht ändern.  

         Folgendes zeigt z. B. die vom Administrator festgelegte Windows Defender-Einstellung in Windows 10 als aktiviert an, und dem Benutzer ist es nicht gestattet, diese zu ändern:  

         ![Windows Defender – Automatische Beispielübermittlung](../../core/get-started/media/TechRef_WinDefender.png)  

    Darüber hinaus wird die vorhandene Einstellung **Dateien und Ordner ausschließen** im Abschnitt „Ausschlusseinstellungen“ der Endpoint Protection-Richtlinie für Antischadsoftware verbessert, um den Ausschluss von Geräten zuzulassen. Sie können jetzt z.B. Folgendes als Ausschluss angeben: **\device\mvfs** (für Dateisysteme mit mehreren Versionen). Die Richtlinie überprüft nicht den Gerätepfad. Die Endpoint Protection-Richtlinie wird der Antischadsoftware-Engine auf dem Client bereitgestellt, die in der Lage sein muss, die Gerätezeichenfolge zu interpretieren.  

**Voraussetzungen für die Verwendung von Endpoint Protection-Richtlinien:**  

Vor der Verwendung von Endpoint Protection-Richtlinien müssen Sie den Endpoint Protection-Client mithilfe der Endpoint Protection-Clienteinstellungen installieren und verwalten. Dies erfolgt mit dem System Center Endpoint Protection-Client für Windows 7, Windows 8, Windows 8.1 oder mit Windows Defender für Windows 10. Weitere Informationen finden Sie unter [Endpoint Protection](../../protect/deploy-use/endpoint-protection.md).  
