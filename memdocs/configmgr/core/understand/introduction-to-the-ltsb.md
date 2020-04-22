---
title: Einführung in Long-Term Servicing Branch
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Long-Term Servicing Branch von Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eda58982094860ccf075bcd2d1d8ed9e3d3bb2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706918"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Einführung in Long-Term Servicing Branch von Configuration Manager

*Gilt für: System Center Configuration Manager (Long-Term Servicing Branch)*

Der Long-Term Servicing Branch von Configuration Manager ist ein eindeutiger Branch, der als Installationsoption allen Kunden zur Verfügung steht. Dies ist jedoch die einzige Option für Kunden, die ihre Software Assurance (SA) oder entsprechende Abonnementrechte für Configuration Manager auslaufen lassen.

Basierend auf der Configuration Manager-Version 1606 weist der Long-Term Servicing Branch im Vergleich zum Current Branch von Configuration Manager eine eingeschränkte Funktionalität auf.

> [!TIP]   
> Der Long-Term Servicing Branch von Configuration Manager bezieht sich nicht auf den Long-Term Servicing Channel (LTSC) der System Center-Suite. Weitere Informationen finden Sie unter [Übersicht über Releaseoptionen von System Center](https://docs.microsoft.com/system-center/ltsc-and-sac-overview).

## <a name="features-that-arent-available"></a>Nicht verfügbare Features

Der Current Branch von Configuration Manager unterstützt folgende Funktionen, die nicht bei der Verwendung des Long-Term Servicing Branch verfügbar sind:

- Konsoleninterne Updates, die neue und verbesserte Funktionen bieten
- Unterstützung für neu veröffentlichte Betriebssysteme zur Verwendung als Standortserver und Clients
- Lokale Verwaltung mobiler Geräte
- Das Windows 10-Wartungsdashboard und die Wartungspläne, einschließlich der Unterstützung für aktuelle Windows 10-Versionen.  
- Unterstützung für zukünftige LTSB-Versionen für Windows Server und Windows 10
- Asset Intelligence
- Cloudbasierte Verteilungspunkte
- Exchange Online als Exchange Connector    

Obwohl die Unterstützung für diese Funktionen nicht im Long-Term Servicing Branch verfügbar ist, bleiben einige davon in der Configuration Manager-Konsole sichtbar, können jedoch nicht ausgewählt oder verwendet werden.

Cloudintegrationen sowie alle Features, die im Current Branch von Configuration Manager, Version 1610 oder höher, enthalten sind, sind für den Long-Term Servicing Branch nicht verfügbar. Zu diesen Features gehören u. a. folgende:<!--SCCMDocs#1823-->

- Co-Verwaltung
- Desktop Analytics
- Cloudverwaltungsgateway
- Azure Active Directory-Integration
- Apps aus dem Microsoft Store für Unternehmen

## <a name="find-ltsb-documentation"></a>Suchen der Long-Term Servicing Branch-Dokumentation

Der Long-Term Servicing Branch basiert auf der Current Branch-Version 1606. Verwenden Sie die [Dokumentation zu Current Branch](https://docs.microsoft.com/sccm/), die Warnungen und Einschränkungen speziell zum Long-Term Servicing Branch enthält. Diese Warnungen und Einschränkungen werden in folgenden Artikeln behandelt:

- [Installieren und Upgraden mit dem Baselinemedium von Version 1606 für System Center Configuration Manager](install-the-ltsb.md)
- [Upgrade von Long-Term Servicing Branch auf Current Branch](convert-to-current-branch.md)
- [Unterstützte Konfigurationen für Long Term Servicing Branch](supported-configurations-for-ltsb.md)
- [Verwalten von Long-Term Servicing Branch von Configuration Manager](manage-the-ltsb.md)

Wenn Sie sich auf die Current Branch-Dokumentation für den Long-Term Servicing Branch beziehen, gelten die Informationen für Version 1606 auch für den Long-Term Servicing Branch. Features oder Informationen, die bei Version 1610 oder höher eingeführt bzw. angegeben werden, werden nicht vom Long-Term Servicing Branch unterstützt.

## <a name="licensing-overview-for-the-ltsb"></a>Lizenzierung für LTSB – Übersicht   

Kunden mit aktiver Software Assurance für Configuration Manager-Lizenzen oder mit entsprechenden Abonnementrechten ab 1. Oktober 2016 verfügen über Benutzungsrechte des Configuration Manager-Release 1606 vom Oktober 2016. Kunden, die ab dem 1. Oktober 2016 oder danach über Rechte für Configuration Manager verfügen, erhalten während der Installation zwei lizenzierte Optionen: Current Branch und Long-Term Servicing Branch (LTSB).

Kunden, die über unbefristete Rechte für System Center Configuration Manager verfügen, oder die die Software Assurance oder das Abonnement nach dem 1. Oktober auslaufen lassen, können die LTSB-Version von System Center Configuration Manager installieren, die zu dem Zeitpunkt vorhanden ist, an dem die Software Assurance oder das Abonnement ausläuft.

Weitere Informationen über diese Lizenzen finden Sie in den [vollständigen Nutzungsbedingungen für die Produkte, die Sie über Microsoft-Volumenlizenzprogramme erwerben können](https://go.microsoft.com/fwlink/?LinkId=800052).

Weitere Informationen zur Lizenzierung für Configuration Manager-Branches finden Sie unter [Lizenzierung und Branches für System Center Configuration Manager](learn-more-editions.md).

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie zu dem Schluss kommen sollten, dass Configuration Manager-LTSB der richtige Branch für Ihre Umgebung ist, [installieren Sie einen neuen LTSB-Standort](install-the-ltsb.md#install-a-new-site) als Teil einer neuen Hierarchie, oder [aktualisieren Sie einen System Center 2012 Configuration Manager-Standort](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager) und die jeweilige Hierarchie.
