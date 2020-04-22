---
title: Zustandsmeldungen
titleSuffix: Configuration Manager
description: Beschreibungen der Zustandsmeldungen in den unterstützten Versionen von Configuration Manager.
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704588"
---
# <a name="state-messages-in-configuration-manager"></a>Zustandsmeldungen in Configuration Manager 

*Gilt für: Configuration Manager (Current Branch)*

Zustandsmeldungen enthalten präzise Informationen zu Bedingungen im Configuration Manager-Client. Das System für Zustandsmeldungen wird von spezifischen Configuration Manager-Komponenten verwendet, z.B. von Softwareupdates und Konfigurationseinstellungen.

Configuration Manager-Clients senden Zustandsmeldungen an die Standortsysteme für Fallbackstatuspunkte oder Verwaltungspunkte, um den aktuellen Zustand der Vorgänge zu melden. Sie können Berichte erstellen, um von Configuration Manager-Clients gesendete Zustandsmeldungen anzuzeigen.

Jedes Configuration Manager-Feature, das Zustandsmeldungen verwendet, wird anhand des Thementyps der Zustandsmeldung identifiziert. Mithilfe der in der folgenden Tabelle aufgelisteten Thementypen für Zustandsmeldungen können Sie das Configuration Manager-Feature definieren, auf das sich eine Zustandsmeldung bezieht.

> [!NOTE]  
> Der ID-Wert 0 für eine Zustandsmeldung weist typischerweise darauf hin, dass sich der Thementyp in einem unbekannten Zustand befindet.

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 0 | Unbekannter Kompatibilitätszustand|
| 1 | Kompatibel | 
| 2 | Nicht kompatibel | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 0  | Unbekannter Erzwingungszustand |
| 1  | Updates werden installiert.        | 
| 2  | Warten auf Neustart.          | 
| 3  | Warten auf das Abschließen einer anderen Installation.         | 
| 4  | Updates wurden erfolgreich installiert.          | 
| 5  | Ausstehender Systemneustart         | 
| 6  | Fehler bei der Installation von Updates.         | 
| 7  | Updates werden heruntergeladen.   | 
| 8  | Updates wurden heruntergeladen.    | 
| 9  | Fehler beim Herunterladen der Updates.     | 
| 10 | Warten auf Wartungsfenster, bevor Installation ausgeführt wird.         | 
| 11 | Warten auf Orchestrierung.         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|      
| 0 | Unbekannter Bewertungszustand|                 
| 1 |Bewertung aktiviert.      |
| 2 |Auswertung war erfolgreich.      |
| 3 |Fehler bei der Auswertung.      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 0 | Unbekannter Erkennungszustand|
| 1 | Nicht erforderlich   |
| 2 | Nicht erkannt    |
| 3 | Erkannt   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 0 | Unbekannter Kompatibilitätszustand|
| 1 |Kompatibel     |
| 2 |Nicht kompatibel     |
| 3 |Konflikt erkannt    |
| 4 |Fehler      |
| 5 |Unbekannt     |
| 6 |Teilweise konform.   |
| 7 |Konformität nicht konfiguriert.    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 0  | Unbekannter Erzwingungszustand|
| 1  |Erzwingung gestartet.          |
| 2  |Erzwingung wartet auf Inhalt.         |
| 3  | Warten auf das Abschließen einer anderen Installation.        |
| 4  |Warten auf Wartungsfenster, bevor Installation ausgeführt wird.         |
| 5  |Vor Ausführen der Installation ist ein Neustart erforderlich.         |
| 6  |Allgemeiner Fehler.        |
| 7  |Ausstehende Installation         |
| 8  |Update wird installiert.          |
| 9  |Ausstehender Systemneustart        |
| 10 |Update wurde erfolgreich installiert.         |
| 11 |Fehler beim Installieren des Updates.        |
| 12 |Update wird heruntergeladen.        |
| 13 | Update wurde heruntergeladen.        |
| 14 |Fehler beim Herunterladen des Updates.        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
|0 |Unbekannter Erkennungszustand|
| 1 | Update ist nicht erforderlich.  |
| 2 | Update ist erforderlich.   |
| 3 | Update wurde installiert.  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 0 |Unbekannter Überprüfungszustand|
| 1 | Scan wartet auf den Inhalt.   |
| 2 | Überprüfung wird ausgeführt.    |
| 3 | Überprüfung wurde abgeschlossen.    |
| 4 | Scan wird einen neuen Versuch durchführen.   |
| 5 | Scan ist fehlgeschlagen.   |
| 6 | Überprüfung wurde mit Fehlern abgeschlossen. |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

