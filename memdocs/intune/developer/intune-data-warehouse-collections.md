---
title: Sammlungen von Intune Date Warehouse
titleSuffix: Microsoft Intune
description: Die Intune Data Warehouse-Sammlungen bieten Details im Zusammenhang mit der Data Warehouse-API.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29f09230-dc56-43db-b599-d961967bda49
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0a9ecebd86404d4218142d1a3acb591974b027d
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608094"
---
# <a name="intune-data-warehouse-collections"></a>Intune Data Warehouse-Sammlungen

Die folgenden Intune Data Warehouse-Sammlungen bieten die Eigenschaften, Beschreibungen und Beispiele für v1.0-Sammlungen der Data Warehouse-API-Entitäten. 

## <a name="apprevisions"></a>appRevisions
Die **appRevision**-Entität listet alle Versionen von Apps auf.

|          Eigenschaft          |                                      Beschreibung                                      |                Beispiel               |
|----------------------------|---------------------------------------------------------------------------------------|--------------------------------------|
| appKey                     | Eindeutiger Bezeichner der App                                                         | 123                                  |
| applicationId              | Eindeutiger Bezeichner einer App – ähnlich wie AppKey, dieser Schlüssel ist jedoch ein natürlicher Schlüssel.        | b66bc706-ffff-7437-0340-032819502773 |
| revision                   | Die Version, die vom Administrator beim Upload der Binärdatei erwähnt wurde.                   | 2                                    |
| title                      | Titel der App                                                                     | Excel                                |
| publisher                  | Herausgeber der App                                                                 | Microsoft                            |
| uploadState                | Hochladestatus der App                                                              | 1                                    |
| appTypeKey                 | Der Verweis zu AppType wird im folgenden Abschnitt beschrieben.                            | 1                                    |
| vppProgramTypeKey          | Der Verweis zu VppProgramType wird weiter unten beschrieben.                                        | 30876                                |
| creationTime               | Der Zeitpunkt, zu dem diese Revision erstellt wurde.                                            | 23.11.2016 0:00                      |
| modifiedTime               | Der letzte Zeitpunkt, zu dem eine Änderung an einem mit dieser Revision verknüpften Element vorgenommen wurde.                            | 23.11.2016 0:00                      |
| size                       | Größe der Binärdatei in Bytes.                                                          | 120.392.000                          |
| startDateInclusiveUTC      | UTC-Zeitpunkt der Erstellung dieser App-Revision in Data Warehouse.      | 23.11.2016 0:00                      |
| endDateExclusiveUTC        | UTC-Zeitpunkt, zu dem diese App-Revision als veraltet gekennzeichnet wurde.                        | 23.11.2016 0:00                      |
| isCurrent                  | Gibt an, ob diese App-Version in Data Warehouse aktuell ist.         | Wahr/falsch                           |
| rowLastModifiedDateTimeUTC | UTC-Zeitpunkt, zu dem diese App-Version zuletzt in Data Warehouse geändert wurde. | 23.11.2016 0:00                      |

## <a name="apptypes"></a>appTypes
Die Entität **appType** führt die Installationsquelle einer App auf.

|   Eigenschaft  |        Beschreibung        |
|-------------|---------------------------|
| appTypeID   | ID für den Typ           |
| appTypeKey  | Untergeordneter Schlüssel für den Schlüssel |
| appTypeName | App-Typ                  |

### <a name="example"></a>Beispiel

| AppTypeID |                Name               |                     Beschreibung                     |
|-----------|-----------------------------------|-----------------------------------------------------|
| 0         | Android Store-App               | Eine Android Store-App.                             |
| 1         | Android-Branchen-App                 | Eine branchenspezifische Android-App.                  |
| 2         | Verwaltete Android Store-App (MAM) | Eine Android Store-App, für die die Verwaltung aktiviert ist. |
| 3         | iOS Store-App                   | Eine iOS Store-App.                                 |
| 4         | Branchenspezifische iOS-App                     | Eine branchenspezifische iOS-App.                      |
| 5         | Verwaltete iOS Store-App (MAM)     | Eine iOS Store-App, die für die Verwaltung aktiviert ist.       |
| 6         | Microsoft 365 Apps for Enterprise        | Die Microsoft 365-Apps für Windows 10.     |
| 7         | Web-App                         | Eine Web-App.                                        |
| 8         | Windows Phone 8.1 Store-App     | Eine Windows Phone 8.1 Store-App.                    |
| 9         | Windows Store-App               | Eine Windows Store-App.                              |
| 10        | Branchenspezifische Windows-Apps                | Eine branchenspezifische Windows-APPX-App.              |
| 11        | Windows Mobile MSI              | Eine branchenspezifische MSI-App.                      |
| 12        | Branchenspezifische Windows Phone-App           | Eine branchenspezifische Windows Phone-App.             |

## <a name="compliancepolicystatusdeviceactivities"></a>compliancePolicyStatusDeviceActivities
In der folgenden Tabelle sind die Zuweisungsstatus der Konformitätsrichtlinien von Geräten zusammengefasst. Es ist die Anzahl der Geräte aufgeführt, die in jedem Konformitätszustand zu finden sind.

|    Eigenschaft   |                                                                                      Beschreibung                                                                                     |  Beispiel |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey       | Datumsschlüssel, der angibt, wann die Zusammenfassung für die Konformitätsrichtlinie erstellt wurde.                                                                                                                   | 20161204 |
| Unbekannt       | Anzahl der Geräte, die offline sind oder aus einem anderen Grund nicht mit Intune oder Azure AD kommunizieren können.                                                                           | 5        |
| notApplicable | Anzahl der Geräte, auf denen vom Administrator festgelegte Gerätekonformitätsrichtlinien nicht angewendet werden.                                                                                     | 201      |
| Kompatibel     | Anzahl der Geräte, für die mindestens eine vom Administrator festgelegte Gerätekompatibilitätsrichtlinie angewendet wurde.                                                                        | 4083     |
| inGracePeriod | Anzahl der Geräte, die nicht konform sind, sich aber in der vom Administrator definierten Toleranzperiode befinden.                                                                                  | 57       |
| nonCompliant  | Anzahl der Geräte, die mindestens eine vom Administrator festgelegte Einstellung der Gerätekompatibilitätsrichtlinie nicht anwenden konnten, oder bei denen der Benutzer gegen die vom Administrator festgelegten Richtlinien verstößt. | 43       |
|    error      |    Anzahl der Geräte, die nicht mit Intune oder Azure AD kommunizieren können und eine Fehlermeldung ausgeben.                                                                          |    3     |

## <a name="compliancepolicystatusdeviceperpolicyactivities"></a>compliancePolicyStatusDevicePerPolicyActivities
In der folgenden Tabelle sind die Zuweisungsstatus der Konformitätsrichtlinien von Geräten auf der Basis von Richtlinien und Richtlinientyp zusammengefasst. Es ist die Anzahl der Geräte aufgeführt, die in jedem Konformitätszustand für jede zugewiesene Konformitätsrichtlinie zu finden sind.

|      Eigenschaft     |                                                                                      Beschreibung                                                                                     |  Beispiel |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey           | Datumsschlüssel, der angibt, wann die Zusammenfassung für die Konformitätsrichtlinie erstellt wurde.                                                                                                                   | 20161219 |
| policyKey         | Schlüssel für die Konformitätsrichtlinie, für die die Zusammenfassung erstellt wurde.                                                                                                                   | 10178    |
| policyPlatformKey | Schlüssel für den Plattformtyp der Konformitätsrichtlinie, für den die Zusammenfassung erstellt wurde.                                                                                            | 5        |
| Unbekannt           | Anzahl der Geräte, die offline sind oder aus einem anderen Grund nicht mit Intune oder Azure AD kommunizieren können.                                                                           | 13       |
| notApplicable     | Anzahl der Geräte, auf denen vom Administrator festgelegte Gerätekonformitätsrichtlinien nicht angewendet werden.                                                                                     | 3        |
| Kompatibel         | Anzahl der Geräte, für die mindestens eine vom Administrator festgelegte Gerätekompatibilitätsrichtlinie angewendet wurde.                                                                        | 45       |
| inGracePeriod     | Anzahl der Geräte, die nicht konform sind, sich aber in der vom Administrator definierten Toleranzperiode befinden.                                                                                  | 3        |
| nonCompliant      | Anzahl der Geräte, die mindestens eine vom Administrator festgelegte Einstellung der Gerätekompatibilitätsrichtlinie nicht anwenden konnten, oder bei denen der Benutzer gegen die vom Administrator festgelegten Richtlinien verstößt. | 7        |
| error             | Anzahl der Geräte, die nicht mit Intune oder Azure AD kommunizieren können und eine Fehlermeldung ausgeben.                                                                             | 3        |
## <a name="compliancestates"></a>complianceStates

|      Eigenschaft      |                       Beschreibung                      |
|--------------------|--------------------------------------------------------|
| complianceStatus   | Konformitätsstatus von Geräten mit mdmStatusKey       |
| complianceStateKey | Konformitätsschlüssel gemäß des Geräte- und Konformitätsstatus |
| complianceStateID  | Die ID, die mit diesem Konformitätsstatus übereinstimmt                |

