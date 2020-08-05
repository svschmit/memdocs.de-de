---
title: Windows Autopilot-Motherboard-Ersetzung
ms.reviewer: ''
manager: laurawi
description: MBR-Szenarien für Windows Autopilot Deployment
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 4c8e66e9fb0ac4527f10824332f8ac5ae1646181
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756770"
---
# <a name="windows-autopilot-motherboard-replacement-scenario-guidance"></a>Leitfaden für Windows Autopilot-Austausch Szenarios

**Zielgruppe**

- Windows 10

Dieses Dokument enthält Anleitungen für Windows Autopilot-Geräte Reparatur Szenarien, die Microsoft-Partner in den MBR-Situationen (Motherboard Replace) und in anderen Wartungs Szenarien verwenden können.

Das Reparieren von Autopilot-registrierten Geräten ist komplex, da versucht wird, OEM-Anforderungen mit den Windows Autopilot-Anforderungen auszugleichen.  Der OEM erfordert insbesondere eine strikte Eindeutigkeit in den einzelnen Fenstern, Mac-Adressen usw., während Windows Autopilot auf der Hardware-ID-Ebene für jedes Gerät eine strikte Eindeutigkeit erfordert, um eine erfolgreiche Registrierung zu ermöglichen.  Die Hardware-ID erfüllt nicht immer alle OEM-Hardwarekomponenten Anforderungen, daher treten diese Anforderungen manchmal in Konflikt, was zu Problemen mit einigen Reparatur Szenarios führt.

**Ersetzung von Motherboards (MBR)**

Wenn auf einem Windows Autopilot-Gerät ein Ersetzungs Austausch erforderlich ist, wird der folgende Prozess empfohlen:

1. Aufheben [der Registrierung des Geräts](#deregister-the-autopilot-device-from-the-autopilot-program) bei Windows Autopilot
2. [Ersetzen der Hauptplatine](#replace-the-motherboard)
3. [Neue Geräte-ID erfassen (4K HH)](#capture-a-new-autopilot-device-id-4k-hh-from-the-device)
4. Erneutes [Registrieren des Geräts](#reregister-the-repaired-device-using-the-new-device-id) bei Windows Autopilot
5. [Zurücksetzen des Geräts](#reset-the-device)
6. [Gerät zurückgeben](#return-the-repaired-device-to-the-customer)

Jeder dieser Schritte wird im Folgenden beschrieben.

## <a name="deregister-the-autopilot-device-from-the-autopilot-program"></a>Aufheben der Registrierung des Autopilot-Geräts über das Autopilot-Programm

Bevor das Gerät bei der reparaturanlage eintrifft, muss es von der Entität, die es registriert hat, deregistrierte werden. Nur die Entität, die das Gerät registriert hat, kann die Registrierung aufheben.   Dabei kann es sich um den IT-Administrator des Kunden, den OEM oder den CSP-Partner handeln.  Wenn der IT-Administrator das Gerät registriert hat, haben Sie es wahrscheinlich über InTune (oder möglicherweise die Microsoft Store für Unternehmen) durchgeführt.  In diesem Fall sollten Sie das Gerät bei InTune (oder msfb) registrieren.  Dies ist erforderlich, weil Geräte, die in InTune registriert sind, nicht in MPC angezeigt werden.  Wenn der OEM-oder CSP-Partner das Gerät jedoch registriert hat, haben Sie es wahrscheinlich über das Microsoft Partner Center (MPC) durchgeführt.  In diesem Fall sollte die Registrierung des Geräts bei MPC aufgehoben werden, wodurch es auch aus dem InTune-Konto des Kunden IT-Administrators entfernt wird.  Im folgenden werden die Schritte beschrieben, die ein IT-Administrator durchlaufen würde, um die Registrierung eines Geräts bei InTune aufzuheben, und die Schritte, die ein OEM oder CSP durchlaufen würde, um die Registrierung eines Geräts bei MPC aufzuheben.

**Hinweis**: Wenn möglich, sollte ein OEM oder CSP Autopilot-Geräte registrieren, anstatt den Kunden dies zu tun.  Dadurch werden Probleme vermieden, bei denen OEMs oder CSPs möglicherweise nicht in der Lage sind, ein Gerät zu registrieren, wenn beispielsweise ein Kunden Leasing ein Gerät ausfällt, bevor es sich selbst registriert.

**Ausnahme**: Wenn ein Kunde eine OEM-Berechtigung zum Registrieren von Geräten in seinem Auftrag über den automatisierten Zustimmungsprozess erteilt, kann ein OEM die API verwenden, um Geräte zu registrieren, die sich nicht selbst registriert haben (Stattdessen hat der Kunde die Geräte registriert).  Beachten Sie jedoch, dass dies nur diese Geräte aus dem Autopilot-Programm entfernen würde, dass Sie nicht von InTune oder von Aad getrennt werden.  Der Kunde muss diese Schritte, falls gewünscht, über InTune ausführen.

### <a name="deregister-from-intune"></a>Aufheben der Registrierung bei InTune

Zum Aufheben der Registrierung eines Autopilot-Geräts bei InTune würde ein IT-Administrator folgende Aktionen ausführen:

1. Melden Sie sich bei Ihrem InTune-Konto an.
2. Navigieren Sie zu InTune > Gruppen > alle Gruppen.
3. Entfernen des gewünschten Geräts aus seiner Gruppe
4. Navigieren Sie zu InTune > Geräte > alle Geräte.
5. Aktivieren Sie das Kontrollkästchen neben dem Gerät, das Sie löschen möchten, und klicken Sie dann im oberen Menü auf die Schaltfläche Löschen.
6. Navigieren Sie zu InTune > Geräte > Azure AD Geräte.
7. Aktivieren Sie das Kontrollkästchen neben dem Gerät, das Sie löschen möchten, und klicken Sie dann auf die Schaltfläche "Löschen" im oberen Menü.
8. Navigieren Sie zu InTune > Geräteregistrierung > Windows-Registrierung > Geräte
9. Aktivieren Sie das Kontrollkästchen neben dem Gerät, das Sie registrieren möchten.
10. Klicken Sie auf das erweiterte Menü Symbol ("...") ganz rechts in der Zeile mit dem Gerät, für das Sie die Registrierung aufheben möchten, um ein zusätzliches Menü mit der Option "Benutzer Zuweisung aufheben" verfügbar zu machen.
11. Klicken Sie auf "Benutzer Zuweisung aufheben", wenn das Gerät zuvor einem Benutzer zugewiesen wurde. Wenn dies nicht der Fall ist, wird diese Option abgeblendet und kann ignoriert werden.
12. Wenn das nicht zugewiesene Gerät noch ausgewählt ist, klicken Sie auf die Schaltfläche "Löschen" im oberen Menü, um dieses Gerät zu entfernen.

**Hinweis**: mit diesen Schritten wird das Gerät bei Autopilot registriert, aber auch die Registrierung des Geräts bei InTune aufgehoben, und das Gerät wird von Aad getrennt.  Obwohl es möglicherweise so aussieht, als ob nur das Aufheben der Registrierung des Geräts von Autopilot erforderlich ist, gibt es in InTune bestimmte Barrieren, die alle oben beschriebenen Schritte erforderlich machen. Dies ist dennoch eine bewährte Methode, falls das Gerät verloren geht oder nicht wiederherstellbar ist, um die Möglichkeit zu vermeiden, dass verwaiste Geräte in der Autopilot-Datenbank oder InTune oder Aad vorhanden sind  Wenn ein Gerät in einen nicht wiederherstellbaren Zustand versetzt wird, können Sie sich für Unterstützung an den entsprechenden [Microsoft-Support-Alias](autopilot-support.md) wenden.

Der Registrierungsvorgang dauert ungefähr 15 Minuten.  Sie können den Prozess beschleunigen, indem Sie auf die Schaltfläche "synchronisieren" klicken und dann die Anzeige aktualisieren, bis das Gerät nicht mehr vorhanden ist.

Weitere Informationen zum Aufheben der Registrierung von Geräten in InTune finden Sie [hier](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group).

### <a name="deregister-from-mpc"></a>Aufheben der Registrierung von MPC

Zum Aufheben der Registrierung eines Autopilot-Geräts aus dem Microsoft Partner Center (MPC) würde ein CSP folgende Aktionen ausführen:

1. Anmelden bei MPC
2. Navigieren zu Kunden > Geräten
3. Wählen Sie das Gerät aus, das registriert werden soll, und klicken Sie auf die Schaltfläche "Gerät löschen".

![devices](images/devices.png)

**Hinweis**: durch das Aufheben der Registrierung eines Geräts von Autopilot in MPC werden nur die folgenden Aktionen durchführt: Außerdem wird die Registrierung des Geräts bei MDM (InTune) nicht aufgehoben, und das Gerät wird nicht von Aad getrennt.  Daher sollte OEM/CSP, wenn möglich, im Idealfall mit dem IT-Administrator des Kunden zusammenarbeiten, damit das Gerät gemäß den InTune-Schritten im vorherigen Abschnitt vollständig entfernt wird.

Alternativ kann ein OEM-Partner, der die OEM Direct-APIs integriert hat, die Registrierung eines Geräts aufheben, indem er die autopilotdeviceregistration-API aufruft, wobei die Felder "tenantid" und "tenantdomain" im Anforderungs Aufruf leer bleiben.  

Da die Reparatur Einrichtung keinen Zugriff auf die Anmelde Informationen des Benutzers hat, muss die Reparatur Einrichtung das Gerät im Rahmen des Reparatur Vorgangs ein reimaging ausführen.  Dies bedeutet, dass der Kunde drei Dinge vor dem Senden des Geräts zur Reparatur durchführen sollte:
1. Kopieren Sie alle wichtigen Daten vom Gerät.
2. Lassen Sie die Reparatur Einrichtung wissen, welche Version von Windows nach der Reparatur neu installiert werden sollte.
3. Stellen Sie ggf. die Reparatur Einrichtung fest, welche Office-Version nach der Reparatur neu installiert werden soll.

## <a name="replace-the-motherboard"></a>Ersetzen der Hauptplatine

Techniker ersetzen das Motherboard (oder andere Hardware) auf dem unterbrochenen Gerät.  Ein Ersatz-DPK wird eingefügt.

Reparatur-und Schlüsselaustausch Vorgänge unterscheiden sich je nach Ausstattung.  Manchmal erhalten Reparaturanlagen von OEMs, bei denen bereits Ersatz-DP-Elemente eingefügt wurden, auch keine Ersatz Komponenten, aber manchmal nicht.  Manchmal erhalten Reparatur Einrichtungen voll funktionsfähige BIOS-Tools von OEMs, aber manchmal nicht.  Dies bedeutet, dass die Qualität der Daten im BIOS nach einem MBR variiert.  Um sicherzustellen, dass das reparierte Gerät nach der Reparatur weiterhin Autopilot-fähig ist, sollte das neue BIOS (nach Reparatur) die folgenden Informationen mindestens erfassen und auffüllen können:

- Diskserialnumber
- Smbiossystemserialnumber
- Smbiossystemhersteller
- Smbiossystemproductname
- Smbiosuuid
- TPM-ekpub
- MacAddress
- ProductKeyID
- OSType

**Hinweis**: der Einfachheit halber und da die Prozesse zwischen den Reparaturfunktionen variieren, haben wir viele der zusätzlichen Schritte ausgeschlossen, die häufig in einem MBR verwendet werden, wie z. b.:
- Vergewissern Sie sich, dass das Gerät noch funktionsfähig ist.
- BitLocker deaktivieren *
- Reparieren des Startkonfigurationsdaten (BCD)
- Reparieren und Überprüfen des Netzwerktreiber Vorgangs

* BitLocker kann angehalten und nicht deaktiviert werden, wenn der Techniker die Möglichkeit hat, ihn nach der Reparatur wieder aufzunehmen.

## <a name="capture-a-new-autopilot-device-id-4k-hh-from-the-device"></a>Erfassen einer neuen Autopilot-Geräte-ID (4K HH) vom Gerät

Reparatur Techniker müssen sich beim reparierten Gerät anmelden, um die neue Geräte-ID zu erfassen.  Wenn der Reparatur Techniker keinen Zugriff auf die Anmelde Informationen des Kunden hat, muss er ein reimaging für das Gerät durchführen, um Zugriff zu erhalten, und zwar gemäß den folgenden Schritten:

1. Der Reparatur Techniker erstellt ein Start [fähiges WinPE-USB-Laufwerk](https://docs.microsoft.com/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#create-a-bootable-windows-pe-winpe-partition).
2. Der Reparatur Techniker startet das Gerät in WinPE.
3. Der Reparatur Techniker [wendet ein neues Windows-Abbild auf das Gerät an](https://docs.microsoft.com/windows-hardware/manufacture/desktop/work-with-windows-images).

    **Hinweis**: im Idealfall sollte die gleiche Version von Windows auf dem Gerät, das sich ursprünglich auf dem Gerät befand, neu erstellt werden. Daher ist eine Koordination zwischen der Reparatur Einrichtung und dem Kunden erforderlich, um diese Informationen zu dem Zeitpunkt zu erfassen, zu dem das Gerät zur Reparatur eintrifft.  Dazu zählt beispielsweise, dass der Kunde die reparaturanlage über einen USB-Stick an eine angepasste Abbild Datei (PPK-Datei) sendet.
 
4. Der Reparatur Techniker startet das Gerät im neuen Windows-Abbild.
5. Auf dem Desktop erfasst der Reparatur Techniker die neue Geräte-ID (4K HH) vom Gerät mithilfe des OA3-Tools oder des PowerShell-Skripts, wie unten beschrieben.

Diese Reparatur Einrichtungen mit Zugriff auf das OA3-Tool (das Teil des ADK ist) können das Tool verwenden, um den 4K-Hardwarehash (4K HH) zu erfassen.

Alternativ kann das [PowerShell-Skript windowsautopilotinfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) verwendet werden, um die 4K HH zu erfassen, indem die folgenden Schritte ausgeführt werden:

1. Installieren Sie das Skript über die [PowerShell-Katalog](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) oder über die Befehlszeile (die Befehlszeilen Installation ist unten dargestellt).
2. Navigieren Sie zum Skriptverzeichnis, und führen Sie es auf dem Gerät aus, wenn sich das Gerät entweder im vollständigen Betriebssystem-oder im Überwachungsmodus befindet. Siehe folgendes Beispiel.

    ```powershell
    md c:\HWID
    Set-Location c:\HWID
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
    Install-Script -Name Get-WindowsAutopilotInfo -Force
    Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
    ```

>Wenn Sie aufgefordert werden, das nuget-Paket zu installieren, wählen Sie **Ja**aus.<br>
>Wenn Sie nach der Installation des Skripts eine Fehlermeldung erhalten, dass Get-WindowsAutopilotInfo.ps1 nicht gefunden wurde, vergewissern Sie sich, dass c:\programme\windowspowershell\scripts in der PATH-Variablen vorhanden ist.<br>
>Wenn beim Cmdlet "Install-Script" ein Fehler auftritt, vergewissern Sie sich, dass Sie das PowerShell-Standard Repository registriert haben (**Get-psrepository**), oder registrieren Sie das standardrepository mit **Register-psrepository-default-Verbose**.

Das Skript erstellt eine CSV-Datei, die die Geräteinformationen einschließlich des kompletten 4K HH enthält.  Speichern Sie diese Datei, damit Sie später darauf zugreifen können. Die Dienst Einrichtung verwendet dieses 4K HH, um das Gerät erneut zu registrieren, wie unten beschrieben. Stellen Sie sicher, dass Sie beim Speichern der Datei den Parameter "-OutputFile" verwenden. Dadurch wird sichergestellt, dass die Datei Formatierung korrekt ist. Versuchen Sie nicht, die Befehlsausgabe manuell an eine Datei zu übergeben.

**Hinweis**: Wenn die Reparatur Funktion nicht die Möglichkeit hat, das OA3-Tool oder PowerShell-Skript auszuführen, um das neue 4K HH zu erfassen, müssen die CSP-Partner (oder OEM-Partner) dies für Sie tun.  Ohne eine Entität, die das neue 4K HH erfasst, gibt es keine Möglichkeit, dieses Gerät als Autopilot-Gerät erneut zu registrieren.


## <a name="reregister-the-repaired-device-using-the-new-device-id"></a>Erneutes Registrieren des reparierten Geräts mithilfe der neuen Geräte-ID

Wenn ein OEM das Gerät nicht erneut registrieren kann, sollte die reparaturanlage oder der CSP das Gerät mithilfe von MPC erneut registrieren, oder der IT-Administrator des Kunden sollte darauf hingewiesen werden, dass das Gerät über InTune (oder msfb) erneut registriert wird.  Beide Methoden zum Erneutes Registrieren eines Geräts sind unten dargestellt.

### <a name="reregister-from-intune"></a>Erneutes Registrieren bei InTune

Ein IT-Administrator würde Folgendes tun, um ein Autopilot-Gerät bei InTune erneut zu registrieren:
1. Melden Sie sich bei Intune an.
2. Navigieren Sie zu Geräteregistrierung > Windows-Registrierung > Geräte > importieren.
3. Klicken Sie auf die Schaltfläche **importieren** , um eine CSV-Datei mit der Geräte-ID des Geräts, das erneut registriert werden soll, hochzuladen. (die Geräte-ID war das von dem zuvor in diesem Dokument beschriebene PowerShell-Skript oder OA3-Tool erfasste 4K hh.)

Das folgende Video bietet einen guten Überblick darüber, wie Sie Geräte über msfb registrieren (erneut).<br>

> [!VIDEO https://www.youtube.com/embed/IpLIZU_j7Z0]

### <a name="reregister-from-mpc"></a>Erneutes Registrieren von MPC

Zum Registrieren eines Autopilot-Geräts von MPC führt ein OEM oder CSP Folgendes durch:

1. Melden Sie sich bei MPC an.
2. Navigieren Sie zur Seite Kunden > Geräte, und klicken Sie auf die Schaltfläche **Geräte hinzufügen** , um die CSV-Datei hochzuladen.

![Gerät](images/device2.png)<br>
![Gerät](images/device3.png)

Wenn Sie ein repariertes Gerät mithilfe von MPC erneut registrieren, muss die hochgeladene CSV-Datei die 4K hh für das Gerät und nicht nur das pkid oder Tupel (SerialNumber + oemname + modelname) enthalten.  Wenn nur das pkid oder Tupel verwendet wurde, wäre der Autopilot-Dienst nicht in der Autopilot-Datenbank in der Lage, eine Entsprechung in der Autopilot-Datenbank zu finden, da zuvor keine Informationen zu 4 KB für dieses "neue" Gerät übermittelt wurden, und der Upload schlägt fehl, und es wird wahrscheinlich ein ztddevicenotfound-Fehler zurückgegeben.  Laden Sie also wieder nur das 4K HH, nicht das Tupel oder pkid.

**Hinweis**: Wenn Sie das 4K HH in die CSV-Datei einfügen, müssen Sie nicht auch das pkid oder Tupel einschließen.  Diese Spalten können leer gelassen werden, wie unten dargestellt:

![hash](images/hh.png)

## <a name="reset-the-device"></a>Zurücksetzen des Geräts

Da sich das Gerät im vollständigen Betriebssystem-oder Überwachungsmodus befinden muss, um das 4K HH zu erfassen, muss die Reparatur Einrichtung das Abbild zurücksetzen, bevor es an den Kunden zurückgegeben wird.  Eine Möglichkeit hierfür ist die Verwendung der integrierten Reset-Funktion in Windows wie folgt:

Wechseln Sie auf dem Gerät zu Einstellungen > aktualisieren Sie & Sicherheit > Wiederherstellung, und klicken Sie dann auf "starten".  Wählen Sie unter diesen PC zurücksetzen die Option Alles entfernen aus, und entfernen Sie einfach meine Dateien. Klicken Sie abschließend auf Zurücksetzen.

![reset](images/reset.png)

Es ist jedoch wahrscheinlich, dass die Reparatur Einrichtung keinen Zugriff auf Windows hat, da Sie nicht über die Anmelde Informationen des Benutzers für die Anmeldung verfügt. in diesem Fall müssen Sie andere Möglichkeiten zum reimaging des Geräts verwenden, wie z. b. das [Abbild für die Abbild Verwaltung für die Bereitstellung](https://docs.microsoft.com/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#use-a-deployment-script-to-apply-your-image).

## <a name="return-the-repaired-device-to-the-customer"></a>Das reparierte Gerät an den Kunden zurückgeben

Nachdem Sie die vorherigen Schritte abgeschlossen haben, kann das reparierte Gerät nun an den Kunden zurückgegeben werden und wird beim ersten Start während der Erstellung automatisch beim Autopilot-Programm registriert.

**Hinweis**: Wenn die Reparatur Einrichtung das Gerät nicht reimagiert, könnte Sie es in einen potenziell fehlerhaft zurücksenden (z. b. gibt es keine Möglichkeit, sich beim Gerät anzumelden, weil es vom einzigen bekannten Benutzerkonto getrennt wurde). in diesem Fall sollten Sie der Organisation mitteilen, dass die Registrierung und das Betriebssystem selbst behoben werden müssen.

**Wichtig**: ein Gerät kann vor dem Einschalten "für Autopilot" registriert werden, aber das Gerät wird nicht als Autopilot-Gerät bereitgestellt (d. h. als Autopilot-Gerät aktiviert), bis es durch OOBE fließt. aus diesem Grund ist das Zurücksetzen des Geräts auf einen Zustand vor dem OOBE-Vorgang ein erforderlicher Schritt.

## <a name="specific-repair-scenarios"></a>Bestimmte Reparatur Szenarios

In diesem Abschnitt werden die häufigsten Reparatur Szenarien und ihre Auswirkungen auf die Autopilot-Aktivierung behandelt.

Hinweise zu Test Ergebnissen:

- Die folgenden Szenarios wurden nur mit InTune getestet (es wurden keine anderen mdms getestet).
- In den meisten Test Szenarios unten mussten das reparierte und erneut zu verwendende Gerät erneut OOBE durchlaufen, damit Autopilot aktiviert wird.
- Die Ersetzungs Szenarios führen häufig zu Datenverlusten, sodass Reparaturzentren oder Kunden vor der Reparatur daran erinnert werden sollten, um Daten zu sichern.
- In Fällen, in denen eine Reparatur Umgebung nicht in der Lage ist, Geräteinformationen in das BIOS des reparierten Geräts zu schreiben, müssen neue Prozesse erstellt werden, damit Autopilot erfolgreich aktiviert werden kann.
- Für das reparierte Gerät sollte der Product Key (DPK) vor dem Erfassen der neuen 4K HH (Geräte-ID) vorab in das BIOS eingefügt werden.

Inhalt der folgenden Tabelle:<br>
- Unterstützt = **Ja**: das Gerät kann für Autopilot erneut aktiviert werden.
- Unterstützt = **Nein**: das Gerät kann für Autopilot nicht erneut aktiviert werden.

<table border="1">
<th>Szenario<th>Unterstützt<th>Microsoft-Empfehlung
<tr><td>Austauschen von Motherboards (MBR) im allgemeinen<td>Ja<td>Die empfohlene Vorgehensweise für MBR-Szenarien sieht wie folgt aus:

1. Autopilot-Gerät wird aus dem Autopilot-Programm aufgehoben
2. Das Motherboard ist "Replace".
3. Für das Gerät wird ein reimaging durchgeführt (mit BIOS-Informationen und der Wiederherstellung von DPK) *
4. Eine neue Autopilot-Geräte-ID (4K HH) wird vom Gerät erfasst.
5. Das reparierte Gerät wird mithilfe der neuen Geräte-ID für das Autopilot-Programm erneut registriert.
6. Das reparierte Gerät wird auf "Oobe" zurückgesetzt.
7. Das reparierte Gerät wird an den Kunden zurückgesendet.

* Es ist nicht erforderlich, ein reimaging für das Gerät durchführen, wenn der Reparatur Techniker Zugriff auf die Anmelde Informationen des Kunden hat.  Es ist technisch möglich, eine erfolgreiche MBR-und Autopilot-erneute Aktivierung ohne Schlüssel oder bestimmte BIOS-Informationen (z. b. Seriennummer, Modellname usw.) durchzuführen. Dies wird jedoch nur für Test-und Schulungszwecke empfohlen.

<tr><td>MBR, wenn die Hauptplatine über einen TPM-Chip (aktiviert) und nur eine Netzwerkkarte für das Netzwerk verfügt (die ebenfalls ersetzt wird)<td>Ja<td>

1. Aufheben der Registrierung beschädigter Geräte
2. Ersetzen von Motherboard
3. Reimaging des Geräts (um Zugriff zu erhalten), sofern Sie nicht über Zugriff auf die Anmelde Informationen des Kunden verfügen
4. Geräteinformationen in BIOS schreiben
5. Neue 4K-HH erfassen
6. Erneutes Registrieren von REPARIERTEM Gerät
7. Zurücksetzen des Geräts auf "Oobe"
8. Durchlaufen von Autopilot OOBE (Customer)
9. Autopilot erfolgreich aktiviert

<tr><td>MBR, wenn die Hauptplatine über einen TPM-Chip (aktiviert) und eine zweite Netzwerkkarte (oder Netzwerkschnittstelle) verfügt, die nicht zusammen mit der Hauptplatine ersetzt wird<td>Nein<td>Dieses Szenario wird nicht empfohlen, da das Autopilot-Verhalten unterbrochen wird, da die resultierende Geräte-ID erst nach Abschluss des TPM-Nachweis stabil bleibt und die Registrierung aufgrund der Mehrdeutigkeit bei der Auflösung von Mac-Adressen möglicherweise falsche Ergebnisse liefert.
<tr><td>MBR, bei dem die NIC-Karte, HDD und WLAN nach der Reparatur unverändert bleiben<td>Ja<td>

1. Aufheben der Registrierung beschädigter Geräte
2. Ersetzen Sie die Hauptplatine (durch neue rdpk im BIOS voreingefügt).
3. Reimaging des Geräts (um Zugriff zu erhalten), sofern Sie nicht über Zugriff auf die Anmelde Informationen des Kunden verfügen
4. Alte Geräteinformationen in BIOS schreiben (Gleiches s/n, Modell usw.) *
5. Neue 4K-HH erfassen
6. Erneutes Registrieren von REPARIERTEM Gerät
7. Zurücksetzen des Geräts auf "Oobe"
8. Durchlaufen von Autopilot OOBE (Customer)
9. Autopilot erfolgreich aktiviert

* Beachten Sie, dass für dieses und nachfolgende Szenarien das Umschreiben von alten Geräteinformationen nicht den TPM 2,0 Endorsement Key enthält, weil der zugehörige private Schlüssel für das TPM-Gerät gesperrt ist.

<tr><td>MBR, bei dem die NIC-Karte unverändert bleibt, aber HDD und WLAN ersetzt werden<td>Ja<td>

1. Aufheben der Registrierung beschädigter Geräte
2. Ersetzen Sie die Hauptplatine (durch neue rdpk im BIOS voreingefügt).
3. Neue HDD und WLAN einfügen
4. Alte Geräteinformationen in BIOS schreiben (Gleiches s/n, Modell usw.)
5. Neue 4K-HH erfassen
6. Erneutes Registrieren von REPARIERTEM Gerät
7. Zurücksetzen des Geräts auf "Oobe"
8. Durchlaufen von Autopilot OOBE (Customer)
9. Autopilot erfolgreich aktiviert

<tr><td>MBR, bei dem die NIC-Karte und das WLAN unverändert bleiben, die HDD jedoch ersetzt wird<td>Ja<td>

1. Aufheben der Registrierung beschädigter Geräte
2. Ersetzen Sie die Hauptplatine (durch neue rdpk im BIOS voreingefügt).
3. Neue HDD einfügen
4. Alte Geräteinformationen in BIOS schreiben (Gleiches s/n, Modell usw.)
5. Neue 4K-HH erfassen
6. Erneutes Registrieren von REPARIERTEM Gerät
7. Zurücksetzen des Geräts auf "Oobe"
8. Durchlaufen von Autopilot OOBE (Customer)
9. Autopilot erfolgreich aktiviert

<tr><td>MBR, bei dem nur die MB ersetzt werden (alle anderen Teile bleiben unverändert), neue MB wurden jedoch von einem zuvor verwendeten Gerät übernommen, für das zuvor noch kein Autopilot-fähig war.<td>Ja<td>

1. Aufheben der Registrierung beschädigter Geräte
2. Ersetzen Sie die Hauptplatine (durch neue rdpk im BIOS voreingefügt).
3. Reimaging des Geräts (um Zugriff zu erhalten), sofern Sie nicht über Zugriff auf die Anmelde Informationen des Kunden verfügen
4. Alte Geräteinformationen in BIOS schreiben (Gleiches s/n, Modell usw.)
5. Neue 4K-HH erfassen
6. Erneutes Registrieren von REPARIERTEM Gerät
7. Zurücksetzen des Geräts auf "Oobe"
8. Durchlaufen von Autopilot OOBE (Customer)
9. Autopilot erfolgreich aktiviert

<tr><td>MBR, bei dem nur die MB ersetzt werden (alle anderen Teile bleiben unverändert), aber neue MB wurden von einem zuvor verwendeten Gerät entnommen, das zuvor Autopilot-fähig war.<td>Ja<td>

1. Aufheben der Registrierung des alten Geräts, von dem MB entnommen werden
2. Aufheben der Registrierung beschädigter Geräte (die Sie reparieren möchten)
3. Ersetzen Sie die "Motherboard" im Reparatur Gerät durch MB von einem anderen Autopilot-Gerät (mit dem neuen rdpk im BIOS voreingefügt).
4. Reimaging des Geräts (um Zugriff zu erhalten), sofern Sie nicht über Zugriff auf die Anmelde Informationen des Kunden verfügen
5. Alte Geräteinformationen in BIOS schreiben (Gleiches s/n, Modell usw.)
6. Neue 4K-HH erfassen
7. Erneutes Registrieren von REPARIERTEM Gerät
8. Zurücksetzen des Geräts auf "Oobe"
9. Durchlaufen von Autopilot OOBE (Customer)
10. Autopilot erfolgreich aktiviert

<b>Hinweis</b>: das reparierte Gerät kann auch erfolgreich als normales, nicht Autopilot-Gerät verwendet werden.

<tr><td>Vom MBR-Gerät ausgeschlossene BIOS-Informationen<td>Nein<td>Die Reparatur Einrichtung verfügt über kein BIOS-Tool zum Schreiben von Geräteinformationen in das BIOS nach MBR.

1. Aufheben der Registrierung beschädigter Geräte
2. "Motherboard ersetzen" (BIOS enthält keine Geräteinformationen)
3. Reimaging und Schreiben von DPK in Image
4. Neue 4K-HH erfassen
5. Erneutes Registrieren von REPARIERTEM Gerät
6. Autopilot-Profil für Gerät erstellen
7. Durchlaufen von Autopilot OOBE (Customer)
8. Autopilot erkennt repariertes Gerät nicht

<tr><td>MBR, wenn kein TPM-Chip vorhanden ist<td>Ja<td>Obwohl es nicht empfohlen wird, Autopilot-Geräte ohne TPM-Chip zu aktivieren (was für die BitLocker-Verschlüsselung empfohlen wird), ist es möglich, ein Autopilot-Gerät im Modus "Standardbenutzer" (aber nicht in der selbst Bereitstellung) zu aktivieren, der nicht über einen TPM-Chip verfügt.  In diesem Fall würden Sie Folgendes tun:

1. Aufheben der Registrierung beschädigter Geräte
2. Ersetzen von Motherboard
3. Reimaging des Geräts (um Zugriff zu erhalten), sofern Sie nicht über Zugriff auf die Anmelde Informationen des Kunden verfügen
4. Alte Geräteinformationen in BIOS schreiben (Gleiches s/n, Modell usw.)
5. Neue 4K-HH erfassen
6. Erneutes Registrieren von REPARIERTEM Gerät
7. Zurücksetzen des Geräts auf "Oobe"
8. Durchlaufen von Autopilot OOBE (Customer)
9. Autopilot erfolgreich aktiviert

<tr><td>Neues DPK, das auf einem reparierten Autopilot-Gerät mit einem neuen MB in Image geschrieben wurde<td>Ja<td>Die reparaturanlage ersetzt normale MB auf einem beschädigten Gerät.  MB enthält kein DPK im BIOS.  Die reparaturanlage schreibt DPK nach MBR in das Image.  

1. Aufheben der Registrierung beschädigter Geräte
2. Replace Motherboard – BIOS enthält keine DPK-Informationen
3. Reimaging des Geräts (um Zugriff zu erhalten), sofern Sie nicht über Zugriff auf die Anmelde Informationen des Kunden verfügen
4. Geräteinformationen in BIOS schreiben (Gleiches s/n, Modell usw.)
5. Neue 4K-HH erfassen
6. Gerät auf "Pre-OOBE" zurücksetzen oder ein reimaging ausführen und DPK in Image schreiben
7. Erneutes Registrieren von REPARIERTEM Gerät
8. Durchlaufen von Autopilot Oobe
9. Autopilot erfolgreich aktiviert

<tr><td>Neuer Product Key reparieren (rdpk)<td>Ja<td>Die Verwendung einer Hauptplatine mit einer neuen vorab eingefügten rdpk führt zu einem erfolgreichen Autopilot-Sanierungs Szenario. 

1. Aufheben der Registrierung beschädigter Geräte
2. Ersetzen Sie die Hauptplatine (durch neue rdpk im BIOS voreingefügt).
3. Reimaging oder Rest-Bild in "Pre-OOBE"
4. Geräteinformationen in BIOS schreiben 
5. Neue 4K-HH erfassen
6. Erneutes Registrieren von REPARIERTEM Gerät
7. Image nach Pre-OOBE reimaging oder Zurücksetzen
8. Durchlaufen von Autopilot Oobe
9. Autopilot erfolgreich aktiviert

<tr><td>Kein Repair Product Key (rdpk) eingefügt<td>Nein<td>Dieses Szenario verstößt gegen die Microsoft-Richtlinie und unterbricht den Windows Autopilot-Vorgang.
<tr><td>Reimaging für beschädigtes Autopilot-Gerät durchführen, das nicht vor der Reparatur registriert wurde<td>Ja, aber das Gerät wird weiterhin mit der vorherigen Mandanten-ID verknüpft und sollte daher nur an denselben Kunden zurückgegeben werden.<td>

1. Reimaging für beschädigte Geräte ausführen
2. Schreiben von DPK in Image
3. Durchlaufen von Autopilot Oobe
4. Autopilot erfolgreich aktiviert (vorherige Mandanten-ID)

<tr><td>Datenträger Ersetzung von einem nicht-Autopilot-Gerät zu einem Autopilot-Gerät<td>Ja<td>

1. Beschädigte Geräte vor der Reparatur nicht registrieren
2. HDD auf beschädigtem Gerät ersetzen
3. Image nach OOBE reimaging oder Zurücksetzen
4. Durchlaufen von Autopilot OOBE (Customer)
5. Autopilot erfolgreich aktiviert (repariertes Gerät wurde als vorheriger Self erkannt)

<tr><td>Datenträger Ersetzung von einem Autopilot-Gerät zu einem anderen Autopilot-Gerät<td>Vielleicht<td>Wenn das Gerät, von dem die HDD übernommen wird, selbst zuvor von Autopilot aus registriert wurde, kann diese HDD in einem Reparatur Gerät verwendet werden.  Wenn die HDD jedoch nie vor der Verwendung in einem reparierten Gerät zuvor von Autopilot registriert wurde, hat das neu reparierte Gerät nicht die richtige Autopilot-Darstellung.

Angenommen, die verwendete HDD wurde zuvor in der Registrierung registriert (bevor Sie in dieser Reparatur verwendet wird):

1. Aufheben der Registrierung beschädigter Geräte
2. HDD auf beschädigtem Gerät durch eine HDD von einem anderen, nicht getosterten Autopilot-Gerät ersetzen
3. Reimaging für das reparierte Gerät wieder in einen Zustand vor dem oobe ausführen
4. Durchlaufen von Autopilot OOBE (Customer)
5. Autopilot erfolgreich aktiviert

<tr><td>Austausch von nicht-Microsoft-Netzwerkkarten <td>Nein<td>Unabhängig davon, ob von einem Autopilot-Gerät zu einem Autopilot-Gerät, von einem Autopilot-Gerät zu einem anderen Autopilot-Gerät oder von einem Autopilot-Gerät zu einem nicht Autopilot-Gerät ein Szenario, in dem eine Drittanbieter-Netzwerkkarte (nicht integriert) ersetzt wird, das Autopilot-Verhalten unterbricht und nicht empfohlen wird.
<tr><td>Ein Gerät wurde mehr als drei mal repariert.<td>Nein<td>Autopilot wird nicht unterstützt, wenn ein Gerät wiederholt repariert wird, sodass alle Teile, die nicht ersetzt wurden, mit zu vielen Teilen verknüpft werden, die ersetzt wurden. Dadurch wird es schwierig, dieses Gerät in Zukunft eindeutig zu identifizieren.
<tr><td>Arbeitsspeicher Ersetzung<td>Ja<td>Das Ersetzen des Speichers auf einem beschädigten Gerät wirkt sich nicht negativ auf die Autopilot-Darstellung auf diesem Gerät aus.  Es ist keine erneute Registrierung erforderlich.  Der Reparatur Techniker muss lediglich den Arbeitsspeicher ersetzen.
<tr><td>GPU-Ersetzung<td>Ja<td>Das Ersetzen der GPU (s) auf einem beschädigten Gerät wirkt sich nicht negativ auf die Autopilot-Darstellung auf diesem Gerät aus.  Es ist keine erneute Registrierung erforderlich.  Der Reparatur Techniker muss lediglich die GPU ersetzen.
</table>

>Wenn Sie Teile von einem anderen Autopilot-Gerät bereinigen, empfiehlt es sich, die Registrierung des von Autopilot abzurufenden Geräts zu aufheben, es zu bereinigen und dann nie das umschaltende Gerät (wieder) für Autopilot zu registrieren, da die Wiederverwendung von Teilen auf diese Weise dazu führen kann, dass zwei aktive Geräte dieselbe ID haben, ohne dass Sie unterscheiden können

**Hinweis**: die folgenden Teile können ersetzt werden, ohne dass die Autopilot-Aktivierung beeinträchtigt wird oder besondere zusätzliche Reparatur Schritte erforderlich sind:
- Arbeitsspeicher (RAM oder Rom)
- Stromversorgung
- Videokarte
- Kartenleser
- Sound Karte
- Erweiterungskarte
- Mikrofon
- Webcam
- Lüfter
- Heat Sink
- CMOS-Akku

Andere Reparatur Szenarien, die noch nicht getestet und überprüft wurden, umfassen Folgendes:
- Ersetzung von Daughterboard
- CPU-Ersetzung
- WiFi-Ersetzung
- Ethernet-Ersetzung

## <a name="faq"></a>Häufig gestellte Fragen

| Frage | Antwort |
| --- | --- |
| Wenn wir über ein Tool verfügen, das Produktinformationen nach dem MBR in das BIOS programmiert, müssen wir noch einen CBR-Bericht einreichen, damit das Gerät Autopilot-fähig ist? | Nein.  Nicht, wenn das interne Tool die erforderlichen minimal Informationen in das BIOS schreibt, nach dem das Autopilot-Programm sucht, um das Gerät zu identifizieren, wie weiter oben in diesem Dokument beschrieben. |
| Was geschieht, wenn nur einige Komponenten anstelle der vollständigen Hauptplatine ersetzt werden? | Obwohl es sich bei einigen begrenzten Reparaturen nicht um eine erfolgreiche Übereinstimmung des Autopilot-Algorithmus mit dem Gerät vor der Reparatur handelt, ist es am besten, den Erfolg von 100% sicherzustellen, indem Sie die oben beschriebenen MBR-Schritte durchlaufen, auch für Geräte, die nur eingeschränkte Reparaturen benötigten. |
| Wie erhält ein Reparatur Techniker Zugang zu einem unterbrochenen Gerät, wenn Sie nicht über die Anmelde Informationen des Kunden verfügen? | Der Techniker muss ein reimaging für das Gerät durchführen und während des Reparatur Vorgangs seine eigenen Anmelde Informationen verwenden. |

## <a name="related-topics"></a>Zugehörige Themen

[Geräte Richtlinien](autopilot-device-guidelines.md)<br>