Kein Zustands-IDs.

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

Kein Zustands-IDs.

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
Kein Zustands-IDs.

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 100 |Clientbereitstellung wurde gestartet      |       
| 101 |Warten auf Download       |       
| 102 |Bereitstellung geplant       |       
| 103 | Warten auf Fenster vor Bereitstellung |
| 104 |Bereitstellung übersprungen       |       
| 301 |Unbekannter Fehler bei der Clientbereitstellung. |       
| 302 |Der Dienst „ccmsetup“ konnte nicht erstellt werden.  |       
| 303 |Der Dienst „ccmsetup“ konnte nicht gelöscht werden. |       
| 304 |Mit dem auf dem Systemlaufwerk aktivierten dateibasierten Schreibfilter (File Based Write Filter, FBWF) kann keine Installation über das eingebettete Betriebssystem vorgenommen werden. |       
| 305 |Unter Windows 2000 ist der einheitliche Sicherheitsmodus ungültig.  |       
| 306 |Der Download von „ccmsetup“ konnte nicht gestartet werden.  |       
| 307 |Ungültige Befehlszeile für „ccmsetup“. |       
| 308 |Fehler beim Download der Datei über WINHTTP von der angegebenen Adresse. |       
| 309 |Fehler beim Download der Dateien über BITS von der angegebenen Adresse. |       
| 310 |Fehler bei der Installation von BITS Version. |       
| 311 |Es kann nicht überprüft werden, ob die erforderliche Datei über eine Microsoft-Signatur verfügt.  |       
| 312 |Fehler beim Kopieren der Datei: Der Datenträger ist voll. |       
| 313 |MSI-Fehler bei der Installation von „Client.msi“. |       
| 314 |Fehler beim Laden von Manifestdatei „ccmsetup.xml“. |       
| 315 |Fehler beim Abrufen eines Clientzertifikats.  |       
| 316 |Als Voraussetzung notwendige Datei ist nicht MS-signiert. |       
| 317 |Zum Fortsetzen der Installation ist ein Neustart erforderlich.  |       
| 318 |Der Client kann nicht auf dem Verwaltungspunkt installiert werden, weil der Verwaltungspunkt und der Client unterschiedliche Versionen ausführen. |       
| 319 |Das Betriebssystem oder Service Pack wird nicht unterstützt.  |       
| 320 |Bereitstellung nicht unterstützt.       |       
| 321 |„Bits“ fehlt.        |       
| 322 |Quellordner nicht verfügbar.       |       
| 323 |„Appv“ nicht unterstützt.              |       
| 324 |Falsche Standortversion.              |       
| 325 |Erforderliche Hashwerte stimmen nicht überein.       |       
| 326 |Fehler beim Aufheben der MDM-Registrierung.      |       
| 327 |MDM-Registrierung erkannt      |       
| 328 |Intune erkannt       |       
| 329 |Getaktetes Netzwerk nicht zulässig.      |       
| 400 |Clientbereitstellung war erfolgreich |  
| 401 |Bereitstellung war erfolgreich, Neustart erforderlich.     |       
| 402 |Bereitstellung und Neustart waren erfolgreich.     |
| 500 |Clientzuweisung wurde gestartet|
| 601 |Unbekannter Fehler bei der Clientzuweisung.|
| 602 |Folgender Standortcode ist ungültig.|
| 603 |Konnte nicht zu MP zugewiesen werden.|
| 604 |Standardverwaltungspunkt konnte nicht gefunden werden.|
| 605 |Standort-Signaturzertifikat konnte nicht heruntergeladen werden.|
| 606 |Standortcode konnte nicht automatisch ermittelt werden.|
| 607 |Standortzuweisung ist fehlgeschlagen. Der Client verfügt über eine höhere Version als der Standort.|
| 608 |Standortversion von Active Directory Domain Services und SLP nicht erhalten.|
| 609 |Clientversion nicht erhalten.|
| 700 |Clientzuweisung war erfolgreich|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

Kein Zustands-IDs.

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 100 | Anmeldungsstatus   |
| 101 | Registrierung geplant   |
| 102 | Registrierung abgebrochen   |
| 105 | Registrierung gestartet   |
| 106 | Registrierung erfolgreich, aber nicht bereitgestellt
| 107 | Registrierung und Bereitstellung erfolgreich
| 108 | Registrierung: kein aktiver Benutzer   |
| 110 | Fehler bei Registrierung.   |