### <a name="example"></a>Beispiel

|  complianceStatus  |                       Beschreibung                      |
|--------------------|--------------------------------------------------------|
|    Unbekannt         |    Unbekannt                                                                        |
|    Kompatibel       |    Kompatibel.                                                                      |
|    Nicht richtlinienkonform    |       Gerät ist nicht konform und wird nicht in die Unternehmensressourcen einbezogen.             |
|    Konflikt        |    Konflikt mit anderen Regeln.                                                      |
|    Fehler           |       Fehler.                                                                       |
|    ConfigManager   |    Vom Configuration Manager verwaltet.                                                      |
|    InGracePeriod   |       Gerät ist nicht konform, hat aber immer noch Zugriff auf Unternehmensressourcen.          |

## <a name="dates"></a>Daten
Die **date**-Entität stellt Datumsangaben dar, die auf mehrere Data Warehouse-Entitäten verweisen.

|     Eigenschaft    |                       Beschreibung                      |    Beispiel    |
|-----------------|--------------------------------------------------------|---------------|
| dateKey         | Eindeutiger Bezeichner für dieses Datum im Data Warehouse | 20160703      |
| FullDate        | Dieses Datum wird im vollständigen Datums- und Uhrzeitformat dargestellt        | 3\.7.2016 0:00 |
| dayOfWeek       | Wochentag                                            | 1             |
| dayOfMonth      | Tag des Monats                                           | 3             |
| dayOfYear       | Tag des Jahres                                            | 185           |
| weekOfYear      | Woche des Jahres                                           | 28            |
| monthOfYear     | Monat des Jahres                                      | 7             |
| calendarQuarter | Kalenderquartal                                       | 3             |
| calendarYear    | Kalenderjahr                                          | 2016          |
| dateKey         | Eindeutiger Bezeichner für dieses Datum im Data Warehouse | 20160703      |
| FullDate        | Dieses Datum wird im vollständigen Datums- und Uhrzeitformat dargestellt        | 3\.7.2016 0:00 |
| dayOfWeek       | Wochentag                                            | 1             |
| dayOfMonth      | Tag des Monats                                           | 3             |
| dayOfYear       | Tag des Jahres                                            | 185           |
| weekOfYear      | Woche des Jahres                                           | 28            |
| monthOfYear     | Monat des Jahres                                      | 7             |
| calendarQuarter | Kalenderquartal                                       | 3             |
| calendarYear    | Kalenderjahr                                          | 2016          |

## <a name="devicecategories"></a>deviceCategories

|      Eigenschaft      |                                    Beschreibung                                   |                Beispiel               |
|--------------------|----------------------------------------------------------------------------------|--------------------------------------|
| deviceCategoryID   | Der eindeutige Bezeichner für die Gerätekategorie.                                       | fb415ba2-7c08-41f6-a5e5-685b50da2c4c |
| deviceCategoryKey  | Der eindeutige Bezeichner der Gerätekategorie im Data Warehouse – Ersatzschlüssel. | 1                                    |
| deviceCategoryName | Der Anzeigename für die Gerätekategorie.                                            | Smartphones                          |

## <a name="deviceconfigurationprofiledeviceactivities"></a>deviceConfigurationProfileDeviceActivities
Die Entität **DeviceConfigurationProfileDeviceActivity** listet die Anzahl der Geräte mit dem Zustand „erfolgreich“, „ausstehend“, „fehlerhaft“ oder „Fehler“ pro Tag auf. Die Anzahl gibt die Gerätekonfigurationsprofile an, die der Entität zugewiesen sind. Wenn ein Gerät beispielsweise den Zustand „erfolgreich“ für alle zugewiesenen Richtlinien aufweist, wird der Zähler für „erfolgreich“ für diesen Tag um eins erhöht. Wenn einem Gerät zwei Profile zugewiesen sind, von denen eines den Zustand „erfolgreich“ und eines den Zustand „Fehler“ aufweist, erhöht die Entität den Zähler für „erfolgreich“ und versetzt das Gerät in den Zustand „Fehler“. Die Entität listet für die letzten 30 Tage auf, wie viele Geräte an einem bestimmten Tag in welchem Zustand waren.

|  Eigenschaft |                                          Beschreibung                                          |  Beispiel |
|-----------|-----------------------------------------------------------------------------------------------|----------|
| dateKey   | Datumsschlüssel für den Zeitpunkt, zu dem das Einchecken des Gerätekonfigurationsprofils im Data Warehouse aufgezeichnet wurde. | 20160703 |
| pending   | Anzahl eindeutiger Geräte im Zustand „ausstehend“                                                    | 123      |
| Erfolgreich | Anzahl eindeutiger Geräte im Zustand „erfolgreich“                                                    | 12       |
| error     | Anzahl eindeutiger Geräte im Zustand „Fehler“                                                      | 10       |
| „Fehlgeschlagen“    | Anzahl eindeutiger Geräte im Zustand „fehlerhaft“                                                     | 2        |

## <a name="deviceconfigurationprofileuseractivities"></a>deviceConfigurationProfileUserActivities 
Die Entität **DeviceConfigurationProfileUserActivity** listet die Anzahl der Benutzer mit dem Zustand „erfolgreich“, „ausstehend“, „fehlerhaft“ oder „Fehler“ pro Tag auf. Die Anzahl gibt die Gerätekonfigurationsprofile an, die der Entität zugewiesen sind. Wenn ein Benutzer beispielsweise den Zustand „erfolgreich“ für alle zugewiesenen Richtlinien aufweist, wird der Zähler für „erfolgreich“ für diesen Tag um eins erhöht. Wenn einem Benutzer zwei Profile zugewiesen sind, von denen eines den Zustand „erfolgreich“ und eines den Zustand „Fehler“ aufweist, wird der Benutzer für den Zustand „Fehler“ gezählt. Die Entität **DeviceConfigurationProfileUserActivity** listet für die letzten 30 Tage auf, wie viele Benutzer an einem bestimmten Tag in welchem Zustand waren. 

| Eigenschaft  | Beschreibung  | Beispiel  |
|------------|----------------------------------------------------------------------------------------------|-----------|
| dateKey  | Date Key für den Zeitpunkt als das Einchecken der Gerätekonfigurationsprofile im Data Warehouse aufgezeichnet wurde  | 20160703  |
| pending  | Anzahl eindeutiger Benutzer im Zustand „ausstehend“  | 123  |
| Erfolgreich  | Anzahl eindeutiger Benutzer im Zustand „erfolgreich“  | 12  |
| error  | Anzahl eindeutiger Benutzer im Zustand „Fehler“  | 10  |
| „Fehlgeschlagen“  | Anzahl eindeutiger Benutzer im Zustand „fehlerhaft“  | 2  |

## <a name="devicepropertyhistories"></a>devicePropertyHistories

|          Eigenschaft          |                                                                                      Beschreibung                                                                                     |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dateKey                    | Verweis auf die Datumstabelle, die den Tag angibt                                                                                                                                          |
| deviceKey                  | Der eindeutige Bezeichner des Geräts im Data Warehouse – Ersatzschlüssel. Dies ist ein Verweis auf die Gerätetabelle, die die Intune-Geräte-ID enthält.                               |
| deviceName                 | Der Name des Geräts auf Plattformen, die das Benennen von Geräten ermöglichen. Auf anderen Plattformen wird von Intune einen Namen aus anderen Eigenschaften erstellt. Dieses Attribut kann nicht für alle Geräte zur Verfügung stehen. |
| deviceRegistrationStateKey | Schlüssel des Attributs für den Geräteregistrierungsstatus dieses Geräts.                                                                                                                    |
| ownerTypeKey               | Schlüssel des Besitzertypattributs für dieses Gerät: Unternehmen, persönlich oder unbekannt.                                                                                                  |
| managementStateKey         | Der Schlüssel des Verwaltungsstatus, der mit diesem Gerät verknüpft ist und den neuesten Zustand einer Remoteaktion angibt oder anzeigt, ob das Gerät per Jailbreak oder Rootzugriff manipuliert wurde.                                                |
| azureADRegistered          | Gibt an, ob das Gerät in Azure Active Directory registriert ist.                                                                                                                             |
| complianceStateKey         | Ein Schlüssel zum Konformitätsstatus.                                                                                                                                                            |
| oSVersion                  | Betriebssystemversion                                                                                                                                                                          |
| jailBroken                 | Gibt an, ob das Gerät mit Jailbreak oder Rooting manipuliert wurde.                                                                                                                                         |
| deviceCategoryKey          | Schlüssel des Gerätekategorieattributs für dieses Gerät.                                                                                                                                    |
| physicalMemoryInBytes      | Der physische Speicher in Bytes.                                                                                                                                    |
| totalStorageSpaceInBytes      | Gesamte Speicherkapazität in Bytes.                                                                                                                                    |


## <a name="deviceregistrationstates"></a>deviceRegistrationStates
Die Entität **DeviceRegistrationState** stellt den Registrierungstyp dar, auf den von anderen Data Warehouse-Sammlungen verwiesen wird. 

