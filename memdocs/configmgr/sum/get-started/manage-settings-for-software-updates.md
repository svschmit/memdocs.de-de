---
title: Verwalten von Einstellungen für Softwareupdates
titleSuffix: Configuration Manager
description: Enthält Informationen zu Clienteinstellungen, die für Softwareupdates an Ihrem Standort geeignet sind, nachdem Sie den Softwareupdatepunkt installiert haben.
ms.date: 03/30/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0a2a45ff866ea02aacc83c42109c8cba4020ed4e
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906800"
---
#  <a name="manage-settings-for-software-updates"></a><a name="BKMK_ManageSUSettings"></a> Verwalten von Einstellungen für Softwareupdates  

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie Softwareupdates in Configuration Manager synchronisiert haben, konfigurieren und überprüfen Sie die Einstellungen in den folgenden Bereichen.

##  <a name="client-settings-for-software-updates"></a><a name="BKMK_ClientSettings"></a> Clienteinstellungen für Softwareupdates  
Nach der Installation des Softwareupdatepunkts sind Softwareupdates auf Clients standardmäßig aktiviert, und für die Clienteinstellungen auf der Seite **Softwareupdates** werden Standardwerte angezeigt. Die Softwareupdateclients werden standordweit verwendet und beeinflussen, zu welchem Zeitpunkt Softwareupdates auf ihre Kompatibilität überprüft werden, sowie auf welche Weise und zu welchem Zeitpunkt Softwareupdates auf Clientcomputern installiert werden. Überprüfen Sie, ob die Clienteinstellungen für Softwareupdates an Ihrem Standort geeignet sind, bevor Sie Softwareupdates bereitstellen.  

> [!IMPORTANT]  
>  Die Einstellung **Softwareupdates auf Clients aktivieren** ist standardmäßig aktiviert. Wenn Sie diese Einstellung deaktivieren, werden die vorhandenen Bereitstellungsrichtlinien vom Client entfernt.  

Informationen zum Konfigurieren von Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md).  

Weitere Informationen zu Clienteinstellungen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../core/clients/deploy/about-client-settings.md).  