## <a name="820--state_topictype_client_wufb"></a>820  STATE_TOPICTYPE_CLIENT_WUFB

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 | Windows Update for Business-Clientstatus| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 | Speicherplatz   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

Kein Zustands-IDs.

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

Kein Zustands-IDs.

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

Kein Zustands-IDs.

## <a name="1000--state_topictype_client_framework_comm"></a>1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 | Kommunikation des Clients mit dem Verwaltungspunkt erfolgreich |
| 2 | Fehler bei der Kommunikation des Clients mit dem Verwaltungspunkt. |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Der Client hat erfolgreich ein Zertifikat aus dem lokalen Zertifikatspeicher abgerufen.    |
| 2 |Der Client konnte kein Zertifikat aus dem lokalen Zertifikatspeicher abrufen. |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

Kein Zustands-IDs.

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

Kein Zustands-IDs.

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

Kein Zustands-IDs.

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

Kein Zustands-IDs.

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

Kein Zustands-IDs.

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

Kein Zustands-IDs.

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

Kein Zustands-IDs.

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

Kein Zustands-IDs.

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

Kein Zustands-IDs.

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

Kein Zustands-IDs.

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

Kein Zustands-IDs.

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

Kein Zustands-IDs.

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

Kein Zustands-IDs.

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

Kein Zustands-IDs.

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Client ist für den einheitlichen Modus nicht bereit.  |
| 2 |Client ist für den einheitlichen Modus bereit.     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 | Erfolgreich|
| 2 | Nicht erfolgreich |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

Kein Zustands-IDs.

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

Kein Zustands-IDs.

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

Kein Zustands-IDs.

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

Kein Zustands-IDs. 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Benutzeraffinitätssatz       |
| 2 |Benutzeraffinität entfernt       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

Kein Zustands-IDs.

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

Kein Zustands-IDs.

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1000  |Konfigurationselement erfolgreich           |
| 1001 |Konfigurationselement bereits erfolgreich installiert         |
| 1002 |Preflightzustand des Konfigurationselements erfolgreich          |
| 1003 |Schnellstatus des Konfigurationselements erfolgreich          |
| 2000 |Konfigurationselement in Bearbeitung           |
| 2001 |Konfigurationselement in Bearbeitung wartet auf Inhalt         |
| 2002 |Konfigurationselement in Bearbeitung wird installiert          |
| 2003 |Konfigurationselement in Bearbeitung wartet auf Neustart         |
| 2004 |Konfigurationselement in Bearbeitung wartet auf Wartungsfenster        |
| 2005 |Konfigurationselement in Bearbeitung wartet auf Zeitplan         |
| 2006 |Konfigurationselement in Bearbeitung lädt abhängigen Inhalt herunter     |
| 2007 |Konfigurationselement in Bearbeitung installiert Abhängigkeiten        |
| 2008 |Konfigurationselement in Bearbeitung wartet auf Neustart         |
| 2009 |Konfigurationselement in Bearbeitung hat Inhalt heruntergeladen         |
| 2010 |Konfigurationselement in Bearbeitung wartet auf Update         |
| 2011 |Konfigurationselement in Bearbeitung wartet auf erneute Benutzerverbindung        |
| 2012 |Konfigurationselement in Bearbeitung wartet auf Benutzerabmeldung         |
| 2013 |Konfigurationselement in Bearbeitung wartet auf Benutzeranmeldung         |
| 2014 |Konfigurationselement in Bearbeitung wartet auf Installation         |
| 2015 |Konfigurationselement in Bearbeitung wartet auf Neuversuch         |
| 2016 |Konfigurationselement in Bearbeitung wartet auf „presmode“         |
| 2017 |Konfigurationselement in Bearbeitung wartet auf Orchestrierung        |
| 2018 |Konfigurationselement in Bearbeitung wartet auf Netzwerk         |
| 2019 |Konfigurationselement in Bearbeitung: VE-Aktualisierung ausstehend         |
| 2020 |Konfigurationselement in Bearbeitung: VE wird aktualisiert         |
| 3000 |Anforderungen für Konfigurationselement nicht erfüllt           |
| 3001 |Anforderungen für Konfigurationselement nicht erfüllt: Host nicht anwendbar        |
| 4000 |Konfigurationselement unbekannt           |
| 5000 |Konfigurationselementfehler            |
| 5001 |Konfigurationselement: Fehler bei Auswertung          |
| 5002 |Konfigurationselement: Fehler bei Installation          |
| 5003 |Konfigurationselement: Fehler beim Abrufen von Inhalt         |
| 5004 |Konfigurationselement: Fehler beim Installieren von Abhängigkeiten         |
| 5005 |Konfigurationselement: Fehler beim Installieren von Inhaltsabhängigkeiten        |
| 5006 |Konfigurationselementfehler: Regelkonflikt          |
| 5007 |Konfigurationselement: Fehler beim Warten auf Neuversuch          |
| 5008 |Konfigurationselement: Fehler beim Deinstallieren von Ablösung        |
| 5009 |Konfigurationselement: Fehler beim Herunterladen von Ablösung         |
| 5010 |Konfigurationselement: Fehler bei VE-Aktualisierung          |
| 5011 |Konfigurationselement: Fehler beim Installieren der Lizenz         |
| 5012 |Konfigurationselement: Fehler beim Abrufen aller vertrauenswürdigen Apps       |
| 5013 |Konfigurationselementfehler: Keine Lizenz verfügbar         |
| 5014 |Konfigurationselementfehler: Betriebssystem nicht unterstützt          |
| 6000 |Konfigurationselement: Start erfolgreich            |
| 6010 |Konfigurationselement: Fehler beim Start            |
| 6020 |Konfigurationselementstart unbekannt|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

