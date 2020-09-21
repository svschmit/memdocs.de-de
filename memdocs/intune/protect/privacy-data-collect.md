---
title: Datensammlung in Intune
titleSuffix: Microsoft Intune
description: Erfahren Sie mehr darüber, wie personenbezogene Daten in Intune gesammelt werden.
keywords: Datenschutz, personenbezogene Daten
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1171740-936d-46a5-af37-f418bd6fa63e
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcd7ff1ae51314bc57be2bed39c7fe8ca7114d82
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076106"
---
# <a name="data-collection-in-intune"></a>Datensammlung in Intune

Wenn Benutzer ihre unternehmenseigenen oder persönlichen Geräte über Intune registrieren, sammelt, verarbeitet und teilt Intune einige personenbezogene Daten. Damit unterstützt Intune Geschäftsvorgänge, die Geschäftsabwicklung mit Kunden sowie den Dienst allgemein. Intune sammelt personenbezogene Daten aus folgenden Quellen:

- Nutzung des Intune-Diensts im Microsoft Endpoint Manager Admin Center durch Administratoren.
- Endbenutzergeräte (während der Registrierung bei der Intune-Verwaltung sowie während der Nutzung).
- Kundenkonten bei Drittanbieterdiensten (gemäß Anweisungen des Administrators).
- Diagnose-, Leistungs- und Nutzungsinformationen.

