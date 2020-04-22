---
title: Dashboard für den Produktlebenszyklus
titleSuffix: Configuration Manager
description: Anzeigen der Microsoft-Lebenszyklusrichtlinie mit dem Dashboard für den Produktlebenszyklus in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695168"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Verwalten der Microsoft-Lebenszyklusrichtlinie mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Ab Version 1806 können Sie das Dashboard für den Produktlebenszyklus von Configuration Manager zum Anzeigen der Microsoft-Lebenszyklusrichtlinie verwenden. Das Dashboard zeigt den Status der Microsoft-Lebenszyklusrichtlinie für Microsoft-Produkte an, die auf mit Configuration Manager verwalteten Geräten installiert sind. Es stellt Ihnen außerdem Informationen zu Microsoft-Produkten in Ihrer Umgebung, deren Supportfähigkeit und den Daten des Supportendes zur Verfügung. Auf diesem Dashboard erfahren Sie, welche Art von Support für die jeweiligen Produkte verfügbar ist. Diese Informationen helfen Ihnen dabei, zu planen, wann Sie die von Ihnen verwendeten Microsoft-Produkte aktualisieren müssen, bevor das Ende des Supports erreicht ist.  

Weitere Informationen finden Sie in der [Microsoft-Lebenszyklusrichtlinie](https://support.microsoft.com/lifecycle).

Ab Version 1810 enthält das Dashboard Informationen für System Center Configuration Manager 2012 und höher.<!--1358702-->  



## <a name="prerequisites"></a>Voraussetzungen 

 Damit Sie Daten auf dem Dashboard für den Produktlebenszyklus anzeigen können, sind folgende Komponenten erforderlich:  

- Auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, muss Internet Explorer 9 oder höher installiert sein.  

- Eine Dienstverbindungspunkt-Rolle muss installiert und konfiguriert werden. Wenn Sie Updates zu den Daten auf diesem Dashboard erhalten möchten, muss der Dienstverbindungspunkt online sein oder regelmäßig synchronisiert werden, sollte er offline sein. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../../../servers/deploy/configure/about-the-service-connection-point.md).

- Ein Reporting Services-Punkt ist für die Funktionalität von Hyperlinks auf dem Dashboard erforderlich. Das Dashboard enthält Links zu SSRS-Berichten (SQL Server Reporting Services). Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../../servers/manage/introduction-to-reporting.md).  