|           Eigenschaft          |                                     BESCHREIBUNG                                     |
|-----------------------------|-------------------------------------------------------------------------------------|
| deviceRegistrationStateID   | Der eindeutige Bezeichner für den Registrierungsstatus                                            |
| deviceRegistrationStateKey  | Der eindeutige Bezeichner des Registrierungsstatus im Data Warehouse – Ersatzschlüssel |
| deviceRegistrationStateName | Registrierungsstatus                                                                  |
|    notRegistered                     |    Nicht registriert                                                                                                                                                                  |
|    Registrierung                        |       Registriert                                                                                                                                                                   |
|    revoked                           |       Der Status bedeutet, dass der IT-Administrator den Client blockiert hat und der Client wieder freigegeben werden kann. Wenn ein Gerät zurückgesetzt oder außer Kraft gesetzt wurde, kann es auch den Status „Revoked“ anzeigen.        |
|    keyConflict                       |    Schlüsselkonflikt                                                                                                                                                                    |
|    approvalPending                   |    Ausstehende Genehmigung                                                                                                                                                                |
|    certificateReset                  |    Zertifikat zurücksetzen                                                                                                                                                               |
|    notRegisteredPendingEnrollment    |    Nicht registriert, Registrierung ausstehend                                                                                                                                               |
|    Unbekannt                           |    Unbekannter Status                                                                                                                                                                   |

## <a name="devices"></a>Geräte
In der Entität **device** werden alle für die Verwaltung registrierten Geräte und ihre entsprechenden Eigenschaften aufgelistet.

|          Eigenschaft          |                                                                                       Beschreibung                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| deviceKey                  | Der eindeutige Bezeichner des Geräts im Data Warehouse – Ersatzschlüssel.                                                                                                               |
| deviceId                   | Eindeutiger Bezeichner des Geräts.                                                                                                                                                     |
| deviceName                 | Der Name des Geräts auf Plattformen, die das Benennen von Geräten ermöglichen. Auf anderen Plattformen wird von Intune ein Name anhand anderer Eigenschaften erstellt. Dieses Attribut kann nicht für alle Geräte zur Verfügung stehen. |
| deviceTypeKey              | Schlüssel des Gerätetypattributs für dieses Gerät.                                                                                                                                    |
| deviceRegistrationState    | Schlüssel des Clientregistrierungsstatus-Attributs für dieses Gerät.                                                                                                                      |
| ownerTypeKey               | Schlüssel des Besitzertypattributs für dieses Gerät: Unternehmen, persönlich oder unbekannt.                                                                                                    |
| enrolledDateTime           | Zeitpunkt der Registrierung dieses Geräts.                                                                                                                                         |
| ethernetMacAddress           | Der eindeutige Netzwerkbezeichner dieses Geräts.                                                                                                                                         |
| lastSyncDateTime           | Letztes bekanntes Einchecken des Geräts mit Intune.                                                                                                                                              |
| managementAgentKey         | Der Schlüssel des Verwaltungs-Agents, der mit diesem Gerät verknüpft ist.                                                                                                                             |
| managementStateKey         | Der Schlüssel des Verwaltungsstatus, der mit diesem Gerät verknüpft ist und den neuesten Zustand einer Remoteaktion angibt oder anzeigt, ob das Gerät per Jailbreak oder Rootzugriff manipuliert wurde.                                                |
| azureADDeviceId            | Die Azure-Geräte-ID für dieses Gerät.                                                                                                                                                  |
| azureADRegistered          | Gibt an, ob das Gerät in Azure Active Directory registriert ist.                                                                                                                             |
| deviceCategoryKey          | Der Schlüssel der Kategorie, die mit diesem Gerät verknüpft ist.                                                                                                                                     |
| deviceEnrollmentType       | Der Schlüssel des Registrierungstyps, der mit diesem Gerät verknüpft ist und die Registrierungsmethode angibt.                                                                                             |
| complianceStateKey         | Der Schlüssel des Konformitätsstatus, der mit diesem Gerät verknüpft ist.                                                                                                                             |
| office365Version           | Die auf dem Gerät installierte Version von Microsoft 365.                                                                                                                             |
| oSVersion                  | Die Betriebssystemversion des Geräts.                                                                                                                                                |
| easDeviceId                | Exchange ActiveSync-ID des Geräts                                                                                                                                                  |
| serialNumber               | SerialNumber                                                                                                                                                                           |
| userId                     | Eindeutiger Bezeichner für den Benutzer, der dem Gerät zugeordnet ist.                                                                                                                           |
| rowLastModifiedDateTimeUTC | UTC-Zeitpunkt, zu dem dieses Gerät zuletzt in Data Warehouse geändert wurde.                                                                                                       |
| Hersteller               | Der Hersteller der CPU                                                                                                                                                             |
| model                      | Gerätemodell                                                                                                                                                                    |
| operatingSystem            | Betriebssystem des Geräts. Windows, iOS/iPadOS, Android usw.                                                                                                                                   |
| isDeleted                  | Binärwert, der anzeigt, ob das Gerät gelöscht wurde oder nicht.                                                                                                                                 |
| androidSecurityPatchLevel  | Android-Sicherheitspatchebene                                                                                                                                                           |
| mEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | Gibt an, ob das Gerät überwacht wird.                                                                                                                                                               |
| freeStorageSpaceInBytes    | Freier Speicherplatz in Bytes.                                                                                                                                                                 |
| encryptionState            | In diesem Feld wird der Verschlüsselungsstatus des Geräts angezeigt.                                                                                                                                                      |
| subscriberCarrier          | Netzbetreiber des Abonnenten des Geräts                                                                                                                                                       |
| phoneNumber                | Telefonnummer des Geräts                                                                                                                                                             |
| iMEI                       | IMEI                                                                                                                                                                                   |
| cellularTechnology         | Mobilfunktechnologie des Geräts                                                                                                                                                    |
| wiFiMacAddress             | WiFi-MAC-Adresse                                                                                                                                                                              |
| windowsOsEdition             | Windows-Betriebssystemedition                                                                                                                                                                              |


## <a name="devicetypes"></a>deviceTypes
Die Entität **deviceType** stellt den Gerätetyp dar, auf den von anderen Data Warehouse-Entitäten verwiesen wird. Der Gerätetyp beschreibt in der Regel entweder das Gerätemodell, den Hersteller oder eine Kombination aus beidem.

|    Eigenschaft    |                                  Beschreibung                                 |
|----------------|------------------------------------------------------------------------------|
| deviceTypeID   | Eindeutiger Bezeichner des Gerätetyps                                       |
| deviceTypeKey  | Der eindeutige Bezeichner des Gerätetyps im Data Warehouse – Ersatzschlüssel. |
| deviceTypeName | Gerätetyp                                                                |

### <a name="example"></a>Beispiel

| deviceTypeID |        Name       |                      BESCHREIBUNG                      |
|--------------|-------------------|-------------------------------------------------------|
| -1           | Nicht verfügbar   | Der Gerätetyp ist nicht verfügbar.                     |
| 0            | desktop-           | Windows Desktop-Gerät                              |
| 1            | Windows           | Windows-Gerät                                      |
| 2            | WinMO6            | Windows Mobile 6.0-Gerät                           |
| 3            | Nokia             | Nokia-Gerät                                        |
| 4            | WindowsPhone      | Windows Phone-Gerät                                |
| 5            | Mac               | Mac-Gerät                                          |
| 6            | WinCE             | Windows CE-Gerät                                   |
| 7            | WinEmbedded       | Windows Embedded-Gerät                             |
| 8            | IPhone            | iPhone-Gerät                                       |
| 9            | IPad              | iPad-Gerät                                         |
| 10           | IPod              | iPod-Gerät                                         |
| 11           | Android           | Mit dem Geräteadministrator verwaltetes Android-Gerät   |
| 12           | ISocConsumer      | iSoc Consumer-Gerät                                |
| 13           | Unix              | Unix-Gerät                                         |
| 14           | MacMDM            | OS X-Gerät, das mit dem integrierten MDM-Agent verwaltet wird |
| 15           | HoloLens          | HoloLens-Gerät                                       |
| 16           | SurfaceHub        | Surface Hub-Gerät                                  |
| 17           | AndroidForWork    | Android-Gerät, das mit dem Android-Profilbesitzer verwaltet wird  |
| 18           | AndroidEnterprise | Android Enterprise-Gerät.                          |
| 100          | BlackBerry        | Blackberry-Gerät                                   |
| 101          | Palm              | Palm-Gerät                                         |
| 255          | Unbekannt           | Unbekannter Gerätetyp                                 |

## <a name="deviceenrollmenttypes"></a>deviceEnrollmentTypes
Die Entität **deviceEnrollmentType** gibt an, wie ein Gerät registriert wurde. Der Registrierungstyp erfasst die Registrierungsmethode. In den Beispielen werden die verschiedenen Registrierungstypen und ihre Bedeutung aufgelistet.

