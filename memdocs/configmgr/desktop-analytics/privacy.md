---
title: Desktop Analytics – Datenschutz
titleSuffix: Configuration Manager
description: Desktop Analytics tritt für den Datenschutz der Kunden ein.
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: eb393b05e1ee93239b43725a67b9a1b3e54e71ed
ms.sourcegitcommit: 693932432270ab3df1df9f5e6783c7f5c6f31252
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997955"
---
# <a name="desktop-analytics-data-privacy"></a>Desktop Analytics – Datenschutz

Der Datenschutz für Kunden ist ein wichtiges Anliegen von Desktop Analytics, das sich auf diese Grundprinzipien stützt:

- **Transparenz:** Wir dokumentieren umfassend Windows-Diagnoseereignisse. Sie können diese mit den Sicherheits-und Compliance-Teams Ihres Unternehmens überprüfen. Mit dem Diagnosedaten-Viewer von Windows können Sie die Diagnosedaten anzeigen, die von einem bestimmten Gerät gesendet wurden. Weitere Informationen hierzu finden Sie unter [Übersicht über den Diagnosedaten-Viewer](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Kontrolle:** Sie haben die Kontrolle über den Umgang der Diagnosedaten, die mit Microsoft geteilt werden. In Windows 10, Version 1709, wird eine neue Richtlinie eingeführt, die erweiterte Diagnosedaten auf das von Desktop Analytics benötigte Minimum begrenzt.  

- **Sicherheit:** Microsoft schützt Ihre Daten mit hoher Sicherheit und starker Verschlüsselung.  

- **Vertrauen:** Desktop Analytics unterstützt die [Datenschutzbestimmungen](https://privacy.microsoft.com/privacystatement) und die [Onlinenutzungsbedingungen](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46) von Microsoft.  

Weitere Informationen finden Sie unter [Windows-Dienste, für die Microsoft der Auftragsverarbeiter im Sinne der DSGVO ist](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr).<!-- 5353168 -->

## <a name="data-flow"></a>Datenfluss

In der folgenden Abbildung wird der Fluss der Diagnosedaten von einzelnen Geräten über den Diagnosedatendienst und den vorübergehenden Speicher zu Ihrem Log Analytics-Arbeitsbereich veranschaulicht:

![Diagramm zur Veranschaulichung des Flusses der Diagnosedaten von Geräten](media/da-data-flow.png)

1. Sie melden sich beim Azure-Portal an und führen das Onboarding in Desktop Analytics durch. Sie erstellen die Azure AD-App, um eine Verbindung mit Configuration Manager herzustellen. Beim Einrichten von Desktop Analytics erstellen Sie einen Azure Log Analytics-Arbeitsbereich am gewünschten Speicherort.  

2. Sie stellen eine Verbindung mit Configuration Manager her und registrieren Geräte.  

    1. Sie konfigurieren den Desktop Analytics-Clouddienst in Configuration Manager mit den Details der Azure AD-App.  

    2. Innerhalb von 15 Minuten synchronisiert Configuration Manager mithilfe Ihrer Mandanten-ID die folgenden Daten mit Desktop Analytics. Dieser Vorgang wird jede Stunde wiederholt.

      - Informationen zu Gerätesammlungen sind für die [Erstellung von Bereitstellungsplänen](create-deployment-plans.md) erforderlich. Diese Informationen beinhalten die Sammlungs-ID, Hierarchie-ID, den Sammlungsnamen und die Geräteanzahl. 
      - Für die [Registrierung von Geräten](enroll-devices.md) sind Informationen nötig. Diese sind u. a. die Sammlungs-ID, eindeutige SMS-Bezeichner, die Buildversion des Betriebssystems, der Gerätename und die Seriennummer.
      - Informationen des Dashboards [Überwachen der Verbindungsintegrität](monitor-connection-health.md). Diese Informationen umfassen die Anzahl der Geräte nach Integritätszustand und die Geräteeigenschaften.
      - Informationen zu Bereitstellungsplänen, die die Sammlungs-ID, Bereitstellungs-ID, den Pilot- oder Produktionsbereitstellungstyp sowie die Anzahl der Geräte nach Upgradeentscheidung beinhalten.

    3. Configuration Manager legt die kommerzielle ID, die Diagnosedatenebene und weitere Einstellungen für die Geräte in der Zielsammlung fest. Diese Konfiguration gibt die Geräte an, die in Ihrem Desktop Analytics-Arbeitsbereich angezeigt werden sollen.  

    4. Sie stellen Kompatibilitätsupdates für alle Zielgeräte bereit.  

3. Geräte senden Diagnosedaten an den Microsoft-Diagnosedatenverwaltungsdienst für Windows. Alle Diagnosedaten werden über HTTPS verschlüsselt und während der Übertragung vom Gerät an diesen Dienst wird das Anheften von Zertifikaten genutzt. Der Microsoft-Diagnosedatenverwaltungsdienst wird in der USA gehostet.

      - Bei Anwendungs- und Kernelfehlern, nicht reagierenden Anwendungen und anderen anwendungsspezifischen Problemen wird die Windows-Fehlerberichterstattungs-API verwendet, um anwendungsspezifische Problemberichte an Microsoft zu senden. Ausführliche Informationen zu diesem Dataflow finden Sie unter [Using WER](https://docs.microsoft.com/windows/win32/wer/using-wer) (Verwenden der Windows-Fehlerberichterstattung).
      
4. Jeden Tag erzeugt Microsoft eine Momentaufnahme der IT-bezogenen Erkenntnisse. In dieser Momentaufnahme werden die Diagnosedaten von Windows mit Ihren Eingaben für die registrierten Geräte kombiniert. Dieser Vorgang erfolgt in einem vorübergehenden Speicher, der nur von Desktop Analytics verwendet wird. Der vorübergehende Speicher wird in Microsoft-Rechenzentren in den USA gehostet. Alle Daten werden über einen verschlüsselten SSL-Kanal (HTTPS) gesendet. Die Momentaufnahmen werden nach kommerzieller ID voneinander abgegrenzt.  

5. Anschließend werden die Momentaufnahmen in Ihren Azure Log Analytics-Arbeitsbereich kopiert. Diese Datenübertragung erfolgt über HTTPS über das Webhookerfassungsprotokoll, ein Feature von Log Analytics. Desktop Analytics verfügt über keine Lese- oder Schreibberechtigungen für Ihren Log Analytics-Speicher. Desktop Analytics ruft die Webhook-API mit einem SAS-URI (Shared Access Signature) auf. Anschließend ruft Log Analytics die Daten aus den Speichertabellen über HTTPS ab.

6. Desktop Analytics speichert Ihre Eingaben im Log Analytics-Speicher. Diese Konfigurationen umfassen Bereitstellungspläne und objektbezogene Entscheidungen hinsichtlich Upgrade und Wichtigkeit.  

## <a name="other-resources"></a>Weitere Ressourcen

Häufig gestellte, auf den Datenschutz bezogene Fragen zu Desktop Analytics werden in [Datenschutz – FAQ](faq.md#privacy) beantwortet.

Weitere Informationen zu datenschutzrelevanten Aspekten finden Sie in den folgenden Artikeln:

- [Windows und die DSGVO: Informationen für IT-Administratoren und Entscheidungsträger](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7, Windows 8, and Windows 8.1 appraiser diagnostic data events and fields](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields) (Appraiser-Diagnosedaten-Ereignisse und -Felder für Windows 7, Windows 8 und Windows 8.1)  

- [Windows10, Version1809 – einfache Windows-Diagnoseereignisse und -felder](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Erweiterte Windows 10-Diagnosedatenereignisse und Felder, die von Windows Analytics verwendet werden](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Fehlerberichterstattung zum Windows-Setup](https://docs.microsoft.com/windows/deployment/upgrade/windows-error-reporting)

- [Übersicht über den Diagnosedaten-Viewer](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Licensing terms and documentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) (Lizenzbedingungen und Dokumentation)  

- [Log Analytics-Datensicherheit](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Security and privacy at Microsoft Azure data centers](https://azure.microsoft.com/global-infrastructure/) (Sicherheit und Datenschutz in Microsoft Azure-Rechenzentren)  

- [Vertrauen Sie Ihrer Cloud](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Trust Center](https://www.microsoft.com/trustcenter)  

Unabhängig von Desktop Analytics sendet Configuration Manager Diagnose-und Verwendungsdaten an Microsoft. Microsoft verwendet diese Daten, um die Anwendungsinstallation, Qualität und Sicherheit künftiger Releases von Configuration Manager zu verbessern. Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten für Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).