- Der Asset Intelligence-Synchronisierungspunkt muss konfiguriert und synchronisiert sein. Das Dashboard verwendet den Asset Intelligence-Katalog als Metadaten für Produkttitel. Die Metadaten werden mit Inventurdaten in Ihrer Hierarchie verglichen. Weitere Informationen finden Sie unter [Konfigurieren von Asset Intelligence in Configuration Manager](configuring-asset-intelligence.md).  
  - Wenn Sie den Asset Intelligence-Dienstpunkt zum ersten Mal konfigurieren, stellen Sie sicher, dass Sie die [Asset Intelligence-Hardwareinventurklassen aktivieren](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). Das Dashboard für den Lebenszyklus ist von den Asset Intelligence-Hardwareinventurklassen abhängig. Auf dem Dashboard werden keine Daten angezeigt, bis Clients auf Hardwareinventur geprüft und diese zurückgegeben haben.  
  - Um Informationen zu Extended Security Updates (ESU) auf diesem Dashboard anzuzeigen, aktivieren Sie die Hardwareinventurklasse **Softwarelizenzierungsprodukt – Asset Intelligence (SoftwareLicensingProduct)** . Weitere Informationen finden Sie unter [Aktivieren von Asset Intelligence-Hardwareinventur-Berichtsklassen](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>Verwenden des Dashboards für den Produktlebenszyklus

Auf dem Dashboard werden Informationen zu allen aktuellen Produkten angezeigt, die auf Inventurdaten basieren, die der Standort von verwalteten Geräten sammelt. Die für Betriebssysteme und SQL Server angezeigten Informationen beschränken sich jedoch auf folgende Versionen:

- Windows Server 2008 und höher
- Windows XP und höher
- SQL Server 2008 und höher

Wechseln Sie zum Arbeitsbereich **Assets und Konformität**, erweitern Sie **Asset Intelligence**, und wählen Sie den Knoten **Produktlebenszyklus** aus, um in der Configuration Manager-Konsole auf das Dashboard für den Lebenszyklus zuzugreifen.

> [!NOTE]  
> Die Daten auf dem Dashboard basieren auf dem Standort, mit dem die Configuration Manager-Konsole verbunden ist. Wenn die Konsole eine Verbindung zu Ihrem Standort der obersten Ebene herstellt, sehen Sie die Daten für die gesamte Hierarchie. Bei einer Verbindung mit einem untergeordneten primären Standort werden nur die Daten aus diesem Standort angezeigt.

### <a name="product-lifecycle-dashboard"></a>Dashboard für den Produktlebenszyklus

![Screenshot vom Dashboard für den Produktlebenszyklus in der Konsole](media/product-lifecycle-dashboard.png)

Ändern Sie die Ansicht, indem Sie eine der folgenden Optionen aus der **Produktkategorieliste** auswählen:  
- **Alle:** Alle Produkte werden zusammen angezeigt  
- **Windows-Client:** Betriebssystemversionen des Windows-Clients werden angezeigt  
- **Windows Server:** Betriebssystemversionen des Windows Server werden angezeigt  
- **Datenbank:** SQL Server-Versionen werden angezeigt  
- **Configuration Manager:** Configuration Manager-Versionen werden angezeigt (ab Version 1810) 
- **Microsoft Office**: Ab Version 1902 können Sie Informationen zu installierten Versionen von Office 2003 bis Office 2016 anzeigen. <!--3556026-->

Das Dashboard verfügt über die folgenden Kacheln:  

- **Top five products past end-of-life** (Top 5 Produkte, die das Ende des Lebenszyklus erreicht haben): Diese Kachel zeigt eine konsolidierte Datenansicht der Produkte in Ihrer Umgebung, deren Lebenszyklus abgelaufen ist. Das Diagramm zeigt installierte Software, deren Lebenszyklus abgelaufen ist, basierend auf dem Supportlebenszyklus für Betriebssysteme und SQL Server-Produkte.  

- **Top five products past end-of-life** (Top 5 Produkte, deren Lebenszyklus in den nächsten sechs Monaten endet): Diese Kachel zeigt eine konsolidierte Datenansicht der Produkte in Ihrer Umgebung, deren Lebenszyklus innerhalb der nächsten 18 Monate abläuft. Das Diagramm zeigt installierte Software, deren Lebenszyklus innerhalb von 18 Monaten ablaufen wird, basierend auf dem Supportlebenszyklus für Betriebssysteme und SQL Server-Produkte.  

- **Lebenszyklusdaten für die installierten Produkte:** Diese Kachel bietet einen allgemeinen Überblick darüber, wann ein Produkt keinen Supportstatus mehr haben wird. Das Diagramm zeigt eine Aufschlüsselung der Anzahl von Clients, auf denen das Produkt installiert ist, den Status der Supportverfügbarkeit sowie einen Link zu weiteren Informationen zu den nächsten Schritten. Das Diagramm enthält die folgenden Informationen:     
    - Verbleibende Supportdauer
    - Anzahl in der Umgebung 
    - Enddatum des grundlegenden Supports
    - Enddatum des erweiterten Supports
    - Nächste Schritte  

> [!IMPORTANT]  
> Die Daten auf diesem Dashboard dienen nur zu Ihrer Information und zur internen Verwendung innerhalb Ihres Unternehmens. Sie sollten sich im Hinblick auf die Konformität nicht ausschließlich auf diese Informationen verlassen. Überprüfen Sie die Genauigkeit der bereitgestellten Informationen sowie die Verfügbarkeit von Supportinformationen in der [Microsoft-Lebenszyklusrichtlinie](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Berichterstellung

Außerdem sind zusätzliche Berichte verfügbar. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** die Knoten **Berichterstellung** und **Berichte**. Die folgenden neuen Berichte werden der Kategorie **Asset Intelligence** hinzugefügt:  

- **Lebenszyklus 01A – Computer mit einem bestimmten Softwareprodukt:** Zeigt eine Liste der Computer an, auf denen ein angegebenes Produkt erkannt wird.  

- **Lebenszyklus 02A – Liste von Computern mit abgelaufenen Produkten in der Organisation:** Zeigt Computer an, auf denen abgelaufene Produkte ausgeführt werden. Sie können diesen Bericht nach dem Produktnamen filtern.

- **Lebenszyklus 03A – In der Organisation vorgefundene Liste abgelaufener Produkte:** Zeigt Details zu Produkten in Ihrer Umgebung an, deren Lebenszyklus abgelaufen ist.  

- **Lebenszyklus 04A – Allgemeine Übersicht über den Produktlebenszyklus:** Zeigt eine Liste der Produktlebenszyklen an. Sie können die Liste nach Produktnamen und Tagen bis zum Ablauf filtern.  

- **Lebenszyklus 05A: Produktlebenszyklus-Dashboard:** Ab Version 1810 enthält dieser Bericht ähnliche Informationen wie das Dashboard in der Konsole. Wählen Sie eine Kategorie aus, um die Anzahl von Produkten in Ihrer Umgebung und die verbleibende Supportdauer in Tagen anzuzeigen.  

Weitere Informationen finden Sie in der [Liste der Berichte](../../../servers/manage/list-of-reports.md#asset-intelligence).<!--SCCMDocs issue 997-->  