##  <a name="group-policy-settings-for-software-updates"></a><a name="BKMK_GroupPolicy"></a> Gruppenrichtlinieneinstellungen für Softwareupdates  
Von Windows Update Agent (WUA) werden auf Clientcomputern bestimmte Gruppenrichtlinieneinstellungen verwendet, um eine Verbindung mit WSUS auf dem Softwareupdatepunkt herzustellen. Diese Gruppenrichtlinieneinstellungen dienen auch dazu, die Kompatibilität von Softwareupdates zu prüfen und die Softwareupdates und WUA automatisch zu aktualisieren.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Lokale Richtlinie „Internen Pfad für den Microsoft Updatedienst angeben“  
Beim Erstellen des Softwareupdatepunkts für einen Standort erhalten Clients eine Computerrichtlinie, die den Namen für den Server des Softwareupdatepunkts enthält. Von der Computerrichtlinie wird außerdem die lokale Richtlinie **Internen Pfad für den Microsoft Updatedienst angeben** auf dem Computer konfiguriert. Der in der Einstellung **Interner Updatedienst zum Ermitteln von Updates** angegebene Servername wird von WUA abgerufen, und beim Überprüfen der Softwareupdatekompatibilität wird eine Verbindung mit diesem Server hergestellt. Wenn für die Einstellung **Internen Pfad für den Microsoft Updatedienst angeben** eine Domänenrichtlinie erstellt wird, wird hierdurch die lokale Richtlinie außer Kraft gesetzt, und über WUA wird möglicherweise eine Verbindung mit einem anderen Server als dem Softwareupdatepunkt hergestellt. In diesem Fall wird vom Client möglicherweise die Kompatibilität von Softwareupdates anhand unterschiedlicher Produkte, Klassifizierungen und Sprachen überprüft. Aus diesem Grund sollten Sie die Active Directory-Richtlinie nicht für Clientcomputer konfigurieren.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Gruppenrichtlinie „Signierten Inhalt von Intranet-Speicherort für Microsoft-Updatedienst zulassen“  
Sie müssen die Gruppenrichtlinieneinstellung **Signierten Inhalt von Intranet-Speicherort für Microsoft-Updatedienst zulassen** aktivieren, damit Computer von WUA auf Softwareupdates überprüft werden können, die mit System Center Updates Publisher erstellt und veröffentlicht wurden. Wenn die Richtlinieneinstellung aktiviert ist, werden von WUA Softwareupdates zugelassen, die von einem Intranet-Speicherort stammen, sofern diese Softwareupdates im Zertifikatspeicher für **vertrauenswürdige Herausgeber** des lokalen Computers signiert wurden. Weitere Informationen zu den für Updates Publisher erforderlichen Gruppenrichtlinieneinstellungen finden Sie unter [Dokumentationsbibliothek für Updates Publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

### <a name="automatic-updates-configuration"></a>Konfiguration „Automatische Updates“  
Mit der Funktion „Automatische Updates“ können Sicherheitsupdates und andere wichtige Downloads auf Clientcomputern empfangen werden. Automatische Updates werden über die Gruppenrichtlinieneinstellung **Automatische Updates konfigurieren** oder die Systemsteuerung des lokalen Computers konfiguriert. Wenn Automatische Updates aktiviert ist, empfangen Clientcomputer Updatebenachrichtigungen, und je nach konfigurierten Einstellungen werden von den Clientcomputern erforderliche Updates heruntergeladen und installiert. Wenn gleichzeitig Automatische Updates und Softwareupdates aktiviert sind, werden von Clientcomputern u. U. Benachrichtigungssymbole und Anzeigebenachrichtigungen für dasselbe Update angezeigt. Zudem kann von jedem Clientcomputer ein Neustartdialogfeld für dasselbe Update angezeigt werden, wenn ein Neustart erforderlich ist.  

### <a name="self-update"></a>Selbstupdate  
Wenn Automatische Updates auf Clientcomputern aktiviert ist, führt der WUA automatisch ein Selbstupdate aus, falls eine neuere Version verfügbar ist oder Probleme mit einer WUA-Komponente auftreten. Wenn Automatische Updates deaktiviert oder nicht konfiguriert ist und Clientcomputer eine frühere WUA-Version aufweisen, müssen die Clientcomputer die WUA-Installationsdatei ausführen.  

## <a name="software-updates-properties"></a>Softwareupdateeigenschaften
Die Softwareupdateeigenschaften enthalten Informationen über Softwareupdates und zugehörige Inhalte. Mit diesen Eigenschaften können Sie auch Einstellungen für Softwareupdates konfigurieren. Wenn Sie die Eigenschaften für mehrere Softwareupdates öffnen, werden nur die Registerkarten **Maximale Laufzeit** und **Benutzerdefinierter Schweregrad** angezeigt.   

Gehen Sie wie folgt vor, um Softwareupdateeigenschaften zu öffnen.  

#### <a name="to-open-software-update-properties"></a>So öffnen Sie die Softwareupdateeigenschaften  

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  
2. Erweitern Sie im Arbeitsbereich „Softwarebibliothek“ den Eintrag **Softwareupdates**, und klicken Sie auf **Alle Softwareupdates**.  
3. Wählen Sie mindestens ein Softwareupdate aus. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften** .  

   > [!NOTE]  
   >  Im Knoten **Alle Softwareupdates** werden von Configuration Manager nur die Softwareupdates angezeigt, die die Klassifizierungen **Kritisch** und **Sicherheit** aufweisen, und in den letzten 30 Tagen veröffentlicht wurden.  

###  <a name="review-software-updates-information"></a><a name="BKMK_SoftwareUpdatesInformation"></a> Prüfen von Informationen zu Softwareupdates  
In den Softwareupdateeigenschaften können Sie ausführliche Informationen über ein Softwareupdate prüfen. Diese ausführlichen Informationen werden nicht angezeigt, wenn Sie mehrere Softwareupdates auswählen. In den folgenden Abschnitten werden die für ein ausgewähltes Softwareupdate verfügbaren Informationen beschrieben.  

####  <a name="software-update-details"></a><a name="BKMK_SoftwareUpdateDetails"></a> Details zu Softwareupdates  
Auf der Registerkarte **Updatedetails** können Sie die folgenden Informationen zum ausgewählten Softwareupdate anzeigen:  

- **Bulletin-ID:** Gibt die ID des Bulletins an, auf das sich das betreffende Sicherheitssoftwareupdate bezieht. Details zu einem Sicherheitsbulletin finden Sie, wenn Sie auf der Webseite [Microsoft Security Response Center](https://portal.msrc.microsoft.com/) im Suchbereich die Bulletin-ID eingeben.  

> [!NOTE]
> Die Art, wie Microsoft Sicherheitsupdates dokumentiert, ändert sich. Im bisherigen Modell wurden Sicherheitsbulletin-Webseiten mit ID-Nummern von Sicherheitsbulletins (z. B. MS16-XXX) als Angelpunkt verwendet. Diese Form der Dokumentation von Sicherheitsupdates, einschließlich der Sicherheitsbulletin-ID-Nummern, wird zurückgezogen und durch den Leitfaden für Sicherheitsupdates ersetzt. Anstelle von Bulletin-IDs stützt sich der neue Leitfaden auf ID-Nummern von Sicherheitsrisiken und ID-Nummern von KB-Artikeln. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zum Leitfaden für Sicherheitsupdates](https://www.microsoft.com/msrc/faqs-security-update-guide).


- **Artikel-ID:** Hier wird die Artikel-ID für das Softwareupdate angegeben. Der referenzierte Artikel enthält ausführlichere Informationen zum Softwareupdate und zu dem Problem, das mit dem Softwareupdate behoben oder gemindert wird.  

- **Überarbeitungsdatum:** Gibt das Datum an, an dem das Softwareupdate zuletzt geändert wurde.  

- **Maximaler Schweregrad:** Gibt den vom Hersteller festgelegten Schweregrad für das Softwareupdate an.  

- **Beschreibung:** Bietet einen Überblick über den Zustand, das vom Softwareupdate korrigiert oder verbessert wird.  

- **Betroffene Sprachen:** Listet die Sprachen auf, für die das Softwareupdate gilt.  

- **Betroffene Produkte:** Listet die Produkte auf, für die das Softwareupdate gilt.  

####  <a name="content-information"></a><a name="BKMK_ContentInformation"></a> Inhaltsinformationen  
Prüfen Sie auf der Registerkarte **Inhaltsinformationen** die folgenden Informationen zu dem Inhalt, der dem ausgewählten Softwareupdate zugeordnet ist:  

-   **Inhalts-ID:** Gibt die Inhalts-ID für das Softwareupdate an.  

-   **Heruntergeladen:** Gibt an, ob die Softwareupdatedateien von Configuration Manager heruntergeladen wurden.  

-   **Sprache:** Gibt die Sprachen des Softwareupdates an.  

-   **Quellpfad:** Gibt den Pfad zu den Quelldateien des Softwareupdates an.  

-   **Größe (MB):** Gibt die Größe der Quelldateien des Softwareupdates an.  

####  <a name="custom-bundle-information"></a><a name="BKMK_CustomBundleInformation"></a> Informationen zum benutzerdefinierten Softwarepaket  
Prüfen Sie auf der Registerkarte **Informationen zum benutzerdefinierten Paket** die Angaben zum Softwareupdate. Wenn das ausgewählte Softwareupdate gebündelte Softwareupdates umfasst, die sich in der Softwareupdatedatei befinden, werden sie im Abschnitt **Paketinformationen** angezeigt. Auf dieser Registerkarte werden keine der gebündelten Softwareupdates angezeigt, die auf der Registerkarte **Inhaltsinformationen** angezeigt werden, wie Updatedateien für verschiedene Sprachen.  

####  <a name="supersedence-information"></a><a name="BKMK_SupersedenceInformation"></a> Ablösungsinformationen  
Auf der Registerkarte **Ablösungsinformationen** können Sie die folgenden Informationen zur Ablösung des Softwareupdates anzeigen:  

- **Dieses Update wurde durch die folgenden Updates ersetzt:** Gibt die Softwareupdates an, die dieses Update ablösen. Dies bedeutet, dass die aufgeführten Updates neuer sind. In der Regel stellen Sie eines der Softwareupdates bereit, durch die das Softwareupdate abgelöst wird. Die in der Liste aufgeführten Softwareupdates enthalten Hyperlinks zu Webseiten, auf denen weitere Informationen zu den Softwareupdates zu finden sind. Wenn dieses Update nicht abgelöst wurde, wird **Keine** angezeigt.  

- **Dieses Update ersetzt die folgenden Updates:** Gibt die Updates an, die durch dieses Softwareupdate abgelöst werden. Dies bedeutet, dass dieses Softwareupdate neuer ist. In der Regel stellen Sie dieses Softwareupdate als Ersatz für die abgelösten Softwareupdates bereit. Die in der Liste aufgeführten Softwareupdates enthalten Hyperlinks zu Webseiten, auf denen weitere Informationen zu den Softwareupdates zu finden sind. Wenn durch dieses Update kein anderes Update abgelöst wird, wird **Keine** angezeigt.  

###  <a name="configure-software-updates-settings"></a><a name="BKMK_SoftwareUpdatesSettings"></a> Konfigurieren von Softwareupdateeinstellungen  
In den Eigenschaften können Sie Softwareupdateeinstellungen für mehrere Softwareupdates konfigurieren. Die meisten Softwareupdateeinstellungen können Sie nur am Standort der zentralen Verwaltung oder an einem eigenständigen primären Standort konfigurieren. In den folgenden Abschnitten wird erläutert, wie Sie Einstellungen für Softwareupdates konfigurieren.  

####  <a name="set-maximum-run-time"></a><a name="BKMK_SetMaxRunTime"></a> Festlegen der maximalen Laufzeit  
Legen Sie auf der Registerkarte **Maximale Laufzeit** den Zeitraum fest, innerhalb dessen ein Softwareupdate auf Clientcomputern abgeschlossen sein muss. Wenn das Update länger als maximal vorgesehen dauert, wird von Configuration Manager eine Statusmeldung erstellt, und die Bereitstellung wird nicht mehr auf die Softwareupdateinstallation überwacht. Sie können diese Einstellung nur am Standort der zentralen Verwaltung oder an einem eigenständigen primären Standort konfigurieren.  

Von Configuration Manager wird auch festgestellt, ob die Softwareupdateinstallation in einem konfigurierten Wartungsfenster gestartet werden muss. Ist der Wert der maximalen Laufzeit größer als die verfügbare verbleibende Zeit im Wartungsfenster, wird die Softwareupdateinstallation bis zum Beginn des nächsten Wartungsfensters aufgeschoben. Müssen mehrere Softwareupdates auf einem Clientcomputer mit einem konfigurierten Wartungsfenster (Zeitraum) installiert werden, wird das Softwareupdate mit der geringsten maximalen Laufzeit zuerst installiert. Dann folgt das Softwareupdate mit der zweitniedrigsten maximalen Laufzeit usw. Vor der Installation der einzelnen Softwareupdates wird vom Client überprüft, ob das verfügbare Wartungsfenster für die Softwareupdateinstallation lang genug ist. Nach Beginn einer Softwareupdateinstallation wird die Installation fortgesetzt, selbst wenn das Ende des Wartungsfensters überschritten wird. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

Auf der Registerkarte **Maximale Laufzeit** können Sie die folgenden Einstellungen anzeigen und konfigurieren:  

- **Maximale Laufzeit:** Hiermit wird die maximale Anzahl von Minuten festgelegt, die für eine Softwareupdateinstallation zur Verfügung stehen, bevor die Installation nicht mehr von Configuration Manager überwacht wird. Mit dieser Einstellung wird auch bestimmt, ob für die Updateinstallation genug Zeit zur Verfügung steht, bevor das Wartungsfenster endet. Die Standardeinstellung lautet 60 Minuten für Service Packs. Für andere Softwareupdatetypen lautet der Standardwert 10 Minuten, wenn Sie eine Neuinstallation der Configuration Manager-Version 1511 oder höher durchführen, und 5 Minuten, wenn Sie von einer früheren Version aktualisiert haben. Die zulässigen Werte reichen von 5 bis 9999 Minuten.  

> [!IMPORTANT]  
>  Stellen Sie sicher, dass der Wert für die maximale Laufzeit kleiner als das konfigurierte Wartungsfenster ist, oder erhöhen Sie die Dauer des Wartungsfensters auf einen Wert, der größer als die maximale Laufzeit ist. Andernfalls wird die Softwareupdateinstallation niemals initiiert.  

####  <a name="set-custom-severity"></a><a name="BKMK_SetCustomSeverity"></a> Festlegen des benutzerdefinierten Schweregrads  
In den Eigenschaften eines Softwareupdates können Sie über die Registerkarte **Benutzerdefinierter Schweregrad** benutzerdefinierte Schweregrade für die Softwareupdates konfigurieren. Dies kann sich als notwendig erweisen, wenn die vordefinierten Schweregrade Ihren Anforderungen nicht gerecht werden. Die benutzerdefinierten Werte werden in der Spalte **Benutzerdefinierter Schweregrad** in der Configuration Manager-Konsole aufgeführt. Sie können die Softwareupdates nach den angegebenen benutzerdefinierten Schweregraden sortieren und außerdem Abfragen und Berichte erstellen, in denen diese Werte als Filter verwendet werden. Sie können diese Einstellung nur am Standort der zentralen Verwaltung oder an einem eigenständigen primären Standort konfigurieren.  

Auf der Registerkarte **Benutzerdefinierter Schweregrad** können Sie die folgenden Einstellungen konfigurieren.  

- **Benutzerdefinierter Schweregrad:** Legt einen benutzerdefinierten Schweregrad für die Softwareupdates fest. Wählen Sie in der Liste **Kritisch**, **Wichtig**, **Mittel**oder **Niedrig** aus. Standardmäßig ist kein Wert angegeben.

## <a name="crl-checking-for-software-updates"></a>Aktivieren der CRL-Prüfung für Softwareupdates
Standardmäßig wird die Zertifikatsperrliste (Certificate Revocation List, CRL) bei der Verifizierung der Signaturen von Softwareupdates in Configuration Manager nicht überprüft. Das Prüfen der CRL bei jeder Verwendung eines Zertifikats bietet einen höheren Schutz vor gesperrten Zertifikaten, führt jedoch zu einer Verbindungsverzögerung und zusätzlichem Verarbeitungsaufwand auf dem Computer, der die CRL-Prüfung ausführt.  

Wenn die Überprüfung der Zertifikatsperrlisten verwendet wird, muss sie in den Configuration Manager-Konsolen aktiviert sein, die Softwareupdates verarbeiten.  

#### <a name="to-enable-crl-checking"></a>So aktivieren Sie die CRL-Prüfung  
Führen Sie auf dem Computer, der die CRL-Prüfung ausführt, von der Produkt-DVD den folgenden Befehl von einer Eingabeaufforderung aus: **\SMSSETUP\BIN\X64\\** <*Sprache*> **\UpdDwnldCfg.exe/checkrevocation aus**.  

Führen Sie für Englisch (USA) den folgenden Befehl aus: **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**  