|         Eigenschaft         |                                    Beschreibung                                    |
|--------------------------|-----------------------------------------------------------------------------------|
| deviceEnrollmentTypeID   | Der eindeutige Bezeichner des Registrierungstyps.                                       |
| deviceEnrollmentTypeKey  | Eindeutiger Bezeichner des Registrierungstyps im Data Warehouse – Ersatzschlüssel. |
| deviceEnrollmentTypeName | Registrierungstypname.                                                           |

### <a name="example"></a>Beispiel

| enrollmentTypeID |                Name                |                                        BESCHREIBUNG                                       |
|------------------|------------------------------------|------------------------------------------------------------------------------------------|
| 0                | Unbekannt                            | Registrierungstyp wurde nicht gesammelt                                                      |
| 1                | UserEnrollment                     | Benutzergesteuerte Registrierung über BYOD-Kanal.                                           |
| 2                | DeviceEnrollmentManager            | Benutzerregistrierung mit einem Geräteregistrierungs-Manager-Konto.                              |
| 3                | AppleBulkWithUser                  | Apple-Massenregistrierung mit Benutzer-Captcha. (DEP, Apple Configurator)                   |
| 4                | AppleBulkWithoutUser               | Apple-Massenregistrierung ohne Benutzer-Captcha.   (DEP, Apple Configurator, Mobile Config) |
| 5                | WindowsAzureADJoin                 | Windows 10-Azure AD-Join.                                                                |
| 6                | WindowsBulkUserless                | Windows 10-Massenregistrierung über ICD mit Zertifikat.                               |
| 7                | WindowsAutoEnrollment              | Automatische Windows 10-Registrierung.   (Geschäftskonto hinzufügen)                                    |
| 8                | WindowsBulkAzureDomainJoin         | Windows 10-Massen-Azure AD-Join.                                                           |
| 9                | WindowsCoManagement                | Von AutoPilot oder Gruppenrichtlinie ausgelöste Windows 10 Co-Verwaltung.                       |
| 10               | WindowsAzureADJoinsUsingDeviceAuth | Windows 10-Azure AD-Join mit Geräteauthentifizierung.                                            |

## <a name="enrollmentactivities"></a>enrollmentActivities 
Die Entität **enrollmentActivity** gibt die Aktivität einer Geräteregistrierung an.

| Eigenschaft                      | Beschreibung                                                               |
|-------------------------------|---------------------------------------------------------------------------|
| dateKey                       | Der Schlüssel des Datums, an dem diese Registrierungsaktivität aufgezeichnet wurde.               |
| deviceEnrollmentTypeKey       | Der Schlüssel des Typs der Registrierung.                                        |
| deviceTypeKey                 | Der Schlüssel des Gerätetyps.                                                |
| enrollmentEventStatusKey      | Der Schlüssel des Status, der auf eine erfolgreiche bzw. fehlgeschlagene Registrierung hinweist.    |
| enrollmentFailureCategoryKey  | Der Schlüssel der Kategorie des Registrierungsfehlers (bei fehlgeschlagener Registrierung).        |
| enrollmentFailureReasonKey    | Der Schlüssel des Grunds des Registrierungsfehlers (bei fehlgeschlagener Registrierung).          |
| osVersion                     | Die Betriebssystemversion des Geräts.                               |
| count                         | Die Gesamtanzahl der Registrierungsaktivitäten, die den oben genannten Klassifizierungen entsprechen.  |

## <a name="enrollmenteventstatuses"></a>enrollmentEventStatuses 
Die Entität **enrollmentEventStatus** gibt das Ergebnis einer Geräteregistrierung an.

| Eigenschaft                   | Beschreibung                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| enrollmentEventStatusKey   | Eindeutiger Bezeichner des Registrierungsstatus im Data Warehouse (Ersatzschlüssel).  |
| enrollmentEventStatusName  | Die Bezeichnung des Registrierungsstatus. Siehe folgende Beispiele.                            |

### <a name="example"></a>Beispiel

| enrollmentEventStatusName  | BESCHREIBUNG                            |
|----------------------------|----------------------------------------|
| Erfolgreich                    | Eine erfolgreiche Geräteregistrierung.         |
| Failed                     | Eine fehlerhafte Geräteregistrierung.             |
| Nicht verfügbar              | Der Registrierungsstatus ist nicht verfügbar.  |

## <a name="enrollmentfailurecategories"></a>enrollmentFailureCategories 
Die Entität **enrollmentFailureCategory** gibt an, warum eine Geräteregistrierung fehlgeschlagen ist. 

| Eigenschaft                       | Beschreibung                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------|
| enrollmentFailureCategoryKey   | Eindeutiger Bezeichner der Fehlerkategorie für die Registrierung im Data Warehouse (Ersatzschlüssel).  |
| enrollmentFailureCategoryName  | Der Name der Fehlerkategorie für die Registrierung. Siehe folgende Beispiele.                            |

### <a name="example"></a>Beispiel

| enrollmentFailureCategoryName   | Beschreibung                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------|
| Nicht zutreffend                  | Die Fehlerkategorie für die Registrierung ist nicht anwendbar.                                                            |
| Nicht verfügbar                   | Die Fehlerkategorie für die Registrierung ist nicht verfügbar.                                                             |
| Unbekannt                         | Unbekannter Fehler.                                                                                                |
| Authentifizierung                  | Fehler bei der Authentifizierung.                                                                                        |
| Autorisierung                   | Aufruf war authentifiziert, aber nicht für eine Registrierung autorisiert.                                                         |
| AccountValidation               | Fehler beim Überprüfen des Kontos für die Registrierung. (Konto gesperrt, Registrierung nicht aktiviert)                      |
| UserValidation                  | Benutzer konnte nicht überprüft werden. (Benutzer ist nicht vorhanden, fehlende Lizenz)                                           |
| DeviceNotSupported              | Das Gerät wird für die mobile Geräteverwaltung nicht unterstützt.                                                         |
| InMaintenance                   | Das Konto befindet sich im Wartungsmodus.                                                                                    |
| BadRequest                      | Der Client hat eine Anforderung gesendet, die vom Dienst nicht verstanden bzw. unterstützt wird.                                        |
| FeatureNotSupported             | Die von dieser Registrierung verwendeten Features werden für dieses Konto nicht unterstützt.                                        |
| EnrollmentRestrictionsEnforced  | Vom Administrator konfigurierte Registrierungseinschränkungen haben diese Registrierung blockiert.                                          |
| ClientDisconnected              | Für den Client gab es eine Zeitüberschreitung, oder die Registrierung wurde vom Endbenutzer abgebrochen.                                                        |
| UserAbandonment                 | Die Registrierung wurde vom Endbenutzer vorzeitig beendet. (Der Endbenutzer hat mit dem Onboarding begonnen, aber dieses nicht rechtzeitig abgeschlossen.)  |

## <a name="enrollmentfailurereasons"></a>enrollmentFailureReasons  
Die Entität **enrollmentFailureReason** gibt eine ausführlichere Ursache für einen Fehler bei der Geräteregistrierung innerhalb einer Fehlerkategorie an.  

| Eigenschaft                     | Beschreibung                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------|
| enrollmentFailureReasonKey   | Eindeutiger Bezeichner für die Fehlerursache bei der Registrierung im Data Warehouse (Ersatzschlüssel).  |
| enrollmentFailureReasonName  | Die Bezeichnung der Fehlerursache bei der Registrierung. Siehe folgende Beispiele.                            |

### <a name="example"></a>Beispiel

| enrollmentFailureReasonName      | Beschreibung                                                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nicht zutreffend                   | Die Fehlerursache für die Registrierung ist nicht anwendbar.                                                                                                                                                       |
| Nicht verfügbar                    | Die Fehlerursache für die Registrierung ist nicht verfügbar.                                                                                                                                                        |
| Unbekannt                          | Unbekannter Fehler.                                                                                                                                                                                         |
| UserNotLicensed                  | Der Benutzer wurde nicht in Intune gefunden oder verfügt über keine gültige Lizenz.                                                                                                                                     |
| UserUnknown                      | Der Benutzer ist Intune nicht bekannt.                                                                                                                                                                           |
| BulkAlreadyEnrolledDevice        | Nur ein Benutzer kann ein Gerät registrieren. Dieses Gerät wurde zuvor von einem anderen Benutzer registriert.                                                                                                                |
| EnrollmentOnboardingIssue        | Die Intune-Autorität für die mobile Geräteverwaltung (MDM) ist noch nicht konfiguriert.                                                                                                                                 |
| AppleChallengeIssue              | Die Installation des iOS-Verwaltungsprofils hat sich verzögert oder war fehlerhaft.                                                                                                                                         |
| AppleOnboardingIssue             | Für die Registrierung in Intune ist ein Apple-MDM-Pushzertifikat erforderlich.                                                                                                                                       |
| DeviceCap                        | Der Benutzer hat versucht, mehr Geräte zu registrieren, als maximal zulässig sind.                                                                                                                                        |
| AuthenticationRequirementNotMet  | Der Intune-Registrierungsdienst konnte diese Anforderung nicht autorisieren.                                                                                                                                            |
| UnsupportedDeviceType            | Das Gerät erfüllt nicht die Mindestanforderungen für die Intune-Registrierung.                                                                                                                                  |
| EnrollmentCriteriaNotMet         | Dieses Gerät konnte aufgrund einer konfigurierten Regel zur Einschränkung von Registrierungen nicht registriert werden.                                                                                                                          |
| BulkDeviceNotPreregistered       | IMEI (International Mobile Equipment Identifier) oder Seriennummer des Geräts wurde nicht gefunden.  Ohne diesen Bezeichner werden Geräte als persönliche Geräte erkannt, die zurzeit gesperrt sind.  |
| FeatureNotSupported              | Der Benutzer hat versucht, auf eine Funktion zuzugreifen, die noch nicht für alle Kunden freigegeben oder nicht mit Ihrer Intune-Konfiguration kompatibel ist.                                                            |
| UserAbandonment                  | Die Registrierung wurde vom Endbenutzer vorzeitig beendet. (Der Endbenutzer hat mit dem Onboarding begonnen, aber dieses nicht rechtzeitig abgeschlossen.)                                                                                           |
| APNSCertificateExpired           | Apple-Geräte können nicht mit einem abgelaufenen Apple-MDM-Pushzertifikat verwaltet werden.                                                                                                                            |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions
Die **intuneManagementExtension** listet täglich den Integritätsstatus von **intuneManagementExtension** auf jedem Windows 10-Gerät auf. Die Daten der letzten 60 Tage werden aufbewahrt.