Kein Zustands-IDs.

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

Kein Zustands-IDs.

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

Kein Zustands-IDs.

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

Kein Zustands-IDs.

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

Kein Zustands-IDs.

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

Kein Zustands-IDs.

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

Kein Zustands-IDs.

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

Kein Zustands-IDs.

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Endpoint Protection: nicht verwaltet   |
| 2 |Endpoint Protection: Warten auf Installation  |
| 3 |Endpoint Protection: verwaltet   |
| 4 |Endpoint Protection: Fehler bei Installation  |
| 5 |Endpoint Protection: Neustart ausstehend  |
| 6 |Endpoint Protection: nicht unterstützt   |
| 7 |Endpoint Protection: Co-Verwaltung   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 0 |Endpoint Protection: Status der Richtlinienanwendung unbekannt    |
| 1 |Endpoint Protection: Richtlinienanwendung erfolgreich    |
| 2 |Endpoint Protection: Fehler bei Richtlinienanwendung    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 0 |  Unbekannt    |
| 1 |  Aktiv    |
| 2 |  Inaktiv    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 | Aktivierungsproxy nicht installiert    |
| 2 | Aktivierungsproxy wartet auf Installation   |
| 3 | Aktivierungsproxy wurde installiert    |
| 4 | Fehler beim Installieren des Aktivierungsproxys   |
| 5 | Aktivierungsproxy wartet auf Neustart   |
| 6 | Aktivierungsproxy für dieses Betriebssystem nicht unterstützt  |
| 7 | Aktivierungsproxyserver deaktivieren   |
| 8 | Fehler beim Deinstallieren des Aktivierungsproxys   |
| 9 | Aktivierungsproxyruntime nicht unterstützt   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

Kein Zustands-IDs.

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

Kein Zustands-IDs.

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

Kein Zustands-IDs.

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
|0 | Kanal für Windows-Pushbenachrichtigungsdienst festgelegt|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

Kein Zustands-IDs.

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

Kein Zustands-IDs.

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

Kein Zustands-IDs.

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

Kein Zustands-IDs.

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

Kein Zustands-IDs.

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

Kein Zustands-IDs.

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

Kein Zustands-IDs.

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

Kein Zustands-IDs.

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

Kein Zustands-IDs.

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

Kein Zustands-IDs.

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

Kein Zustands-IDs.

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

