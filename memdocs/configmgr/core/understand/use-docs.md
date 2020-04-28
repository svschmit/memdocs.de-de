---
title: Verwenden der Dokumentation
titleSuffix: Configuration Manager
description: Hier finden Sie Tipps zum Verwenden der technischen Dokumentationsbibliothek von Configuration Manager.
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d694f9985e6d1e5118f2620e5cbd556de249788a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771313"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Verwenden der Configuration Manager-Dokumentation

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel finden Sie Ressourcen und Tipps zur Verwendung der Configuration Manager-Dokumentationsbibliothek.

- Suchen
- Übermitteln von Fehlern in der Dokumentation, Verbesserungen, Fragen und neuen Ideen
- Benachrichtigung über Änderungen
- Mitwirken an der Dokumentation

Allgemeine Hilfe zum Produkt finden Sie unter [Suchen nach Hilfe](find-help.md).

## <a name="search"></a><a name="bkmk_searchtips"></a> Suchen

Die folgende Suchtipps sollen Ihnen dabei helfen, die benötigten Informationen zu finden:

- Wenn Sie Ihre bevorzugte Suchmaschine verwenden, um nach Inhalten von Configuration Manager zu suchen, fügen Sie `ConfigMgr` zu Ihren Suchbegriffen hinzu.

  - Suchen Sie nach Ergebnissen von `docs.microsoft.com/configmgr` für Configuration Manager (Current Branch). Ergebnisse für `docs.microsoft.com/previous-versions` gelten für ältere Versionen.

  - Fügen Sie `site:docs.microsoft.com` zum Bereich der Suchmaschine hinzu, um die Suchergebnisse weiter auf die aktuelle Inhaltsbibliothek zu konzentrieren.

- Verwenden Sie Suchbegriffe, die der Terminologie in der Benutzeroberfläche und der Onlinedokumentation entsprechen. Vermeiden Sie die Verwendung von Begriffen oder Abkürzungen, die möglicherweise von der Community, aber nicht offiziell verwendet werden. Suchen Sie beispielsweise folgendermaßen:

  - „management point“ (Verwaltungspunkt) anstelle von „MP“
  - „deployment type“ (Bereitstellungstyp) anstelle von „DT“
  - „software updates“ (Softwareupdates) anstelle von „SUM“

- Zur Suche im aktuellen Artikel können Sie die **Suchfeatures** Ihres Browsers verwenden. In den meisten modernen Webbrowsern können Sie **STRG**+**F** drücken und anschließend Ihre Suchbegriffe eingeben.

- Jeder Artikel auf `docs.microsoft.com` enthält die folgenden Felder, die Ihnen bei der Suche von Inhalten helfen sollen:

  - **Suchen** in der oberen rechten Ecke. Geben Sie die Begriffe in dieses Feld ein, um in allen Artikeln zu suchen. Artikel in der Configuration Manager-Bibliothek schließen automatisch den `ConfigMgr`-Bereich ein, sodass nur diese Dokumentationsbibliothek durchsucht wird.

  - **Nach Titel filtern** oberhalb des Inhaltsverzeichnisses auf der linken Seite. Geben Sie in dieses Feld Begriffe ein, um sie im aktuellen Inhaltsverzeichnis zu suchen. Über dieses Feld werden nur Begriffe gesucht, die in den Titeln der Artikel für den aktuellen Knoten vorkommen, beispielsweise **Core Infrastructure** (Kerninfrastruktur, `docs.microsoft.com/configmgr/core`) oder **Application Management** (Anwendungsverwaltung, `docs.microsoft.com/configmgr/apps`).

