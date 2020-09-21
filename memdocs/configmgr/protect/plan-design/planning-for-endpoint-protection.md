---
title: Planen von Endpoint Protection
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: mestew
ms.author: mstewart
manager: dougeby
description: Planen für Richtlinien für Antischadsoftware und Windows-Firewall-Sicherheit
ms.openlocfilehash: 2e3904b7b7232e92fd4a246d2e0519ef32fb67f6
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606827"
---
# <a name="planning-for-endpoint-protection-in-configuration-manager"></a>Planen von Endpoint Protection in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


Mithilfe von Endpoint Protection in Configuration Manager können Sie Richtlinien für Antischadsoftware und die Sicherheit der Windows-Firewall für Clientcomputer in Ihrer Configuration Manager-Hierarchie verwalten.  

> [!IMPORTANT]  
>  Sie benötigen eine Lizenz für die Verwendung von Endpoint Protection, damit Sie Clients in der Configuration Manager-Hierarchie verwalten können.  

Bei der Verwendung von Endpoint Protection mit Configuration Manager ergeben sich für Sie die folgenden Vorteile:  

-   Sie können Antischadsoftware-Richtlinien und Windows-Firewall-Einstellungen erstellen und Microsoft Defender Advanced Threat Protection für ausgewählte Computergruppen verwalten.  

-   Sie können mit Configuration Manager-Softwareupdates die neuesten Definitionsdateien für Antischadsoftware herunterladen, um Clientcomputer auf dem neuesten Stand zu halten.  

-   Sie können E-Mail-Benachrichtigungen senden, die Überwachung in der Konsole nutzen und Berichte anzeigen, damit Administratoren über erkannte Schadsoftware auf Clientcomputern informiert werden.  

Windows 10-Computer benötigen keinen zusätzlichen Client für die Verwaltung von Endpoint Protection. Unter Windows 8.1 und älteren Computern installiert Endpoint Protection zusätzlich zum Configuration Manager-Client einen eigenen Client. Der Endpoint Protection-Client verfügt über folgende Funktionen:  

-   Erkennung von Schadsoftware und Spyware sowie Wiederherstellung  

-   Erkennung von Rootkits und Wiederherstellung  

-   Bewertung kritischer Sicherheitsrisikos und automatische Definitions- und Engine-Updates  

-   Erkennung von Sicherheitslücken im Netzwerk über das Netzwerkinspektionssystem  

-   Integration mit Cloud Protection Service, um Microsoft Schadsoftware zu melden. Wenn Sie diesem Dienst beitreten, können von Windows Defender oder vom Endpoint Protection-Client die neuesten Definitionen aus dem Microsoft Center zum Schutz vor Schadsoftware heruntergeladen werden, sobald nicht identifizierte Schadsoftware auf einem Computer erkannt wird.  

> [!NOTE]  
>  Der Endpoint Protection-Client kann auf einem Server, auf dem Hyper-V ausgeführt wird, sowie auf virtuellen Gastcomputern mit unterstützten Betriebssystemen installiert werden. Um eine übermäßige CPU-Auslastung zu verhindern, weisen Endpoint Protection-Aktionen eine integrierte zufällige Verzögerung auf, damit Dienste nicht gleichzeitig ausgeführt werden.  

  Darüber hinaus können Sie Endpoint Protection in Configuration Manager zum Verwalten von Windows-Firewall-Einstellungen in der Configuration Manager-Konsole nutzen.  

 [Beispielszenario: Verwenden von Endpoint Protection zum Schutz von Computern vor Schadsoftware](../deploy-use/scenarios-endpoint-protection.md). Diesem Szenario können Sie entnehmen, wie Sie Endpoint Protection und die Windows-Firewall konfigurieren und verwalten können.  

## <a name="managing-malware-with-endpoint-protection"></a>Verwalten von Schadsoftware mit Endpoint Protection  

Mit Endpoint Protection in Configuration Manager können Sie Antischadsoftware-Richtlinien erstellen, in denen Einstellungen für Endpoint Protection-Clientkonfigurationen enthalten sind. Sie können diese Antischadsoftware-Richtlinien auf Clientcomputern bereitstellen und sie im Knoten **Endpoint Protection-Status**im Arbeitsbereich **Überwachung** oder mithilfe von Configuration Manager-Berichten überwachen.  

 Zusätzliche Informationen:  

-   [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection](../deploy-use/endpoint-antimalware-policies.md) ‒ Erstellen, Bereitstellen und Überwachen von Richtlinien für Antischadsoftware mit einer Liste der Einstellungen, die Sie konfigurieren können  

-   [Überwachen von Endpoint Protection](../deploy-use/monitor-endpoint-protection.md) ‒ Überwachen von Aktivitätsberichten, infizierten Clientcomputern und mehr.   