|       Eigenschaft      |                          BESCHREIBUNG                          | Beispiel |
|---------------------|---------------------------------------------------------------|---------|
| dateKey             | Eindeutiger Datumsbezeichner                                | 123     |
| tenantKey           | Eindeutiger Mandantenbezeichner                              | 456     |
| deviceKey           | Eindeutiger Bezeichner des Geräts                              | 789     |
| extensionVersionKey | Eindeutiger Bezeichner für die IntuneManagementExtension-Version. | 1       |
| extensionStateKey   | Eindeutiger Bezeichner des Integritätszustands                            | 2       |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates
**intuneManagementExtensionHealthState** listet alle möglichen Status der **IntuneManagementExtension** auf.

|      Eigenschaft     |                   BESCHREIBUNG                  | Beispiel |
|-------------------|------------------------------------------------|---------|
| extensionStateKey | Eindeutiger Bezeichner des Integritätszustands.           | 2       |
| extensionState    | Der Integritätsstatus einer IntuneManagementExtension. | Healthy |

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions
Die Entität **IntuneManagementExtensionVersion** listet alle von **IntuneManagementExtension** verwendeten Versionen auf.

|       Eigenschaft      |                          BESCHREIBUNG                          | Beispiel |
|---------------------|---------------------------------------------------------------|---------|
| extensionVersionKey | Eindeutiger Bezeichner für die IntuneManagementExtension-Version. | 1       |
| extensionVersion    | Die vierstellige Versionsnummer                                   | 1.0.2.0 |

## <a name="mamapplications"></a>MamApplications

Die Entität **MamApplication** führt branchenspezifische Apps (LOB, Line-of-Business) auf, die über die Verwaltung mobiler Geräte (MAM) ohne Registrierung in Ihrem Unternehmen verwaltet werden.

| Eigenschaft | BESCHREIBUNG | Beispiel |
|---------|------------|--------|
| mamApplicationKey |Eindeutiger Bezeichner der MAM-Anwendung. | 432 |
| mamApplicationName |Name der MAM-Anwendung. |Beispielname für MAM-Anwendung |
| mamApplicationId |Anwendungs-ID der MAM-Anwendung. | 123 |
| isDeleted |Gibt an, ob dieser MAM-App-Datensatz aktualisiert wurde <br>Wahr: MAM-App verfügt über einen neuen Datensatz mit aktualisierten Feldern in dieser Tabelle. <br>Falsch: der neueste Datensatz für diese MAM-App. |Wahr/falsch |
| startDateInclusiveUTC |Datum und Uhrzeit in UTC, als diese MAM-App im Data Warehouse erstellt wurde |23.11.2016 12:00:00 Uhr |
| deletedDateUTC |Datum und Uhrzeit in UTC, als IsDeleted in TRUE geändert wurde |23.11.2016 12:00:00 Uhr |
| rowLastModifiedDateTimeUTC |Datum und Uhrzeit in UTC, als diese MAM-App zuletzt im Data Warehouse geändert wurde |23.11.2016 12:00:00 Uhr |


## <a name="mamapplicationinstances"></a>MamApplicationInstances

Die Entität **MamApplicationInstance** führt verwaltete MAM-Apps (Mobile Application Management, Verwaltung von mobilen Anwendungen) als Singularinstanz pro Benutzer pro Gerät auf. Alle aufgeführten Benutzer und Geräte in der Entität sind geschützt, d.h., ihnen wurde mindestens eine MAM-Richtlinie zugewiesen.


|          Eigenschaft          |                                                                                                  BESCHREIBUNG                                                                                                  |               Beispiel                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   applicationInstanceKey   |                                                               Eindeutiger Bezeichner für die MAM-App-Instanz im Data Warehouse – Ersatzschlüssel                                                                |                 123                  |
|           userId           |                                                                              Benutzer-ID des Benutzers, der diese MAM-App installiert hat                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   applicationInstanceId    |                                              Eindeutiger Bezeichner der MAM-App-Instanz – ähnlich wie ApplicationInstanceKey, jedoch ist der Bezeichner ein natürlicher Schlüssel                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | Anwendungs-ID der MAM-Anwendung, die für die diese MAM-Anwendungsinstanz erstellt wurde.   | 23.11.2016 12:00:00 Uhr   |
|     applicationVersion     |                                                                                     Anwendungsversion dieser MAM-App                                                                                      |                  2                   |
|        createdDate         |                                                                 Datum, als dieser Datensatz der MAM-App-Instanz erstellt wurde. Der Wert kann NULL sein.                                                                 |        23.11.2016 12:00:00        |
|          platform          |                                                                          Plattform des Geräts, auf dem diese MAM-App installiert wurde                                                                           |                  2                   |
|      platformVersion       |                                                                      Plattformversion des Geräts, auf dem diese MAM-App installiert wurde                                                                       |                 2.2                  |
|         sdkVersion         |                                                                            Die Version des MAM SDKs, mit der diese MAM-App umschlossen wurde                                                                            |                 3.2                  |
| mamDeviceId | Geräte-ID des Geräts, dem die MAM-Anwendungsinstanz zugeordnet ist.   | 23.11.2016 12:00:00 Uhr   |
| mamDeviceType | Gerätetyp des Geräts, dem die MAM-Anwendungsinstanz zugeordnet ist.   | 23.11.2016 12:00:00 Uhr   |
| mamDeviceName | Gerätename des Geräts, dem die MAM-Anwendungsinstanz zugeordnet ist.   | 23.11.2016 12:00:00 Uhr   |
|         isDeleted          | Gibt an, ob dieser Datensatz der MAM-App-Instanz aktualisiert wurde <br>Wahr: Diese MAM-App-Instanz verfügt über einen neuen Datensatz mit aktualisierten Feldern in dieser Tabelle. <br>Falsch: der neueste Datensatz für diese MAM-App-Instanz. |              Wahr/falsch              |
|   startDateInclusiveUtc    |                                                              Datum und Uhrzeit in UTC, als diese MAM-App-Instanz im Data Warehouse erstellt wurde                                                               |        23.11.2016 12:00:00 Uhr        |
|       deletedDateUtc       |                                                                             Datum und Uhrzeit in UTC, als IsDeleted in TRUE geändert wurde                                                                              |        23.11.2016 12:00:00 Uhr        |
| rowLastModifiedDateTimeUtc |                                                           Datum und Uhrzeit in UTC, als diese MAM-App-Instanz im Data Warehouse zuletzt geändert wurde                                                            |        23.11.2016 12:00:00 Uhr        |

## <a name="mamcheckins"></a>MamCheckins

Die Entität **MamCheckin** stellt Daten dar, die gesammelt wurden, als eine MAM-App-Instanz sich bei Intune Service gemeldet hat. 

> [!Note]  
> Wenn eine App-Instanz sich mehrmals pro Tag meldet, speichert das Data Warehouse dies als einmalige Anmeldung.

| Eigenschaft | BESCHREIBUNG | Beispiel |
|---------|------------|--------|
| dateKey |Date Key für den Zeitpunkt als das Einchecken der MAM-App im Data Warehouse aufgezeichnet wurde | 20160703 |
| applicationInstanceKey |Schlüssel der App-Instanz, der diesem Eincheckvorgang der MAM-App zugeordnet wird | 123 |
| userKey |Schlüssel des Benutzers, der diesem Eincheckvorgang der MAM-App zugeordnet wird | 4323 |
| mamApplicationKey |Anwendungsschlüssel der Anwendung, die dem Einchecken der MAM-Anwendung zugeordnet ist. | 432 |
| deviceHealthKey |Schlüssel von DeviceHealth, der diesem Eincheckvorgang der MAM-App zugeordnet wird | 321 |
| platformKey |Stellt die Plattform des Geräts dar, die diesem Eincheckvorgang der MAM-App zugeordnet wird |123 |
| lastCheckInDate |Datum und Uhrzeit, wann diese MAM-App zuletzt eingecheckt wurde. Der Wert kann NULL sein. |23.11.2016 12:00:00 Uhr |