- Haben Sie Probleme bei der Suche? [Senden Sie Feedback!](#bkmk_docfeedback) Wenn Sie Probleme melden, geben Sie die verwendete Suchmaschine, die getesteten Schlüsselwörter und den Zielartikel an. Durch dieses Feedback kann Microsoft den Inhalt für bessere Suchergebnisse optimieren.

> [!TIP]
> Ab der Configuration Manager-Version 1902 befindet sich im neuen Arbeitsbereich **Community** der Configuration Manager-Konsole ein Knoten **Dokumentation**. Dieser Knoten enthält aktuelle Informationen zur Configuration Manager-Dokumentation und Supportartikel. Weitere Informationen finden Sie unter [Verwenden der Configuration Manager-Konsole](../servers/manage/admin-console.md#bkmk_doc-dashboard).

## <a name="feedback"></a><a name="bkmk_docfeedback"></a> Feedback

Klicken Sie auf den Link **Feedback** in der oberen rechten Ecke eines Artikels, um zum Abschnitt „Feedback“ im unteren Bereich zu gelangen. In diesem Abschnitt sind GitHub-Links zu Problemen enthalten. Weitere Informationen zur Verknüpfung mit GitHub-Problemen finden Sie in diesem [Blogbeitrag zur Dokumentationsplattform](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

Klicken Sie auf **Produktfeedback**, um Feedback zu Configuration Manager zu geben. Weitere Informationen finden Sie unter [Produktfeedback](find-help.md#product-feedback).

Ein [GitHub-Konto](https://github.com/join) ist eine Voraussetzung dafür, Feedback zur Dokumentationen zu senden. Sobald Sie sich angemeldet haben, müssen Sie sich einmalig für die MicrosoftDocs-Organisation autorisieren. Wenn Sie dann auf **Inhaltsfeedback** klicken, geben Sie einen Titel und einen Kommentar ein, und klicken Sie dann auf **Feedback senden**. Durch diese Aktion wird ein neues Problem für den Zielartikel im [SCCMdocs-Repository](https://github.com/MicrosoftDocs/SCCMdocs/issues) erstellt.

Durch diese Integration werden alle vorhandenen offenen oder geschlossenen Probleme für den Zielartikel angezeigt. Falls vorhanden, lesen Sie diese durch, bevor Sie ein neues Problem erstellen. Wenn Sie ein ähnliches Problem finden, klicken Sie auf das Symbol mit dem Gesicht, um eine Reaktion hinzuzufügen. Alternativ können Sie es erweitern, um einen Kommentar hinzuzufügen.

#### <a name="types-of-feedback"></a>Arten von Feedback

Verwenden Sie GitHub-Probleme, um folgende Arten von Feedback zu senden:

- Fehler in der Dokumentation: Der Inhalt ist nicht mehr aktuell, unklar, verwirrend oder fehlerhaft.
- Verbesserung der Dokumentation: Ein Vorschlag, um den Artikel zu verbessern.
- Fragen zur Dokumentation: Sie benötigen Hilfe, um eine vorhandene Dokumentation zu finden.
- Ideen zur Dokumentation: Ein Vorschlag für einen neuen Artikel. Verwenden Sie diese Methode statt UserVoice, um Feedback zur Dokumentation zu senden.
- Lob: Positives Feedback zu einem hilfreichen oder informativen Artikel.
- Lokalisierung: Feedback zur Übersetzung des Inhalts.
- Suchmaschinenoptimierung (Search Engine Optimization, SEO): Feedback zu Problemen bei der Suche nach Inhalten. Fügen Sie die Suchmaschine, die Schlüsselwörter und den Zielartikel in den Kommentaren ein.

Wenn Sie ein Issue erstellen, das nicht auf die Themen der Dokumentation bezogen ist, wird es von Microsoft geschlossen. Beispiel:

- [Produktfeedback](find-help.md#product-feedback)
- [Produktfragen](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [Supportanfragen](https://aka.ms/cmcbsupport)

Weitere Informationen zum Senden von allgemeinem Feedback zur docs.microsoft.com-Plattform finden Sie unter [Feedback zur Dokumentation](https://aka.ms/sitefeedback). Diese Plattform umfasst alle Wrapperkomponenten wie den Header, das Inhaltsverzeichnis und das Menü auf der rechten Seite. Es ist ebenfalls enthalten, wie Artikel im Browser gerendert werden, also z.B. die Schriftart, Warnungen und die Textmarken der Seite.

## <a name="notifications"></a><a name="bkmk_notifications"></a> Benachrichtigungen

Verwenden Sie folgende Schritte, um Benachrichtigungen zu enthalten, wenn Inhalte in der Dokumentationsbibliothek geändert werden:

1. Verwenden Sie die [Suche](https://docs.microsoft.com/search/index?scope=ConfigMgr) der Dokumentationsbibliothek, um einen oder mehrere Artikel zu finden. Beispiel:

    - Suchen Sie mithilfe des Titels nach einem einzelnen Artikel: [„Log files for troubleshooting – Configuration Manager“](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr) (Protokolldateien zur Behebung von Problemen (Configuration Manager)).

    - Suchen Sie nach einem Artikel zu [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr).

2. Klicken Sie in der oberen rechten Ecke auf den Link **RSS**.

3. Verwenden Sie diesen Feed in RSS-Anwendungen, um Benachrichtigungen zu erhalten, wenn es Änderungen an den Suchergebnissen gibt.

> [!TIP]
> Sie können ebenfalls das Repository [SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs) auf GitHub **verfolgen**. Diese Methode generiert viele Benachrichtigungen. Darüber hinaus sind keine Änderungen von privaten Repositorys enthalten, die von Microsoft verwendet werden.

## <a name="contribute"></a><a name="bkmk_contribute"></a> Mitwirken

Die Configuration Manager-Dokumentationsbibliothek ist wie die meisten Inhalte unter docs.microsoft.com auf GitHub als Open Source vorhanden. Für diese Bibliothek werden Beiträge aus der Community akzeptiert und gefördert. Weitere Informationen zu den ersten Schritten finden Sie unter [Contributor Guide (Leitfaden für Mitwirkende)](https://docs.microsoft.com/contribute). Als einzige Voraussetzung müssen Sie ein [GitHub-Konto erstellen](https://github.com/join).

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>Grundlegende Schritte zum Mitwirken an SCCMdocs

1. Klicken Sie im Zielartikel auf **Bearbeiten**. Dadurch wird die Quelldatei in GitHub geöffnet.

2. Klicken Sie auf das Stiftsymbol, um die Quelldatei zu bearbeiten.

3. Nehmen Sie Änderungen in der Markdownquelle vor. Weitere Informationen finden Sie unter [How to use Markdown for writing Docs (Verwenden von Markdown für das Schreiben von Dokumentationen)](https://docs.microsoft.com/contribute/markdown-reference).

4. Geben Sie im Abschnitt „Propose file change“ (Änderung an der Datei vorschlagen) den öffentlichen Kommentar für den Commit ein, in dem Sie beschreiben, *was* Sie geändert haben. Klicken Sie dann auf **Propose file change** (Änderung an Datei vorschlagen).

5. Scrollen Sie nach unten, und überprüfen Sie Ihre Änderungen. Klicken Sie auf **Pull Request erstellen**, um das Formular zu öffnen. Beschreiben Sie, *warum* Sie diese Änderung vornehmen. Markieren Sie den Autor des Artikels, und fordern Sie an, dass dieser die Änderung überprüft. Klicken Sie auf **Pull Request erstellen**.

### <a name="what-to-contribute"></a>Was Sie beitragen können

Wenn Sie etwas beitragen möchten, jedoch nicht wissen, wo Sie anfangen sollen, finden Sie unten Vorschläge:

- Durchsuchen Sie die Liste der Probleme nach diesen communityeigenen Bezeichnungen:

  - [good-first-issue](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [help-wanted](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Microsoft-Autoren weisen diese Bezeichnungen den Problemen zu, die gut für die Beteiligung der Community geeignet sind.

- Überprüfen Sie einen Artikel nach Genauigkeit. Aktualisieren Sie die Metadaten **ms.date** mithilfe des Formats `mm/dd/yyyy`. Dieser Beitrag hilft dabei, den Inhalt aktuell zu halten.

- Fügen Sie je nach Ihrer Erfahrung Klarstellungen, Beispiele oder Anleitung hinzu. Dadurch wird die Erfahrung der Community genutzt, um Wissen zu verbreiten.

- Korrigieren Sie Übersetzungen in anderen Sprachen als Englisch. Dadurch wird die Verwendbarkeit von lokalisierten Inhalten verbessert.

> [!NOTE]
> Um umfangreiche Beiträge zu verfassen, müssen Sie zunächst der Lizenzvereinbarung für Mitwirkende (CLA) zustimmen, sofern Sie kein Microsoft-Mitarbeiter sind. GitHub fordert Sie automatisch auf, diese Vereinbarung zu akzeptieren, sobald ein Beitrag die vorgegebene Länge erreicht.

### <a name="tips"></a>Tipps

Befolgen Sie diese allgemeinen Richtlinien, wenn Sie zur Configuration Manager-Dokumentation beitragen möchten:

- Vermeiden Sie lange Pull Requests. [Melden Sie stattdessen ein Problem](#bkmk_docfeedback), und starten Sie eine Diskussion. Dann können wir uns auf eine Vorgehensweise einigen, bevor Sie zu viel Zeit investieren.

- Lesen Sie den [Microsoft-Styleguide](https://aka.ms/MicrosoftStyle). Berücksichtigen Sie die [10 Grundprinzipien der optimalen Textgestaltung für Microsoft](https://docs.microsoft.com/style-guide/top-10-tips-style-voice).

- Verwenden Sie die [Pull Request-Vorlage](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md) als Ausgangspunkt Ihres Beitrags.

- Befolgen Sie den [GitHub Flow-Workflow](https://guides.github.com/introduction/flow/).

- Verfassen Sie regelmäßig Blogs, Tweets oder andere Features über Ihre Beiträge.

(Diese Liste wurde dem [.NET-Leitfaden für Mitwirkende](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts) entlehnt.)

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Konsolidierung der Dokumentation für Microsoft Endpoint Manager

Zur besseren Unterstützung kombinierter Szenarien für Intune und Configuration Manager sind deren Dokumentationsbibliotheken auf der [Microsoft Endpoint Manager-Website](https://docs.microsoft.com/mem) konsolidiert. Die Intune-Dokumentation befindet sich jetzt unter [docs.microsoft.com/mem/intune](https://docs.microsoft.com/mem/intune), während sich die Dokumentation zu Configuration Manager jetzt unter [docs.microsoft.com/mem/configmgr](https://docs.microsoft.com/mem/configmgr) befindet. Wenn Sie weiterhin eine veraltete URL verwenden, werden Sie automatisch umgeleitet, sodass Sie keine Änderungen zum Lesen dieses Inhalts vornehmen müssen.

Wenn Sie Feedback geben oder an Artikeln mitwirken, sind einige Änderungen erforderlich:

- Vorhandene GitHub-Issues verbleiben im ursprünglichen Repository ([IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) oder [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues)).

  - Diese Issues werden nicht als offene oder geschlossene Issues im Abschnitt „Feedback“ des verknüpften Artikels angezeigt.

  - Wir arbeiten weiterhin daran, diese Issues zu beheben.

  - In einigen Fällen muss ggf. die schwierige Entscheidung getroffen werden, ein Issue zu schließen, das unserer Meinung nach nicht behoben werden kann.

  - Senden Sie Feedback zum migrierten Artikel im [MEMDocs-Repository](https://github.com/MicrosoftDocs/MEMDocs), wenn Sie ein Issue im vorhandenen Repository haben und eine Lösung dafür finden möchten.

- Wenn Sie jetzt Feedback senden oder einen Artikel bearbeiten, wird das Issue oder der Pull Request im MEMDocs-Repository angezeigt.
