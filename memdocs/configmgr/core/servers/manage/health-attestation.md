---
title: Integritätsnachweis
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zum Integritätsnachweis, der in der Configuration Manager-Konsole angezeigt werden kann.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ed155fb61491a273732ed3b974b6ddb5ac29bc89
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904016"
---
# <a name="health-attestation-for-configuration-manager"></a>Integritätsnachweis für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Administratoren können den Status des [Windows 10-Nachweises zur Geräteintegrität](https://docs.microsoft.com/windows/security/threat-protection/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices) in der Configuration Manager-Konsole anzeigen.  Mit dem Nachweis der Geräteintegrität kann der Administrator sicherstellen, dass Clientcomputer über die folgenden aktivierten vertrauenswürdigen BIOS-, TPM- und Startsoftwarekonfigurationen verfügen:  

-   Antischadsoftware-Frühstart – Antischadsoftware-Frühstart (Early Launch Anti-Malware, ELAM) schützt Ihren Computer beim Starten und bevor Drittanbietertreiber initialisiert werden. [Informationen zum Aktivieren von ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker – Mit der Windows-BitLocker-Laufwerkverschlüsselungs-Software können Sie alle Daten verschlüsseln, die auf dem Windows-Betriebssystemvolume gespeichert sind.  [How to turn on BitLocker (Informationen zum Aktivieren von BitLocker)](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Sicherer Start – Sicherer Start ist ein Sicherheitsstandard, der von Mitgliedern der PC-Industrie entwickelt wurde, um sicherzustellen, dass Ihr PC nur mit Software startet, die der PC-Hersteller als vertrauenswürdig eingestuft hat. [Weitere Informationen zu Sicherer Start](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh824987(v=win.10))  
-   Codeintegrität – Codeintegrität ist ein Feature, das die Sicherheit des Betriebssystems verbessert, indem es die Integrität einer Treiber- oder Systemdatei jedes Mal überprüft, wenn sie in den Arbeitsspeicher geladen wird. [Erfahren Sie mehr über Codeintegrität](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd348642(v=ws.10))  

Diese Funktion ist für PCs und lokale Ressourcen verfügbar, die von Configuration Manager verwaltet werden sowie für mobile Geräte, die von Microsoft Intune verwaltet werden. Administratoren können angeben, ob die Berichterstellung über die Cloud oder über die lokale Infrastruktur durchgeführt wird. Die lokale Überwachung des Nachweises der Geräteintegrität ermöglicht dem Administrator die Überwachung des Client-PCs ohne Internetzugriff.

## <a name="enable-health-attestation"></a>Aktivieren des Integritätsnachweises

 **Anforderungen:**  

-   Clientgeräte unter Windows 10 Version 1607 oder Windows Server 2016 Version 1607 mit [Nachweis der Geräteintegrität aktiviert](https://docs.microsoft.com/windows-server/security/device-health-attestation)
-   TPM 1.2- oder TPM 2-fähige Geräte
-   Bei der Verwendung der Cloudverwaltung erfolgt die Kommunikation zwischen dem Configuration Manager-Client-Agent und dem Verwaltungspunkt mit *has.spserv.microsoft.com* (Port 443) Integritätsnachweisdienst (Cloud-Verwaltung). Wenn sich der Client lokal befindet, muss er fähig sein, mit dem Verwaltungspunkt mit aktiviertem Nachweis der Geräteintegrität zu kommunizieren.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Aktivieren der Kommunikation mit dem Integritätsnachweisdienst auf Configuration Manager-Clientcomputern

Verwenden Sie dieses Verfahren, um die Überwachung des Nachweises der Geräteintegrität für Geräte zu aktivieren, die mit dem Internet verbunden sind.

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Übersicht** > **Clienteinstellungen**aus.  Wählen Sie die Registerkarte für **Computer-Agent** -Einstellungen aus.  
2.  Wählen Sie im Dialogfeld **Standardeinstellungen** **Computer-Agent** aus, und scrollen Sie nach unten zu **Kommunikation mit Integritätsnachweisdienst aktivieren**.  
3.  Legen Sie **Kommunikation mit Integritätsnachweisdienst aktivieren** auf **Ja**fest, und klicken Sie anschließend auf **OK**.  
4. Zielsammlungen von Geräten, die die Geräteintegrität melden sollen.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Aktivieren der lokalen Kommunikation mit dem Integritätsnachweisdienst auf Configuration Manager-Clientcomputern
Verwenden Sie dieses Verfahren, um die Überwachung des Nachweises der Geräteintegrität für lokale Geräte zu aktivieren, die nicht mit dem Internet verbunden sind.

Ab Configuration Manager 1702 kann die lokale Dienst-URL des Nachweises der Geräteintegrität auf dem Verwaltungspunkt zur Unterstützung von Client-Geräten ohne Zugriff auf das Internet konfiguriert werden.

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.
2. Klicken Sie mit der rechten Maustaste auf den primären oder sekundären Standort mit dem Verwaltungspunkt, der lokale Clients für den Nachweis der Geräteintegrität unterstützt, und wählen Sie **Standortkomponenten konfigurieren** > **Verwaltungspunkt** aus. Die Seite **Eigenschaften der Verwaltungspunktkomponente** öffnet sich.
3. Wählen Sie auf der Registerkarte **Erweiterte Optionen** **Hinzufügen** aus, und geben Sie eine gültige lokale Dienst-URL für den Nachweis der Geräteintegrität an. Sie können mehrere URLs hinzufügen. Wenn mehrere lokale URLs angegeben sind, erhalten Clients den vollständigen Satz und wählen nach dem Zufallsprinzip aus, welche sie verwenden.
4.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Übersicht** > **Clienteinstellungen**aus.  Wählen Sie die Registerkarte für **Computer-Agent** -Einstellungen aus.  
5.  Scrollen Sie nach unten zu **Kommunikation mit Integritätsnachweisdienst aktivieren**, und legen Sie **Ja** fest.
7.  Klicken Sie auf die Option **Lokalen Integritätsnachweisdienst verwenden**, und legen Sie **Ja** fest.
8. Setzen Sie die Sammlung von Geräten als Ziel, die die Geräteintegrität mit den Client-Agent-Einstellungen melden sollen, um die Berichterstattung für den Nachweis der Geräteintegrität zu aktivieren.

Sie können die Dienst-URLs für den Nachweis der Geräteintegrität auch **bearbeiten** oder **entfernen**.

> [!NOTE]
> Wenn Sie den Nachweis der Geräteintegrität vor dem Upgrade auf Configuration Manager 1702 verwendet haben, werden die in den Einstellungen des Client-Agent angegebenen lokalen URLs vorab während des Upgrades in den Eigenschaften des Verwaltungspunkts eingefügt. Lokale Clients werden weiterhin die URL verwenden, die in den Einstellungen des Client-Agents angegeben werden, bis sie aktualisiert werden. Sie werden dann auf eine der im Verwaltungspunkt angegebenen URLs umschalten.

## <a name="monitor-device-health-attestation"></a>Überwachung des Nachweises der Geräteintegrität

1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung** , klicken Sie auf den Knoten **Sicherheit** und anschließend auf **Integritätsnachweis**, um den Nachweis der Geräteintegrität anzuzeigen.  
2.  Der Nachweis der Geräteintegrität wird angezeigt.  

Der Configuration Manager-Geräteintegritätsnachweis zeigt Folgendes an:  

-   **Integritätsnachweisstatus** – Zeigt die Anteile der Geräte in kompatiblem, nicht kompatiblem, Fehler- und unbekanntem Status an  
-   **Geräte mit Health Attestation-Unterstützung** – Zeigt den Prozentsatz der Geräte an, die den Integritätsnachweisstatus berichten  
-   **Nicht kompatible Geräte nach Clienttyp** – Zeigt den Anteil an mobilen Geräten und Computern an, die nicht kompatibel sind  
-   **Wichtigste fehlende Integritätsnachweiseinstellungen** – Zeigt nach Einstellungen gelistet die Anzahl von Geräte an, für die die Health Attestation-Einstellung fehlt
