---
title: Antivirenausschlüsse
titleSuffix: Configuration Manager
description: Informieren Sie sich über empfohlene Antivirenausschlüsse beim Beheben möglicher Probleme.
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f3f38de1d7440ffd0293bde359deeb6be3bbeffb
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906209"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Empfohlene Antivirenausschlüsse für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel enthält Empfehlungen, die einem Administrator dabei helfen können, die Ursache einer möglichen Instabilität auf einem Computer zu ermitteln, auf dem eine unterstützte Version von Configuration Manager-Standortservern, -Standortsystemen und -Clients ausgeführt und eine Antivirensoftware verwendet wird.

> [!IMPORTANT]
>
> - Es wird empfohlen, diese Verfahren vorübergehend anzuwenden, um ein System zu evaluieren. Wenn die Systemleistung oder -stabilität durch die Empfehlungen dieses Artikels verbessert wird, wenden Sie sich an den Anbieter Ihrer Antivirensoftware, um Informationen zu einer aktualisierten Version dieser Software zu erhalten.
> - Dieser Artikel bietet Informationen dazu, wie Sie die Sicherheitseinstellungen senken oder Sicherheitsfeatures auf dem Computer vorübergehend deaktivieren. Nehmen Sie diese Änderungen vor, um die Beschaffenheit eines bestimmten Problems zu verstehen. Es empfiehlt sich, vor dem Durchführen dieser Änderungen die Risiken zu bewerten, die mit der Implementierung der Problemumgehung in Ihrer speziellen Umgebung einhergehen.

## <a name="possible-symptoms"></a>Mögliche Symptome 

Der Echtzeitschutz vor Viren kann viele Probleme auf Configuration Manager-Standortservern, -Standortsystemen und -Clients verursachen.

Im Folgenden finden Sie eine nicht erschöpfende Liste möglicher Symptome:

- Am Remotestandort sind einige Systemkomponenten nicht installiert. „SiteComp.log“, „Distmgr.log“, „hman.log“ oder andere Configuration Manager-Protokolldateien enthalten Fehler wie z. B. Fehler 80070005.
- Der Configuration Manager-Client kann nicht per Clientpush installiert werden.
- Die Clientbestandsinformationen sind nicht korrekt, fehlen oder sind veraltet.
- In den Ordnern „*Installationsverzeichnis*\Program Files\Microsoft Configuration Manager\Inboxes“ sind Rückstände vorhanden.
- Das Softwarecenter wird nicht mit auf Clientsystemen bereitgestellter Software aufgefüllt oder startet nicht. Auch die Datei „CCMRepair.log“ kann Fehler enthalten, wie im folgenden Beispiel gezeigt:

  > Fehler bei der Datenbanküberprüfung: 0x80004005, aber Datenbank: „C:\Windows\CCM\filename.sdf“ konnte geöffnet werden. Datenbankreparatur wird übersprungen.

- Für Clients bereitgestellte Software kann nicht installiert werden.
- Konformitätsdaten für Softwarebereitstellungen sind falsch.

## <a name="exclusions"></a>Ausschlüsse

Um solche Probleme zu vermeiden, wird empfohlen, die folgenden Ausschlüsse des Echtzeitschutzes hinzuzufügen:

### <a name="default-installation-folders"></a>Standardinstallationsordner

|  |  |
| - | - |
|*Configuration Manager-Installationsordner*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*MP-Installationsordner*  |%ProgramFiles%\SMS_CCM  |  
|*Clientinstallationsordner*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>Ordnerausschlüsse für Standortserver

- *Configuration Manager-Installationsordner*\Inboxes
- *Configuration Manager-Installationsordner*\Logs
- *Configuration Manager-Installationsordner*\EasySetupPayload

### <a name="folder-exclusions-for-site-systems"></a>Ordnerausschlüsse für Standortsysteme

- Verwaltungspunkte
  - *MP-Installationsordner*\ServiceData
  - Einer der folgenden Ordner:
    - *Configuration Manager-Installationsordner*\MP\OUTBOXES
    - *Installationsverzeichnis*\SMS\MP\OUTBOXES
- Verteilungspunkte
  - *Clientinstallationsordner*\ServiceData
  - *ContentLib-Laufwerk*\SMS_DP$
  - *ContentLib-Laufwerk*\SMSPKG*Laufwerkbuchstabe*$
  - *ContentLib-Laufwerk*\SMSPKG
  - *ContentLib-Laufwerk*\SMSPKGSIG
  - *ContentLib-Laufwerk*\SMSSIG$
- Standortdatenbankserver
  - [Auswählen der Antivirensoftware für Computer, auf denen SQL Server ausgeführt wird](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>Ordnerausschlüsse für Clients

- *Clientinstallationsordner*\\\*.sdf
- *Clientinstallationsordner*\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *Clientinstallationsordner*\Logs

### <a name="file-exclusions-for-mps"></a>Dateiausschlüsse für MPs

- POL00000.pol in
  - *MP-Installationsordner*\PolReqStaging

### <a name="process-exclusions"></a>Prozessausschlüsse

Prozessausschlüsse sind nur dann notwendig, wenn aggressive Antivirenprogramme Configuration Manager-Programmdateien (EXE-Dateien) als Prozesse mit hohem Risiko einstufen.

- *Configuration Manager-Installationsordner*\bin\64\Smsexec.exe
- Einer der folgenden Prozesse:
  - *Clientinstallationsordner*\Ccmexec.exe
  - *MP-Installationsordner*\Ccmexec.exe
- *Clientinstallationsordner*\CmRcService.exe (clientseitig)
- *Configuration Manager-Installationsordner*\bin\64\Sitecomp.exe
- *Configuration Manager-Installationsordner*\bin\64\Smswriter.exe
- *Configuration Manager-Installationsordner*\bin\64\Smssqlbkup.exe oder SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- *Configuration Manager-Installationsordner*\bin\64\Cmupdate.exe
- *Clientinstallationsordner*\Ccmrepair.exe (clientseitig)
- %*windir*%\CCMSetup\Ccmsetup.exe (clientseitig)

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Antivirenausschlüssen finden in den folgenden Artikeln:

[Configuration Manager Current Branch Antivirus Exclusions -System Center Premier Field Engineer Blog](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-current-branch-antivirus-exclusions/ba-p/884831) (Antivirenausschlüsse für Configuration Manager Current Branch – Blog eines Premier Field Engineer)

[Updated System Center 2012 Configuration Manager Antivirus Exclusions with more details on OSD and Boot Images](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/updated-system-center-2012-configuration-manager-antivirus/ba-p/884371) (Aktualisierte Antivirenausschlüsse für System Center 2012 Configuration Manager mit weiteren Details zu Betriebssystembereitstellung und Startimages)

[Auswählen der Antivirensoftware für Computer, auf denen SQL Server ausgeführt wird](https://support.microsoft.com/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Empfehlungen zum Virenscan auf Unternehmenscomputern, auf denen unterstützte Windows-Versionen ausgeführt werden](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