Kein Zustands-IDs.

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Captcha ausgestellt         |
| 2 |Fehler bei Captcha-Ausstellung        |
| 3 |Fehler beim Erstellen der Anforderung        |
| 4 |Fehler bei Anforderungsübermittlung        |
| 5 |Captcha-Überprüfung erfolgreich       |
| 6 |Fehler bei Captcha-Überprüfung       |
| 7 |Fehler bei Ausstellung         |
| 8 |Ausstellung ausstehend         |
| 9 |Ausgestellt          |
| 10 |Fehler bei Antwortverarbeitung       |
| 11 |Antwort ausstehend         |
| 12 |Registrierung erfolgreich         |
| 13 |Registrierung nicht erforderlich         |
| 14 |Widerrufen          |
| 15 |Aus Sammlung entfernt        |
| 16 |Erneuerung verifiziert         |
| 17 |Installationsfehler        |
| 18 |Installiert         |
| 19 |Fehler beim Löschen         |
| 20 |Gelöscht         |
| 21 |Erneuerung angefordert        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Captcha ausgestellt         |
| 2 |Fehler bei Captcha-Ausstellung        |
| 3 |Fehler beim Erstellen der Anforderung        |
| 4 |Fehler bei Anforderungsübermittlung        |
| 5 |Captcha-Überprüfung erfolgreich       |
| 6 |Fehler bei Captcha-Überprüfung       |
| 7 |Fehler bei Ausstellung         |
| 8 |Ausstellung ausstehend         |
| 9 |Ausgestellt          |
| 10 |Fehler bei Antwortverarbeitung       |
| 11 |Antwort ausstehend         |
| 12 |Registrierung erfolgreich         |
| 13 |Registrierung nicht erforderlich         |
| 14 |Widerrufen          |
| 15 |Aus Sammlung entfernt        |
| 16 |Erneuerung verifiziert         |
| 17 |Installationsfehler        |
| 18 |Installiert         |
| 19 |Fehler beim Löschen         |
| 20 |Gelöscht         |
| 21 |Erneuerung angefordert        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 | Statusanheftung: Einrichtung erfolgreich       |
| 2 | Statusanheftung: Fehler bei Einrichtung       |
| 3 | Statusanheftung: Einrichtung nicht unterstützt      |
| 4 | Statusanheftung in Bearbeitung      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

Kein Zustands-IDs.

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

Kein Zustands-IDs.

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

Kein Zustands-IDs.

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

Kein Zustands-IDs.

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

Kein Zustands-IDs.

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

Kein Zustands-IDs.

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Captcha ausgestellt    |
| 2 |Fehler bei Captcha-Ausstellung   |
| 3 |Fehler beim Erstellen der Anforderung   |
| 4 |Fehler bei Anforderungsübermittlung   |
| 5 |Captcha-Überprüfung erfolgreich  |
| 6 |Fehler bei Captcha-Überprüfung  |
| 7 |Fehler bei Ausstellung    |
| 8 |Ausstellung ausstehend    |
| 9 |Ausgestellt     |
| 10 |Fehler bei Antwortverarbeitung  |
| 11 |Antwort ausstehend    |
| 12 |Registrierung erfolgreich    |
| 13 |Registrierung nicht erforderlich    |
| 14 |Widerrufen     |
| 15 |Aus Sammlung entfernt   |
| 16 |Erneuerung verifiziert    |
| 17 |Installationsfehler   |
| 18 |Installiert    |
| 19 |Fehler beim Löschen    |
| 20 |Gelöscht    |
| 21 |Erneuerung angefordert   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
|| 1 | Konformität erfolgreich    |
| 2 | Konformitätsfehler bei Verwaltungspunkt   |
| 3 | Konformitätsfehler bei Client   |
| 4 | Konformitätsfehler bei Intune   |
| 5 | Konformitätsfehler bei AAD   |
| 6 | Konformität: Co-Verwaltung Intune   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Peercachequelle hinzugefügt       |
| 2 |Peercachequelle entfernt      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Peercachequelle deaktiviert       |
| 2 |Peercachequelle ist aktiv       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Download: aggregierter Datenupload       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Peerquelle: Ablehnung Datenupload     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

Kein Zustands-IDs.

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

Kein Zustands-IDs.

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

Kein Zustands-IDs.

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

Kein Zustands-IDs.

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     Zustandsmeldungs-ID     |  Zustandsmeldungsbeschreibung |
|:-------------|:------|
| 1 |Integritätsnachweis wird unterstützt      |
| 2 |Integritätsnachweis wird nicht unterstützt      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

Kein Zustands-IDs.

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

Kein Zustands-IDs.

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

Kein Zustands-IDs.

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

Kein Zustands-IDs.

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

Kein Zustands-IDs.

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

Kein Zustands-IDs.

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

Kein Zustands-IDs.

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

Kein Zustands-IDs.

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

Kein Zustands-IDs.

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

Kein Zustands-IDs.

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

Kein Zustands-IDs.

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

Kein Zustands-IDs.

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

Kein Zustands-IDs.

## <a name="next-steps"></a>Nächste Schritte

- [Beschreibung von Zustandsmeldungen in Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Whitepaper zur Softwareupdateverwaltung für Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)