## <a name="mamdevicehealths"></a>MamDeviceHealths

Die Entität **MamDeviceHealth** stellt Geräte dar, die bereitgestellte MAM-Richtlinien besitzen, auch wenn sie per Jailbreak manipuliert wurden.

| Eigenschaft | BESCHREIBUNG | Beispiel |
|---------|------------|--------|
| deviceHealthKey |Eindeutiger Bezeichner des Geräts, der der Integrität im Data Warehouse zugeordnet wird – Ersatzschlüssel |123 |
| deviceHealth |Eindeutiger Bezeichner des Geräts und dessen Integrität – ähnlich wie DeviceHealthKey, allerdings ist der Bezeichner ein natürlicher Schlüssel |b66bc706-ffff-7777-0340-032819502773 |
| deviceHealthName |Stellt den Status des Geräts dar. <br>Nicht verfügbar – keine Informationen zu diesem Gerät. <br>Fehlerfrei: Gerät wurde nicht per Jailbreak manipuliert. <br>Nicht Fehlerfrei: Gerät wurde per Jailbreak manipuliert. |Nicht verfügbar fehlerfrei nicht fehlerfrei |
| rowLastModifiedDateTimeUtc |Datum und Uhrzeit in UTC, als diese bestimmte MAM-Geräteintegrität im Data Warehouse zuletzt geändert wurde |23.11.2016 12:00:00 Uhr |

## <a name="mamplatforms"></a>MamPlatforms

Die Entität **MamPlatform** führt Plattformnamen und -typen auf, auf denen eine MAM-App installiert wurde.


|          Eigenschaft          |                                    BESCHREIBUNG                                    |                         Beispiel                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        platformKey         |     Eindeutiger Bezeichner für die Plattform im Data Warehouse – Ersatzschlüssel      |                           123                           |
|          platform          | Eindeutiger Bezeichner der Plattform – ähnlich wie PlatformKey, es handelt sich allerdings um einen natürlichen Schlüssel |                           123                           |
|        platformName        |                                   Plattformname                                   | Nicht verfügbar <br>Keine <br>Windows <br>IOS <br>Android: |
| rowLastModifiedDateTimeUtc | Datum und Uhrzeit in UTC, als diese Plattform zuletzt im Data Warehouse geändert wurde  |                 23.11.2016 12:00:00 Uhr                  |

## <a name="managementagenttypes"></a>managementAgentTypes
Die Entität **managementAgentType** stellt die Agents dar, die zum Verwalten von Geräten verwendet werden.

|         Eigenschaft        |                                       Beschreibung                                       |
|-------------------------|-----------------------------------------------------------------------------------------|
| managementAgentTypeID   | Eindeutige Bezeichner des Verwaltungs-Agent-Typen                                         |
| managementAgentTypeKey  | Eindeutiger Bezeichner des Verwaltungs-Agent-Typen im Data Warehouse – Ersatzschlüssel. |
| managementAgentTypeName | Gibt an, welche Art von Agent zum Verwalten des Geräts verwendet wird                              |

### <a name="example"></a>Beispiel

| ManagementAgentTypeID |                Name               |                                  BESCHREIBUNG                                 |
|-----------------------|-----------------------------------|------------------------------------------------------------------------------|
| 1                     | EAS                               | Das Gerät wird mithilfe von Exchange Active Sync verwaltet.                         |
| 2                     | MDM                               | Das Gerät wird mit einem MDM-Agent verwaltet.                                   |
| 3                     | EasMdm                            | Das Gerät wird sowohl von Exchange Active Sync als auch einem MDM-Agent verwaltet.        |
| 4                     | IntuneClient                      | Das Gerät wird vom Intune-PC-Agent verwaltet.                               |
| 5                     | EasIntuneClient                   | Das Gerät wird sowohl von Exchange ActiveSync als auch vom Intune-PC-Agent verwaltet. |
| 8                     | ConfigManagerClient               | Das Gerät wird vom Configuration Manager-Agent verwaltet.     |
| 10                    | ConfigurationManagerClientMdm     | Das Gerät wird vom Configuration Manager und MDM verwaltet.                    |
| 11                    | ConfigurationManagerCLientMdmEas  | Das Gerät wird von Configuration Manager, MDM und Exchange Active Sync verwaltet.               |
| 16                    | Unbekannt                           | Unbekannter Verwaltungs-Agent-Typ                                              |
| 32                    | Jamf                              | Die Geräteattribute werden von Jamf abgerufen.                               |
| 64                    | GoogleCloudDevicePolicyController |  Das Gerät wird von CloudDPC von Google verwaltet.                                 |

## <a name="managementstates"></a>managementStates
Die Entität **managementState** stellt Details zum Status des Geräts bereit. Details können nützlich sein, wenn Remoteaktionen angewendet werden, das Gerät per Jailbreak oder Rootzugriff manipuliert wurde.

|       Eigenschaft      |                                     Beschreibung                                    |
|---------------------|------------------------------------------------------------------------------------|
| managementStateID   | Der eindeutige Bezeichner des Verwaltungsstatus.                                       |
| managementStateKey  | Der eindeutige Bezeichner des Verwaltungsstatus im Data Warehouse – Ersatzschlüssel. |
| managementStateName | Gibt den Status der Remoteaktion an, die auf dieses Gerät angewendet wurde.                 |

### <a name="example"></a>Beispiel

| managementStateID |      Name      |                                                   BESCHREIBUNG                                                   |
|-------------------|----------------|-----------------------------------------------------------------------------------------------------------------|
| 0                 | Verwaltet        | Verwaltet ohne ausstehende Remoteaktionen.                                                                       |
| 1                 | RetirePending  | Für das Gerät steht ein Befehl zum Außerkraftsetzen aus.                                                             |
| 2                 | RetireFailed   | Der Befehl zum Außerkraftsetzen konnte auf dem Gerät nicht ausgeführt werden.                                                                      |
| 3                 | WipePending    | Für das Gerät steht ein Zurücksetzungsbefehl aus.                                                               |
| 4                 | WipeFailed     | Der Zurücksetzungsbefehl konnte auf dem Gerät nicht ausgeführt werden.                                                                        |
| 5                 | Unhealthy      | Fehlerhafter Zustand.                                                                                              |
| 6                 | DeletePending  | Für das Gerät steht ein Löschungsbefehl aus.                                                             |
| 7                 | RetireIssued   | Ein Befehl zum Außerkraftsetzen wurde an das Gerät ausgegeben.                                                               |
| 8                 | WipeIssued     | Ein Zurücksetzungsbefehl wurde ausgegeben.                                                                               |
| 9                 | WipeCanceled   | Ein Zurücksetzungsbefehl wurde abgebrochen.                                                                               |
| 10                | RetireCanceled | Ein Befehl zum Außerkraftsetzen wurde abgebrochen.                                                                             |
| 11                | Discovered     | Das Gerät wird von Intune neu ermittelt und erhält beim ersten Einchecken den Status „Verwaltet“. |

## <a name="mobileappinstallstates"></a>mobileAppInstallStates
Die Entität MobileAppInstallState stellt den Installationsstatus für eine mobile Anwendung dar, nachdem sie einer Gruppe, die Geräte und/oder Benutzer enthält, zugewiesen wurde.

|       Eigenschaft      |                        Beschreibung                       |
|---------------------|----------------------------------------------------------|
| appInstallStateKey  | Die eindeutige ID des App-Installationsstatus für Ihr Konto |
| appInstallState     | Enumerationswert des App-Installationsstatus                     |
| appInstallStateName | Name des App-Installationsstatus                           |

## <a name="mobileappinstallstatuscounts"></a>mobileAppInstallStatusCounts
Stellt den Installationsstatus einer mobilen App für einen bestimmten Gerätetyp unter Verwendung der mobilen Anwendungsverwaltung mit Microsoft Intune dar.

|      Eigenschaft      |                                                          Beschreibung                                                          |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------|
| dateKey            | Schlüssel des Datums, an dem der App-Installationsstatus erfasst wurde                                                                     |
| appKey             | Schlüssel der mobilen App, mit der eine Instanz von AppRevision identifiziert wird.                                                          |
| deviceTypeKey      | Schlüssel des Gerätetyps, der der mobilen Anwendung zugeordnet ist.                                                              |
| appInstallStateKey | Schlüssel des App-Installationsstatus, der zur Identifizierung einer Instanz von MobileAppInstallState verwendet wird.                                         |
| errorCode          | Der vom App-Installer zurückgegebene Fehlercode, die mobile Plattform oder der Dienst zur Installation der App. |
| count              | Gesamtanzahl.                                                                                                                  |