Intune sammelt Informationen aus diesen Quellen in den folgenden beiden Kategorien: [Erforderlich](#required-data) und [Optional](#optional-data). In jeder dieser Kategorien werden die Daten weiter nach Kundendaten, personenbezogenen Daten, Diagnosedaten und durch den Dienst generierte Daten aufgeschlüsselt. 

> [!NOTE]
> Die von unserem Dienst gesammelten Daten werden keinesfalls an Dritte verkauft.

## <a name="required-data"></a>Erforderliche Daten

Daten in der Kategorie „Erforderlich“ sind Daten, die für die vom Kunden erwartete Funktionsweise unseres Diensts erforderlich sind. Die meisten von Intune gesammelten Daten fallen in diese Kategorie. Diese Daten werden an einen Benutzer, ein Gerät oder eine Anwendung gebunden und sind für die Verwaltung wichtig. Gesammelt werden sowohl personenbezogene als auch nicht personenbezogene Daten. Personenbezogene Daten können identifizierbare Daten sein, mit denen Endbenutzer direkt identifiziert werden können. Es können auch pseudonymisierte Daten sein, für die vom System ein eindeutiger Bezeichner generiert wird und die zum Bereitstellen des Unternehmensdiensts für die Benutzer verwendet werden. Auch Supportdaten und Kontodaten gehören zu dieser Kategorie. Nicht personenbezogene Daten umfassen vom Dienst generierte Systemmetadaten und Informationen zur Organisation bzw. zum Mandanten. Intune sammelt auch Daten zur Zugriffssteuerung, um den Zugriff auf administrative Rollen und Funktionen über Features wie die [rollenbasierte Zugriffssteuerung](../fundamentals/role-based-access-control.md) zu verwalten.

Zu den von Intune gesammelten erforderlichen Daten zählen unter anderem die folgenden: 

- Benutzerinformationen
  - Besitzername/Anzeigename des Benutzers (der in Azure registrierte Name des Benutzers, der durch die AzureUserID identifiziert wird)
  - Benutzerprinzipalname oder E-Mail-Adresse
  - Telefonnummer
  - Benutzer-IDs von Drittanbietern (z.B. Apple-ID)
- Hardwareinventurinformationen
  - Gerätename
  - Hersteller
  - Betriebssystem
  - Seriennummer
  - IMEI-Nummer
  - IP-Adresse
  - WLAN-MAC-Adresse
  - ICCID
- Überwachungsprotokollinformationen, einschließlich Daten zu folgenden Aktivitäten:
  - Verwalten
  - Erstellen
  - Aktualisieren (Bearbeiten)
  - Löschen
  - Zuweisen
  - Remoteaufgaben
- Supportinformationen
  - Kontaktinformationen (Name, Telefonnummer, E-Mail-Adresse)
  - E-Mail-Unterhaltungen mit Mitgliedern des Microsoft-Supportteams, -Produktteams oder des Teams für Benutzerzufriedenheit
- Informationen zur Zugriffssteuerung 
  - Statische Authentifikatoren (Kennwort des Kunden)
  - Datenschutzschlüssel für Zertifikate 
- Administrator- und Kontoinformationen
  - Vor- und Nachname des Administratorbenutzers
  - Administratorbenutzername
  - UPN (E-Mail)
  - Telefonnummer
  - E-Mail-Adresse des Kontobesitzers
  - Active Directory-ID jedes IT-Administrators des Kunden
  - Zahlungsdaten für die Kundenabrechnung
  - Abonnementschlüssel
- Anwendungsbestand, z.B.:
  - App-Name
  - -Version
  - App-ID
  - Größe
  - Installationspfad
  - Anwendungsbestandsdaten werden nur gesammelt, wenn das Gerät vom Administrator als unternehmenseigenes Gerät markiert wird oder das kompatible App-Feature aktiviert ist.  
- Mandanten-IDs von Drittanbietern des Kunden (z. B. die Apple-ID)
- Gerätedaten
  - Intune-Geräte-ID
  - Azure Active Directory-Geräte-ID
  - Intune-Geräteverwaltungs-ID
  - Mandanten-ID
  - Konto-ID
  - EAS-Geräte-ID
  - Plattformspezifische IDs
  - Apple-ID für iOS/iPadOS-Geräte
  - MAC-Adressen für Mac-Geräte
  - Windows-ID für Windows-Geräte
- Verwaltete Anwendungsinformationen
  - Verwaltete Anwendungs-ID
  - Gerätetag der verwalteten Anwendung
  - Intune-Geräteverwaltungs-ID
  - Azure Active Directory-Geräte-ID
  - Verschlüsselungsschlüssel
- Administratornutzungsdaten aller Intune-Mandanten (z.B. ausgewählte Administrator-Steuerelemente, wenn mit der Administratorkonsole interagiert wird)
- Informationen zum Mandantenkonto (diese Daten sind im Blatt „Intune“ verfügbar)
  - Die Anzahl der registrierten Geräte oder Benutzer
  - Die Anzahl der identifizierten Geräteplattformen  
  - Die Anzahl der installierten Geräte
  - installedDeviceCount: die Anzahl der Geräte, auf denen die Anwendung installiert ist
  - notApplicableDeviceCount: die Anzahl der Geräte, für die die Anwendung nicht verfügbar ist
  - notInstalledDeviceCount: die Anzahl der Geräte, für die die Anwendung zwar verfügbar, auf denen sie jedoch nicht installiert ist
  - pendingInstallDeviceCount: die Anzahl der Geräte, für die die Anwendung verfügbar ist und bei denen die Installation noch aussteht

## <a name="optional-data"></a>Optionale Daten

Daten in der Kategorie „Optional“ sind für die Nutzung des Produkts oder Dienst nicht essenziell. Kunden können die Sammlung optionaler Daten steuern. Intune ermöglicht es Kunden, die Sammlung von optionalen Daten zu aktivieren oder zu deaktivieren. Optionale Daten sind beispielsweise Daten, die Intune zu Diagnose- und Telemetriezwecken sammelt. Wir sind davon überzeugt, dass es gute Gründe dafür gibt, optionale Daten zu teilen, da dadurch neue und bessere Benutzererlebnisse geschaffen werden können. Wir wissen aber auch, wie wichtig es ist, Benutzern die Möglichkeit zu geben, diese Entscheidung selbst zu treffen. 

Optionale Diagnosedaten sind beispielsweise Daten zur Anwendungsnutzung sowie Fehler- und Leistungsdaten. Alle von Microsoft während der Verwendung einer Microsoft 365-App für Unternehmensanwendungen und -dienste gesammelten Daten werden gemäß der Definition in der Norm ISO/IEC 19944:2017 (Abschnitt 8.3.3) pseudonymisiert.

## <a name="certain-end-user-data-or-content-is-never-collected"></a>Bestimmte Endbenutzerdaten oder -inhalte werden niemals gesammelt

Intune sammelt folgende Daten von Endbenutzern nicht und erlaubt auch keinem Administrator, diese Daten anzuzeigen: Anruf- oder Webbrowserverlauf, persönliche E-Mails, Textnachrichten, Kontakte, Kennwörter für persönliche Konten, Kalenderveranstaltungen oder Fotos (einschließlich Fotos in einer Foto-App oder Kamera). Weitere Informationen finden Sie unter [Erste Schritte bei der Geräteregistrierung](../enrollment/device-enrollment.md).

Informationen zu Datentypen und -definitionen finden Sie unter [So kategorisiert Microsoft Daten in Onlinediensten](https://www.microsoft.com/trust-center/privacy/customer-data-definitions). 

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr darüber, wie Intune personenbezogene Daten [sichert und verarbeitet](privacy-data-store-process.md) und [freigibt](privacy-data-secure-share.md). 
