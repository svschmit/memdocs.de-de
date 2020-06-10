---
title: Intune wird in China von 21Vianet betrieben
titleSuffix: ''
description: Intune wird in China von 21Vianet betrieben.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 879cb5d1659b886a01e564574452bd9e5370664c
ms.sourcegitcommit: b0ae4a9972bac3518d0d4f33e033ac492eefe3c1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84126813"
---
# <a name="intune-operated-by-21vianet-in-china"></a>Intune wird in China von 21Vianet betrieben  

Intune wird von 21ViaNet betrieben und ist dazu ausgelegt, die Anforderungen für sichere, zuverlässige und skalierbare Clouddienste in China zu erfüllen. Intune ist ein Dienst, der auf Microsoft Azure basiert. Microsoft Azure, das von 21ViaNet betrieben wird, ist eine physisch getrennte Instanz von Cloud Services in China. Es wird unabhängig von 21ViaNet betrieben und transaktiv ausgeführt. Dieser Dienst basiert auf der Technologie, die Microsoft für 21ViaNet lizenziert hat.

Microsoft ist nicht selbst Betreiber des Dienstes. 21ViaNet ist für den Betrieb, die Bereitstellung und die Verwaltung des Dienstes verantwortlich. 21ViaNet ist ein Dienstanbieter für Internet-Rechenzentren in China. Es stellt Hosting-, verwaltete Netzwerkdienste und Cloud Computing Infrastrukturdienste bereit. Durch die Lizenzierung von Microsoft-Technologien betreibt 21ViaNet lokale Rechenzentren, um Ihnen die Möglichkeit zu bieten, den Intune-Dienst zu nutzen und gleichzeitig Ihre Daten in China zu halten. 21ViaNet bietet auch Abonnement-, Abrechnungs- und Supportdienstleistungen.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>Funktionsunterschiede in Intune bei Betrieb durch 21ViaNet

Da die China-Dienste von einem Partner aus China betrieben werden, gibt es einige Unterschiede in Bezug auf die Funktionen von Intune. 

- Das von 21ViaNet betriebene Intune unterstützt nur eigenständige Bereitstellungen. Die Unterstützung für die Co-Verwaltung mit System Center Configuration Manager befindet sich derzeit in der Entwicklung.
- Migrationen von öffentlichen Clouds zu unabhängigen Clouds werden nicht unterstützt. Kunden, die von 21ViaNet auf Intune umsteigen möchten, müssen die Migration manuell durchführen.
- Die Funktion zum Anfügen von Mandanten (das Synchronisieren von Geräten mit Intune ohne Registrierung zur Unterstützung von Cloud-Konsolenszenarien) wird derzeit nicht unterstützt.
- Das von 21ViaNet betriebene Intune unterstützt nicht den Intune-Agent und unterstützt daher keine Legacy-PC-Verwaltung.
- Die Verwaltung von Windows 10 wird über den modernen MDM-Kanal unterstützt.
- Das von 21ViaNet betriebene Intune unterstützt nicht den lokalen Exchange-Connector.
- Windows Autopilot-und Business-Store-Funktionen sind zurzeit nicht verfügbar.
- Da Google Mobile Services in China nicht verfügbar ist, können Kunden in Intune, das von 21ViaNet betrieben wird, keine Funktionen verwenden, die Google Mobile Services erfordern. Zu diesen Funktionen gehören:
  - Google Play Protect-Funktionen wie z. B. dem SafetyNet-Gerätenachweis
  - Verwalten von Apps aus dem Google Play Store
  - Android-Unternehmensfunktionen Weitere Informationen finden Sie in dieser [Google-Dokumentation](https://support.google.com/work/android/answer/6270910?hl=en).
- In der Intune Unternehmensportal-App für Android erfolgt die Kommunikation mit dem Microsoft Intune-Dienst über Google Mobile Services. Da Google Play-Dienste in China nicht verfügbar sind, kann es bis zu 8 Stunden dauern, bis einige Aufgaben abgeschlossen sind. Weitere Informationen finden Sie in [diesem Artikel](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable). 
- Zur Einhaltung der lokalen Bestimmungen und zur Bereitstellung verbesserter Funktionalität kann sich die Intune-Clientumgebung (Unternehmensportal-APP) in China unterscheiden.
- Das Fencing ist nicht verfügbar.
- Die Verfügbarkeit der mobilen Anwendungsverwaltung (Mobile Application Management, MAM) ist abhängig von den Apps, die in China verfügbar sind.

## <a name="you-control-customer-data"></a>Sie haben die Kontrolle über die Kundendaten

In Microsoft Azure, Intune, Office 365 und Power BI, das von 21ViaNet betrieben wird, haben Sie vollständige Kontrolle über Ihre Daten:
- Sie wissen, wo sich die Kundendaten befinden.
- Sie haben die Kontrolle über den Zugriff auf Ihre Kundendaten.
- Sie haben die Kontrolle über Ihre Kundendaten, wenn Sie den Dienst verlassen.
- Sie haben Optionen, um die Sicherheit Ihrer Kundendaten zu kontrollieren.

Mit Microsoft Azure, Intune, Office 365 und Power BI, das von 21ViaNet betrieben wird, sind Sie der Besitzer Ihrer Daten:
- 21ViaNet verwendet keine Kundendaten zu Werbezwecken.
- Sie haben die Kontrolle, wer Zugriff auf Ihre Kundendaten hat.
- Wir verwenden logische Isolation, um die Daten jedes Kunden voneinander zu trennen.
- Wir stellen einfache und transparente Richtlinien zur Datenverwendung bereit und werden von unabhängiger Seite überprüft.
- Unsere Unterauftragnehmer sind vertraglich dazu verpflichtet, unsere Datenschutzanforderungen zu erfüllen.

## <a name="data-subject-requests"></a>Datensubjektanforderungen

Mit der Mandantenadministrator-Rolle für Intune, das von 21ViaNet betrieben wird, können Daten für Datensubjekte auf folgende Weise angefordert werden:

- Mithilfe des Azure Active Directory Admin Centers kann ein Mandantenadministrator ein Datensubjekt dauerhaft aus Azure Active Directory und verwandten Diensten löschen. Weitere Informationen finden Sie unter [Azure-Datensubjektanforderungen – Löschen](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete)
- Vom System generierte Protokolle für Microsoft-Dienste, die von 21ViaNet betrieben werden, können von Mandantenadministratoren mithilfe des Datenprotokollexports exportiert werden. Weitere Informationen finden Sie unter [Azure-Datensubjektanforderungen – Exportieren](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export).

## <a name="next-steps"></a>Nächste Schritte

[Weitere Informationen zu von Intune unterstützten Konfigurationen](supported-devices-browsers.md)