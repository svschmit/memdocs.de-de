---
title: Endpoint Protection – von Kunden häufig gestellte Fragen
titleSuffix: Configuration Manager
description: Erhalten Sie Antworten auf häufig gestellte Fragen zu Windows Defender und Endpoint Protection.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3b206c1556c2e9550ade5c2322acd65ad2b19412
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906826"
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Endpoint Protection – von Kunden häufig gestellte Fragen

*Gilt für: Configuration Manager (Current Branch)*


Diese häufig gestellten Fragen sind für Computerbenutzer vorgesehen, deren IT-Administrator Windows Defender oder Endpoint Protection auf ihrem verwalteten Computer bereitgestellt hat. Der Inhalt hier gilt möglicherweise nicht für andere Antischadsoftware. Microsoft System Center Endpoint Protection verwaltet Windows Defender auf Windows 10. Endpoint Protection-Clients können auch auf Computern vor Windows 10 bereitgestellt und verwaltet werden. Wenngleich Windows Defender in diesem Artikel beschrieben wird, gelten die Informationen auch für Endpoint Protection.  

-   [Weshalb benötige ich Antiviren- und Antispywaresoftware?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [Woran erkenne ich, ob mein Computer mit Schadsoftware infiziert ist?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [Wie finde ich die Version von Windows Defender?](#how-can-i-find-the-version-of-windows-defender)
-   [Was soll ich tun, wenn Windows Defender oder Endpoint Protection Schadsoftware auf meinem Computer ermitteln?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer)  
-   [Was ist ein Virus?](#what-is-a-virus)  
-   [Was ist Spyware?](#what-is-spyware)  
-   [Was ist der Unterschied zwischen Viren, Spyware und anderer potenziell schädlicher Software?](#whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [Woher kommen Viren, Spyware und andere potenziell unerwünschte Software?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [Kann Schadsoftware ohne mein Wissen installiert werden?](#can-i-get-malicious-software-without-knowing-it)  
-   [Warum sollten Lizenzvereinbarungen vor dem Installieren von Software gelesen werden?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Was ist der Unterschied zwischen Endpoint Protection und Windows Defender?](#whats-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Warum erkennt Windows Defender keine Cookies?](#why-doesnt-windows-defender-detect-cookies)  
-   [Wie kann ich Schadsoftware verhindern?](#how-can-i-prevent-malware)  
-   [Was sind Viren- und Spywaredefinitionen?](#what-are-virus-and-spyware-definitions)  
-   [Wie halte ich Viren- und Spywaredefinitionen auf dem neuesten Stand?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [Wie kann ich Elemente entfernen oder wiederherstellen, die von Windows Defender oder Endpoint Protection unter Quarantäne gestellt wurden?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [Was ist Echtzeitschutz?](#what-is-real-time-protection)  
-   [Wie kann ich feststellen, ob Windows Defender oder Endpoint Protection auf meinem Computer ausgeführt werden?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [Wie werden Windows Defender- oder Endpoint Protection-Warnungen eingerichtet?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>Weshalb benötige ich Antiviren- und Antispywaresoftware?  

 Es muss unbedingt sichergestellt werden, dass auf dem Computer eine Software zum Schutz vor Schadsoftware (oder Malware) ausgeführt wird. Schadsoftware – also Viren, Spyware und andere potenziell unerwünschte Software – kann sich unter Umständen selbst auf dem Computer installieren, wenn Sie eine Verbindung mit dem Internet herstellen. Der Computer kann auch beim Installieren eines Programms von einer CD, DVD oder einem anderen austauschbaren Datenträger infiziert werden. Schadsoftware kann auch so programmiert sein, dass sie zu einem unerwarteten Zeitpunkt (also nicht direkt bei der Installation) ausgeführt wird.  

 Windows Defender oder Endpoint Protection bieten drei Möglichkeiten, den Computer vor dem Eindringen von Schadsoftware zu schützen.  

-   **Verwenden des Echtzeitschutzes** – Dank des Echtzeitschutzes von Windows Defender kann Ihr Computer permanent überwacht werden. Sie werden benachrichtigt, wenn versucht wird, Schadsoftware, einschließlich Viren, Spyware oder andere potenziell unerwünschte Software auf Ihrem Computer zu installieren oder auszuführen. Die Software wird dann von Windows Defender ausgesetzt, und Sie haben die Möglichkeit, den entsprechenden Empfehlungen bezüglich der Software zu folgen oder andere Maßnahmen zu ergreifen.

-   **Überprüfungsoptionen** – Sie können Windows Defender verwenden, um Ihren Computer auf potenzielle Bedrohungen wie Viren, Spyware und andere Schadsoftware zu überprüfen, die möglicherweise ein Risiko für Ihren Computer darstellen. Sie können außerdem regelmäßige Scans planen und automatisch schädliche Software, die während eines Scanvorgangs ermittelt wurde, löschen.  

-   **Microsoft Active Protection Service-Community** – In der Online-Community von Microsoft Active Protection Service können Sie verfolgen, wie andere Benutzer auf Software mit ausstehender Risikoklassifizierung reagieren. Mithilfe dieser Informationen können Sie entscheiden, ob Sie diese Software auf Ihrem Computer zulassen möchten oder nicht. Umgekehrt werden Ihre Entscheidungen – wenn Sie Mitglied der Community werden – als Bewertungen hinzugefügt und helfen wiederum anderen Benutzern bei ihrer Entscheidung.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>Woran erkenne ich, ob mein Computer mit Schadsoftware infiziert ist?  

 Sie haben möglicherweise eine Form schädlicher Software (z. B. Viren, Spyware oder andere potenziell unerwünschte Software) auf Ihrem Computer, wenn Folgendes zutrifft:  

-   Sie bemerken neue Symbolleisten, Links oder Favoriten, die Sie Ihrem Webbrowser nicht wissentlich hinzugefügt haben.  

-   Ihre Startseite, Ihr Mauszeiger oder Ihr Suchprogramm hat sich unerwartet geändert.  

-   Sie geben die Adresse für eine bestimmte Website (beispielsweise eine Suchmaschine) ein, werden jedoch ohne Benachrichtigung auf eine andere Website weitergeleitet.  

-   Dateien werden automatisch vom Computer gelöscht.  

-   Ihr Computer wird für Angriffe auf andere Computer verwendet.  

-   Es werden Werbeanzeigen eingeblendet, auch wenn Sie nicht im Internet sind.  

-   Ihr Computer reagiert plötzlich langsamer als gewöhnlich. Nicht alle Probleme in Bezug auf die Leistung des Computers sind auf schädliche Software zurückzuführen. Diese Software, insbesondere Spyware, kann jedoch deutlich erkennbare Änderungen verursachen.  

Ihr Computer kann von schädlicher Software befallen sein, selbst wenn Sie keine derartigen Symptome feststellen. Diese Art von Software kann ohne Ihre Kenntnis oder Zustimmung beispielsweise Informationen über Sie und Ihren Computer erfassen. Zum Schutz Ihrer Privatsphäre und Ihres Computers empfiehlt es sich, Windows Defender oder Endpoint Protection immer auszuführen.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>Wie finde ich die Version von Windows Defender?
 Öffnen Sie zum Anzeigen der Version von Windows Defender, die auf Ihrem Computer ausgeführt wird, Windows Defender (klicken Sie auf **Start** und suchen Sie nach **Windows Defender**), klicken Sie auf **Einstellungen**, und scrollen Sie zum unteren Rand der Windows Defender-Einstellungen, um **Versionsinfo** zu finden.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>Was soll ich tun, wenn von Windows Defender oder Endpoint Protection Schadsoftware auf dem Computer ermittelt wird?  

 Wenn von Windows Defender Schadsoftware oder möglicherweise unerwünschte Software auf Ihrem Computer ermittelt wird (entweder bei der Überwachung des Computers mithilfe des Echtzeitschutzes oder nach einem Scanvorgang), werden Sie über das erkannte Element benachrichtigt, indem in der unteren rechten Ecke des Bildschirms eine Meldung angezeigt wird.  

 Diese Meldung enthält auch eine Schaltfläche **Computer bereinigen** sowie einen Link **Details anzeigen** , über den Sie zusätzliche Informationen zum gefundenen Element erhalten. Klicken Sie auf den Link **Details anzeigen** , um das Fenster **Details zu potenziellen Bedrohungen** zu öffnen und so zusätzliche Informationen zum gefundenen Element abzurufen. Anschließend können Sie auswählen, welche Aktion Sie für das gefundene Element ausführen möchten, oder Sie klicken auf **Computer bereinigen**. Orientieren Sie sich bei der Entscheidung, welche Aktion Sie auf das gefundene Element anwenden sollten, an der von Windows Defender zugewiesenen Warnstufe. Weitere Informationen hierzu finden Sie unter „Grundlegendes zu Warnstufen“.  

 Warnstufen erleichtern die Entscheidung, wie auf Viren, Spyware und andere potenziell unerwünschte Software reagiert werden soll. Von Windows Defender wird zwar empfohlen, sämtliche Viren und Spyware zu entfernen, aber nicht die gesamte markierte Software ist tatsächlich Schadsoftware oder unerwünschte Software. Die folgenden Informationen dienen als Entscheidungshilfe für die Vorgehensweise, die verwendet werden soll, wenn von Windows Defender möglicherweise unerwünschte Software auf dem Computer erkannt wird.  

 Je nach Warnstufe können Sie eine der folgenden Aktionen für das gefundene Element anwenden:  

- **Entfernen** – Mit dieser Aktion wird die Software dauerhaft von Ihrem Computer entfernt.  

- **Quarantäne** – Mit dieser Aktion wird die Software unter Quarantäne gestellt, sodass sie nicht ausgeführt werden kann. Wenn Software von Windows Defender unter Quarantäne gestellt wird, wird sie an einen anderen Ort auf Ihrem Computer verschoben. Die Ausführung der Software wird dann solange blockiert, bis Sie die Software wiederherstellen oder vom Computer entfernen.  

- **Zulassen** – Mit dieser Aktion wird die Software der Liste für zugelassene Software von Windows Defender hinzugefügt, und die Software kann auf Ihrem Computer ausgeführt werden. Sie werden nicht mehr von Windows Defender über mögliche Risiken informiert, die diese Software für Sie und Ihren Computer darstellen könnte.  

  Wenn Sie für ein Element (z. B. eine Software) die Option **Zulassen** auswählen, werden Sie nicht mehr von Windows Defender über mögliche Risiken benachrichtigt, die diese Software für Sie und Ihren Computer darstellen könnte. Sie sollten daher eine Software nur dann der Liste der zugelassenen Elemente hinzufügen, wenn die Software und der Hersteller vertrauenswürdig sind.  

### <a name="how-to-remove-potentially-harmful-software"></a>Entfernen möglicherweise schädlicher Software

Verwenden Sie die Option **Computer bereinigen** , wenn Sie auf schnelle und einfache Weise alle von Windows Defender erkannten unerwünschten und möglicherweise schädlichen Elemente entfernen möchten.  

1.  Wenn Sie die Benachrichtigung sehen, die von Windows Defender nach dem Ermitteln potenzieller Bedrohungen im Infobereich angezeigt wird, klicken Sie auf **Computer bereinigen**.  

2.  Windows Defender entfernt mögliche Bedrohungen, und Sie erhalten eine Benachrichtigung, sobald der Computer bereinigt ist.  

3.  Wenn Sie weitere Informationen über die erkannten Bedrohungen erhalten möchten, klicken Sie auf die Registerkarte **Verlauf** , und wählen Sie **Alle erkannten Elemente**aus.  

4.  Wenn nicht alle ermittelten Elemente angezeigt werden, klicken Sie auf **Details anzeigen**. Wenn Sie zur Eingabe eines Administratorkennworts oder zur Bestätigung aufgefordert werden, geben Sie das Kennwort ein, oder bestätigen Sie die Aktion.

> [!NOTE]  
>  Bei der Bereinigung des Computers wird von Windows Defender – sofern möglich – nur der infizierte Teil einer Datei und nicht die gesamte Datei entfernt.  

##  <a name="what-is-a-virus"></a>Was ist ein Virus?  
 Computerviren sind Softwareprogramme, die absichtlich dazu entwickelt wurden, den Computerbetrieb zu stören, Daten aufzuzeichnen, zu beschädigen oder zu löschen sowie über das Internet andere Computer zu infizieren. Computer werden durch Viren häufig verlangsamt, wobei auch andere Probleme verursacht werden.  

##  <a name="what-is-spyware"></a>Was ist Spyware?  
 Bei Spyware handelt es sich um Software, die ohne Ihre Zustimmung oder anderweitige Kontrollen unbemerkt auf Ihrem PC installiert und ausgeführt wird. Bei einer Infektion mit Spyware treten auf dem PC möglicherweise keine Symptome auf, viele bösartige oder unerwünschte Programme können sich jedoch auf den Betrieb Ihres PCs auswirken. Mit Spyware können beispielsweise Ihr Verhalten im Internet überwacht oder Informationen über Ihre Person erfasst werden (einschließlich Informationen, anhand derer Sie identifiziert werden können, oder andere sensible Daten), es können Einstellungen auf Ihrem Computer geändert werden, oder sie kann dazu führen, dass der Computer nur sehr langsam arbeitet.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a>Was ist der Unterschied zwischen Viren, Spyware und anderer potenziell schädlicher Software?  
 Sowohl Viren als auch Spyware werden ohne Ihr Wissen auf dem PC installiert und können beide aufdringlich und zerstörerisch wirken. Sie können zudem Informationen auf dem PC erfassen und diese Informationen beschädigen oder löschen. Beide können die Computerleistung beeinträchtigen.  

 Der Hauptunterschied zwischen Viren und Spyware liegt in ihrem Verhalten auf dem PC. Viren haben wie lebende Organismen das Ziel, einen Computer zu infizieren, sich zu replizieren und dann auf möglichst viele andere Computer weiterzuverteilen. Spyware verhält sich dagegen eher wie ein Maulwurf. Sie nistet sich in Ihrem PC ein und bleibt dort solange wie möglich, um während dieses Zeitraums wertvolle Informationen über Ihren Computer an eine externe Quelle zu senden.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>Woher kommen Viren, Spyware und andere potenziell unerwünschte Software?  
 Die Installation von unerwünschter Software wie Viren erfolgt über Websites oder Programme, die Sie herunterladen oder von einer CD, DVD, externen Festplatte oder einem anderen Gerät installieren. Spyware wird am häufigsten durch kostenlose Software installiert, z. B. File-Sharing-Anwendungen, Bildschirmschoner oder Suchsymbolleisten.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a>Kann Schadsoftware ohne mein Wissen installiert werden?  
 Ja, einige Arten von Schadsoftware können von Websites mithilfe eines auf der Webseite eingebetteten Skripts oder eines Programms installiert werden. Einige Schadsoftware benötigt Ihre Hilfe zur Installation. Für diese Software werden Web-Popups oder kostenlose Software eingesetzt, bei der Sie eine herunterladbare Datei annehmen sollen. Wenn Sie jedoch Microsoft Windows® auf dem neuesten Stand halten und Ihre Sicherheitseinstellungen nicht reduzieren, können Sie die Wahrscheinlichkeit einer Infektion auf ein Minimum verringern.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>Warum sollten Lizenzvereinbarungen vor dem Installieren von Software gelesen werden?  
 Beim Besuch einer Website stimmen Sie nicht automatisch zu, irgendetwas herunterzuladen, das die Website anbietet. Lesen Sie beim Herunterladen kostenloser Software, z. B. Dateifreigabeprogrammen oder Bildschirmschonern, die Lizenzbedingungen sorgfältig durch. Achten Sie auf Klauseln, die besagen, dass Sie mit Werbung oder Popups des Unternehmens einverstanden sind oder dass die Software bestimmte Informationen an den Softwareherausgeber zurücksendet.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>Was ist der Unterschied zwischen Endpoint Protection und Windows Defender?  
 Endpoint Protection ist eine Antischadsoftware, d. h. sie ist darauf ausgerichtet, verschiedenste Schadsoftware einschließlich Viren, Spyware und anderer möglicherweise unerwünschter Software zu erkennen und Ihren Computer vor solcher zu schützen. Bei Windows Defender, der automatisch mit dem Windows-Betriebssystem installiert wird, handelt es sich um eine Software zum Erkennen und Stoppen von Spyware.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>Warum erkennt Windows Defender keine Cookies?  
 Cookies sind kleine Textdateien, die von Websites auf Ihrem PC abgelegt werden, um Information zu Ihrer Person und Ihren Vorlieben zu speichern. Websites nutzen Cookies, um Ihnen eine personalisierte Erfahrung zu bieten, und um Daten zur Websitenutzung zu sammeln. Windows Defender erkennt Cookies nicht, da sie nicht als Bedrohung Ihrer Privatsphäre oder der Sicherheit Ihres PCs angesehen werden. Die meisten Internetbrowserprogramme erlauben es Ihnen, Cookies zu blockieren.  

##  <a name="how-can-i-prevent-malware"></a>Wie kann ich Schadsoftware verhindern?  
 Viren und Spyware stellen heutzutage für Computerbenutzer zwei der größten Probleme dar. Zwar können sowohl Viren als auch Spyware Probleme verursachen, durch Berücksichtigung verschiedener Aspekte können Sie sich jedoch auf einfache Weise dagegen schützen:  

-   Achten Sie darauf, dass die Software auf Ihrem Computer aktuell ist und alle Patches installiert sind. Aktualisieren Sie Ihr Betriebssystem regelmäßig.  

-   Stellen Sie sicher, dass von Windows Defender, Ihrer Antivirus- und Antispywaresoftware, aktuelle Updates gegen potenzielle Bedrohungen verwendet werden (siehe „Wie halte ich Viren- und Sypwaredefinitionen auf dem neuesten Stand?“). Stellen Sie außerdem sicher, dass Sie immer die neueste Version von Windows Defender verwenden.  

-   Laden Sie Updates nur aus vertrauenswürdigen Quellen herunter. Bei Windows-Betriebssystemen wechseln Sie immer zum [Microsoft Update-Katalog](https://catalog.update.microsoft.com).  Verwenden Sie bei anderer Software immer die offiziellen Websites des Unternehmens oder der Person, die sie erstellt hat.

-   Wenn Sie eine E-Mail mit einem Anhang erhalten und Sie die Quelle nicht kennen, sollten Sie die E-Mail unverzüglich löschen. Laden Sie keine Anwendungen oder Dateien aus unbekannten Quellen herunter, und gehen Sie beim Austausch von Dateien mit anderen Benutzern sorgfältig vor.  

-   Installieren und verwenden Sie eine Firewall. Es wird empfohlen, die Windows-Firewall zu aktivieren.  

##  <a name="what-are-virus-and-spyware-definitions"></a>Was sind Viren- und Spywaredefinitionen?  
 Wenn Sie Windows Defender oder Endpoint Protection verwenden, ist es wichtig, dass die Viren- und Spywareschutzdefinitionen auf dem aktuellen Stand sind. Definitionen sind Dateien, die wie eine sich ständig erweiternde Enzyklopädie für potenzielle Softwarebedrohungen funktionieren. Von Windows Defender oder Endpoint Protection werden diese Definitionen verwendet, um festzustellen, ob es sich bei der erkannten Software um einen Virus, Spyware oder eine andere möglicherweise unerwünschte Software handelt, und um Sie anschließend über das potenzielle Risiko zu informieren. Damit die Definitionen immer auf dem neuesten Stand sind, wird Windows Defender oder Endpoint Protection in Verbindung mit Windows Updates eingesetzt, um neue Definitionen automatisch zu installieren, sobald sie veröffentlicht werden. Sie können Windows Defender oder Endpoint Protection auch so einrichten, dass online eine Überprüfung auf aktualisierte Definitionen erfolgt, bevor nach Viren oder Spyware gescannt wird.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>Wie halte ich Viren- und Sypwaredefinitionen auf dem neuesten Stand?  
 Viren- und Spywaredefinitionen sind Dateien, die wie eine Enzyklopädie für bekannte Schadsoftware wie Viren, Spyware oder andere potenziell unerwünschte Software funktionieren. Da es ständig neue Entwicklungen von Schadsoftware gibt, werden für Windows Defender oder Endpoint Protection aktuelle Definitionen verwendet, um festzustellen, ob es sich bei Software, die auf Ihrem Computer installiert oder ausgeführt wird oder von der versucht wird, Einstellungen auf dem Computer zu ändern, um einen Virus, um Spyware oder um andere möglicherweise unerwünschte Software handelt.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>So führen Sie automatisch eine Überprüfung auf neue Definitionen aus, bevor Sie geplante Scans ausführen (empfohlen)  

1.  Öffnen Sie Windows Defender oder den Endpoint Protection-Client durch Klicken auf das Symbol im Infobereich der Taskleiste, oder starten Sie ihn im **Startmenü**.  

2.  Klicken Sie auf **Einstellungen**und dann auf **Geplanter Scan**.  

3.  Stellen Sie sicher, dass das Kontrollkästchen **Vor dem geplanten Scanvorgang nach neuen Viren- und Spywaredefinitionen suchen** aktiviert ist, und klicken Sie auf **Änderungen speichern**. Wenn Sie zur Eingabe eines Administratorkennworts oder zur Bestätigung aufgefordert werden, geben Sie das Kennwort ein, oder bestätigen Sie die Aktion.  

### <a name="to-check-for-new-definitions-manually"></a>So führen Sie eine manuelle Überprüfung auf neue Definitionen aus

 Die Viren- und Spywareschutzdefinitionen werden von Windows Defender oder Endpoint Protection automatisch auf Ihrem Computer aktualisiert. Wenn die Definitionen länger als sieben Tage nicht aktualisiert wurden (wenn Sie beispielsweise Ihren Computer eine Woche lang nicht angeschaltet haben), werden Sie von Windows Defender oder Endpoint Protection benachrichtigt, dass die Definitionen nicht auf dem aktuellen Stand sind.  

1.  Öffnen Sie Windows Defender oder den Endpoint Protection-Client durch Klicken auf das Symbol im Infobereich der Taskleiste, oder starten Sie ihn im **Startmenü**.  

2.  Klicken Sie auf die Registerkarte **Aktualisieren** und dann auf **Aktualisieren**, um manuell eine Überprüfung auf neue Definitionen auszuführen.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Wie kann ich Elemente entfernen oder wiederherstellen, die von Windows Defender oder Endpoint Protection unter Quarantäne gestellt wurden?  

 Wenn Software durch Windows Defender oder Endpoint Protection unter Quarantäne gestellt wird, wird sie an einen anderen Ort auf Ihrem Computer verschoben. Die Ausführung der Software wird dann solange blockiert, bis Sie die Software wiederherstellen oder vom Computer entfernen.  

 Für alle in dieser Prozedur beschriebenen Schritte gilt: Wenn Sie zur Eingabe eines Administratorkennworts oder einer Bestätigung aufgefordert werden, geben Sie das Kennwort ein oder bestätigen Sie die Aktion.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>So werden von Windows Defender oder Endpoint Protection unter Quarantäne gestellte Elemente entfernt oder wiederhergestellt


1.  Klicken Sie auf die Registerkarte **Verlauf** , wählen Sie **Unter Quarantäne gestellte Elemente**und dann die Option **Unter Quarantäne gestellte Elemente** aus.  

2.  Klicken Sie auf **Details anzeigen** , damit alle Elemente angezeigt werden.  

3.  Überprüfen Sie die einzelnen Elemente, und klicken Sie dann für jedes einzelne Element auf **Entfernen** oder **Wiederherstellen**. Wenn Sie alle unter Quarantäne gestellten Elemente vom Computer entfernen möchten, klicken Sie auf **Alle entfernen**.  

##  <a name="what-is-real-time-protection"></a>Was ist Echtzeitschutz?  

 Über den Echtzeitschutz von Windows Defender kann Ihr Computer permanent überwacht werden. Sie werden alarmiert, wenn potenzielle Bedrohungen durch Viren oder Spyware bestehen und versucht wird, diese auf Ihrem Computer zu installieren oder auszuführen. Diese Funktion stellt ein wichtiges Element für die Funktionalität von Windows Defender im Hinblick auf den Schutz Ihres Computers dar. Daher sollte sichergestellt sein, dass der Echtzeitschutz immer aktiviert ist. Wenn der Echtzeitschutz deaktiviert wird, werden Sie von Windows Defender benachrichtigt, und der Status Ihres Computers wird auf **„Gefährdet“** festgelegt.  

 Wenn vom Echtzeitschutz eine potenzielle Bedrohung ermittelt wird, werden Sie von Windows Defender mit einer Meldung benachrichtigt. Sie können nun aus den folgenden Optionen auswählen:  

- Klicken Sie auf **Computer bereinigen** , um das ermittelte Element zu entfernen. Das Element wird von Windows Defender automatisch von Ihrem Computer entfernt.  

- Klicken Sie auf den Link **Details anzeigen** , um das Fenster „Details zu potenziellen Bedrohungen“ zu öffnen und auszuwählen, welche Aktion Sie auf das ermittelte Element anwenden möchten.  

  Sie können auswählen, welche Software und welche Einstellungen von Windows Defender überwacht werden sollen. Es wird jedoch empfohlen, den Echtzeitschutz sowie alle Echtzeitschutzoptionen zu aktivieren. In der folgenden Tabelle werden die verfügbaren Optionen erläutert.  

|||  
|-|-|  
|**Echtzeitschutzoption**|**Zweck**|  
|Alle heruntergeladene Dateien überprüfen|Mit dieser Option werden heruntergeladene Dateien und Programme überwacht. Hierzu zählen auch Dateien und Programme, die automatisch mittels Windows Internet Explorer und Microsoft Outlook® Express heruntergeladen werden (beispielsweise ActiveX®-Steuerelemente und Softwareinstallationsprogramme). Diese Dateien können vom Browser selbst heruntergeladen, installiert oder ausgeführt werden. Schadsoftware wie Viren, Spyware oder andere potenziell unerwünschte Software kann in diesen Dateien enthalten sein und ohne Ihr Wissen installiert werden.<br /><br /> Bei Verwendung der Echtzeitschutzoption wird Ihr Computer ständig von Windows Defender überwacht, und es erfolgt eine Überprüfung auf bösartige Dateien oder Programme, die Sie möglicherweise heruntergeladen haben. Bei dieser Überwachungsoption muss die Browser- oder E-Mail-Nutzung durch Windows Defender nicht verlangsamt werden, um eine Überprüfung sämtlicher Dateien oder Programme vorzunehmen, die Sie möglicherweise herunterladen möchten.|  
|Datei- und Programmaktivität auf Ihrem Computer überwachen|Mit dieser Option wird überwacht, wenn Dateien und Programme auf dem Computer ausgeführt werden. Sie werden dann über alle von ihnen ausgeführten bzw. daran vorgenommenen Aktionen benachrichtigt. Dies ist wichtig, da Schadsoftware Schwachstellen in Programmen ausnutzen kann, die Sie installiert haben, um ohne Ihr Wissen Schadsoftware oder unerwünschte Software auszuführen. So kann beispielsweise Spyware von selbst im Hintergrund ausgeführt werden, wenn Sie ein Programm starten, das Sie häufig verwenden. Mit Windows Defender werden Ihre Programme überwacht, und Sie werden benachrichtigt, sobald eine verdächtige Aktivität erfolgt.|  
|Verhaltensüberwachung aktivieren|Diese Option dient zum Überwachen von Verhaltenssammlungen auf verdächtige Muster, die bei herkömmlichen Schutzmethoden zum Erkennen von Viren unter Umständen nicht erkannt werden.|  
|Netzwerkinspektionssystem aktivieren|Mithilfe dieser Option wird der Computer vor Zero-Day-Exploits geschützt. Hierbei wird das Zeitfenster zwischen dem Erkennen eines Sicherheitsrisikos und dem Anwenden eines Updates verkürzt.|  

### <a name="to-turn-off-real-time-protection"></a>So deaktivieren Sie den Echtzeitschutz  

1.  Klicken Sie auf **Einstellungen**und dann auf **Echtzeitschutz**.  

2.  Deaktivieren Sie die Echtzeitschutzoptionen, die Sie nicht verwenden möchten, und klicken Sie dann auf **Änderungen speichern**. Wenn Sie zur Eingabe eines Administratorkennworts oder zur Bestätigung aufgefordert werden, geben Sie das Kennwort ein, oder bestätigen Sie die Aktion.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>Wie kann ich feststellen, ob Windows Defender oder Endpoint Protection auf meinem Computer ausgeführt wird?  

 Nachdem Windows Defender auf Ihrem Computer installiert wurde, können Sie das Hauptfenster schließen, und Windows Defender kann unbeaufsichtigt im Hintergrund ausgeführt werden. Windows Defender wird weiterhin auf dem Computer ausgeführt. Der Computer wird auf diese Weise überwacht und vor Bedrohungen geschützt.  

 Dass Windows Defender ausgeführt wird, erkennen Sie daran, dass im Infobereich entsprechende Benachrichtigungen angezeigt werden. Anhand dieser Benachrichtigungen werden Sie über potenzielle Bedrohungen informiert, die von Windows Defender ermittelt wurden.  

 Es werden auch andere Benachrichtigungen angezeigt, beispielsweise wenn der Echtzeitschutz deaktiviert wurde, über mehrere Tage die Virus- und Spywaredefinitionen nicht aktualisiert wurden oder wenn Upgrades für das Programm verfügbar sind. Von Windows Defender wird auch eine Informationsmeldung mit dem Hinweis angezeigt, dass der Computer gerade gescannt wird.  

> [!TIP]
> 
> Wenn Sie das Windows Defender-Symbol nicht im Infobereich sehen, klicken Sie auf den Pfeil im Infobereich, um ausgeblendete Symbole anzuzeigen, z.B. das Windows Defender-Symbol.  


 Die Farbe des Symbols hängt dabei vom aktuellen Zustand des Computers ab:  

-   Mit der Farbe Grün wird angegeben, dass Ihr Computer geschützt ist.  

-   Mit der Farbe Gelb wird angegeben, dass Ihr Computer möglicherweise nicht geschützt ist.  

-   Mit der Farbe Rot wird angegeben, dass Ihr Computer gefährdet ist.  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>Wie werden Windows Defender- oder Endpoint Protection-Warnungen eingerichtet?  
 Wenn Windows Defender auf dem Computer ausgeführt wird, werden Sie automatisch benachrichtigt, falls Viren, Spyware und andere möglicherweise unerwünschte Software gefunden wird. Sie können Windows Defender auch so einrichten, dass Sie benachrichtigt werden, wenn Sie eine Software ausführen, die noch nicht auf Risiken analysiert wurde. Darüber hinaus können Sie auswählen, dass Sie benachrichtigt werden möchten, wenn eine Software Änderungen auf Ihrem Computer verursacht.  

### <a name="to-set-up-alerts"></a>So richten Sie Benachrichtigungen ein  

1.  Klicken Sie auf **Einstellungen**und dann auf **Echtzeitschutz**.  

2.  Stellen Sie sicher, dass das Kontrollkästchen **Echtzeitschutz aktivieren (empfohlen)** aktiviert ist.  

3.  Aktivieren Sie die Kontrollkästchen neben den Echtzeitüberwachungsoptionen, die Sie verwenden möchten, und klicken Sie dann auf **Änderungen speichern**. Wenn Sie zur Eingabe eines Administratorkennworts oder zur Bestätigung aufgefordert werden, geben Sie das Kennwort ein, oder bestätigen Sie die Aktion.  

### <a name="see-also"></a>Weitere Informationen:  
 [Problembehandlung für Windows Defender oder den Endpoint Protection-Client](troubleshoot-endpoint-client.md)   

 [Hilfe zu Endpoint Protection-Client](endpoint-protection-client-help.md)
