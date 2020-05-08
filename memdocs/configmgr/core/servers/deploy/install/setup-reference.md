---
title: Setupreferenz
titleSuffix: Configuration Manager
description: Überprüfen Sie diese Referenz zur Vorbereitung der Installation eines Configuration Manager-Standorts oder einer Configuration Manager-Hierarchie.
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff2d5c6df0da6b25395858a55ef1ee8a3c0da00b
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906522"
---
# <a name="reference-for-configuration-manager-setup"></a>Referenz zum Setup für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Im Setup für Configuration Manager werden Links zu verschiedenen Themen bereitgestellt, die in den folgenden Abschnitten erläutert werden. Die hier aufgeführten Informationen helfen Ihnen beim Vorbereiten der Installation eines Configuration Manager-Standorts oder einer Hierarchie und bereiten Sie auf einige Entscheidungen vor, die Sie während der Installation treffen müssen.  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a> Vorbereitung  
Stellen Sie vor der Installation neuer Configuration Manager-Standorte sicher, dass Sie die folgenden Informationen gelesen haben, die als Grundlage für den Entwurf einer erfolgreichen Bereitstellung dienen können:  

-   [Grundlagen von Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Planen der Configuration Manager-Infrastruktur](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Vorbereiten auf die Installation von Configuration Manager-Standorten](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a> Bewerten der Serverbereitschaft  
Stellen Sie vor Beginn der Installation eines neuen Standorts sicher, dass der Standortserver und die Remote-Standortsystemserver, die Sie für den Standort verwenden möchten (wie z.B. der Server, der die Standortdatenbank hostet), alle Konfigurationsvoraussetzungen erfüllen. Diese Themen in der Dokumentationsbibliothek können dabei behilflich sein:  

-   [Unterstützte Konfigurationen für Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Voraussetzungsprüfung](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Clients für weitere Betriebssysteme  
Sie können Clientsoftware für Configuration Manager für die folgenden Betriebssysteme aus dem Microsoft Download Center herunterladen:  

- macOS (Apple)
- UNIX
- Linux

Verwenden Sie die folgenden Links zum Herunterladen von Clients für Ihre verwendete Version von Configuration Manager:  

- [Microsoft Endpoint Configuration Manager – macOS-Client (64-Bit)](https://www.microsoft.com/download/details.aspx?id=100850)

- [Microsoft Configuration Manager-Clients für weitere Betriebssysteme](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Ebenen und Einstellungen für Nutzungsdaten  
Bei der Installation des ersten Configuration Manager-Standorts wird von Configuration Manager automatisch eine neue Standortsystemrolle, der **Dienstverbindungspunkt**, auf dem Standortserver installiert und konfiguriert. Der Dienstverbindungspunkt weist die folgenden Standardeinstellungen auf:  

-   **Onlinemodus** (ein Offlinemodus ist ebenfalls verfügbar)  
-   **Erweiterte** Datensammlungsebene (zwei weitere Datensammlungsebenen, „Grundlegend“ und „Vollständig“, sind ebenfalls verfügbar)  

Wenn die Rolle „Dienstverbindungspunkt“ online ist, kann Microsoft automatisch Diagnose- und Nutzungsinformationen über das Internet sammeln. Die gesammelten Informationen geben uns folgende Möglichkeiten:  

-   Erkennen und Beheben von Problemen  
-   Verbesserung unserer Produkte und Dienste  
-   Ermitteln von Updates für Configuration Manager, die für die von Ihnen verwendete Configuration Manager-Version gelten  

### <a name="levels-of-data-collection"></a>Datensammlungsebenen  
Die drei Ebenen der Datensammlung:

-   **Grundlegend** umfasst Daten zu Setup und Upgrade, wie z.B. die Anzahl der Standorte und welche Configuration Manager-Features aktiviert sind. Es werden keine personenbezogenen Informationen übertragen.  

-   **Erweitert** umfasst die Daten der Ebeneneinstellung „Grundlegend“ und zusätzlich Daten zur Hierarchie, zur Verwendung der einzelnen Funktionen (Häufigkeit und Dauer) sowie erweiterte Diagnoseinformationen, wie z.B. den Speicherzustand des Servers bei einem System- oder Anwendungsabsturz. Es werden keine personenbezogenen Daten übertragen.  

-   **Vollständig** umfasst die Daten der Ebeneneinstellungen „Grundlegend“ und „Erweitert“ und sendet zusätzlich erweiterte Diagnoseinformationen wie z.B. Systemdateien und Momentaufnahmen des Arbeitsspeichers. Diese Option kann personenbezogene Informationen enthalten, die jedoch nicht dazu verwendet werden, Sie zu identifizieren, Kontakt mit Ihnen aufzunehmen oder Ihnen Werbung zukommen zu lassen.  

Weitere Informationen, z. B. bezüglich der Offenlegung der auf den einzelnen Ebenen erfassten Details, finden Sie unter [Diagnose- und Nutzungsdaten für Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Weitere Informationen finden Sie in der [Datenschutzerklärung von Microsoft](https://privacy.microsoft.com/privacystatement).
