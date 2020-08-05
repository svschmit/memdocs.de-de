---
title: FAQ zu Windows Autopilot
ms.reviewer: This topic provides OEMs, partners, administrators, and end users with answers to some frequently asked questions about deploying Windows 10 with Windows Autopilot.
manager: laurawi
description: Support Informationen für Windows Autopilot
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 060f2188be0c4674a7770e36c4bfdf26def669f4
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756775"
---
# <a name="windows-autopilot-faq"></a>FAQ zu Windows Autopilot

**Gilt für: Windows 10**

Dieser Artikel bietet OEMs, Partnern, Administratoren und Endbenutzern Antworten auf einige häufig gestellte Fragen zur Bereitstellung von Windows 10 mit Windows Autopilot. 

Ein [Glossar](#glossary) der Abkürzungen, die in diesem Artikel verwendet werden, wird am Ende bereitgestellt.


## <a name="microsoft-partner-center"></a>Microsoft Partner Center

| Frage | Antwort |
| --- | --- |
| Im Partner Center muss die Mandanten-ID bei jedem Hochladen von Gerätedateien bereitgestellt werden? Ist es erforderlich, dass der geschäftliche Kunde auf seine Geräte in Microsoft Store for Business (msfb) zugreifen kann?     | Nein. Die Angabe der Mandanten-ID ist ein Einzeiger Eintrag im Partner Center, der mit zukünftigen Geräte Uploads wieder verwendet werden kann. |
| Wie weiß der Kunde oder Mandant, dass seine Geräte in msfb beansprucht werden können?    |  Nachdem der Upload der Gerätedatei im Partner Center abgeschlossen ist, kann der Mandant die für das Windows Autopilot-Setup verfügbaren Geräte in msfb sehen. Der OEM muss dem Mandanten den Zugriff auf msfb mitteilen. Die automatische Identifizierung von msfb zum Mandanten wird entwickelt.  |
| Wie autorisiere ein Kunde einen OEM-oder Channel-Partner, Autopilot-Geräte im Auftrag des Kunden zu registrieren?   |  Bevor ein OEM-oder Kanal Partner ein Gerät für Autopilot im Auftrag eines Kunden registrieren kann, muss der Kunde ihm zunächst seine Zustimmung erteilen.  Der Genehmigungsprozess beginnt mit dem OEM-oder Channel-Partner, der einen Link zum Kunden sendet, der den Kunden zu einer Zustimmungs Seite in msfb leitet.  Weitere Informationen finden Sie unter [Registrierung](registration-auth.md).  |
|  Gibt es Einschränkungen, wenn ein Geschäftskunde Geräte in msfb registriert hat und diese Geräte später durch einen cloudlösungsanbieter (Cloud Solution Provider, CSP) über das Partner Center verwaltet werden sollen? | Die Geräte müssen vom Kunden des Unternehmens in msfb gelöscht werden, bevor Sie vom CSP im Partner Center hochgeladen und verwaltet werden können. | 
| Unterstützt Windows Autopilot das Entfernen der Option zum Aktivieren eines lokalen Administrator Kontos?    |  Das Entfernen des lokalen Administrator Kontos wird von Windows Autopilot nicht unterstützt. Es unterstützt jedoch das Einschränken des Benutzers, der Azure Active Directory (Azure AD)-Domänen Beitritt in OOBE in ein Standardkonto (im Gegensatz zu einem Administrator Konto standardmäßig) ausführt.|
| Wie kann ich die Windows Autopilot-CSV-Datei im Partner Center testen?    |  Nur CSP-Partner haben Zugriff auf das Partner Center-Portal. Wenn Sie CSP sind, können Sie ein Sales Agent-Benutzerkonto erstellen, das Zugriff auf Geräte hat, um die Datei zu testen. Dies kann heute im Partner Center erfolgen. <br><br>Weitere Informationen finden Sie unter [Erstellen von Benutzerkonten und Festlegen von Berechtigungen](https://msdn.microsoft.com/partner-center/create-user-accounts-and-set-permissions). |
|  Muss ich ein CSP werden, um an Windows Autopilot teilnehmen zu können? | Die wichtigsten Volumen OEMs sind nicht, da Sie die OEM Direct-API verwenden können.  Alle anderen Benutzer, die die Verwendung von MPC zum Registrieren von Geräten auswählen, müssen CSPs werden, um auf MPC zugreifen zu können.  |
| Verfügen die verschiedenen CSP-Ebenen über die gleichen Funktionen, wenn es um Windows Autopilot geht?   |  Für Windows Autopilot gibt es drei verschiedene Arten von CSPs, die jeweils über unterschiedliche autoritätsstufen und Zugriff verfügen: <br><br>1. <b>Direct CSP</b>: Ruft die direkte Autorisierung vom Kunden zum Registrieren von Geräten ab. <br><br>2. <b>indirekter CSP-Anbieter</b>: Ruft die implizite Berechtigung zum Registrieren von Geräten über die Beziehung ab, die ihr CSP-Reseller-Partner mit dem Kunden hat.  Indirekte CSP-Anbieter registrieren Geräte über das Microsoft Partner Center. <br><br>3. <b>indirekter CSP-Reseller</b>: Ruft die direkte Autorisierung vom Kunden zum Registrieren von Geräten ab.  Gleichzeitig erhält der indirekte CSP-Anbieter Partner auch die Autorisierung, was bedeutet, dass entweder der indirekte Anbieter oder der indirekte Reseller Geräte für den Kunden registrieren kann.  Allerdings muss der indirekte CSP-Reseller Geräte über die MPC-Benutzeroberfläche registrieren (Manuelles Hochladen der CSV-Datei), während der indirekte CSP-Anbieter die Möglichkeit hat, Geräte mithilfe der MPC-APIs zu registrieren. |


## <a name="manufacturing"></a>Fertigung

| Frage | Antwort |
| --- | --- |
| Welche Änderungen müssen im Betriebssystem Image für die Kunden Konfigurationseinstellungen vorgenommen werden?     |Im Werk ist keine Änderung erforderlich, um die Windows Autopilot-Bereitstellung zu aktivieren.  |
| Welche Version des OA3-Tools erfüllt die Windows Autopilot-Bereitstellungs Anforderungen?     | Windows Autopilot kann mit jeder Version des OA3-Tools verwendet werden. Es wird empfohlen, eine unterstützte Version des halbjährlichen Kanals von Windows 10 zu verwenden, um den 4K-Hardware Hash zu generieren.    |
|  Wenn Kunden zum Zeitpunkt der Bestellung eine Bestellung haben möchten, müssen Sie Ihre Kunden mit oder ohne Windows Autopilot-Optionen angeben?   | Ja, wenn Sie Windows Autopilot wünschen, benötigen Sie eine unterstützte Version des halbjährlichen Kanals von Windows 10. Außerdem ist es ratsam, die CSV-Datei zu erhalten oder den Datei Upload (d. h. die Registrierung) in Ihrem Namen abzuschließen.    |
|  Muss der OEM benutzerdefinierte Abbild Erstellungs Dateien von Kunden verwalten oder erfassen und Image Uploads an Microsoft durchführen?   | Keine Änderung, OEMs senden die cbrs einfach wie gewohnt an Microsoft. Es werden keine Images an Microsoft gesendet, um Windows Autopilot zu aktivieren.  Windows Autopilot passt nur OOBE an und ermöglicht Richtlinien Konfigurationen (z. b. das Administrator Konto).  |
|  Gibt es Kunden Auswirkungen auf das Upgrade von Windows 8 auf Windows 10?    | Auf den Geräten muss eine unterstützte Version des halbjährlichen Kanals von Windows 10 ausgeführt werden, um sich bei der Windows Autopilot-Bereitstellung anzumelden. Andernfalls gibt es keine Auswirkungen.    |
| Gibt es eine Änderung an der vorhandenen CBR mit einem Hardware-Hashwert von 4K?    | Nein.  |
| Welche neuen Informationen müssen vom OEM an Microsoft gesendet werden?    | Nichts, es sei denn, der OEM kann das Gerät im Auftrag des Kunden registrieren. in diesem Fall würden Sie die Geräte-ID mithilfe einer CSV-Datei in das Microsoft Partner Center hochladen oder die OEM Direct-API verwenden.  |
| Gibt es einen Vertrag oder einen Zusatz für einen OEM zur Teilnahme an der Windows Autopilot-Bereitstellung?    | Nein.  |

## <a name="csv-schema"></a>CSV-Schema

| Frage | Antwort |
| --- | --- |
|  Kann ein Komma in der CSV-Datei verwendet werden? | Nein.   |
| Welche Fehlermeldungen können vom Benutzer beim Hochladen einer Datei im Partner Center oder msfb angezeigt werden?    | Weitere Informationen finden Sie im Abschnitt in Microsoft Store for Business dieses Handbuchs.  |
| Gibt es eine Beschränkung für die Anzahl der Geräte, die in der CSV-Datei aufgelistet werden können?    | Ja, die CSV-Datei kann nur 1.000-Geräte enthalten, die auf ein einzelnes Profil angewendet werden können. Wenn mehr als 1.000 Geräte auf ein Profil angewendet werden müssen, müssen die Geräte über mehrere CSV-Dateien hochgeladen werden.    |
| Hat Microsoft Empfehlungen dazu, wie ein OEM die CSV-Datei für Ihre Kunden bereitstellen sollte?    |  Es wird empfohlen, die CSV-Datei beim Senden an den Geschäftskunden zu verschlüsseln, um Ihre Windows Autopilot-Geräte selbst zu registrieren (entweder über MPC, msfb oder InTune).   |


## <a name="hardware-hash"></a>Hardwarehash

| Frage | Antwort |
| --- | --- |
| Muss jeder vom OEM gesendete Hardware Hash die SMBIOS-UUID (universell eindeutiger Bezeichner), die Mac-Adresse (Media Access Control) und die Seriennummer des eindeutigen Datenträgers (bei Verwendung des Windows 10 OEM Activation 3,0-Tools) enthalten?    | Ja. Da Windows Autopilot auf der Fähigkeit basiert, Geräte, die auf die cloudkonfiguration angewendet werden, eindeutig zu identifizieren, ist es wichtig, hardwarehashes zu übermitteln, die den beschriebenen Anforderungen entsprechen.   |
| Was ist der Grund für die Notwendigkeit, die SMBIOS-UUID, Mac-Adresse und Datenträger Seriennummer in den Hardware Hash Details zu benötigen?    | Zum Erstellen des Hardware Hashs sind dies die Felder, die zum Identifizieren eines Geräts erforderlich sind, da Teile des Geräts hinzugefügt oder entfernt werden. Da wir keinen eindeutigen Bezeichner für Windows-Geräte haben, ist dies die beste Logik, um ein Gerät zu identifizieren.    |
| Worin besteht der Unterschied zwischen OA3 Hardware Hash, 4K Hardware Hash und Windows Autopilot Hardware Hash?    | Keine.  Sie sind unterschiedliche Namen für dasselbe.  Die Ausgabe des OA3-Tools heißt OA3 Hash mit einer Größe von 4 KB, der für das Windows Autopilot-Bereitstellungs Szenario verwendet werden kann. Hinweis: Wenn Sie eine ältere, nicht unterstützte Windows-Version OA3Tool verwenden, erhalten Sie einen anderen Hashwert, der möglicherweise nicht für die Windows Autopilot-Bereitstellung verwendet wird.  |
|  Wie geht es um das ersetzen und Reparieren von Teilen für die NIC (Netzwerkschnittstellen Controller) und den Datenträger? Wird der Hardware Hash ungültig?   |  Ja.  Wenn Sie Teile ersetzen, müssen Sie den neuen Hardwarehash erfassen, obwohl er davon abhängt, was ersetzt wird, und die Merkmale der Teile. Wenn Sie z. b. das TPM oder die Hauptplatine ersetzen, handelt es sich um ein neues Gerät, und Sie müssen über einen neuen Hardware Hash verfügen. Wenn Sie eine Netzwerkkarte ersetzen, ist dies wahrscheinlich kein neues Gerät, und das Gerät wird mit dem alten Hardware Hash funktionieren.  Als bewährte Vorgehensweise sollten Sie jedoch davon ausgehen, dass der alte Hardwarehash ungültig ist und nach Hardwareänderungen einen neuen Hardware Hash erhält. Dies wird empfohlen, wenn Sie Teile ersetzen. |

## <a name="motherboard-replacement"></a>Ersetzung von Motherboards

| Frage | Antwort |
| --- | --- |
| Wie behandelt Autopilot die Ersetzungs Szenarios?  |  Der Austausch von Motherboards ist für den Bereich für Autopilot nicht vorgesehen. Alle Geräte, die auf eine Weise repariert oder gewartet werden, die die Fähigkeit zur Identifizierung des Geräts für Windows Autopilot ändert, müssen den normalen OOBE-Prozess durchlaufen und die richtigen Einstellungen manuell auswählen oder ein benutzerdefiniertes Image anwenden, wie es heute der Fall ist.  <br><br>Um das gleiche Gerät für Windows Autopilot nach einem Motherboard-Austausch wiederzuverwenden, muss das Gerät von Autopilot deaktiviert werden, die Platine ersetzt, eine neue 4-KB-Nummer erfasst und dann mithilfe des neuen Hardware Hashs (oder der Geräte-ID) von 4K erneut registriert werden. <br><br>**Hinweis**: ein OEM kann die OEM Direct-API nicht zum erneuten Registrieren des Geräts verwenden, da die OEM Direct-API nur ein Tupel oder pkid akzeptiert.  In diesem Fall müsste der OEM entweder die neuen Hardware Hash Informationen von 4K mithilfe einer CSV-Datei an den Kunden senden und dem Kunden ermöglichen, das Gerät mit msfb oder InTune erneut zu registrieren.|

## <a name="smbios"></a>SMBIOS

| Frage | Antwort |
| --- | --- |
| Alle speziellen Anforderungen an die SMBIOS-UUID?    | Er muss eindeutig sein, wie in den Windows 10-Hardwareanforderungen angegeben.    |
| Welche Anforderungen erfüllt die SMBIOS-Tabelle, um den Windows Autopilot-Hardware Hash Bedarf zu erfüllen?    | Er muss alle Windows 10-Hardwareanforderungen erfüllen.  Weitere Informationen finden Sie [hier](https://msdn.microsoft.com/library/jj128256(v=vs.85).aspx).    |
| Wenn das SMBIOS UUID und Seriennummer unterstützt, ist es ausreichend, damit das OA3-Tool den Hardware Hash generiert?    | Nein.  Die folgenden SMBIOS-Felder müssen mindestens mit eindeutigen Werten aufgefüllt werden: productkeyid smbiossystemhersteller smbiossystemproductname smbiossystemserialnumber smbiosskunzuber smbiossystemfamily MACAddress smbiosuuid diskserialnumber TPM ekpub |

## <a name="technical-interface"></a>Technische Oberfläche

| Frage | Antwort |
| --- | --- |
|  Was ist die Schnittstelle, um die Mac-Adresse und die Datenträger Seriennummer zu erhalten? Wie erhält das OA-Tool den Mac und die Seriennummer des Datenträgers?   | Die Seriennummer des Datenträgers wurde in IOCTL_STORAGE_QUERY_PROPERTY mit storagedeviceproperty/propertystandardquery gefunden.   Die Mac-Adresse des Netzwerks wird von OID_802_3_PERMANENT_ADDRESS IOCTL_NDIS_QUERY_GLOBAL_STATS.  Die Methode zum Ausführen dieses Vorgangs variiert jedoch je nach Szenario.  |
| Nachverfolgung: Wenn 2-3 Macs auf dem System vorhanden sind, wie kann das OA-Tool auswählen, welche Mac-Adresse und die Seriennummer des Datenträgers auf dem System vorhanden sind, weil mehrere Instanzen von jeweils vorhanden sind? Welche Mac-Plattform wird ausgewählt, wenn eine Plattform über LAN und WLAN verfügt?     |  Kurz gesagt werden alle verfügbaren Werte verwendet.  Im Detail gibt es möglicherweise bestimmte Verwendungs Regeln. Die Seriennummer des System Datenträgers ist wichtiger als die anderen verfügbaren Datenträger. Austauschbare Netzwerkschnittstellen sollten nicht verwendet werden, wenn Sie beim Austausch erkannt werden. LAN und WLAN sollten nicht von Bedeutung sein, da beide verwendet werden.  |

## <a name="the-end-user-experience"></a>Ablauf für den Endbenutzer

|Frage|Antwort|
|----|-----|
|Gewusst wie wissen, dass ich Autopilot erhalten habe?|Sie können feststellen, dass Sie Windows Autopilot erhalten haben (wie auf dem Gerät, das eine Konfiguration erhalten hat, aber noch nicht angewendet hat), wenn Sie die Auswahl Seite überspringen (wie unten gezeigt), und sofort zu einer generischen oder angepassten Anmeldeseite gelangen.|
|Windows Autopilot war nicht funktionsfähig. Was soll ich jetzt tun?| Fragen und Aktionen zur Unterstützung bei der Problembehandlung: wurde ein Bildschirm nicht übersprungen?   Wurde ein Benutzer als Administrator beendet, wenn er nicht auf konfiguriert ist? Beachten Sie, dass Azure AD Administratoren lokale Administratoren sein werden, unabhängig davon, ob Windows Autopilot zum Deaktivieren der Informationen zur lokalen Administrator Sammlung konfiguriert ist: führen Sie licensingdiag.exe aus, und senden Sie die CAB-Datei (CAB-Datei), die an generiert wird AutopilotHelp@microsoft.com . Erfassen Sie nach Möglichkeit eine ETL aus Windows Performance Recorder (WPR). In diesen Fällen melden sich Benutzer oft nicht bei dem richtigen Azure AD Mandanten an oder erstellen lokale Benutzerkonten.  Eine umfassende Liste der Supportoptionen finden Sie unter [Windows Autopilot-Unterstützung](autopilot-support.md). |
| Wenn ein Administrator Änderungen an einem vorhandenen Profil vornimmt, werden die Änderungen auf Geräten wirksam, denen dieses Profil zugewiesen ist, die bereits bereitgestellt wurden? |Nein. Windows Autopilot-Profile sind nicht auf dem Gerät ansässig. Sie werden während der OOBE heruntergeladen, die zu diesem Zeitpunkt definierten Einstellungen werden angewendet. Anschließend wird das Profil auf dem Gerät verworfen. Wenn das Gerät neu erstellt oder zurückgesetzt wird, werden die neuen Profileinstellungen beim nächsten durchlaufen des Geräts wirksam.|
|Wie sieht die Erfahrung aus, wenn ein Gerät nicht registriert ist oder wenn ein IT-Administrator Windows Autopilot nicht konfiguriert, bevor ein Endbenutzer versucht, sich selbst bereitzustellen? |Wenn das Gerät nicht registriert ist, wird es nicht in Windows Autopilot angezeigt, und der Endbenutzer wird das normale OOBE durchlaufen. Die Windows Autopilot-Konfigurationen werden erst angewendet, wenn der Benutzer nach der Registrierung erneut OOBE durchläuft. Wenn ein Gerät gestartet wird, bevor ein MDM-Profil erstellt wird, durchläuft das Gerät die standardmäßige OOBE-Darstellung.  Der IT-Administrator müsste dieses Gerät dann manuell bei der MDM registrieren, nachdem das Gerät das nächste Mal zurückgesetzt wird, wird es in der Windows Autopilot OOBE-Darstellung durchlaufen.|
|Warum erhalte ich keinen angepassten Anmeldebildschirm bei Autopilot? |Das Mandanten Branding muss in Portal.Azure.com konfiguriert werden, um eine angepasste Anmelde Funktion zu erhalten.|
|Was geschieht, wenn ein Gerät bei Azure AD registriert ist, aber kein Windows Autopilot-Profil zugewiesen wurde?                                |Der reguläre Azure AD OOBE tritt auf, da dem Gerät kein Windows Autopilot-Profil zugewiesen wurde.|
|Wie kann ich Protokolle auf Autopilot erfassen?|Die beste Möglichkeit, Protokolle auf Windows Autopilot-Leistung zu erfassen, besteht darin, eine WPR-Ablauf Verfolgung während OOBE zu erfassen. Die XML-Datei (wprp-Erweiterung) für diese Ablauf Verfolgung kann auf Anforderung bereitgestellt werden.|

## <a name="mdm"></a>MDM

| Frage | Antwort |
| --- | --- |
| Muss InTune für unsere MDM verwendet werden?  |  Nein, jede MDM funktioniert mit Autopilot, aber andere verfügen wahrscheinlich nicht über dieselbe vollständige Sammlung von Windows Autopilot-Features wie InTune.  Sie erhalten das Beste aus InTune. |
| Kann InTune Win32-App-Vorinstallationen unterstützen?  | Ja.  Ab dem Windows 10-Update für Oktober (Version 1809) unterstützt InTune Win32-apps mit MSI-und msix-Wrapper.  |
| Was ist Co-Verwaltung?  | Die Co-Verwaltung ist, wenn Sie eine Kombination aus einem Cloud-MDM-Tool (InTune) und einem lokalen Konfigurationstool wie Microsoft Endpoint Configuration Manager verwenden. Sie müssen den Configuration Manager nur verwenden, wenn InTune nicht unterstützt, was Sie mit Ihrem Profil ausführen möchten.  Wenn Sie sich für die Co-Verwaltung mit InTune und Configuration Manager entscheiden, müssen Sie dazu einen Configuration Manager-Agent in Ihr InTune-Profil einschließen. Wenn dieses Profil per Pushvorgang auf das Gerät übermittelt wird, wird der Configuration Manager-Agent angezeigt, und der Configuration Manager wird zum Abrufen zusätzlicher Profileinstellungen verwendet. |
| Muss Microsoft Endpoint Configuration Manager für Windows Autopilot verwendet werden  |  Nein.  Die Co-Verwaltung (oben beschrieben) ist optional. |


## <a name="features"></a>Features

| Frage | Antwort |
| --- | --- |
| Selbstbereitstellungs Modus  | Eine neue Version von Windows Autopilot, bei der der Benutzer nur das Gerät schaltet, und nichts anderes.  Dies ist nützlich für Szenarien, in denen ein Standardbenutzer Konto nicht benötigt wird (z. b. freigegebene Geräte oder Kiosk-Geräte).  |
| Hybrid Azure Active Directory beitreten  |  Ermöglicht Windows Autopilot-Geräten das Herstellen einer Verbindung mit einem lokalen Active Directory Domänen Controller (zusätzlich zu Azure AD verknüpft). |
| Windows Autopilot Reset  | Entfernt Benutzer-apps und-Einstellungen von einem Gerät, behält jedoch Azure AD Domänen Beitritt und MDM-Registrierung bei.  Nützlich, wenn ein Gerät von einem Benutzer auf einen anderen übertragen wird.  |
| Personalisierung  | Fügt der OOBE-Darstellung Folgendes hinzu: eine personalisierte Willkommensnachricht kann erstellt werden. Ein Benutzernamen Hinweis kann hinzugefügt werden. der Text der Anmeldeseite kann personalisiert werden. Das Logo des Unternehmens kann eingeschlossen werden. |
| [Autopilot für vorhandene Geräte](existing-devices.md)  |  Bietet einen Upgradepfad zu Windows Autopilot für alle vorhandenen Windows 7-und Windows 8-basierten Geräte. |



## <a name="general"></a>Allgemein

|Frage|Antwort
|------------------|-----------------|
|Wenn ich den Computer neu verwende und neu verwende, erhalte ich weiterhin Windows Autopilot?|Ja, wenn das Gerät weiterhin für Windows Autopilot registriert ist und eine unterstützte Version des halbjährlichen Kanals von Windows 10 ausgeführt wird, wird die Windows Autopilot-Funktion empfangen.|
|Kann ich den Geräte Fingerabdruck auf vorhandenen Computern ernten?|Ja, wenn auf dem Gerät eine unterstützte Version des halbjährlichen Kanals von Windows 10 ausgeführt wird, können Sie Geräte Fingerabdrücke für die Registrierung sammeln. Es ist nicht geplant, die Funktionalität auf ältere Releases zu portieren, und Sie können Sie nicht auf Geräten mit nicht unterstützten Versionen von Windows sammeln.|
|Wird Windows Autopilot von anderen SKUs unterstützt, z. b. Surface Hub, hololens und Windows Mobile.|Nein, Windows Autopilot wird von anderen SKUs nicht unterstützt.|
|Funktioniert Windows Autopilot nach einer MBR-oder Image-Neuinstallation?|Ja.|
| Können Computer, die mehrmals neu erstellt wurden, Autopilot durchlaufen? Was bedeutet die Fehlermeldung "dieser Benutzer ist nicht zum Registrieren autorisiert"? Fehlercode 801c0003. |Es gibt Grenzwerte für die Anzahl der Geräte, die ein bestimmter Azure AD Benutzer in Azure AD registrieren kann, sowie die Anzahl der Geräte, die pro Benutzer in InTune unterstützt werden.  (Diese sind konfigurierbar, aber nicht unendlich.)  Dies tritt häufig auf, wenn Sie die Geräte wieder verwenden oder wenn Sie ein Rollback auf vorherige Momentaufnahmen des virtuellen Computers ausführen.|
|Was geschieht, wenn ein Gerät bei einem böswilligen Agent registriert wird?                                                   |Windows Autopilot wendet das Profil erst dann an, wenn sich der Benutzer mit dem entsprechenden Mandanten für das konfigurierte Azure AD Profil anmeldet. Was geschieht, ist nachstehend dargestellt.  Wenn badguys.com ein Gerät registriert, das im Besitz von contoso.com ist, wird der Benutzer am schlechtesten zum Anmelden bei badguys.com geleitet. Wenn der Benutzer seine e-Mail-Adresse/das Kennwort eingibt, werden die Anmelde Informationen über Azure AD an die ordnungsgemäße Azure AD Authentifizierung umgeleitet, und der Benutzer wird aufgefordert, sich bei Contoso.com anzumelden. Da contoso.com nicht mit badguys.com als Mandant identisch ist, wird das Windows Autopilot-Profil nicht angewendet, und das reguläre Azure AD OOBE-Vorgang wird ausgeführt.|
|Wo werden die Windows Autopilot-Daten gespeichert?                                                            |Windows Autopilot-Daten werden in der USA (USA) und nicht in einem Sovereign Cloud gespeichert, auch wenn der Azure AD Mandanten in einem Sovereign Cloud registriert ist. Dies gilt für alle Windows Autopilot-Daten, unabhängig davon, welches Portal zum Bereitstellen von Autopilot genutzt wird.|
|Warum werden Windows Autopilot-Daten in den USA und nicht in einem Sovereign Cloud gespeichert?|Dabei handelt es sich nicht um Kundendaten, die wir speichern, sondern um Unternehmensdaten, die Microsoft die Bereitstellung eines Dienstanbieter ermöglichen, sodass sich die Daten in den USA befinden. Kunden können den Dienst jederzeit jederzeit abonnieren, und in diesem Fall werden die Geschäftsdaten von Microsoft entfernt.|
|Wie viele Möglichkeiten gibt es, ein Gerät für Windows Autopilot zu registrieren?|Es gibt sechs Möglichkeiten, ein Gerät zu registrieren, je nachdem, wer die Registrierung durchläuft: <br><br>1. OEM Direct-API (nur für tvos verfügbar) <br>2. MPC mit der MPC-API (muss ein CSP sein) <br>3. MPC mit manuellem Hochladen der CSV-Datei in der Benutzeroberfläche (muss ein CSP sein) <br>4. msfb mit CSV-Datei Upload <br>5. InTune mit CSV-Datei Upload <br>6. Microsoft 365 Business-Portal mit CSV-Datei Upload|
|Wie viele Möglichkeiten gibt es, ein Windows Autopilot-Profil zu erstellen?|Es gibt vier Möglichkeiten, ein Windows Autopilot-Profil zu erstellen und zuzuweisen: <br><br>1. bis MPC (muss ein CSP sein) <br>2. über msfb <br>3. über InTune (oder eine andere MDM) <br>4. Microsoft 365 Business-Portal <br><br>Microsoft empfiehlt die Erstellung und Zuweisung von Profilen über InTune.  |
| Was sind einige häufige Gründe für Registrierungsfehler? |1. ungültige oder fehlende Hardware Hash Einträge können zu fehlerhaften Registrierungs versuchen führen. <br>2. ausgeblendete Sonderzeichen in CSV-Dateien.  <br><br>Um dieses Problem zu vermeiden, öffnen Sie es nach dem Erstellen der CSV-Datei in Editor, um nach ausgeblendeten oder nachfolgenden Leerzeichen oder anderen Beschädigungen zu suchen.|
|  Wird Autopilot auf IOT-Geräten unterstützt? |  Autopilot wird auf IOT Core-Geräten nicht unterstützt, und es ist zurzeit nicht geplant, diese Unterstützung hinzuzufügen. Autopilot wird auf Windows 10 IOT Enterprise SAC-Geräten unterstützt. Autopilot wird unter Windows 10 Enterprise LTSC 2019 und höher unterstützt. in früheren Versionen von LTSC wird dies nicht unterstützt.|
|  Wird Autopilot in allen Regionen/Ländern unterstützt? |  Autopilot unterstützt nur Kunden, die Global Azure verwenden. Globale Azure umfasst nicht die drei unten aufgeführten Entitäten:<br>-Azure Deutschland <br>-Azure China 21ViaNet<br>-Azure Government<br>Wenn also ein Kunde in einer globalen Azure-Umgebung eingerichtet ist, gibt es keine Einschränkungen hinsichtlich der Region. Wenn z. b. "Azure Global Azure" verwendet, aber Mitarbeiter in China arbeiten, können die Mitarbeiter von Azure, die in China arbeiten, mit Autopilot Geräte bereitstellen. Wenn Azure China 21ViaNet von Azure verwendet wird, sind die Mitarbeiter von "Azure" nicht in der Lage, Autopilot zu verwenden.|

## <a name="glossary"></a>Glossar

| Begriff | Bedeutung |
| --- | --- |
| CSV  | Durch Trennzeichen getrennte Werte (Dateityp ähnlich wie Excel-Tabelle)  |
| MPC  | Microsoft Partner Center   |
| MDM  | Verwaltung mobiler Geräte   |
| OEM  | Original Equipment Manufacturer   |
| CSP  |  Cloud Solution Provider  |
| Msfb  | Microsoft Store für Unternehmen   |
| Azure AD  | Azure Active Directory   |
| 4K HH  |  4K Hardware Hash |
| CBR  | Bericht "Computer Erstellung"  |
| EC  |  Unternehmens Commerce  |
| DDS  | Geräte Verzeichnisdienst    |
| OOBE  | Standardmäßig   |
| UUID  | Universell eindeutiger Bezeichner   |
