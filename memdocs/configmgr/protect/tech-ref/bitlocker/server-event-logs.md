---
title: Serverereignisprotokolle
titleSuffix: Configuration Manager
description: Eine technische Referenz für die möglichen BitLocker-Servereinträge (MBAM) im Windows-Ereignisprotokoll
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe7d24bc1cad27094d720a5cb5aa487caec9199d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127864"
---
# <a name="server-event-logs"></a>Serverereignisprotokolle

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

Verwenden Sie die Windows-Ereignisanzeige, um Ereignisprotokolle für die folgenden Komponenten des BitLocker-Verwaltungsservers in Configuration Manager anzuzeigen:

- Wiederherstellungsdienst auf dem Verwaltungspunkt
- Self-Service-Portal
- Administration and Monitoring-Website

Öffnen Sie auf einem Server, auf dem eine oder mehrere dieser Komponenten gehostet werden, die Ereignisanzeige. Navigieren Sie dann zu **Anwendungs- und Dienstprotokolle**, **Microsoft**, **Windows**, und klappen Sie **MBAM-Web** auf. Standardmäßig sind dort die Ereignisprotokolle [Admin](#admin) (Administrator) und [Operational](#operational) (Betrieb) zu finden.

Die folgenden Abschnitte enthalten Nachrichten und Informationen zur Problembehandlung für Ereignis-IDs, die bei den Komponenten des BitLocker-Verwaltungsservers auftreten können.

## <a name="admin"></a>Administrator

### <a name="1-webappspnerror"></a>1: WebAppSpnError

In der Anwendung {SiteName}{VirtualDirectory} fehlen die folgenden Dienstprinzipalnamen (Service Principal Names, SPNs):{ListOfSpns} Registrieren Sie die erforderlichen SPNs für das Konto: {ExecutionAccount}.

Damit die integrierte Windows-Authentifizierung erfolgreich sein kann, müssen die erforderlichen SPNs vorhanden sein. Diese Nachricht gibt an, dass der für die Anwendung erforderliche SPN nicht ordnungsgemäß konfiguriert ist. Die in diesem Ereignis enthaltenen Details sollten weitere Informationen bereitstellen.

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100: AdminServiceRecoveryDbError

Mögliche Fehlermeldungen:

- GetMachineUsers: Beim Abrufen von Benutzerinformationen aus der Datenbank ist ein Fehler aufgetreten.
- GetRecoveryKey: Beim Abrufen des Wiederherstellungsschlüssels aus der Datenbank ist ein Fehler aufgetreten.
- GetRecoveryKey: Beim Abrufen von Benutzerinformationen aus der Datenbank ist ein Fehler aufgetreten.
- GetRecoveryKeyIds: Beim Abrufen der IDs von Wiederherstellungsschlüsseln aus der Datenbank ist ein Fehler aufgetreten.
- GetTpmHashForUser: Beim Abrufen von TPM-Hashdaten aus der Wiederherstellungsdatenbank ist ein Fehler aufgetreten.
- GetTpmHashForUser: Beim Abrufen von TPM-Hashdaten aus der Wiederherstellungsdatenbank ist ein Fehler aufgetreten.
- QueryDriveRecoveryData: Beim Abrufen von Laufwerk-Wiederherstellungsdaten aus der Datenbank ist ein Fehler aufgetreten.
- QueryRecoveryKeyIdsForUser: Beim Abrufen der IDs von Wiederherstellungsschlüsseln aus der Datenbank ist ein Fehler aufgetreten.
- QueryVolumeUsers: Beim Abrufen von Benutzerinformationen aus der Datenbank ist ein Fehler aufgetreten.

Diese Nachricht wird immer dann protokolliert, wenn bei der Kommunikation mit der Wiederherstellungsdatenbank eine Ausnahme auftritt. Lesen Sie die in der Ablaufverfolgung enthaltenen Informationen, um spezifische Details zur Ausnahme zu erhalten.

### <a name="101-adminservicecompliancedberror"></a>101: AdminServiceComplianceDbError

Mögliche Fehlermeldungen:

- GetRecoveryKey: Fehler beim Protokollieren eines Überwachungsereignisses in der Kompatibilitätsdatenbank.
- GetRecoveryKeyIds: Fehler beim Protokollieren eines Überwachungsereignisses in der Kompatibilitätsdatenbank.
- GetTpmHashForUser: Fehler beim Protokollieren eines Überwachungsereignisses in der Kompatibilitätsdatenbank.
- QueryRecoveryKeyIdsForUser: Fehler beim Protokollieren eines Überwachungsereignisses in der Kompatibilitätsdatenbank.
- QueryDriveRecoveryData: Fehler beim Protokollieren eines Überwachungsereignisses in der Kompatibilitätsdatenbank.

Diese Nachricht wird immer dann protokolliert, wenn bei der Kommunikation mit der Kompatibilitätsdatenbank eine Ausnahme auftritt. Lesen Sie die in der Ablaufverfolgung enthaltenen Informationen, um spezifische Details zur Ausnahme zu erhalten.

### <a name="102-agentservicerecoverydberror"></a>102: AgentServiceRecoveryDbError

Diese Nachricht zeigt eine Ausnahme bei der Kommunikation des Diensts mit der Wiederherstellungsdatenbank an. Lesen Sie die im Ereignis enthaltene Nachricht durch, um spezifische Informationen zur Ausnahme zu erhalten.

Vergewissern Sie sich, dass das Konto des MBAM-App-Pools über die erforderlichen Berechtigungen zum Herstellen von Verbindungen mit der Wiederherstellungsdatenbank verfügt.

### <a name="103-agentserviceerror"></a>103: AgentServiceError

Mögliche Fehlermeldungen:

- Es wurde kein Benutzerkonto für den Clientcomputer oder die Datenmigration gefunden.

    Bei jedem Aufruf der Webmethoden `PostKeyRecoveryInfo`, `IsRecoveryKeyResetRequired`, `CommitRecoveryKeyRest` oder `GetTpmHash` wird der Aufruferkontext abgerufen, um die Anmeldeinformationen des Aufrufers zu erhalten. Wenn der Aufruferkontext null oder leer ist, protokolliert der Dienst diese Nachricht.

- Account verification failed for caller identity (Fehler bei der Kontoüberprüfung aufgrund der Identität des Aufrufers).

    Diese Nachricht wird protokolliert, wenn die Webmethode ein Computerkonto als Aufrufer erwartet, der Aufrufer aber kein Computerkonto ist. Sie kann ebenfalls ausgelöst werden, wenn die Webmethode ein Benutzerkonto als Aufrufer erwartet, es sich aber nicht um ein Benutzerkonto oder um ein Mitglied eines Gruppenkontos für die Datenmigration handelt.

### <a name="104-statusservicecompliancedbconfigerror"></a>104: StatusServiceComplianceDbConfigError

Die Verbindungszeichenfolge für die Kompatibilitätsdatenbank in der Registrierung ist leer.

Diese Nachricht wird protokolliert, wenn die Verbindungszeichenfolge für die Kompatibilitätsdatenbank ungültig ist. Überprüfen Sie den Wert am Registrierungsschlüssel `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`.

### <a name="105-statusservicecompliancedberror"></a>105: StatusServiceComplianceDbError

Dieser Fehler weist darauf hin, dass die Websites oder Webdienste keine Verbindung mit der Kompatibilitätsdatenbank herstellen konnten. Überprüfen Sie, ob das Konto des IIS-App-Pools eine Verbindung mit der Datenbank herstellen kann.

### <a name="106-helpdeskerror"></a>106: HelpdeskError

Bekannte Fehler und mögliche Ursachen:

- Die Anforderung der URL hat einen internen Fehler verursacht.

    In der Anwendung für die Administration and Monitoring-Website (Helpdesk) ist ein Ausnahmefehler aufgetreten. Überprüfen Sie die Protokolleinträge im **Admin**-Ereignisprotokoll, um die spezifische Ausnahme zu finden.

- Fehler beim Abrufen von Informationen zum Ausführungskontext. Die Registrierung des Dienstprinzipalnamens (Service Principal Name, SPN) konnte nicht überprüft werden.

    Der SPN wird während des erstmaligen Ladevorgangs der Helpdesk-Website überprüft. Zum Überprüfen des SPNs sind die Kontoinformationen, der IIS-Websitename und der ApplicationVirtualPath erforderlich, die der Helpdesk-Website entsprechen. Diese Fehlernachricht wird protokolliert, wenn mindestens eins dieser Attribute fehlt oder ungültig ist.

- Fehler beim Überprüfen der Registrierung des Dienstprinzipalnamens (SPN).

    Diese Nachricht gibt an, dass beim Überprüfen des SPNs eine Sicherheitsausnahme ausgelöst wird. Informationen dazu finden Sie in der Ausnahme, die in den Ereignisdetails enthalten ist.

### <a name="107-selfserviceportalerror"></a>107: SelfServicePortalError

Bekannte Fehler und mögliche Ursachen:

- Fehler beim Abrufen des Wiederherstellungsschlüssels für einen Benutzer

    Gibt an, dass beim versuchten Abruf eines Wiederherstellungsschlüssels eine unerwartete Ausnahme ausgelöst wurde. Informationen dazu finden Sie in der Ausnahme, die in den Ereignisdetails enthalten ist. Wenn für die Helpdesk-App Ablaufverfolgung aktiviert ist, beziehen Sie sich auf Ablaufverfolgungsdaten, um detaillierte Ausnahmenachrichten anzuzeigen.

- Fehler beim Abrufen von Informationen zum Ausführungskontext. Die Registrierung des Dienstprinzipalnamens (Service Principal Name, SPN) konnte nicht überprüft werden

    Während des anfänglichen Ladevorgangs ruft das Self-Service-Portal Kontoinformationen, den IIS-Websitenamen und den ApplicationVirtualPath für die Self-Service-Website ab, um den SPN zu überprüfen. Diese Fehlernachricht wird protokolliert, wenn mindestens eins dieser Attribute ungültig ist.

- Fehler beim Überprüfen der Registrierung des Dienstprinzipalnamens (SPN). EventDetails:{ExceptionMessage}

    Diese Nachricht gibt an, dass beim Überprüfen des SPNs eine Sicherheitsausnahme ausgelöst wurde. Informationen dazu finden Sie in der Ausnahme, die in den Ereignisdetails enthalten ist.

### <a name="108-domaincontrollererror"></a>108: DomainControllerError

Bekannte Fehler und mögliche Ursachen:

- Fehler beim Auflösen eines Domänennamens {DomainName} aufgrund eines Fehlers bei der Speicherbelegung.

    Zum Auflösen des Domänennamens wird die `DsGetDcName`-Windows-API aufgerufen. Diese Nachricht wird protokolliert, wenn diese API `ERROR_NOT_ENOUGH_MEMORY` zurückgibt, was auf einen Speicherbelegungsfehler hinweist.

- Die DsGetDcName-Methode konnte nicht aufgerufen werden

    Diese Nachricht gibt an, dass die `DsGetDcName`-API auf dem Host nicht verfügbar ist.

### <a name="109-webapprecoverydberror"></a>109: WebAppRecoveryDbError

Bekannte Fehler und mögliche Ursachen:

- Fehler beim Lesen der Konfiguration der Wiederherstellungsdatenbank. Die Verbindungszeichenfolge für die Wiederherstellungsdatenbank ist nicht konfiguriert.

    Diese Nachricht gibt an, dass die Informationen in der Verbindungszeichenfolge für die Wiederherstellungsdatenbank unter `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` ungültig sind. Überprüfen Sie den angegebenen Wert des Registrierungsschlüssels.

Wenn eine der folgenden Nachrichten auftritt, überprüfen Sie, ob Sie mithilfe der App-Pool-Anmeldeinformationen vom IIS-Server eine Verbindung mit der Wiederherstellungsdatenbank herstellen können:

- DoesUserHaveMatchingRecoveryKey: Fehler beim Abrufen von Wiederherstellungsschlüssel-IDs für einen Benutzer.
- QueryDriveRecoveryData: Fehler beim Abrufen von Daten für die Laufwerkswiederherstellung.
- QueryRecoveryKeyIdsForUser: Fehler beim Abrufen von Wiederherstellungsschlüssel-IDs für einen Benutzer.
- Fehler beim Abrufen des TPM-Kennworthashs aus der Wiederherstellungsdatenbank.

### <a name="110-webappcompliancedberror"></a>110: WebAppComplianceDbError

Bekannte Fehler und mögliche Ursachen:

- Fehler beim Lesen der Konfiguration der Kompatibilitätsdatenbank. Die Verbindungszeichenfolge für die Kompatibilitätsdatenbank ist nicht konfiguriert.

    Diese Nachricht gibt an, dass die Informationen in der Verbindungszeichenfolge für die Kompatibilitätsdatenbank unter `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` ungültig sind. Überprüfen Sie den Wert dieses Registrierungsschlüssels.

Wenn eine der folgenden Nachrichten auftritt, überprüfen Sie, ob Sie mithilfe der App-Pool-Anmeldeinformationen vom IIS-Server eine Verbindung mit der Kompatibilitätsdatenbank herstellen können:

- GetRecoveryKeyForCurrentUser: Fehler beim Protokollieren eines Überwachungsereignisses in der Kompatibilitätsdatenbank.
- QueryRecoveryKeyIdsForUser: Fehler beim Protokollieren eines Überwachungsereignisses in der Kompatibilitätsdatenbank.
- QueryRecoveryKeyIdsForUser: Fehler beim Protokollieren eines Überwachungsereignisses in der Kompatibilitätsdatenbank.

### <a name="111-webappdberror"></a>111: WebAppDbError

Diese Fehler weisen auf eine der folgenden zwei Bedingungen hin

- MBAM-Websites/Webdienste konnten entweder zur Kompatibilitäts- oder zur Wiederherstellungsdatenbank keine Verbindung herstellen
- Das Ausführungskonto für MBAM-Websites/Webdienste (App-Pool-Konto) konnte die gespeicherte Prozedur `GetVersion` in der Kompatibilitäts- oder der Wiederherstellungsdatenbank nicht ausführen

Weitere Details zu der Ausnahme können Sie der im Ereignis enthaltenen Nachricht entnehmen.

Überprüfen Sie, ob mit dem App-Pool-Konto Verbindungen mit der Kompatibilitäts- oder der Wiederherstellungsdatenbank hergestellt werden können. Vergewissern Sie sich, dass es über die Berechtigungen zum Ausführen der gespeicherten Prozedur `GetVersion` verfügt.

### <a name="112-webapperror"></a>112: WebAppError

Fehler beim Überprüfen der Registrierung des Dienstprinzipalnamens (SPN).

Um den SPN zu überprüfen, wird Active Directory abgefragt, um eine Liste der dem SPN zugeordneten Ausführungskonten abzurufen. Außerdem wird der `ApplicationHost.config` abgefragt, um die Websitebindungen zu erhalten. Diese Fehlernachricht zeigt an, dass keine Kommunikation mit Active Directory möglich war oder die `ApplicationHost.config`-Datei nicht geladen werden konnte.

Vergewissern Sie sich, dass das Konto des App-Pools über Berechtigungen zum Abfragen von Active Directory oder der `ApplicationHost.config`-Datei verfügt. Überprüfen Sie darüber hinaus die Websitebindungseinträge in der `ApplicationHost.config`-Datei.

## <a name="operational"></a>Betriebsbereit

### <a name="4-performancecountererror"></a>4: PerformanceCounterError

Fehler beim Abrufen eines Leistungsindikators.

Die Ablaufverfolgungsnachricht enthält die eigentliche Ausnahmenachricht, von denen einige hier aufgeführt sind:

- ArgumentNullException: Diese Ausnahme wird ausgelöst, wenn die Kategorie, der Zähler oder die Instanz des angeforderten Leistungsindikators ungültig ist.
- System.InvalidOperationException: categoryName ist eine leere Zeichenfolge (""). counterName ist eine leere Zeichenfolge ("").
- Die angeforderte Lese-/Schreibberechtigungseinstellung ist für diesen Indikator ungültig.
- Die angegebene Kategorie ist nicht vorhanden (wenn readOnly WAHR ist).
- Bei der angegebenen Kategorie handelt es sich nicht um eine benutzerdefinierte .NET Framework-Kategorie (wenn readOnly FALSCH ist).
- Die angegebene Kategorie ist als Mehrfachinstanz gekennzeichnet und erfordert es, dass der Leistungsindikator mit einem Instanznamen erstellt wird.
- instanceName ist länger als 127 Zeichen.
- categoryName und counterName wurden in verschiedene Sprachen lokalisiert.
- System.ComponentModel.Win32Exception: Fehler beim Zugriff auf eine System-API.
- System.UnauthorizedAccessException: Code, der ohne Administratorberechtigungen ausgeführt wird, hat versucht, einen Leistungsindikator zu lesen.

Weitere Details zu der Ausnahme können Sie der im Ereignis enthaltenen Nachricht entnehmen.

Überprüfen Sie für die `System.UnauthorizedAccessException`, ob das App-Pool-Konto Zugriff auf die Leistungsindikator-APIs hat.

### <a name="200-helpdeskinformation"></a>200: HelpDeskInformation

Die Verwaltungswebsiteanwendung hat eine unterstützte Version der Wiederherstellungs-/Kompatibilitätsdatenbank gefunden und erfolgreich eine Verbindung hergestellt.

Dies zeigt eine erfolgreiche hergestellte Verbindung von der Helpdesk-Website mit der Wiederherstellungs- oder Kompatibilitätsdatenbank an.

### <a name="201-selfserviceportalinformation"></a>201: SelfServicePortalInformation

Die Self-Service-Portal-Anwendung hat eine unterstützte Version der Wiederherstellungs-/Kompatibilitätsdatenbank gefunden und erfolgreich eine Verbindung hergestellt.

Dies zeigt eine erfolgreiche hergestellte Verbindung vom Self-Service-Portal mit der Wiederherstellungs- oder Kompatibilitätsdatenbank an.

### <a name="202-webappinformation"></a>202: WebAppInformation

Die SPNs der Anwendung sind ordnungsgemäß registriert.

Zeigt an, dass die für die Helpdesk-Website erforderlichen SPNs ordnungsgemäß beim ausführenden Konto registriert sind.

## <a name="see-also"></a>Weitere Informationen:

Weitere Informationen zur Verwendung dieser Protokolle finden Sie unter [BitLocker-Ereignisprotokolle](about-event-logs.md).

Weitere Informationen zur Problembehandlung finden Sie unter [Problembehandlung für BitLocker](troubleshoot.md).

Weitere Informationen zum Installieren dieser Websites finden Sie unter [Einrichten von BitLocker-Berichten und -Portalen](../../deploy-use/bitlocker/setup-websites.md).