## <a name="ownertypes"></a>ownerTypes
Die Entität **ownerType** gibt an, ob ein Gerät einem Unternehmen oder einer Privatperson gehört, oder ob der Besitzer unbekannt ist.

|    Eigenschaft   |                                                                                     BESCHREIBUNG                                                                                    |           Beispiel          |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| ownerTypeID   | Eindeutiger Bezeichner des Besitzertyps                                                                                                                                               |                            |
| ownerTypeKey  | Eindeutiger Bezeichner des Besitzertyps im Data Warehouse – Ersatzschlüssel.                                                                                                       |                            |
| ownerTypeName | Stellt den Besitzertypen der Geräte dar:  Corporate (Unternehmen): Das Gerät gehört einem Unternehmen.  Persönlich: Das Gerät befindet sich im Privatbesitz (BYOD).   Unbekannt: Es liegen keine Informationen zu diesem Gerät vor. | Corporate Personal Unknown |

> [!Note]  
> Für den Filter `ownerTypeName` in AzureAD müssen Sie beim Erstellen dynamischer Gruppen für Geräte den Wert `deviceOwnership` als `Company` festlegen. Weitere Informationen finden Sie unter [Regeln für Geräte](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices). 

## <a name="policies"></a>Richtlinien
Die Entität **Policy** (Richtlinie) listet Gerätekonfigurationsprofile, Appkonfigurationsprofile und Kompatibilitätsrichtlinien auf. Sie können die Richtlinien mit der mobilen Geräteverwaltung (MDM) zu einer Gruppe in Ihrem Unternehmen zuweisen.

|          Eigenschaft          |                                                                       BESCHREIBUNG                                                                      |                Beispiel               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| policyKey                  | Eindeutiger Schlüssel, der die Richtlinie im Data Warehouse darstellen soll                                                                                              | 123                                  |
| policyId                   | Eindeutiger Bezeichner der Richtlinie im Data Warehouse                                                                                                 | b66bc706-ffff-7437-0340-032819502773 |
| policyName                 | Name der Richtlinie                                                                                                                                    | "Windows 10-Baseline"                |
| policyVersion              | Version der Richtlinie Wenn die Richtlinie bearbeitet oder geändert wird, wird eine neuere Version erstellt.                                                             | 1, 2, 3                              |
| isDeleted                  | Gibt an, ob der Richtliniendatensatz aktualisiert wurde.  Wahr: Richtlinie verfügt über einen neuen Datensatz mit aktualisierten Feldern.  Falsch: Der neueste Datensatz für die Richtlinie. | Wahr/falsch                           |
| startDateInclusiveUTC      | UTC-Zeitpunkt, zu dem diese Richtlinie im Data Warehouse erstellt wurde.                                                                              | 23.11.2016 0:00                      |
| deletedDateUTC             | Datum und Uhrzeit in UTC, als IsDeleted in TRUE geändert wurde                                                                                                   | 23.11.2016 0:00                      |
| rowLastModifiedDateTimeUTC | UTC-Zeitpunkt, zu dem die Richtlinie zuletzt im Data Warehouse geändert wurde.                                                                        | 23.11.2016 0:00                      |

## <a name="policydeviceactivities"></a>policyDeviceActivities
In der folgenden Tabelle ist die Anzahl der Geräte mit dem Zustand „erfolgreich“, „ausstehend“, „fehlerhaft“ oder „Fehler“ pro Tag aufgeführt. Die Anzahl spiegelt die Daten pro Richtlinientypprofil wider. Wenn ein Gerät beispielsweise den Zustand „erfolgreich“ für alle zugewiesenen Richtlinien aufweist, wird der Zähler für „erfolgreich“ für diesen Tag um eins erhöht. Wenn einem Gerät zwei Profile zugewiesen sind, von denen eines den Zustand „erfolgreich“ und eines den Zustand „Fehler“ aufweist, erhöht die Entität den Zähler für „erfolgreich“ und versetzt das Gerät in den Zustand „Fehler“. Die Entität **policyDeviceActivity** listet für die letzten 30 Tage auf, wie viele Geräte an einem bestimmten Tag in welchem Zustand waren.

|  Eigenschaft |                                           BESCHREIBUNG                                           |        Beispiel        |
|-----------|-------------------------------------------------------------------------------------------------|-----------------------|
| dateKey   | Datumsschlüssel für den Zeitpunkt, zu dem das Einchecken des Gerätekonfigurationsprofils im Data Warehouse aufgezeichnet wurde. | 20160703              |
| pending   | Anzahl eindeutiger Geräte im Zustand „ausstehend“.                                                    | 123                   |
| Erfolgreich | Anzahl eindeutiger Geräte im Zustand „erfolgreich“.                                                    | 12                    |
| policyKey | Der Richtlinienschlüssel kann mit der Richtlinie verknüpft werden, um den Richtliniennamen zu erhalten.                                  | Windows 10-Baseline |
| error     | Anzahl eindeutiger Geräte im Zustand „Fehler“.                                                      | 10                    |
| „Fehlgeschlagen“    | Anzahl eindeutiger Geräte im Zustand „fehlerhaft“.                                                     | 2                     |

## <a name="policyplatformtypes"></a>policyPlatformTypes

|        Eigenschaft        |                      BESCHREIBUNG                      |     Beispiel    |
|------------------------|-------------------------------------------------------|----------------|
| policyPlatformTypeKey  | Der eindeutige Schlüssel für den Plattformtyp der Richtlinie.        | 20170519       |
| policyPlatformTypeId   | Der eindeutige Bezeichner für den Plattformtyp der Richtlinie. | 1              |
| policyPlatformTypeName | Der Name für den Plattformtyp der Richtlinie.              | AndroidForWork |

## <a name="policytypeactivities"></a>policyTypeActivities
Die Entität **PolicyTypeActivity** listet die Gesamtzahl der Geräte im Zustand „erfolgreich“, „ausstehend“, „fehlerhaft“ oder „Fehler“ auf. Diese Zustände werden im Bezug auf ein Gerätekonfigurationsprofil, ein Appkonfigurationsprofil oder eine Kompatibiliätsrichtlinie pro Tag aufgelistet.

|    Eigenschaft   |                                          BESCHREIBUNG                                          |           Beispiel           |
|---------------|-----------------------------------------------------------------------------------------------|-----------------------------|
| dateKey       | Datumsschlüssel für den Zeitpunkt, zu dem das Einchecken des Gerätekonfigurationsprofils im Data Warehouse aufgezeichnet wurde. | 20160703                    |
| policyKey     | Der Richtlinienschlüssel kann mit der Richtlinie verknüpft werden, um den Richtliniennamen zu erhalten.                                | Windows 10-Baseline         |
| policyTypeKey | Der Typ des Richtlinienschlüssels kann mit dem Richtlinientyp verknüpft werden, um den Namen des Richtlinientyps zu erhalten.             | Windows 10-Kompatibilitätsrichtlinien |
| pending       | Anzahl eindeutiger Geräte im Zustand „ausstehend“                                                    | 123                         |
| Erfolgreich     | Anzahl eindeutiger Geräte im Zustand „erfolgreich“                                                    | 12                          |
| error         | Anzahl eindeutiger Geräte im Zustand „Fehler“                                                      | 10                          |
| „Fehlgeschlagen“        | Anzahl eindeutiger Geräte im Zustand „fehlerhaft“                                                     | 2                           |

## <a name="policytypes"></a>policyTypes
Die Entität **PolicyType** listet Gerätekonfigurationsprofile, Appkonfigurationsprofile und Kompatibilitätsrichtlinien auf. Sie können die Richtlinien mit der mobilen Geräteverwaltung (MDM) zu einer Gruppe in Ihrem Unternehmen zuweisen.

|    Eigenschaft    |                       BESCHREIBUNG                      |            Beispiel            |
|----------------|--------------------------------------------------------|-------------------------------|
| policyTypeId   | Eindeutiger Bezeichner der Richtlinie im Quellsystem  | 123                           |
| policyTypeKey  | Eindeutiger Bezeichner der Richtlinie im Data Warehouse | 1                             |
| policyTypeName | Name des Richtlinientyps                               | Windows 10-Kompatibilitätsrichtlinie |

## <a name="policyuseractivities"></a>policyUserActivities
In der folgenden Tabelle ist die Anzahl der Benutzer mit dem Zustand „erfolgreich“, „ausstehend“, „fehlerhaft“ oder „Fehler“ pro Tag aufgeführt. Die Anzahl spiegelt die Daten pro Richtlinientypprofil wider. Wenn ein Benutzer beispielsweise den Zustand „erfolgreich“ für alle zugewiesenen Richtlinien aufweist, wird der Zähler für „erfolgreich“ für diesen Tag um eins erhöht. Wenn einem Benutzer zwei Profile zugewiesen sind, von denen eines den Zustand „erfolgreich“ und eines den Zustand „Fehler“ aufweist, wird der Benutzer für den Zustand „Fehler“ gezählt. Die Entität **PolicyUserActivity** listet für die letzten 30 Tage auf, wie viele Benutzer an einem bestimmten Tag in welchem Zustand waren.

