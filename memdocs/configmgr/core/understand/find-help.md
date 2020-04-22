---
title: Suchen nach Hilfe
titleSuffix: Configuration Manager
description: Suchen Sie Ressourcen für zusätzliche Informationen zu Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6610e86c12b6f7704b65dc11c476fa09e8f2ae63
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707158"
---
# <a name="find-help-for-using-configuration-manager"></a>Suchen nach Hilfe für die Verwendung von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden die folgenden Abschnitte mit mehreren Ressourcen genannt, die Ihnen bei der Verwendung von Configuration Manager helfen sollen:  

- [Produktdokumentation](#bkmk_Info)  

- [Produktfeedback teilen](#product-feedback)  

- [Teamblog zu Configuration Manager folgen](#BKMK_ProductGroupBlog)  

- [Supportoptionen und Communityressourcen](#BKMK_SupportOptions)  

Hilfe zur Barrierefreiheit für Produkte finden Sie unter [Barrierefreiheitsfeatures](accessibility-features.md).  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a> Produktdokumentation  

Beginnen Sie beim [Bibliotheksindex](https://docs.microsoft.com/sccm/), um auf die aktuellste Produktdokumentation zuzugreifen.  

<a name="BKMK_SearchTips"></a>  

Tipps zur Suche und zum Bereitstellen von Feedback sowie weitere Informationen zur Verwendung der Produktdokumentation finden Sie unter [Verwenden der Dokumentation](use-docs.md).  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a> Produktfeedback ab Version 1806

Ab Configuration Manager Version 1806 können Sie Feedback zu Produkten direkt über die Konsole senden. Verwenden Sie den [Feedback-Hub](#BKMK_FeedbackHub), wenn Sie Protokolle anfügen müssen. Sie haben folgende Möglichkeiten: <!--1357542-->

- **Lächeln senden**: Senden Sie Feedback zu Dingen, die Ihnen gefallen haben.
- **Stirnrunzeln senden**: Senden Sie Feedback zu Dingen, die Ihnen nicht gefallen haben.
- **Vorschlag senden**: Leitet Sie zur [UserVoice-Website](https://configurationmanager.uservoice.com/) weiter, wo Sie Ihre Ideen teilen können.

  ![Feedback senden in Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>Senden eines Lächelns oder eines Stirnrunzelns

Folgen Sie den folgenden Anweisungen, um Feedback für etwas zu senden, das Ihnen gefallen hat:

1. Klicken Sie in der oberen rechten Ecke der Konsole auf das Smileysymbol.
2. Klicken Sie im Dropdownmenü auf **Lächeln senden** oder **Stirnrunzeln senden**.
3. Verwenden Sie das Textfeld, um zu beschreiben, was Ihnen gefallen oder nicht gefallen hat. 
4. Wählen Sie aus, ob Sie Ihre E-Mail-Adresse und einen Screenshot freigeben möchten.
5. Klicken Sie auf **Feedback senden**.
     - Wenn Sie keine Internetverbindung haben, klicken Sie auf **Speichern** am unteren Rand. Folgen Sie den Anweisungen im Abschnitt [Feedback senden, das für die spätere Übermittlung gespeichert wurde](#BKMK_NoInternet), um es an Microsoft zu senden. 

![Formular „Feedback senden“ in Configuration Manager 1806](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>Statusmeldungen für „Lächeln senden“
<!--5891852-->
Ab Configuration Manager 2002 wird beim Übermitteln von Feedback für die Optionen **Lächeln senden** oder **Stirnrunzeln senden** eine Statusmeldung erstellt. Diese Verbesserung bietet einen Datensatz zu folgenden Punkten:
- Informationen zum Zeitpunkt der Übermittlung
- Absender des Feedbacks
- Feedback-ID
- Informationen zur erfolgreichen oder nicht erfolgreichen Übermittlung des Feedbacks
   - Nachrichten-ID 53900 für eine erfolgreiche Übermittlung
   - Nachrichten-ID 53901 für eine fehlgeschlagene Übermittlung

Sie können die Statusmeldungen unter **Überwachung** > **Systemstatus** > **Statusmeldungsabfragen** anzeigen. Beginnen Sie mit der Abfrage **Alle Statusmeldungen**, und wählen Sie den gewünschten Zeitrahmen aus. Klicken Sie beim Laden der Meldungen auf die Schaltfläche **Meldungen filtern**, und suchen Sie nach Meldungs-ID 53900 oder 53901.

Wenn Sie [Feedback senden, das Sie zur späteren Übermittlung gespeichert haben](find-help.md#BKMK_NoInternet), werden keine Statusmeldungen erstellt.

[![Statusmeldung für erfolgreiche Übermittlung von Feedback](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>Senden eines Vorschlags

Wenn Sie einen **Vorschlag senden**, werden Sie auf [UserVoice](https://configurationmanager.uservoice.com/) weitergleitet, eine Drittanbieterwebsite, über die Sie Ihre Idee teilen können. Das Configuration Manager-Produktteam verwendet die folgenden UserVoice-Statuswerte:

- **Noted** (Notiert): Wir können den Vorschlag nachvollziehen, und er erscheint uns als sinnvoll. Wir haben ihn zu unserem Backlog hinzugefügt.
- **Geplant:** Wir haben mit der Entwicklung dieses Features begonnen. In den nächsten Monaten sollte eine Technical Preview-Version veröffentlicht werden.
- **Gestartet:** Es gibt jetzt eine Technical Preview-Version des Features. Testen Sie sie, und geben Sie uns Feedback. Teilen Sie uns mit, ob wir auf dem richtigen Weg sind. Fügen Sie zusätzliches Feedback zum Kommentarbereich der ursprünglichen Anfrage hinzu, damit dieses von anderen gesehen und mit weiteren Kommentaren versehen werden kann. Wir werden uns alles durchlesen und das Feedback nutzen, um das Feature zu verbessern.
- **Abgeschlossen:** Die erste Version des Features ist in einem Produktionsbuild enthalten. Das bedeutet nicht, dass wir die Entwicklung des Features abgeschlossen haben und nicht mehr an Verbesserungen arbeiten. Vielmehr bedeutet es, dass sich die erste Version des Features in einem Produktionsbuild befindet und Sie es verwenden können. Wir legen nur aus den folgenden Gründen den Status „Abgeschlossen“ fest:
  - Wir möchten Sie darüber informieren, dass das Feature bereit für die Produktion ist.
  - Wir möchten Ihre UserVoice-Stimmen wieder für Sie freigeben, damit Sie sie für andere Items verwenden können.
  - Sie können neue Änderungsanfragen in Bezug auf das Design des Features senden, um uns mitzuteilen, welche Verbesserungen für dieses Feature am wichtigsten sind.

### <a name="information-sent-with-feedback"></a>Informationen, die mit dem Feedback gesendet werden

Wenn Sie uns ein **Lächeln** oder ein **Stirnrunzeln senden**, werden die folgenden Informationen zusammen mit dem Feedback gesendet:

- Betriebssystem-Buildinformationen
- Configuration Manager-Hierarchie-ID
- Produkt-Buildinformationen
- Sprachinformationen
- Gerätebezeichner 
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a> Feedback senden, das für die spätere Übermittlung gespeichert wurde

1. Klicken Sie am unteren Rand des Fensters **Feedback bereitstellen** auf **Speichern**. 
2. Speichern Sie die ZIP-Datei. Wenn der lokale Computer keinen Internetzugriff hat, kopieren Sie die Datei auf einen Computer, der mit dem Internet verbunden ist. 
3. Kopieren Sie gegebenenfalls den Ordner „UploadOfflineFeedback.exe“, den Sie hier finden: `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`.
    - Weitere Informationen über den Ordner „CD.Latest“ finden Sie unter [Der Ordner „CD.Latest“](../servers/manage/the-cd.latest-folder.md).

4. Öffnen Sie auf einem Computer mit Internetzugriff eine Eingabeaufforderung. 
5. Führen Sie den folgenden Befehl aus: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Optional können Sie die folgenden Parameter angeben:
        -  `-t, --timeout` Zeitlimit in Sekunden für das Senden von Daten. 0 ist unbegrenzt. Standard ist 30.
        - `-s --silent` Keine Protokollierung an die Konsole (Kann nicht mit --verbose kombiniert werden)
        - `-v, --verbose` Ausgabe ausführlicher Protokolle an die Konsole (Kann nicht mit --silent kombiniert werden)
        - `--help` Zeigt den Hilfebildschirm an

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a> Confirmation of console feedback (Bestätigung des Konsolenfeedbacks)

<!--3556010-->
Ab Version 1902 erhalten Sie eine Bestätigungsmeldung, wenn Sie Feedback über die Configuration Manager-Konsole oder die Datei „UploadOfflineFeedback.exe“ senden. Diese enthält eine **Feedback-ID**, die Sie zur Nachverfolgung an Microsoft übermitteln können.

- Klicken Sie auf das Symbol neben der **Feedback-ID**, um diese zu kopieren. Alternativ können Sie auch **STRG** + **C** drücken.
  - Die ID wird nicht auf Ihrem Computer gespeichert, Sie sollten Sie also kopieren, bevor Sie das Fenster schließen.
- Wenn Sie auf **Diese Meldung nicht mehr anzeigen** klicken, wird das Dialogfeld ausgeblendet und auch in Zukunft nicht wieder angezeigt.

   ![Bestätigungsmeldung für Feedback in der Configuration Manager-Konsole, Version 1902](media/1902-feedback-id-example.png)
- Das Befehlszeilentool **UploadOfflineFeedback** schreibt die **FeedbackID** in die Konsole, wenn nicht „-s“ oder „--silent“ verwendet wird.

  ![Bestätigungsmeldung für Feedback über die Datei „UploadOfflineFeedback.exe“ in Configuration Manager, Version 1902](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a> Produktfeedback für Version 1802 und früher

Melden Sie mögliche Produktfehler über die in Windows 10 integrierte [Feedback Hub-App](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app). Wenn Sie **neues Feedback übermitteln**, achten Sie darauf, erst die Kategorie **Enterprise Management** und dann eine der folgenden Unterkategorien auszuwählen:
- Konfigurations-Manager-Client
- Configuration Manager-Konsole
- Betriebssystembereitstellung von Configuration Manager
- Configuration Manager-Server

Nutzen Sie weiterhin die [Seite für Benutzerfeedback](https://configurationmanager.uservoice.com/), um über Ideen für neue Features von Configuration Manager abzustimmen. Das Configuration Manager-Produktteam verwendet die folgenden UserVoice-Statuswerte:

- **Noted** (Notiert): Wir können den Vorschlag nachvollziehen, und er erscheint uns als sinnvoll. Wir haben ihn zu unserem Backlog hinzugefügt.
- **Geplant:** Wir haben mit der Entwicklung dieses Features begonnen. In den nächsten Monaten sollte eine Technical Preview-Version veröffentlicht werden.
- **Gestartet:** Es gibt jetzt eine Technical Preview-Version des Features. Testen Sie sie, und geben Sie uns Feedback. Teilen Sie uns mit, ob wir auf dem richtigen Weg sind. Fügen Sie zusätzliches Feedback zum Kommentarbereich der ursprünglichen Anfrage hinzu, damit dieses von anderen gesehen und mit weiteren Kommentaren versehen werden kann. Wir werden uns alles durchlesen und das Feedback nutzen, um das Feature zu verbessern.
- **Abgeschlossen:** Die erste Version des Features ist in einem Produktionsbuild enthalten. Das bedeutet nicht, dass wir die Entwicklung des Features abgeschlossen haben und nicht mehr an Verbesserungen arbeiten. Vielmehr bedeutet es, dass sich die erste Version des Features in einem Produktionsbuild befindet und Sie es verwenden können. Wir legen nur aus den folgenden Gründen den Status „Abgeschlossen“ fest:
  - Wir möchten Sie darüber informieren, dass das Feature bereit für die Produktion ist.
  - Wir möchten Ihre UserVoice-Stimmen wieder für Sie freigeben, damit Sie sie für andere Items verwenden können.
  - Sie können neue Änderungsanfragen in Bezug auf das Design des Features senden, um uns mitzuteilen, welche Verbesserungen für dieses Feature am wichtigsten sind.

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a> Teamblog zu Configuration Manager  

Das Configuration Manager-Engineering-Team und die Partnerteams stellen im [Enterprise Mobility + Security-Blog](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) technische Informationen und andere Neuigkeiten zu Configuration Manager und entsprechenden Technologien bereit. Unsere Blogbeiträge ergänzen die Produktdokumentation und Supportinformationen.  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a> Supportoptionen und Communityressourcen  

Über die folgenden Links finden Sie weitere Informationen zu Supportoptionen und Communityressourcen:  

-   [Microsoft-Support](https://aka.ms/cmcbsupport)  

-   [Configuration Manager Community: Configuration Manager (Current Branch) Survival Guide (Configuration Manager-Community: Übersicht über nützliche Ressourcen für System Center Configuration Manager (Current Branch))](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Configuration Manager-Forenübersicht](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
