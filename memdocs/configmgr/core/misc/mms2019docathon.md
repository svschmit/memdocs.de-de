---
title: MMS 2019-Docathon
ms.date: 05/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
description: Informationen und Regeln für MMS 2019-Docathon
ms.assetid: 8fe2ecfc-f5c1-4fa6-8703-245339400723
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 91430688fd2af93e5d5b5ce7eb0cbc6358388ea4
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607836"
---
# <a name="mms-2019-docathon"></a>MMS 2019-Docathon

Während der Midwest Management Summit 2019 (MMS 2019) veranstaltet das Microsoft-Team für die Configuration Manager- und Microsoft Intune-Inhalte einen Docathon. Wenn Sie am 6. Mai am [praktischen Lab für docs.microsoft.com](https://sched.co/N6fd) teilnehmen, haben Sie die Gelegenheit, sich von Microsoft-Autoren bei Ihren Beiträgen unterstützen zu lassen. Der Docathon läuft während der gesamten Konferenz, und alle registrierten Teilnehmer der MMS 2019 können teilnehmen.

Sie fragen sich, warum Sie teilnehmen sollten? Bei docs.microsoft.com handelt es sich um eine Open-Source-Plattform für Microsoft-Produkte, die von GitHub unterstützt wird. Microsoft schätzt jeden Beitrag zur Dokumentation! Wenn Sie Beiträge erstellen, werden Sie auf der Plattform in der Liste der Mitwirkenden für die jeweiligen Artikel aufgeführt. Folgende Beiträge zur Dokumentation können von der Community geleistet werden:

- Korrektur von Tippfehlern
- Erläuterungen
- Beispiele
- Praxisanweisungen und Tipps
- Überprüfung des Inhalts, Aktualität

## <a name="set-up"></a>Einrichten

Wenn Sie mitwirken möchten, müssen Sie vorher diese Schritte durchführen.

### <a name="github-account"></a>GitHub-Konto

Erstellen Sie ein [GitHub-Konto](https://github.com/join).

- Ermitteln Sie alle Zuordnungen in Ihrem Profil.  

- Aktivieren Sie die zweistufige Authentifizierung.  

#### <a name="additional-considerations"></a>Weitere Überlegungen

- Überprüfen Sie die Richtlinien Ihres Unternehmens zu Open-Source-Beiträgen.  

    > [!Note]  
    > Für größere Open-Source-Beiträge müssen Sie die [Microsoft-CLA (Lizenzvereinbarung für Mitwirkende)](https://cla.opensource.microsoft.com/) akzeptieren. Lesen Sie sich diese Vereinbarung zuvor genau durch.  

- Beiträge zu docs.microsoft.com werden für den Microsoft MVP Award angerechnet.  

- Für Microsoft-Mitarbeiter umfasst die Einrichtung zusätzliche einmalige Schritte, und der Prozess für das Mitwirken unterscheidet sich geringfügig.  

Weitere Informationen finden Sie im Leitfaden für Mitwirkende an docs.microsoft.com unter [Einrichten eines GitHub-Kontos](/contribute/get-started-setup-github).

## <a name="scope"></a>`Scope`

Für dieses Event werden nur die folgenden GitHub-Repositorys berücksichtigt:

- [Intune-Dokumentation](https://github.com/MicrosoftDocs/IntuneDocs)
- [SCCM-Dokumentation](https://github.com/MicrosoftDocs/SCCMdocs)
- [sccm-docs-powershell-ref](https://github.com/MicrosoftDocs/sccm-docs-powershell-ref)

Sie können auch andere Inhalte auf docs.microsoft.com bearbeiten, diese Änderungen werden jedoch nicht für das Event angerechnet.

## <a name="learn-the-process"></a>Informieren Sie sich über die Vorgehensweise

Lesen Sie Informationen zum [Erstellen von Issues](../understand/use-docs.md#bkmk_docfeedback) und zum [Mitwirken](../understand/use-docs.md#bkmk_contribute). Die meisten grundlegenden Änderungen können über GitHub im Browser vorgenommen werden.  

> [!Note]  
> Wenn Sie den komplexeren Workflow mit git und Visual Studio Code testen möchten, finden Sie weitere Informationen unter [Installieren von Tools für die Inhaltsentwicklung](/contribute/get-started-setup-tools). Sie können sich auch an Aaron oder Erik wenden, wenn Sie Hilfe benötigen. Folgendes spricht für den komplexeren Workflow:
>
> - Das Erstellen neuer Artikel
> - Hinzufügen von Bildern
> - Das Suchen und Ersetzen von Zeichenfolgen (einschließlich reguläre Ausdrücke)
> - Die Möglichkeit, umfassendere und komplexere Änderungen vorzunehmen  

## <a name="determine-your-goals"></a>Setzen Sie sich Ziele

Setzen Sie sich Ziele für dieses Event, und überlegen Sie sich, wie Sie diese erreichen können. Was möchten Sie erreichen?

- Sehen Sie vorhandene Issues in den relevanten Repositorys durch. Bezeichnungen wie **good-first-issue** oder **help-wanted** können dabei gute Ausgangspunkte darstellen. Wenn Sie sich einem dieser Issues annehmen möchten, kommentieren Sie diesen mit **#MMS2019Docathon**, und verwenden Sie das Tag @author, damit der Autor Ihnen das Issue zuweist. In anderen Worten: [Erheben Sie Anspruch](https://www.merriam-webster.com/words-at-play/word-origin-dibs) darauf. Wiederholen Sie diesen Vorgang so oft Sie möchten.  
    Schreiben Sie beispielsweise in der SCCM-Dokumentation Folgendes, wenn Aaron der Autor des Artikels ist: `@aczechowski I'm claiming this issue for #MMS2019Docathon`

- Sie wissen, dass in einem Artikel ein Problem vorliegt, aber es wurde noch kein Feedback eingereicht. Der Abschnitt **Feedback** im unteren Bereich des Artikels ist also leer. Erstellen Sie ein neues Issue, und befolgen Sie dieselben Anweisungen wie oben beschrieben, um Anspruch zu erheben.  

    - Fügen Sie beispielsweise ein Codebeispiel, ein Praxisbeispiel oder einen allgemeinen Tipp hinzu.  

    - Nehmen Sie keine Änderungen an Grammatik oder Stil vor, ohne sich zuvor mit Aaron oder Erik abzusprechen.  

    - Das Datum des gewählten Artikels liegt über 90 Tage zurück, also vor dem 6. Februar 2019. Sie können diesen überprüfen und dann die Metadateneigenschaft **ms.date** bearbeiten. Dieser Beitrag bedeutet dann: „Ich habe diesen Artikel überprüft. Er ist weiterhin inhaltlich korrekt. Bitte aktualisieren Sie das Datum.“ Eröffnen Sie ein Issue, um Anspruch zu erheben.  

    - Überprüfen Sie zunächst, ob es schon Feedback zum Artikel gibt, um sicherzugehen, dass es nicht bereits ein offenes Issue gibt und das Problem von einem anderen Benutzer beansprucht wurde. Aus technischer Sicht ist diese Aktion nicht erforderlich. Wenn Sie das Feedback nicht überprüfen und ein anderer Benutzer zuerst ein Issue erstellt, werten wir nur den ersten Beitrag.  

- Die einstündige Sitzung zur Mittagspause am Montag ist dafür gedacht, auf diese Ziele hinzuarbeiten. Aaron und Erik sind anwesend, um Fragen zu beantworten oder bei Problemen zu helfen.

## <a name="contest-summary"></a>Zusammenfassung des Wettbewerbs

Der Wettbewerb läuft in der gesamten Woche vom 6. bis 9. Mai. Alle registrierten Teilnehmer der MMS 2019 können teilnehmen. Übermitteln Sie Ihre Beiträge bis Donnerstag, 9. Mai 2019, 15:00 CT. Die Preise werden am Donnerstag, den 9. Mai, nach der Sitzung [ConfigMgr Product Team Q&A](https://sched.co/N6ge) vergeben. Sie müssen an der MMS 2019 teilnehmen, um als Sieger in Frage zu kommen, aber nicht an dieser Sitzung teilnehmen. Wenn Sie nicht bei der Sitzung anwesend sind, kontaktieren Sie Aaron, bevor er am Freitagmorgen abreist, um Ihren Preis entgegenzunehmen.

> [!Important]  
> Sie müssen das Hashtag **#MMS2019Docathon** in allen Beiträgen verwenden, damit diese angerechnet werden.

### <a name="award-categories"></a>Auszeichnungskategorien

#### <a name="grand-prize"></a>Hauptpreis

- **Bedeutendster Beitrag:** Dieser wird anhand der folgenden Kriterien ermittelt. Die Beurteilung erfolgt durch Aaron und Erik. Wenn Sie der Meinung sind, dass Ihr Beitrag qualifiziert ist, überzeugen Sie uns in einem Pull Request davon.

    - Nutzen für die Community (50 %)
    - Einhaltung des Microsoft-Stils (25 %)
    - Richtiges Markdown (25 %)  

Der Sieger des Hauptpreises erhält Folgendes:

- Einen Registrierungspass für die [MMS Jazz Edition](https://mmsmoa.com/sessions/jazz-edition.html). Dieser wird vom Lenkungsausschuss der MMS 2019 gestellt und entspricht einem Wert von 1799 USD.
- Einen Yeti Rambler-Becher mit fast 900 ml Fassungsvermögen und Markenkennzeichen
- Eine Popsocket-Smartphonehalterung für das Auto mit Markenkennzeichen

#### <a name="first-place-prizes"></a>Preise für Erstplatzierte

Folgende Auszeichnungen werden anhand der Anzahl der zulässigen Beiträge zu den relevanten Repositorys vergeben. Diese müssen nicht gemergt oder veröffentlicht werden, sondern nur bis zum Ende der Konferenz als Pull Request übermittelt werden. Wir behalten uns das Recht vor, Personen zu disqualifizieren, die das System manipulieren. Der Sieger jeder Kategorie erhält einen Yeti Rambler-Becher mit fast 900 ml Fassungsvermögen und eine Popsocket-Smartphonehalterung für das Auto (jeweils mit Markenkennzeichen). Pro Kategorie gibt es nur einen Sieger.

- **Meiste übermittelte Commits**

- **Meiste geänderte Zeilen**

- **Meiste bearbeitete Artikel**

> [!Note]  
> Es wird keine Auszeichnung für die meisten erstellten Issues vergeben. Feedback ist zwar nützlich, aber für das Event werden nur Beiträge berücksichtigt.

## <a name="resources"></a>Ressourcen

- [Microsoft-Stil](https://aka.ms/MicrosoftStyle)

    - [Schnellstart](/contribute/style-quick-start)

    - [Top 10 tips for Microsoft style and voice (10 Grundprinzipien der optimalen Textgestaltung für Microsoft)](/style-guide/top-10-tips-style-voice)

- [Handbuch für Mitwirkende](/contribute)

- [Verwenden von Markdown für das Schreiben von Dokumentationsartikeln](/contribute/markdown-reference)

## <a name="official-rules"></a>Offizielle Regeln

Offizielle Regeln für den Microsoft Cloud + AI Developer Relations Content & Learning MMS 2019 Docathon Event Contest

1. SPONSOR

    Diese offiziellen Regeln („Regeln“) gelten für den Microsoft Cloud + AI Developer Relations Content & Learning MMS 2019 Docathon Event Contest („Wettbewerb“). Die Microsoft Corporation ist der Sponsor („Sponsor“).

2. DEFINITIONEN

    Innerhalb dieser Regeln sind „Microsoft“, „wir“, „unser“ und „uns“ auf den Sponsor bezogen. „Sie“ und „sich“ beziehen sich auf den Teilnehmer eines Wettbewerbs. „Event“ bezieht sich auf das auf der MMS 2019 in Minneapolis (Minnesota) ausgetragene Docathon-Event. Mit der Teilnahme verpflichten Sie sich zur Einhaltung dieser Regeln.

3. BEITRAGSZEITRAUM

    Der Wettbewerb wird vom 6. Mai 2019 bis 9. Mai 2019 während der regulären Zeiten des Events ausgetragen („Beitragszeitraum“).

4. TEILNAHMEBERECHTIGUNG

    Zur Teilnahme sind alle registrierten Teilnehmer des Events berechtigt, die mindestens 18 Jahre alt sind und deren rechtmäßiger Wohnsitz in einem der 50 US-Bundesstaaten liegt (einschließlich District of Columbia). Mitarbeiter und Vorstandsmitglieder der Microsoft Corporation sowie Tochtergesellschaften, Personen, die an der Umsetzung oder Verwaltung dieser Aktion beteiligt sind sowie die Familienmitglieder der zuvor aufgeführten Personengruppen (Familienangehörige, direkte Familienmitglieder und Personen, die in deren Haushalt leben), sind von der Teilnahme ausgeschlossen. Diese Regelung ist dann ungültig, wenn sie gegen geltendes Gesetz verstößt.

    Für Unternehmens- und Messeevents: Wenn Sie in Ihrer Funktion als Mitarbeiter an einem Event teilnehmen, sind ausschließlich Sie dafür verantwortlich, die Schenkungsregeln Ihres Arbeitgebers einzuhalten. Microsoft tritt bei einem Rechtsstreit oder Klagen in dieser Angelegenheit nicht als Partei auf. BEHÖRDENMITARBEITER, EINSCHLIESSLICH LEHRKRÄFTE: Microsoft verpflichtet sich der Einhaltung der ethischen Grundsätze und Schenkungsregeln von Behörden. Deshalb sind Behördenmitarbeiter und Mitarbeiter des öffentlichen Diensts von der Teilnahme an dieser Aktion ausgeschlossen.

5. TEILNAHME

    Sie können einen Beitrag einreichen, indem Sie Artikel in den folgenden GitHub-Repositorys bearbeiten: Intune-Dokumentation, SCCM-Dokumentation und sccm-docs-powershell-ref. Weitere Informationen zur Vorgehensweise finden Sie unter [Mitwirken](/sccm/core/understand/use-docs#bkmk_contribute).

    Übermitteln Sie einen Pull Request auf GitHub, um einen Beitrag einzureichen.

    Sie können beliebig viele Beiträge einreichen. Pro Kategorie und pro Person wird nur ein Preis vergeben.

    Wir sind nicht für überschüssige, verloren gegangene, verspätete, beschädigte oder unvollständige Beiträge verantwortlich. Im Streitfall werden Beiträge dem autorisierten Besitzer des GitHub-Kontos zugerechnet.

6. ZULÄSSIGE BEITRÄGE

    Ein Beitrag muss die folgenden inhaltlichen und technischen Anforderungen erfüllen, um als zulässig zu gelten:

    - Ihr Beitrag muss eine Originalarbeit von Ihnen sein, und
    - Ihr Beitrag darf nicht als Siegerbeitrag in einem anderen Wettbewerb ausgewählt worden sein, und
    - Sie müssen die erforderliche Zustimmung, Genehmigung und Lizenz für die Einreichung Ihres Beitrags nachweisen können, und
    - Sofern für Ihren Beitrag von Benutzern generierte Inhalte wie Software, Fotos, Videos, Musik, Grafiken oder Essays verwendet werden müssen, gewährleistet der Teilnehmer, dass es sich bei seinem Beitrag um seine Originalarbeit handelt, die nicht von Dritten ohne Zustimmung oder erkennbare Berechtigung kopiert wurde, und dass keine Datenschutzbestimmungen, Rechte an geistigem Eigentum oder andere Rechte einer Person oder Entität verletzt wurden. Sie können Microsoft-Marken, -Logos und -Designs verwenden, für die Microsoft Ihnen eine eingeschränkte Lizenz erteilt. Diese gilt ausschließlich für die Nutzung zur Einreichung von Beiträgen für diesen Wettbewerb, und
    - Ihr Beitrag darf KEINE Inhalte aufweisen, die nach unserem alleinigen Ermessen als obszön oder anstößig, gewalttätig, verleumderisch, abschätzig oder illegal wahrgenommen werden können, oder die Alkohol, illegale Drogen, Tabak oder ein politisches Programm bewerben, dessen Botschaften sich negativ auf den Geschäftswert von Microsoft auswirken können.

7. NUTZUNG DER BEITRÄGE

    Wir erheben keine Besitzansprüche auf Ihre Beiträge. Wenn Sie einen Beitrag einreichen, gewähren Sie uns jedoch die unwiderrufliche, lizenzgebührenfreie und weltweite Berechtigung, Ihren Beitrag und dessen mit dem Wettbewerb in Zusammenhang stehenden Inhalte zu verwenden, überprüfen, bewerten, testen oder anderweitig zu analysieren und in zum Zeitpunkt des Wettbewerbs bekannten oder nach dem Wettbewerb neu aufkommenden Medien zu kommerziellen oder nicht kommerziellen Zwecken (einschließlich, aber nicht beschränkt auf Marketing, Vertrieb von oder Werbung für Microsoft-Produkte) zu verwenden, ohne dass weitere Berechtigung von Ihnen eingeholt werden müssen. Sie erhalten keine Vergütung oder Gutschriften für die Nutzung Ihres Beitrags, die über die in diesen offiziellen Regeln genannten Preise hinausgehen.

    Mit der Teilnahme am Wettbewerb nehmen Sie zur Kenntnis, dass wir Materialien entwickelt oder in Auftrag gegeben haben, die Ihrem Beitrag ähnlich oder identisch mit diesem sind, und Sie bestätigen, dass Sie auf alle Ansprüche verzichten, die aus Ähnlichkeiten zu Ihrem Beitrag resultieren könnten. Weiterhin nehmen Sie zur Kenntnis, dass wir die Arbeitsvorgaben von Vertretern, die Zugriff auf Ihren Beitrag hatten, nicht einschränken werden. Sie stimmen weiterhin zu, dass durch die Nutzung der Informationen durch das ungestützte Gedächtnis unserer Vertreter für die Entwicklung oder Bereitstellung unserer Produkte oder Dienste keine Haftung im Rahmen dieser Vereinbarung oder des Urheberrechts- oder Geschäftsgeheimnisgesetzes für uns entsteht.

    Ihr Beitrag kann auf einer öffentlichen Website veröffentlicht werden. Wir sind nicht für die unbefugte Nutzung Ihres Beitrags durch die Besucher der Website verantwortlich. Wir sind nicht verpflichtet, Ihren Beitrag zu verwenden, auch wenn dieser als Siegerbeitrag ausgewählt wurde.

8. AUSWAHL UND BENACHRICHTIGUNG DER SIEGER

    Sofern die Zulässigkeit der Teilnahme und der Beiträge bestätigt wurde, werden die potenziellen Sieger von Microsoft, einem Vertreter oder einer qualifizierten Jury aus allen eingegangenen zulässigen Beiträgen anhand der folgenden Bewertungskriterien ausgewählt:

    - Hauptpreis: Bedeutendster Beitrag –folgende Kriterien zählen:
        - 50 %: Nutzen für die Community
        - 25 %: Einhaltung des Microsoft-Stils
        - 25 %: Richtiges Markdown
    - Folgende Preise für die Erstplatzierten werden anhand der Anzahl der zulässigen Beiträge zu den relevanten Repositorys vergeben. Diese müssen nicht gemergt oder veröffentlicht werden, sondern nur bis zum Ende der Konferenz als Pull Request übermittelt werden. Wir behalten uns das Recht vor, Personen zu disqualifizieren, die das System manipulieren.
        - Meiste übermittelte Commits
        - Meiste geänderte Zeilen
        - Meiste bearbeitete Artikel

    Die Sieger werden am Donnerstag, den 9. Mai 2019, nach 15 Uhr (Central Time) ausgewählt.

    Die Sieger werden während des Events benachrichtigt und müssen ihren Preis vor dem Ende des Events beanspruchen.

    Bei einem Gleichstand zwischen zwei Beiträgen fällt ein zusätzlicher Juror die Entscheidung anhand der oben beschrieben Bewertungskriterien. Die Entscheidung der Jury ist endgültig und bindend. Wenn keine ausreichende Anzahl von Beiträgen eingereicht wird, die den Anforderungen entsprechen, liegt es in unserem Ermessen, weniger Sieger als die Anzahl der im Folgenden aufgeführten Preise für den Wettbewerb auszuwählen.

    Die Sieger werden über die Kontaktinformationen benachrichtigt, die Sie beim Antreten des Wettbewerbs angegeben haben, und können dazu verpflichtet werden, ein Antrags- und Steuerformular auszufüllen („Formulare“). Sofern ein ausgewählter Sieger nicht kontaktiert werden kann, nicht qualifiziert ist, seinen Preis nicht in Anspruch nimmt oder die notwendigen Formulare nicht einreicht, verfällt dessen Anspruch auf den Preis, und ein anderer Sieger wird zeitnah ausgewählt. Es werden nur drei alternative Sieger ausgewählt. Falls diese den Preis nicht beanspruchen, wird der entsprechende Preis nicht vergeben.  

9. PREISE

    Folgende Preise werden vergeben:

    - Ein (1) Hauptpreis. Ein Preispaket enthält Folgendes:
        - Einen Registrierungspass für [MMS Jazz Edition](https://mmsmoa.com/sessions/jazz-edition.html) (vom Lenkungsausschuss der MMS 2019 gestellt), dessen ungefährer Verkaufswert bei 1799 USD liegt.
        - Einen Yeti Rambler-Becher mit fast 900 ml Fassungsvermögen dessen ungefährer Verkaufswert bei 35.00 USD liegt.
        - Eine Popsocket-Smartphonehalterung für das Auto, dessen ungefährer Verkaufswert bei 15.00 USD liegt.

        Der ungefähre Verkaufswert dieses Pakets beträgt 1849 USD.

    - Drei (3) Preise für Erstplatzierte. Ein Preispaket enthält Folgendes:
        - Einen Yeti Rambler-Becher mit fast 900 ml Fassungsvermögen dessen ungefährer Verkaufswert bei 35.00 USD liegt.
        - Eine Popsocket-Smartphonehalterung für das Auto, dessen ungefährer Verkaufswert bei 15.00 USD liegt.

        Der ungefähre Verkaufswert dieses Pakets beträgt 50 USD.

    Der ungefähre Verkaufswert aller Preise beträgt 1999 USD.

    Pro Person wird nur ein (1) Preis vergeben. Es werden nur die aufgeführten Preise vergeben. Die Ersetzung, Übertragung oder Abtretung des Preises ist nicht zulässig. Microsoft behält sich jedoch das Recht vor, einen Preis durch einen gleich- oder höherwertigen Preis zu ersetzen, falls der angebotene Preis nicht verfügbar ist. Die Preise werden im vorliegenden Zustand ohne ausdrückliche oder konkludente Gewährleistung – einschließlich, aber nicht beschränkt auf konkludente Gewährleistungen oder Verkäuflichkeit, Eignung für bestimmte Zwecke oder Nichtverletzung – überreicht. Die Sieger müssen gegebenenfalls innerhalb der in der Siegerbenachrichtigung genannten Frist Antrags- und/oder Steuerformulare („Formulare“) ausfüllen und zurückgeben. Für eventuell auf den Preis anfallende Steuern trägt der Sieger die alleinige Verantwortung. Diesem wird zudem empfohlen, eine unabhängige Beratung hinsichtlich der Steuerfolgen aufzusuchen, die infolge der Annahme des Preises entstehen können. Durch die Annahme eines Preises stimmen Sie zu, dass Microsoft Ihren Beitrag, Namen, ihr Bild und ihren Wohnort in Zusammenhang mit diesem Wettbewerb in Onlinemedien, Printmedien oder sonstigen Medien im Rahmen des geltenden Rechts verwenden darf, ohne dass ein Anspruch auf Bezahlung oder Vergütung besteht.

10. WAHRSCHEINLICHKEITEN

    Die Wahrscheinlichkeit auf einen Sieg basiert auf der Anzahl und der Qualität der eingegangenen zulässigen Beiträge.

11. ALLGEMEINE BEDINGUNGEN UND HAFTUNGSFREISTELLUNG

    Im Rahmen des geltenden Rechts stimmen Sie mit der Teilnahme am Wettbewerb zu, Microsoft und die jeweiligen Muttergesellschaften, Partner, Tochtergesellschaften, Mitarbeiter und Vertreter von jeglicher Haftung und jeglichen Schäden, Verlusten oder Beschädigungen freizustellen und schadlos zu halten, die in Verbindung mit diesem Wettbewerb oder einem gewonnenen Preis entstehen.

    Es gelten sämtliche lokalen Gesetze. Die Entscheidung von Microsoft ist endgültig und bindend.

    Wir behalten uns das Recht vor, diesen Wettbewerb aus beliebigen Gründen – einschließlich Betrug, technische Fehler, Katastrophen, Kriege oder andere unvorhersehbare oder unerwartete Ereignisse – abzubrechen, zu verändern oder auszusetzen. Falls die Integrität des Wettbewerbs nicht wiederhergestellt werden kann, behalten wir uns vor, Sieger aus allen eingegangenen zulässigen Beiträgen auszuwählen, bevor der Wettbewerb abgebrochen, verändert oder ausgesetzt wird. Teilnehmer, die gegen die Regeln verstoßen, werden im vollen Umfang des Gesetzes strafrechtlich verfolgt und können von der Teilnahme an Microsoft-Wettbewerben ausgeschlossen werden.

12. SIEGERLISTE

    Die Liste der Sieger wird innerhalb von 30 Tagen (ab dem 9. Mai 2019) auf https://aka.ms/mms2019docathon veröffentlicht.

13. DATENSCHUTZ

    Microsoft verpflichtet sich, Ihre Privatsphäre zu schützen. Microsoft verwendet die auf diesem Formular angegebenen Daten, um Ihnen wichtige Informationen zu unseren Produkten, Upgrades und Verbesserungen sowie Informationen zu anderen Microsoft-Produkten und -Diensten zukommen zu lassen. Microsoft gibt diese Daten nicht ohne Ihre Zustimmung an Drittanbieter weiter, sofern dies nicht notwendig ist, um die von Ihnen angeforderten Dienste oder Transaktionen abzuschließen, oder es vom Gesetz erforderlich ist. Microsoft sorgt für die Sicherheit Ihrer persönlichen Daten. Wir verwenden eine Vielzahl von Sicherheitstechnologien und -verfahren, um Ihre persönlichen Daten vor nicht autorisiertem Zugriff, Gebrauch oder Veröffentlichung zu schützen. Ihre personenbezogenen Informationen werden ohne Ihre Zustimmung nur außerhalb des Unternehmens weitergegeben, wenn die oben genannten Bedingungen zutreffen.

    Wenn Sie der Meinung sind, dass Microsoft die Datenschutzrichtlinie verletzt hat, kontaktieren Sie uns, indem Sie eine E-Mail an privrc@microsoft.com oder einen Brief an die Adresse „Microsoft Privacy Response Center, Microsoft Corporation, One Microsoft Way, Redmond, WA 98052“ senden.