|  Eigenschaft |                                          BESCHREIBUNG                                          |       Beispiel       |
|-----------|-----------------------------------------------------------------------------------------------|---------------------|
| dateKey   | Datumsschlüssel für den Zeitpunkt, zu dem das Einchecken des Gerätekonfigurationsprofils im Data Warehouse aufgezeichnet wurde. | 20160703            |
| pending   | Anzahl eindeutiger Geräte im Zustand „ausstehend“                                                    | 123                 |
| Erfolgreich | Anzahl eindeutiger Geräte im Zustand „erfolgreich“                                                    | 12                  |
| policyKey | Der Richtlinienschlüssel kann mit der Richtlinie verknüpft werden, um den Richtliniennamen zu erhalten.                                | Windows 10-Baseline |
| error     | Anzahl eindeutiger Geräte im Zustand „Fehler“                                                      | 10                  |

## <a name="termsandconditions"></a>termsAndConditions
Eine **termsAndConditions**-Entität stellt Metadaten und Inhalt einer bestimmten Richtlinie für Geschäftsbedingungen (T&C, Terms and Conditions) dar. Die Inhalte der T&C-Richtlinien werden Benutzern bei ihrem ersten Versuch angezeigt, sich bei Intune zu registrieren, und in der Folge bei Änderungen, zu denen ein Administrator eine erneute Zustimmung anfordert. Mit ihnen können Administratoren die Bedingungen kommunizieren, denen ein Benutzer zustimmen muss, um Geräte in Intune registrieren zu lassen.

|    Eigenschaft        |    BESCHREIBUNG    |    Beispiel        |
|----------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
|    termsAndConditionsKey    |    Ein Schlüssel, der einem Eintrag in der Sammlung „userTermsAndConditionsAcceptances“ entspricht    |    123    |
|    termsAndCondidionsId    |    Die ID für diesen termsAndConditions-Eintrag.    |    276edcb7-7440-4339-b6c5-8b6fc556fee6    |
|    termsAndConditionsVersion    |    Die Version dieses termsAndConditions-Eintrags.    |    1    |
|    Name    |    Der Name dieses termsAndConditions-Eintrags.        |    Intune-Nutzungsbedingungen     |
|    description    |    Die Beschreibung dieser Geschäftsbedingungen.     |         |
|    title    |    Der Titel dieser Geschäftsbedingungen.     |    Unternehmensrichtlinie zur Geräteverwaltung        |
|    summaryOfTerms    |    Die Zusammenfassung der Nutzungsbedingungen, die dem Benutzer übergeben wird.     |    Ich stimme den Geschäftsbedingungen zu.    |
|    termsAndConditionsBodyText    |    Der Text dieser Geschäftsbedingungen.       |    *Geräteverschlüsselung:* Durchsetzung einer 6-stelligen PIN    |
|    isDeleted    |    „True“ oder „False“, je nachdem, ob dieser Wert gelöscht ist.     |    False    |
|    startDateInclusiveUTC    |    Das Startdatum dieser Geschäftsbedingungen.     |    23.8.2018 4:01:34 Uhr    |
|    endDateEclusiveUTC    |    Das Enddatum dieser Geschäftsbedingungen.     |    31.12.9999 0:00:00 Uhr    |

## <a name="userdeviceassociations"></a>userDeviceAssociations
Die Entität **UserDeviceAssociation** enthält Zuweisungen von Benutzergeräten in Ihrer Organisation.

|        Name        |                                             BESCHREIBUNG                                            |     Beispiel     |
|--------------------|----------------------------------------------------------------------------------------------------|-----------------|
| userKey            | Eindeutiger Bezeichner für den Benutzer im Data Warehouse   (Ersatzschlüssel)                            | 123             |
| deviceKey          | Eindeutiger Bezeichner für das Gerät im Data Warehouse                                             | 123             |
| CreatedDateTimeUTC | Zeitpunkt, zu dem die Benutzergerätezuordnung erstellt wurde. Verwendet UTC-Format                     | 23.11.2016 0:00 |
| isDeleted          | Gibt an, dass der Benutzer dieses Geräts die Registrierung aufgehoben hat und die Zuordnung nicht mehr aktuell ist. | Wahr/falsch      |
| EndedDateTimeUTC   | Datum und Uhrzeit in UTC, als IsDeleted in TRUE geändert wurde                                               | 23.6.2017 0:00 Uhr  |

## <a name="users"></a>Benutzer
Die Entität **user** listet alle Benutzer von Azure Active Directory (Azure AD) mit zugewiesenen Lizenzen in Ihrem Unternehmen auf.

Die Entitätssammlung **user** enthält Benutzerdaten. Zu diesen Datensätzen gehören Benutzerzustände während der Datensammlung, selbst wenn der Benutzer entfernt wurde. Beispielsweise kann ein Benutzer in Intune hinzugefügt und dann im Verlauf des letzten Monats entfernt worden sein. Auch wenn dieser Benutzer zum Zeitpunkt der Berichterstellung nicht vorhanden ist, liegen Angaben zu Benutzer und Zustand in den Daten aus dem vorherigen Monat vor. Sie können einen Bericht erstellen, der die Dauer der Präsenz des Benutzers in Ihren Daten zeigt.

|          Eigenschaft          |                                                                                                           BESCHREIBUNG                                                                                                          |                Beispiel               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| userKey                    | Eindeutiger Bezeichner des Benutzers im Data Warehouse – Ersatzschlüssel.                                                                                                                                                         | 123                                  |
| userId                     | Eindeutiger Bezeichner des Benutzers – ähnlich wie UserKey, ist jedoch ein natürlicher Schlüssel.                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| UserEmail                  | E-Mail-Adresse des Benutzers                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName                        | Benutzerprinzipalname des Benutzers                                                                                                                                                                                               | John@constoso.com                    |
| displayName                | Anzeigename des Benutzers                                                                                                                                                                                                      | John                                 |
| intuneLicensed             | Gibt an, ob dieser Benutzer über Intune lizenziert ist oder nicht.                                                                                                                                                                              | Wahr/falsch                           |
| isDeleted                  | Gibt an, ob alle Lizenzen des Benutzers abgelaufen sind und ob der Benutzer daher aus Intune entfernt wurde. Dieses Flag wird für einen einzelnen Datensatz nicht geändert. Stattdessen wird ein neuer Datensatz für einen neuen Benutzerzustand erstellt. | Wahr/falsch                           |
| rowLastModifiedDateTimeUTC | UTC-Zeitpunkt, zu dem der Datensatz im Data Warehouse zuletzt geändert wurde.                                                                                                                                                 | 23.11.2016 0:00                      |

## <a name="usertermsandconditionsacceptances"></a>userTermsAndConditionsAcceptances
Eine **userTermsAndConditionsAcceptance**-Entität stellt den Akzeptanzstatus einer bestimmten Richtlinie von Geschäftsbedingungen (T&C) von einem bestimmten Benutzer dar. Benutzer müssen die aktuelle Version der Nutzungsbedingungen akzeptieren, um den Zugriff auf das Unternehmensportal zu behalten.

|    Eigenschaft    |    BESCHREIBUNG    |    Beispiel    |
|-------------------------------|--------------------------------------------------------------------------------|----------------------------|
|    dateKey    |    Ein Schlüssel, der einem Datumswert in der Sammlung „dates“ entspricht     |    20180823    |
|    userKey    |    Ein Benutzerschlüssel, der einem Benutzer in der Sammlung „users“ zugeordnet ist     |    20000    |
|    termsAndConditionsKey    |    Ein Schlüssel, der einem Eintrag in der Sammlung „termsAndConditions“ entspricht.    |    1    |
|    acceptedDateTimeUTC    |    Der Zeitpunkt, zu dem der Benutzer diese Geschäftsbedingungen akzeptiert hat.    |    23.8.2018 4:01:34 Uhr    |
|    lastModifiedDateTimeUTC    |    Der Zeitpunkt, zu dem dieser Eintrag zuletzt geändert wurde.     |    23.8.2018 4:01:34 Uhr    |

## <a name="vppprogramtypes"></a>vppProgramTypes 
Die Entität **vppProgramType** führt mögliche VPP-Programmtypen für eine App auf.

|      Eigenschaft      |          Beschreibung         |
|--------------------|------------------------------|
| vppProgramTypeID   | ID für den Typen.           |
| vppProgramTypeKey  | Ersatzschlüssel für den Schlüssel. |
| vppProgramTypeName | VPP-Programmtyp.          |

### <a name="example"></a>Beispiel

|             VppProgramID             |         Name        | BESCHREIBUNG                |
|--------------------------------------|---------------------|----------------------------|
| 3DDA2474-470B-4503-9830-2665C21C1945 | Microsoft           | VPP-Programm von Microsoft. |
| 00000000-0000-0000-0000-000000000000 | Noch nicht verfügbar | Standardwert, kein VPP.   |
| B54814E0-68EA-4BA4-8088-B5AAB58E737B | Apple               | VPP-Programm von Apple.     |

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen über das Intune Data Warehouse finden Sie unter [Datenmodell von Data Warehouse](reports-ref-data-model.md).