-   [Verwalten von Richtlinien für Antischadsoftware und Firewalleinstellungen für Endpoint Protection](../deploy-use/endpoint-antimalware-firewall.md) – Sie können die Richtlinien für [Antischadsoftware](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) oder [Firewall](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies) ändern, [auf Clientcomputern gefundene Schadsoftware beseitigen](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware) und weitere Aufgaben ausführen.

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Verwalten der Windows-Firewall mit Endpoint Protection  
 Durch Endpoint Protection in Configuration Manager verfügen Sie über eine grundlegende Verwaltung der Windows-Firewall auf Clientcomputern. Für jedes Netzwerkprofil können Sie die folgenden Einstellungen konfigurieren:  

-   Aktivieren oder Deaktivieren der Windows-Firewall  

-   Blockieren eingehender Verbindungen, einschließlich der in der Liste der zugelassenen Programme aufgeführten Verbindungen  

-   Benachrichtigen des Benutzers, wenn ein neues Programm von der Windows-Firewall blockiert wird  

> [!NOTE]  
>  Von Endpoint Protection wird nur die Verwaltung der Windows-Firewall unterstützt.  

  Weitere Informationen zur Erstellung und Bereitstellung von Windows-Firewallrichtlinien für Endpoint Protection finden Sie unter [Erstellen und Bereitstellen von Windows-Firewallrichtlinien für Endpoint Protection](../deploy-use/create-windows-firewall-policies.md).  

## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Ab Version 1606 von Configuration Manager (Current Branch) kann Endpoint Protection Microsoft Defender Advanced Threat Protection (ATP) (früher als Windows Defender ATP bezeichnet) verwalten und überwachen. Microsoft Defender ATP ist ein Dienst, der Unternehmen dabei unterstützt, erweiterte Angriffe auf ihre Netzwerke zu entdecken, zu untersuchen, und darauf zu reagieren. Weitere Informationen finden Sie unter [Microsoft Defender Advanced Threat Protection](../deploy-use/defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Endpoint Protection-Workflow  
 Das folgende Diagramm bringt Ihnen den Workflow zur Implementierung von Endpoint Protection in Ihrer Configuration Manager-Hierarchie näher.  

 ![Endpoint Protection-Workflow](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Endpoint Protection-Client für Macintosh-Computer und Linux-Server  
 System Center umfasst einen Endpoint Protection-Client für Linux- und Mac-Computer. Diese Clients sind nicht im Lieferumfang von Configuration Manager enthalten. Stattdessen müssen Sie die folgenden Produkte aus dem [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx) herunterladen.  

> [!IMPORTANT]  
>  Sie müssen ein Microsoft-Volumenlizenz-Kunde sein, damit Sie die Endpoint Protection-Installationsdateien für Linux und den Macintosh herunterladen können.  

 Diese Produkte können nicht über die Configuration Manager-Konsole verwaltet werden. Allerdings wird mit den Installationsdateien ein System Center Operations Manager-Management Pack bereitgestellt, das es Ihnen ermöglicht, den Client für Linux mit Operations Manager zu verwalten.  

 Weitere Informationen zum Installieren und Verwalten von Endpoint Protection-Clients für Linux und Macintosh-Computer finden Sie in der Dokumentation des jeweiligen Produkts im Ordner **Documentation** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Bewährte Methoden für Endpoint Protection in Configuration Manager  
 Verwenden Sie die folgenden bewährten Methoden für Endpoint Protection in System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Konfigurieren benutzerdefinierter Clienteinstellungen für Endpoint Protection  
 Verwenden Sie beim Konfigurieren der Clienteinstellungen für Endpoint Protection nicht die Standardclienteinstellungen, da diese Einstellungen auf alle Computer in Ihrer Hierarchie angewendet werden. Konfigurieren Sie stattdessen benutzerdefinierte Clienteinstellungen, und weisen Sie ihnen Computersammlungen in Ihrer Hierarchie zu.  

 Wenn Sie benutzerdefinierte Clienteinstellungen konfigurieren, können Sie Folgendes tun:  

-   Passen Sie Antischadsoftware und Sicherheitseinstellungen an unterschiedliche Bereiche Ihrer Organisation an.  
-   Testen Sie vor einer Bereitstellung für die gesamte Hierarchie an einer kleinen Gruppe von Computern die Auswirkungen, die das Ausführen von Endpoint Protection hat.  
-   Fügen Sie im Lauf der Zeit weitere Clients zur Sammlung hinzu, um Ihre Bereitstellung des Endpoint Protection-Clients in Phasen zu untergliedern.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Verteilen von Definitionsupdates mithilfe von Softwareupdates  
 Bei Verwendung von Configuration Manager-Softwareupdates zur Verteilung der Definitionsupdates, sollten Sie Definitionsupdates in einem Paket platzieren, das keine anderen Softwareupdates enthält. Dadurch wird der Größe des Updatepakets Definition kleiner wodurch an Verteilungspunkte schneller replizieren.
