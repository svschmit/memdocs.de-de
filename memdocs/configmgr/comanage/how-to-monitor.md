---
title: Überwachen der Co-Verwaltung
titleSuffix: Configuration Manager
description: Verwenden Sie das Dashboard für die Co-Verwaltung zum Überprüfen von Informationen zu gemeinsam verwalteten Geräten.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 64d34cef57a3d5f141093d2b099c0b352604be42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688698"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Überwachen der Co-Verwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie die Co-Verwaltung aktiviert haben, überwachen Sie der Co-Verwaltung unterliegende Geräte mithilfe der folgenden Methoden:

- [Dashboard für die Co-Verwaltung](#co-management-dashboard)  

- [Bereitstellungsrichtlinien](#deployment-policies)

- [WMI-Gerätedaten](#wmi-device-data)

## <a name="co-management-dashboard"></a>Dashboard für die Co-Verwaltung

Ab Version 1802 können Sie ein Dashboard mit Informationen zur Co-Verwaltung aufrufen. Mithilfe des Dashboards können Sie die Computer überprüfen, die in Ihrer Umgebung gemeinsam verwaltet werden. Mithilfe der Diagramme können Geräte identifiziert werden, bei denen möglicherweise ein Eingriff erforderlich ist.<!--1356648-->

Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Co-Verwaltung** aus.

Das Dashboard für die Co-Verwaltung wurde mit Version 1810 mit ausführlichen Informationen erweitert. <!--1358980-->

![Screenshot des Dashboards für die Co-Verwaltung](media/co-management-dashboard.png)

### <a name="co-managed-devices"></a>Gemeinsam verwaltete Geräte

*Gilt für die Versionen 1802 und 1806*

Zeigt den Prozentsatz der gemeinsam verwalteten Geräte in Ihrer gesamten Umgebung an.

![Kachel „Gemeinsam verwaltete Geräte“](media/co-management-dashboard/Percent-Co-managed-graph.PNG)

### <a name="client-os-distribution"></a>Clientbetriebssystemverteilung

*Gilt für alle Versionen* 

Zeigt Anzahl der Clientgeräte pro Betriebssystem nach Version an. Dabei werden folgende Gruppierungen verwendet:  

- Windows 7 und 8.x
- Windows 10 niedriger als 1709  
- Windows 10 1709 und höher  

    > [!Tip]  
    > Voraussetzung für die Co-Verwaltung ist die Version 1709 oder höher von Windows 10.  

Wenn Sie mit dem Mauszeiger auf einen Diagrammabschnitt zeigen, wird die Prozentzahl der Geräte angezeigt, die zur jeweiligen Betriebssystemgruppe gehören.

![Kachel „Clientbetriebssystemverteilung“](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status-donut"></a>Co-Verwaltungsstatus (Ringdiagramm)

*Gilt für die Versionen 1802 und 1806*

Zeigt die Aufschlüsselung nach erfolgreichen und fehlgeschlagenen Gerätevorgängen für die folgenden Kategorien an:

- Erfolgreich, in Hybrid-Azure AD eingebunden
- Erfolgreich, in Azure AD eingebunden  
- Fehler: Fehler bei automatischer Registrierung  

Wenn Sie mit dem Mauszeiger auf einen Diagrammabschnitt zeigen, wird die Prozentzahl der Geräte angezeigt, die zur jeweiligen Kategorie gehören.

![Kachel „Co-Verwaltungsstatus“ (Ringdiagramm)](media/co-management-dashboard/Co-management-status-graph.PNG)

Wählen Sie einen Diagrammabschnitt aus, um die Geräteliste der jeweiligen Kategorie anzuzeigen.

![Liste für Geräte, bei denen die Registrierung fehlgeschlagen ist](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)

### <a name="co-management-status-funnel"></a>Co-Verwaltungsstatus (Trichterdiagramm)

*Gilt für Version 1810 und höher*

Ein Trichterdiagramm zeigt die Anzahl von Geräten an, die folgende Registrierungsstatus aufweisen:
  
- Eligible devices (Berechtigte Geräte)
- Scheduled  
- Enrollment initiated (Registrierung gestartet)  
- Enrolled (Registriert)  

![Kachel „Co-Verwaltungsstatus“ (Trichterdiagramm)](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>Registrierungsstatus der Co-Verwaltung

*Gilt für Version 1810 und höher*

Zeigt die Aufschlüsselung der Gerätestatus für die folgenden Kategorien an:

- Erfolgreich, in Hybrid-Azure AD eingebunden  
- Erfolgreich, in Azure AD eingebunden  
- Wird registriert, in Hybrid-Azure AD eingebunden  
- Fehler, in Hybrid-Azure AD eingebunden  
- Fehler, in Azure AD eingebunden  
- Benutzeranmeldung steht aus  

    > [!Note]  
    > Ab Version 1906 wird zum Verringern der Anzahl von Geräten in diesem ausstehenden Status ein neues co-verwaltetes Gerät jetzt automatisch basierend auf dem Azure AD-*Gerätetoken* beim Microsoft Intune-Dienst registriert. Es muss nicht warten, bis ein Benutzer sich bei dem Gerät anmeldet, um die automatische Registrierung zu starten. Um dieses Verhalten zu unterstützen, muss auf dem Gerät Windows 10, Version 1803 oder höher ausgeführt werden.
    >
    > Wenn bei dem Gerätetoken ein Fehler auftritt, fällt es auf sein früheres Verhalten mit dem Benutzertoken zurück. Suchen Sie in **ComanagementHandler.log** nach folgendem Eintrag: `Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

Wählen Sie in der Kachel einen Status aus, um ein Drillthrough zu einer Liste von Geräten mit diesem Status durchzuführen.  

![Kachel „Registrierungsstatus der Co-Verwaltung“](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>Workloadübergang

*Gilt für alle Versionen*

Zeigt ein Balkendiagramm mit der Anzahl der Geräte an, die Sie für die verfügbaren Workloads zu Microsoft Intune übertragen haben.

Die Liste der Workloads variiert je nach Version von Configuration Manager. Weitere Informationen finden Sie unter [Auf Intune umstellbare Workloads](workloads.md).

Wenn Sie mit dem Mauszeiger auf einen Diagrammabschnitt zeigen, wird die Anzahl der umgestellten Geräte für die Workload angezeigt. 

![Balkendiagramm „Workloadübergang“](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>Registrierungsfehler

*Gilt für Version 1810 und höher*

Diese Tabelle stellt eine Liste der Registrierungsfehler von Geräten zur Verfügung. Diese Fehler können von der MDM-Komponente in Windows, aus dem Windows-Kernbetriebssystem oder aus dem Configuration Manager-Client stammen.

Es gibt Hunderte von möglichen Fehlern. In der folgenden Tabelle werden die häufigsten Fehler aufgeführt
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Fehler | Beschreibung |
|---------|---------|
| 2147549183 (0x8000FFFF) | Die MDM-Registrierung wurde noch nicht für Azure AD konfiguriert, oder die Registrierungs-URL wird nicht erwartet.<br><br>[Aktivieren der automatischen Registrierung von Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | Die Lizenz des Benutzers weist einen fehlerhaften Status auf und blockiert die Registrierung.<br><br>[Zuweisen von Lizenzen zu Benutzern](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Tritt beim Versuch der automatischen Registrierung bei Intune auf, wenn die Azure AD-Konfiguration nicht vollständig angewendet wurde. Dieses Problem sollte vorübergehend sein, da das Gerät nach kurzer Zeit Wiederholungsversuche ausführt. |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | Der Benutzer hat den Vorgang abgebrochen.<br><br>Wenn die MDM-Anmeldung mehrstufige Authentifizierung erfordert und der Benutzer sich nicht mit einer unterstützten zweiten Stufe angemeldet hat, zeigt Windows dem Benutzer eine Popupbenachrichtigung an, dass er sich anmelden soll. Wenn der Benutzer auf die Popupbenachrichtigung nicht reagiert, tritt dieser Fehler auf. Dieses Problem sollte vorübergehend sein, weil Configuration Manager einen Wiederholungsversuch ausführt und den Benutzer zur Anmeldung auffordert. Benutzer sollten mehrstufige Authentifizierung verwenden, wenn sie sich bei Windows anmelden. Informieren Sie sie auch darüber, dass ein solches Verhalten zu erwarten ist und Maßnahmen ergriffen werden müssen, wenn sie dazu aufgefordert werden. | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Verwaltung mobiler Geräte wird allgemein nicht unterstützt. | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Fehler bei Authentifizierung des Benutzers durch den Server.<br><br> Es ist kein Azure AD-Token für den Benutzer vorhanden. Stellen Sie sicher, dass sich der Benutzer in Azure AD authentifizieren kann. |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | Die automatische MDM-Registrierung wird nur unter Windows RS3 und höher unterstützt.<br><br>Stellen Sie sicher, dass das Gerät die [Mindestanforderungen](overview.md#windows-10) für Co-Verwaltung erfüllt. |
| 3400073293 | ADAL-Benutzerbereich-Kontoantwort unbekannt.<br><br>Überprüfen Sie die Azure AD-Konfiguration, und stellen Sie sicher, dass sich Benutzer erfolgreich authentifizieren können. | 
| 3399548929 | Benutzeranmeldung erforderlich.<br><br>Dieses Problem sollte vorübergehend sein. Es tritt auf, wenn sich der Benutzer schnell abmeldet, bevor der Registrierungstask erfolgt. | 
| 3400073236 | Fehler bei der ADAL-Sicherheitstokenanforderung.<br><br>Überprüfen Sie die Azure AD-Konfiguration, und stellen Sie sicher, dass sich Benutzer erfolgreich authentifizieren können. |
| 2149122477 | Generisches HTTP-Problem. |
| 3400073247 | ADAL-integrierte Windows-Authentifizierung wird nur im Verbundfluss unterstützt.<br><br>[Planen der Implementierung Ihrer Azure Active Directory-Hybrideinbindung](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | Der Server oder Proxy wurde nicht gefunden.<br><br>Dieses Problem sollte vorübergehend sein, wenn der Client nicht mit der Cloud kommunizieren kann. Wenn es weiterhin besteht, stellen Sie sicher, dass der Client über konsistente Konnektivität mit Azure verfügt. | 
| 2149056532 | Die jeweilige Plattform oder Version wird nicht unterstützt.<br><br>Stellen Sie sicher, dass das Gerät die [Mindestanforderungen](overview.md#windows-10) für Co-Verwaltung erfüllt. |
| 2147943568 | Das Element wurde nicht gefunden.<br><br>Dieses Problem sollte vorübergehend sein. Wenn das Problem weiterhin auftritt, wenden Sie sich an den Microsoft-Support. |
| 2192179208 | Für die Verarbeitung dieses Befehls sind nicht genügend Speicherressourcen verfügbar.<br><br>Dieses Problem sollte vorübergehend sein und durch einen Wiederholungsversuch des Clients behoben werden. |
| 3399614467 | Fehler bei der ADAL-Autorisierungsgewährung für diese Assertion.<br><br>Überprüfen Sie die Azure AD-Konfiguration, und stellen Sie sicher, dass sich Benutzer erfolgreich authentifizieren können. |
| 2149056517 | Generischer Fehler vom Verwaltungsserver, z.B. DB-Zugriffsfehler.<br><br>Dieses Problem sollte vorübergehend sein. Wenn das Problem weiterhin auftritt, wenden Sie sich an den Microsoft-Support. |
| 2149134055 | Der WinHTTP-Name wurde nicht aufgelöst.<br><br>Der Client kann den Namen des Diensts nicht auflösen. Überprüfen Sie die DNS-Konfiguration. | 
| 2149134050 | Internettimeout.<br><br>Dieses Problem sollte vorübergehend sein, wenn der Client nicht mit der Cloud kommunizieren kann. Wenn es weiterhin besteht, stellen Sie sicher, dass der Client über konsistente Konnektivität mit Azure verfügt. |

Weitere Informationen finden Sie unter [Fehlerwerte für MDM-Registrierung](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants).

## <a name="deployment-policies"></a>Bereitstellungsrichtlinien

Im Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung** wurden zwei Richtlinien erstellt. Eine Richtlinie ist für die Pilotgruppe und die andere für die Produktion. Diese Richtlinien melden nur die Anzahl der Geräte, auf die Configuration Manager die Richtlinie angewendet hat. Dabei wird nicht berücksichtigt, wie viele Geräte bei Intune registriert sind, was eine Voraussetzung dafür ist, dass Geräte gemeinsam verwaltet werden können.  

Die Produktionsrichtlinie (CoMgmtSettingsProd) zielt auf die Sammlung **Alle Systeme** ab. Sie enthält eine Anwendbarkeitsbedingung, mit der Typ und Version des Betriebssystems überprüft werden. Handelt es sich beim Client um ein Serverbetriebssystem bzw. nicht um Windows 10, gilt die Richtlinie nicht, und es wird keine Aktion ausgeführt.

## <a name="wmi-device-data"></a>WMI-Gerätedaten

Fragen Sie die WMI-Klasse **SMS_Client_ComanagementState** ab. Sie können in Configuration Manager benutzerdefinierte Sammlungen erstellen, um den Bereitstellungsstatus Ihrer Co-Verwaltung zu ermitteln. Weitere Informationen zum Erstellen benutzerdefinierter Sammlungen finden Sie unter [Erstellen von Sammlungen](../core/clients/manage/collections/create-collections.md).

Die folgenden Felder sind in der WMI-Klasse verfügbar:  

- **MachineId:** Eine eindeutige Geräte-ID für den Configuration Manager-Client.  

- **MDMEnrolled:** Gibt an, ob das Gerät bei MDM registriert ist.  

- **Autorität:** Die Autorität, für die das Gerät registriert ist.  

- **ComgmtPolicyPresent:** Gibt an, ob die Co-Verwaltungsrichtlinie von Configuration Manager auf dem Client vorhanden ist. Wenn **MDMEnrolled** den Wert **0** aufweist, wird das Gerät nicht gemeinsam verwaltet, und zwar unabhängig davon, ob die Co-Verwaltungsrichtlinie auf dem Client vorhanden ist.  

Ein Gerät unterliegt der Co-Verwaltung, wenn die Felder **MDMEnrolled** und **ComgmtPolicyPresent** den Wert **1** haben.  
