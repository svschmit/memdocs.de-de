---
title: Hilfe zu Endpoint Protection-Client
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Features und Verbesserungen in Endpoint Protection, mit denen Sie Ihren Computer besser vor Angriffen schützen können.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eba7de1705212bb5cb329282bc407317995b82f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709208"
---
# <a name="endpoint-protection-client-help"></a>Hilfe zu Endpoint Protection-Client

*Gilt für: Configuration Manager (Current Branch)*


Diese Version von Windows Defender oder Endpoint Protection enthält die folgenden Features, mit denen Sie Ihren Computer besser vor Bedrohungen schützen können:  

-   **Windows-Firewall-Integration.** Während des Setups von Endpoint Protection können Sie die Windows-Firewall aktivieren oder deaktivieren.  
-   **Netzwerkprüfungssystem.** Diese Funktion verbessert den Echtzeitschutz, indem der Netzwerkdatenverkehr geprüft wird, um das Ausnutzen bekannter Sicherheitsschwachstellen proaktiv zu verhindern.  
-   **Schutz-Engine.** Der Echtzeitschutz sucht nach Schadsoftware und verhindert, dass diese auf Ihrem PC installiert oder ausgeführt wird. Die aktualisierte Engine bietet erweiterte Schutz- und Bereinigungsfunktionen mit besserer Leistung.  

Windows Defender ist im Lieferumfang des Windows 10-Betriebssystems enthalten.  Unter früheren Versionen von Windows kann Ihr Administrator Windows Defender oder Endpoint Protection mithilfe von Verwaltungssoftware bereitstellen.

Sie können auch eine Liste von [häufig gestellten Fragen zu Windows Defender und Endpoint Protection](endpoint-protection-client-faq.md) finden. Informationen zur Problembehandlung finden Sie unter [Problembehandlung für Windows Defender oder den Endpoint Protection-Client](troubleshoot-endpoint-client.md). Eine Liste der neuen Features finden Sie unter [Neuigkeiten in Windows Defender](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender).

## <a name="windows-firewall-integration"></a>Windows-Firewall-Integration  
 Mit der Windows-Firewall kann verhindert werden, dass sich ein Angreifer oder eine Schadsoftware über das Internet oder über ein Netzwerk Zugriff auf den Computer verschafft. Wenn Sie Endpoint Protection installieren, stellt der Installations-Assistent jetzt sicher, dass die Windows-Firewall aktiviert ist. Wenn Sie Windows-Firewall bewusst deaktiviert haben, können Sie das Aktivieren der Windows-Firewall verhindern, indem Sie das entsprechende Kontrollkästchen deaktivieren. Sie können die Windows-Firewalleinstellungen jederzeit über die System- und Sicherheitseinstellungen in der Systemsteuerung ändern.  

## <a name="network-inspection-system"></a>Netzwerkprüfungssystem  
 Angreifer führen zunehmend netzwerkbasierte Angriffe auf bekannte Schwachstellen durch, bevor Softwarehersteller Sicherheitsupdates entwickeln und verteilen können. Untersuchungen der Schwachstellen zeigen, dass es nach dem ersten Melden eines Angriffs einen Monat oder länger dauern kann, bis ein geeignetes Sicherheitsupdate entwickelt, getestet und freigegeben wird. Aufgrund dieser Problematik sind viele Computer für einen erheblich langen Zeitraum der Gefahr von Angriffen und dem Ausnutzen von Sicherheitslücken ausgesetzt. Das Netzwerkinspektionssystem kann Sie zusammen mit dem Echtzeitschutz besser vor netzwerkbasierten Angriffen schützen, indem die Zeit zwischen dem Bekanntwerden von Sicherheitsrisiken und der Entwicklung eines Updates auf wenige Stunden reduziert wird.  

## <a name="award-winning-protection-engine"></a>Preisgekrönte Schutz-Engine  
 In Windows Defender oder Endpoint Protection ist eine vielfach ausgezeichnete Schutz-Engine integriert, die regelmäßig aktualisiert wird. Die Engine wird unterstützt von einem Team aus Antischadsoftware-Forschern aus dem Microsoft Center zum Schutz vor Malware, das rund um die Uhr daran arbeitet, Patches und Updates zum Schutz vor der neuesten Schadsoftware bereitzustellen.  

## <a name="windows-defender-settings"></a>Windows Defender-Einstellungen
Windows Defender-Einstellungen aktivieren Einstellungen, die den Schutz Ihres PCs vor böswilliger Software unterstützen. Der Administrator kann möglicherweise einige Windows Defender-Einstellungen für Sie verwalten. Sie können andere Einstellungen mithilfe der Windows Defender-Einstellungen verwalten. Es wird empfohlen, dass Sie die Windows Defender-Einstellungen aktivieren, um den Schutz Ihres PCs und Ihrer Daten zu unterstützen.

Wenn Sie die Windows Defender-Einstellungen anzeigen möchten, suchen Sie nach `Windows Defender` auf Ihrem PC. Öffnen Sie **Windows Defender**, und wählen Sie **Einstellungen** aus. Zu den Windows Defender-Einstellungen zählen:
- **Echtzeitschutz**: Sucht nach Schadsoftware und verhindert, dass diese auf Ihrem PC installiert oder ausgeführt wird.
- **Cloudbasierter Schutz**: Windows Defender sendet Informationen über potentielle Sicherheitsrisiken an Microsoft.
- **Automatische Beispielübermittlung**: Ermöglicht es Windows Defender, Beispiele böswilliger Dateien an Microsoft zu senden, um die Erkennung von Schadsoftware zu verbessern.
- **Ausschlüsse**: Sie können bestimmte Dateien, Ordner, Dateierweiterungen oder Prozesse von der Überprüfung durch Windows Defender ausschließen.
- **Erweiterte Benachrichtigungen**: Aktiviert Benachrichtigungen, die über die Integrität Ihres PCs informieren. Sogar wenn diese Einstellung **Deaktiviert** ist, erhalten Sie kritische Benachrichtigungen.
- **Windows Defender Offline**: Sie können Windows Defender Offline ausführen, um böswillige Software zu suchen und zu entfernen. Durch diese Überprüfung wird Ihr PC neu gestartet. Dies dauert ungefähr 15 Minuten.

### <a name="see-also"></a>Weitere Informationen:  
 [Häufig gestellte Fragen zum Endpoint Protection-Client](endpoint-protection-client-faq.md)   
 [Problembehandlung für Windows Defender oder den Endpoint Protection-Client](troubleshoot-endpoint-client.md)
