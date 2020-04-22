---
title: Verwalten von Windows as a Service
titleSuffix: Configuration Manager
description: Lassen Sie sich mit Configuration Manager den Status von Windows as a Service (WaaS) anzeigen, erstellen Sie Wartungspläne, um Bereitstellungsringe zu bilden, und lassen Sie sich Warnungen anzeigen, wenn Windows 10-Clients das Ende des Supports erreichen.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690328"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>Verwalten von Windows als Dienst mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In Configuration Manager können Sie nun den Zustand von Windows as a Service (WaaS) in Ihrer Umgebung anzeigen. Erstellen Sie Wartungspläne, um Bereitstellungsringe zu bilden und sicherzustellen, dass Windows 10-Systeme auf dem neuesten Stand gehalten werden, wenn neue Builds veröffentlicht werden. Sie können auch Warnungen anzeigen, wenn der Support für den halbjährlichen Kanalbuild für Windows 10-Clients sich dem Ende nähert.

Weitere Informationen zu Windows 10-Wartungsoptionen finden Sie unter [Übersicht über Windows as a Service](/windows/deployment/update/waas-overview#servicing-channels).

Gehen Sie wie in den folgenden Abschnitten beschrieben vor, um Windows als Dienst zu verwalten.

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a> Voraussetzungen

Um Daten im Windows 10-Wartungsdashboard anzuzeigen, führen Sie die folgenden Aktionen aus:

- Auf Windows 10-Computern müssen Configuration Manager-Softwareupdates mit Windows Server Update Services (WSUS) für die Verwaltung von Softwareupdates verwendet werden. Wenn auf Computern Windows Update for Business (oder Windows Insider) für die Verwaltung von Softwareupdates verwendet wird, erfolgt in Windows 10-Wartungsplänen keine Auswertung des Computers. Weitere Informationen finden Sie unter [Integration mit Windows Update für Unternehmen in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).

- Verwendung einer unterstützten WSUS-Version:
  - WSUS 10.0.14393 (Rolle in Windows Server 2016)
  - WSUS 10.0.17763 (Rolle in Windows Server 2019) (erfordert Configuration Manager 1810 oder höher)
  - WSUS 6.2 und 6.3 (Rolle in Windows Server 2012 und Windows Server 2012 R2)
    - Bei WSUS 6.2 und 6.3 [müssen KB 3095113 und KB 3159706 (oder ein vergleichbares Update) installiert sein](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012).

- Aktivieren Sie die Frequenzermittlung. Die im Windows 10-Wartungsdashboard angezeigten Daten werden mithilfe der Ermittlung gesammelt. Weitere Informationen finden Sie unter [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).

    Die folgenden Kanal- und Buildinformationen zu Windows 10 werden ermittelt und in den folgenden Attributen gespeichert:  

    - **Bereitstellungsoption für Betriebssystem**: Gibt den Betriebssystemkanal an. Beispielsweise **0** = Halbjährlicher Kanal - Ziel (Updates nicht verzögern), **1** = Halbjährlicher Kanal (Updates verzögern), **2** = Long-Term Servicing Channel (LTSC)

    - **Betriebssystembuild**: Gibt den Betriebssystembuild an Beispiel: **10.0.10240** (RTM) oder **10.0.10586** (Version 1511)

- Der Dienstverbindungspunkt muss installiert und für den Modus **Online, dauerhafte Verbindung** konfiguriert werden, um Daten im Windows 10-Wartungsdashboard anzuzeigen. Wenn Sie im Offlinemodus arbeiten, werden Datenaktualisierungen erst dann im Dashboard angezeigt, wenn Sie Configuration Manager-Wartungsupdates erhalten. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../../core/servers/deploy/configure/about-the-service-connection-point.md).

- Auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, muss Internet Explorer 9 installiert sein.

- Softwareupdates müssen konfiguriert und synchronisiert werden. Windows 10-Featureupgrades sind erst dann in der Configuration Manager-Konsole verfügbar, wenn Sie die Klassifizierung **Upgrades** ausgewählt und Softwareupdates synchronisiert haben. Weitere Informationen finden Sie unter [Prepare for software updates management (Vorbereiten der Softwareudateverwaltung)](../../sum/get-started/prepare-for-software-updates-management.md).

- Überprüfen Sie ab der Configuration Manager-Version 1902 die [Clienteinstellung](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority) **Threadpriorität für Featureupdates angeben**, um sicherzustellen, dass sie für Ihre Umgebung geeignet ist.

- Überprüfen Sie ab der Configuration Manager-Version 1906 die [Clienteinstellung](../../core/clients/deploy/about-client-settings.md#bkmk_du) **Dynamisches Update für Featureupdates aktivieren**, um sicherzustellen, dass sie für Ihre Umgebung geeignet ist. <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a> Windows 10-Wartungsdashboard

Das Windows 10-Wartungsdashboard stellt Informationen zu Windows 10-Computern in Ihrer Umgebung, aktive Wartungspläne, Informationen zu Kompatibilität usw. bereit. Damit Daten im Windows 10-Wartungsdashboard angezeigt werden, muss der Dienstverbindungspunkt installiert sein. Das Dashboard verfügt über die folgenden Kacheln:

- **Kachel „Windows 10-Verwendung“** : Enthält eine Aufschlüsselung der öffentlichen Builds von Windows 10. Windows Insider-Builds sind unter **Sonstige** aufgelistet, genau wie alle Builds, die Ihrem Standort noch nicht bekannt sind. Der Dienstverbindungspunkt lädt die Metadaten herunter, mit denen er über die Windows-Builds informiert wird. Anschließend werden diese Daten mit Ermittlungsdaten verglichen.

- **Kachel „Windows 10-Ringe“** : Enthält eine Aufschlüsselung von Windows 10 nach Kanal und Bereitschaftsstatus. Das LTSC-Segment enthält alle LTSC-Versionen. Die erste Kachel gliedert die bestimmten Versionen, z.B. Windows 10 LTSC 2015.

- **Kachel „Wartungsplan erstellen“** : Bietet eine schnelle Möglichkeit zum Erstellen eines Wartungsplans. Sie geben den Namen, die Sammlung (angezeigt werden nur die 10 kleinsten Sammlungen), das Bereitstellungspaket (angezeigt werden nur die 10 Pakete, die zuletzt geändert wurden) und den Bereitschaftsstatus an. Für die anderen Einstellungen werden Standardwerte verwendet. Klicken Sie auf **Erweiterte Einstellungen**, um den Assistenten zum Erstellen eines Wartungsplans zu starten, in dem Sie alle Einstellungen für den Wartungsplan konfigurieren können.

- **Kachel „Abgelaufen“** : Zeigt den Prozentsatz der Geräte mit einem abgelaufenen Build von Windows 10 an. Configuration Manager ermittelt den Prozentsatz anhand der Metadaten, die der Dienstverbindungspunkt herunterlädt, und vergleicht ihn mit Ermittlungsdaten. Ein Build erhält nach Ablauf seiner Lebensdauer keine monatlichen kumulativen Updates, einschließlich Sicherheitsupdates, mehr. Die Computer in dieser Kategorie sollte auf die nächste Buildversion aktualisiert werden. Configuration Manager rundet auf die nächste ganze Zahl auf. Wenn Sie z.B. über rund 10.000 Computer verfügen, aber nur einen mit einem abgelaufenen Build, zeigt die Kachel 1 % an.

- **Kachel „Bald ablaufend“** : Zeigt, ähnlich wie die Kachel **Abgelaufen**, den Prozentsatz der Computer mit einem Build an, dessen Lebensdauer in Kürze abläuft (innerhalb von ca. vier Monaten). Configuration Manager rundet auf die nächste ganze Zahl auf.

- **Kachel „Warnungen“** : Zeigt aktive Warnungen an.

- **Kachel „Wartungsplanüberwachung“** : Zeigt die von Ihnen erstellten Wartungspläne und ein Konformitätsdiagramm für jeden Plan an. Diese Kachel gibt Ihnen einen schnellen Überblick über den aktuellen Zustand der Wartungsplanbereitstellungen. Wenn ein früherer Bereitstellungsring Ihre Erwartungen hinsichtlich der Kompatibilität erfüllt hat, können Sie einen späteren Wartungsplan (Bereitstellungsring) auswählen und auf **Jetzt bereitstellen** klicken, anstatt zu warten, bis die Wartungsplanregeln automatisch ausgelöst werden.

- **Kachel „Windows 10-Builds“** : Die Anzeige ist eine feste Imagezeitachse mit einer Übersicht der bisher veröffentlichten Windows 10-Builds. Sie bietet Ihnen einen allgemeinen Überblick darüber, wann Builds in die verschiedenen Zustände übergehen. Diese Kachel wurde ab der Configuration Manager-Version 1902 entfernt, da detailliertere Informationen im [Dashboard zum Produktlebenszyklus](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md) geboten werden. <!--3446861-->

> [!IMPORTANT]
> Die im Windows 10-Wartungsdashboard angezeigten Informationen (z. B. der Supportlebenszyklus für Windows 10-Versionen) dienen lediglich der Arbeitserleichterung und sind nur für die Verwendung innerhalb Ihres Unternehmens bestimmt. Sie sollten sich im Hinblick auf die Updatekompatibilität nicht ausschließlich auf diese Informationen verlassen. Überprüfen Sie stets die Richtigkeit der bereitgestellten Informationen.

## <a name="drill-through-required-updates"></a>Ausführen eines Drillthrough durch erforderliche Updates
<!--4224414-->
*(Eingeführt in Version 1906)*

Sie können einen Drillthrough durch die Konformitätsstatistiken durchführen, um herauszufinden, auf welchen Geräten ein bestimmtes Windows 10-Featureupdate erforderlich ist. Sie benötigen zum Abrufen der Geräteliste die Berechtigung, Updates und die jeweiligen Sammlungen abzurufen, zu denen die Geräte gehören. Gehen Sie wie folgt vor, um einen Drilldown in der Geräteliste auszuführen:

1. Wechseln Sie zu **Softwarebibliothek** > **Windows 10-Wartung** > **Alle Windows 10-Updates**.
1. Wählen Sie ein beliebiges Update aus, das für mindestens ein Gerät erforderlich ist.
1. Öffnen Sie die Registerkarte **Zusammenfassung**, und sehen Sie sich das Kreisdiagramm unter **Statistiken** an.
1. Klicken Sie auf der rechten Seite neben dem Kreisdiagramm auf den Link **Erforderliche anzeigen**, um einen Drilldown für die Geräteliste auszuführen.
1. Über diese Aktion gelangen Sie unter **Geräte** zu einem temporären Knoten, unter dem die Geräte angezeigt werden, für die das Update erforderlich ist. Außerdem können Sie Aktionen für den Knoten ausführen, z. B. können Sie eine neue Sammlung aus der Liste erstellen.

## <a name="servicing-plan-workflow"></a>Wartungsplanworkflow

Windows 10-Wartungspläne in Configuration Manager ähneln Regeln zur automatischen Bereitstellung von Softwareupdates. Sie erstellen einen Wartungsplan mit den folgenden Kriterien, die von Configuration Manager ausgewertet werden:

- **Klassifizierung „Upgrades“** : Nur Updates, die zur Klassifizierung **Upgrades** gehören, werden ausgewertet.

- **Bereitschaftsstatus**: Der im Wartungsplan definierte Bereitschaftsstatus wird mit dem Bereitschaftsstatus für das Upgrade verglichen. Die Metadaten für das Upgrade werden abgerufen, wenn der Dienstverbindungspunkt nach Updates sucht.

- **Zeitverzögerung**: Die Anzahl der Tage, die Sie im Wartungsplan für **Wie viele Tage möchten Sie nach der Veröffentlichung eines neuen Upgrades durch Microsoft warten, bevor Sie es in Ihrer Umgebung bereitstellen?** angegeben haben. Configuration Manager wertet aus, ob ein Upgrade in die Bereitstellung eingeschlossen werden soll, und zwar, wenn das aktuelle Datum nach dem Veröffentlichungsdatum plus der konfigurierten Anzahl von Tagen liegt.

  Wenn ein Upgrade die Kriterien erfüllt, fügt der Wartungsplan das Upgrade zum Bereitstellungspaket hinzu, verteilt das Paket an Verteilungspunkte und stellt der Sammlung das Upgrade basierend auf den im Wartungsplan konfigurierten Einstellungen bereit. Sie können die Bereitstellungen über die Kachel „Wartungsplanüberwachung“ im Windows 10-Wartungsdashboard überwachen. Weitere Informationen finden Sie unter [Monitor software updates (Überwachen von Softwareupdates)](../../sum/deploy-use/monitor-software-updates.md).

> [!NOTE]
> **Windows 10, Version 1903 und höher** wurde Microsoft Update als eigenes Produkt hinzugefügt, anstatt wie frühere Versionen Teil des Produkts **Windows 10** zu sein. Aufgrund dieser Änderung mussten Sie eine Reihe von manuellen Schritten ausführen, um sicherzustellen, dass Ihre Clients diese Updates sehen. Nun wurde die Anzahl der manuellen Schritte, die Sie für das neue Produkt in Configuration Manager, Version 1906 ausführen müssen, erfolgreich verringert. Weitere Informationen finden Sie unter [Konfigurieren von Produkten für Windows 10-Versionen](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later).<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Windows 10-Wartungsplan

Bei der Bereitstellung des halbjährlichen Kanals von Windows 10 können Sie einen oder mehrere Wartungspläne erstellen, um die Bereitstellungsringe für Ihre Umgebung zu definieren, und sie dann im Windows 10-Wartungsdashboard überwachen. Wartungspläne verwenden nur die Softwareupdateklassifizierung **Upgrades** und keine kumulativen Updates für Windows 10. Für diese Updates müssen Sie Bereitstellungen weiterhin mit dem Softwareupdateworkflow vornehmen. Die Endbenutzerumgebung mit einem Wartungsplan entspricht derjenigen mit Softwareupdates, einschließlich der Einstellungen, die Sie im Wartungsplan konfigurieren.  

> [!NOTE]
> Sie können eine Tasksequenz zum Bereitstellen eines Upgrades für jeden Windows 10-Build verwenden, dazu ist jedoch mehr manuelle Arbeit erforderlich. Sie müssten die aktualisierten Quelldateien als Upgradepaket für Betriebssysteme importieren, die Tasksequenz erstellen und dann in der entsprechenden Gruppe von Computern bereitstellen. Eine Tasksequenz bietet jedoch zusätzliche benutzerdefinierte Optionen, wie z. B. die Aktionen vor und nach der Bereitstellung.

Sie können einen grundlegenden Wartungsplan über das Windows 10-Wartungsdashboard erstellen. Nachdem Sie den Namen, die Sammlung (angezeigt werden nur die 10 kleinsten Sammlungen), das Bereitstellungspaket (angezeigt werden nur die 10 Pakete, die zuletzt geändert wurden) und den Bereitschaftszustand angegeben haben, erstellt Configuration Manager den Wartungsplan mit Standardwerten für die übrigen Einstellungen. Sie können auch den Assistenten zum Erstellen eines Wartungsplans starten, um alle Einstellungen zu konfigurieren. Verwenden Sie das folgende Verfahren zum Erstellen eines Wartungsplans mit dem Assistenten zum Erstellen eines Wartungsplans.  

> [!NOTE]  
> Sie können das Verhalten für Bereitstellungen mit hohem Risiko verwalten. Bei einer Bereitstellung mit hohem Risiko handelt es sich um eine Bereitstellung, die automatisch installiert wird und zu unerwünschten Ergebnissen führen kann. Beispielsweise wird eine Tasksequenz, die als Zweck **Erforderlich** aufweist und Windows 10 bereitstellt, als eine Bereitstellung mit hohem Risiko betrachtet. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments (Einstellungen zum Verwalten risikoreicher Bereitstellungen)](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

### <a name="to-create-a-windows-10-servicing-plan"></a>So erstellen Sie einen Windows 10-Wartungsplan

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.

1. Erweitern Sie **Windows 10-Wartung**im Arbeitsbereich „Softwarebibliothek“, und klicken Sie dann auf **Wartungspläne**.

1. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Wartungsplan erstellen**. Der Assistent zum Erstellen eines Wartungsplans wird geöffnet.

1. Konfigurieren Sie auf der Seite **Allgemein** die folgenden Einstellungen:

    - **Name:** Geben Sie den Namen für den Wartungsplan an. Der Name muss eindeutig sein, das Ziel der Regel angeben und sich am Configuration Manager-Standort leicht von anderen Namen unterscheiden lassen.

    - **Beschreibung:** Geben Sie eine Beschreibung für den Wartungsplan an. Die Beschreibung muss einen Überblick über den Wartungsplan und alle anderen relevanten Informationen umfassen, die die Identifizierung und Unterscheidung des Plans am Configuration Manager-Standort erleichtern. Das Feld „Beschreibung“ ist optional, hat eine Begrenzung auf 256 Zeichen und ist standardmäßig leer.

1. Geben Sie auf der Seite „Wartungsplan“ die **Zielsammlung** an. Mitglieder dieser Sammlung erhalten die im Wartungsplan definierten Windows 10-Upgrades.

    - Bei einer Bereitstellung mit hohem Risiko wie z.B. einem Wartungsplan werden im Fenster **Sammlung auswählen** nur die benutzerdefinierten Sammlungen angezeigt, die den in den Eigenschaften des Standorts konfigurierten Einstellungen zur Bereitstellungsüberprüfung entsprechen.

    - Bereitstellungen mit hohem Risiko sind immer auf benutzerdefinierte Sammlungen, von Ihnen erstellte Sammlungen und die integrierte Sammlung **Unbekannte Computer** beschränkt. Beim Erstellen einer Bereitstellung mit hohem Risiko können Sie keine integrierte Sammlung auswählen, wie z.B. **Alle Systeme**. Deaktivieren Sie die Einstellung **Hide collections with a member count greater than the site's minimum size configuration** (Sammlungen mit einer Anzahl der Mitglieder ausblenden, die größer als die minimale Größenkonfiguration des Standorts ist), um alle benutzerdefinierten Sammlungen anzuzeigen, die weniger Clients als die konfigurierte maximale Größe enthalten. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments (Einstellungen zum Verwalten risikoreicher Bereitstellungen)](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

    - Die Einstellungen zur Bereitstellungsüberprüfung basieren auf der aktuellen Mitgliedschaft der Sammlung. Nach der Bereitstellung des Wartungsplans wird die Sammlungsmitgliedschaft für die Einstellungen für eine Bereitstellung mit hohem Risiko nicht erneut bewertet.

      - Angenommen, Sie legen **Standardgröße** auf 100 und **Maximale Größe** auf 1000 fest. Wenn Sie eine Bereitstellung mit hohem Risiko erstellen, werden im Fenster **Sammlung auswählen** nur die Sammlungen angezeigt, die weniger als 100 Clients enthalten. Wenn Sie die Einstellung **Hide collections with a member count greater than the site's minimum size configuration** (Sammlungen mit einer Anzahl der Mitglieder ausblenden, die größer als die minimale Größenkonfiguration des Standorts ist) deaktivieren, werden im Fenster Sammlungen angezeigt, die weniger als 1.000 Clients enthalten.  
      Wenn Sie eine Sammlung auswählen, die eine Standortrolle enthält, gelten folgende Kriterien:
        - Wenn die Sammlung einen Standortsystemserver enthält und Sie die Einstellungen zur Bereitstellungsüberprüfung so konfigurieren, dass Sammlungen mit Standortsystemservern blockiert werden, tritt ein Fehler auf, und Sie können nicht fortfahren.
        - Wenn die Sammlung einen Standortsystemserver enthält und Sie die Einstellungen zur Bereitstellungsüberprüfung so konfigurieren, dass Sie im Fall von Sammlungen mit Standortsystemservern gewarnt werden, wird im Assistenten zum Bereitstellen von Software eine Warnung über ein hohes Risiko angezeigt, falls die Sammlung den Standardwert für die Größe überschreitet oder falls die Sammlung einen Server enthält. Sie müssen der Erstellung einer Bereitstellung mit hohem Risiko zustimmen, und eine Überwachungsstatusmeldung wird erstellt.

1. Konfigurieren Sie auf der Seite „Bereitstellungsring“ die folgenden Einstellungen:

   - **Geben Sie den Windows-Bereitschaftsstatus an, für den dieser Wartungsplan gelten soll**: Wählen Sie eine der folgenden Optionen aus:

      - **Halbjährlicher Kanal (Ziel):** In diesem Wartungsmodell sind Featureupdates verfügbar, sobald sie von Microsoft veröffentlicht werden.

      - **Halbjährlicher Kanal**: Dieser Wartungskanal wird in der Regel für die allgemeine Bereitstellung verwendet. Windows 10-Clients im halbjährlichen Kanal empfangen denselben Build von Windows 10 wie die Geräte im gezielten Kanal, nur zu einem späteren Zeitpunkt.

        Weitere Informationen zu Wartungskanälen und die für Sie am besten geeignete Option finden Sie unter [Wartungskanäle](/windows/deployment/update/waas-overview#servicing-channels).

   - **Wie viele Tage möchten Sie nach der Veröffentlichung eines neuen Upgrades durch Microsoft warten, bevor Sie es in Ihrer Umgebung bereitstellen**: Configuration Manager wertet aus, ob ein Upgrade in die Bereitstellung eingeschlossen werden soll, und zwar, wenn das aktuelle Datum nach dem Veröffentlichungsdatum plus der von Ihnen für diese Einstellung konfigurierten Anzahl von Tagen liegt.

1. Konfigurieren Sie auf der Seite „Upgrades“ die Suchkriterien zum Filtern der Upgrades, die dem Wartungsplan hinzugefügt werden. Nur Upgrades, die die angegebenen Kriterien erfüllen, werden der entsprechenden Bereitstellung hinzugefügt. Die folgenden Eigenschaftenfilter sind verfügbar: <!--3098809, 3113836, 3204570 -->

   - **Architektur** (ab Version 1810)
   - **Sprache**
   - **Produktkategorie** (ab Version 1810)
   - **Erforderlich**
      > [!IMPORTANT]
      > Es wird empfohlen, das Feld **Erforderlich** als Teil Ihrer Suchkriterien mit einem Wert von **> = 1** festzulegen. Durch dieses Kriterium wird sichergestellt, dass nur anwendbare Updates zum Wartungsplan hinzugefügt werden.
   - **Ersetzt** (ab Version 1810)
   - **Titel**

    Klicken Sie auf **Vorschau** , um die Upgrades anzeigen, die die angegebenen Kriterien erfüllen.

1. Konfigurieren Sie auf der Seite Bereitstellungszeitplan die folgenden Einstellungen:

   - **Auswertung planen**: Geben Sie an, ob die verfügbare Zeit und die Installationsstichtage von Configuration Manager mit UTC oder der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird, ausgewertet werden sollen.

       > [!NOTE]
       > Wenn Sie die Ortszeit auswählen und dann **So bald wie möglich** für **Zeitpunkt der Verfügbarkeit der Software** oder **Installationsstichtag** auswählen, wird die aktuelle Uhrzeit auf dem Computer mit der Configuration Manager-Konsole verwendet, um zu bestimmen, wann Updates verfügbar sind, oder auf einem Client installiert werden. Wenn sich der Client in einer anderen Zeitzone befindet, erfolgen diese Aktionen, sobald die Evaluierungszeit des Clients erreicht ist.

   - **Zeitpunkt der Verfügbarkeit der Software**: Wählen Sie eine der folgenden Einstellungen aus, um anzugeben, wann die Softwareupdates den Clients zur Verfügung gestellt werden sollen:

        - **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates so bald wie möglich in der Bereitstellung für die Clientcomputer zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung ausgewählt ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abrufzyklus der Clientrichtlinie über die Bereitstellung benachrichtigt. Die zur Installation verfügbaren Updates können dann abgerufen werden.

        - **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates zu einem bestimmten Zeitpunkt (Datum und Uhrzeit) in der Bereitstellung für die Clientcomputer zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung aktiviert ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Allerdings stehen die Softwareupdates in der Bereitstellung erst nach dem konfigurierten Termin (Datum und Uhrzeit) für die Installation zur Verfügung.

   - **Installationsstichtag**: Wählen Sie eine der folgenden Einstellungen, um den Installationsstichtag für die Softwareupdates in der Bereitstellung anzugeben:

        - **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates so bald wie möglich automatisch in der Bereitstellung installiert werden.

        - **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates zu einem bestimmten Termin (Datum und Uhrzeit) automatisch in der Bereitstellung installiert werden. Configuration Manager bestimmt den Stichtag zum Installieren von Softwareupdates durch Hinzufügen der konfigurierten Intervalle **Bestimmte Zeit** zu **Zeitpunkt der Verfügbarkeit der Software**.

           > [!NOTE]
           > Der tatsächliche Installationsstichtag ergibt sich aus der Addition des angezeigten Stichtags und eines willkürlichen Zeitraums von bis zu 2 Stunden. Dadurch werden die potenziellen Auswirkungen reduziert, die mit der gleichzeitigen Installation der Updates in der Bereitstellung durch alle Clientcomputer in der Zielsammlung einhergehen.
           >
           > Sie können die Clienteinstellung **Zufällige Stichtaganordnung deaktivieren** für **Computer-Agent** konfigurieren, um die zufällige Verzögerung der Installation für erforderliche Updates zu deaktivieren. Weitere Informationen finden Sie unter [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).

        - **Delay enforcement of this deployment according to user preferences, up to the grace period defined on the client** (Erzwingung für diese Bereitstellung basierend auf den Benutzereinstellungen innerhalb der Karenzzeit verzögern, die im Client definiert ist): Wählen Sie diese Option aus, um die Clienteinstellung [**Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** ](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours) zu berücksichtigen.

1. Konfigurieren Sie auf der Seite Benutzerfreundlichkeit die folgenden Einstellungen:  

    - **Benutzerbenachrichtigungen**: Geben Sie an, ob zum vorgegebenen **Zeitpunkt der Verfügbarkeit der Software** eine Benachrichtigung zu den Updates im Softwarecenter auf dem Clientcomputer angezeigt werden soll. Geben Sie auch an, ob auf den Clientcomputern Benutzerbenachrichtigungen eingeblendet werden sollen.

    - **Verhalten am Stichtag**: Geben Sie das gewünschte Verhalten am Stichtag der Updatebereitstellung an. Geben Sie an, ob die Updates in der Bereitstellung installiert werden sollen. Geben Sie auch, ob nach einer Updateinstallation unabhängig von einem konfigurierten Wartungsfenster ein Systemneustart ausgeführt werden soll. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

    - **Verhalten beim Geräteneustart**: Geben Sie an, ob nach der Installation der Updates ein Systemneustart auf den Servern und Arbeitsstationen unterdrückt werden soll, wenn der Systemneustart zum Abschließen der Installation erforderlich ist.

    - **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Beim Bereitstellen von Updates für Windows Embedded-Geräte mit aktiviertem Schreibfilter können Sie angeben, dass das Update auf dem temporären Overlay installiert wird und die Änderungen entweder später, am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.
        - Stellen Sie beim Bereitstellen eines Updates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist.

    - **Verhalten für erneute Auswertung der Bereitstellung von Softwareupdates bei Neustart:** Aktivieren Sie die Option **Nach dem Neustart Auswertungszyklus für Updatebereitstellung ausführen, wenn ein Update in dieser Bereitstellung einen Systemneustart erfordert**, um nach dem Neustart einen weiteren Auswertungszyklus für die Updatebereitstellung zu erzwingen.

1. Auf der Seite „Bereitstellungspaket“ wählen Sie entweder ein vorhandenes oder kein Bereitstellungspaket aus oder erstellen anhand der nachfolgenden Einstellungen ein neues Bereitstellungspaket:

    1. **Name:** Geben Sie den Namen des Bereitstellungspakets an. Dies muss ein eindeutiger Name sein, der den Paketinhalt beschreibt. Dieser ist auf 50 Zeichen begrenzt.

    1. **Beschreibung:** Geben Sie eine Beschreibung mit Informationen zum Bereitstellungspaket ein. Die Beschreibung ist auf 127 Zeichen begrenzt.

    1. **Paketquelle**: Gibt den Speicherort der Quelldateien für das Softwareupdate an. Geben Sie für den Quellspeicherort einen Netzwerkpfad wie **\\\Server\\Freigabename\\Pfad** ein. Alternativ können Sie auf **Durchsuchen** klicken, um den Netzwerkpfad zu suchen. Erstellen Sie den freigegebenen Ordner für die Quelldateien des Bereitstellungspakets, bevor Sie mit der nächsten Seite fortfahren.
        - Der von Ihnen angegebene Quellspeicherort des Bereitstellungspakets kann von keinem anderen Softwarebereitstellungspaket verwendet werden.
        - Das Computerkonto für den SMS-Anbieter und der Benutzer, der den Assistenten zum Herunterladen der Softwareupdates ausführt, müssen über die NTFS-Berechtigung **Schreiben** für den Downloadort verfügen. Sie müssen den Zugriff auf den Downloadort beschränken, um das Risiko zu verringern, dass Angreifer die Quelldateien der Softwareupdates manipulieren.
        - Sie können den Paketquellspeicherort in den Eigenschaften des Bereitstellungspakets ändern, nachdem das Bereitstellungspaket von Configuration Manager erstellt wurde. In diesem Fall müssen Sie jedoch zuerst den Inhalt von der ursprünglichen Paketquelle an den neuen Paketquellspeicherort kopieren.

    1. **Sendepriorität**: Geben Sie die Sendepriorität für das Bereitstellungspaket an. Configuration Manager verwendet Sendepriorität für das Bereitstellungspaket beim Senden des Pakets an Verteilungspunkte. Bereitstellungspakete werden in der Reihenfolge ihrer Priorität gesendet: hoch, mittel oder niedrig. Pakete mit identischer Priorität werden in der Reihenfolge ihrer Erstellung gesendet. Wenn es keinen Rückstand gibt, wird das Paket unabhängig von seiner Priorität sofort verarbeitet.

    1. **Binäre differenzielle Replikation aktivieren:** Aktivieren Sie diese Option, wenn Sie binäre differenzielle Replikation verwenden wollen.

1. Geben Sie auf der Seite „Verteilungspunkte“ die Verteilungspunkte oder Verteilungspunktgruppen an, auf denen die Updatedateien gehostet werden sollen. Weitere Informationen zu Verteilungspunkten finden Sie unter [Konfigurieren eines Verteilungspunkts](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).

    > [!NOTE]
    > Diese Seite ist nur verfügbar, wenn Sie ein neues Softwareupdate-Bereitstellungspaket erstellen.  

1. Geben Sie auf der Seite „Downloadpfad“ an, ob die Updatedateien vom Internet oder aus dem lokalen Netzwerk heruntergeladen werden sollen. Konfigurieren Sie die folgenden Einstellungen:

    - **Softwareupdates aus dem Internet herunterladen**: Wählen Sie diese Einstellung aus, um die Updates von einem bestimmten Speicherort im Internet herunterzuladen. Diese Einstellung ist standardmäßig aktiviert.

    - **Softwareupdates von einem Pfad im lokalen Netzwerk herunterladen**: Wählen Sie diese Einstellung aus, um die Updates aus einem lokalen Verzeichnis oder aus einem freigegebenen Ordner herunterzuladen. Diese Einstellung ist nützlich, wenn der Computer, auf dem der Assistent ausgeführt wird, keine Internetverbindung aufweist. Die Updates können von jedem Computer mit Internetzugriff vorläufig heruntergeladen und im lokalen Netzwerk an einem Speicherort abgelegt werden, der von dem Computer aus zugänglich ist, auf dem der Assistent ausgeführt wird.

1. Wählen Sie auf der Seite „Sprachauswahl“ die Sprachen aus, für die die ausgewählten Updates heruntergeladen werden. Die Updates werden nur dann heruntergeladen, wenn sie in den ausgewählten Sprachen verfügbar sind. Updates, die nicht sprachspezifisch sind, werden immer heruntergeladen. Standardmäßig werden vom Assistenten die Sprachen ausgewählt, die Sie in den Eigenschaften des Softwareupdatepunkts konfiguriert haben. Es muss mindestens eine Sprache ausgewählt werden, bevor die nächste Seite angezeigt werden kann. Wenn Sie nur Sprachen auswählen, die von einem Update nicht unterstützt werden, kann das Update nicht heruntergeladen werden.

1. Überprüfen Sie auf der Seite „Zusammenfassung“ die Einstellungen, und klicken Sie auf **Weiter** , um den Wartungsplan zu erstellen.  

Nachdem Sie den Assistenten abgeschlossen haben, wird der Wartungsplan ausgeführt. Dabei werden die Updates, die die angegebenen Kriterien erfüllen, einer Softwareupdategruppe hinzugefügt. Dann werden die Updates in die Inhaltsbibliothek auf dem Standortserver heruntergeladen und an die konfigurierten Verteilungspunkte verteilt. Die Softwareupdategruppe wird schließlich den Clients in der Zielsammlung bereitgestellt.

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> Ändern eines Wartungsplans

Nachdem Sie einen grundlegenden Wartungsplan über das Windows 10-Wartungsdashboard erstellt haben, oder wenn Sie die Einstellungen für einen vorhandenen Wartungsplan ändern müssen, können Sie zu den Eigenschaften für den Wartungsplan navigieren.

> [!NOTE]
> Sie können die Einstellungen in den Eigenschaften für den Wartungsplan konfigurieren, die bei der Erstellung des Wartungsplans im Assistenten nicht verfügbar sind. Im Assistenten werden für Downloadeinstellungen, Bereitstellungseinstellungen und Warnungen jeweils die Standardeinstellungen verwendet.  

Wenden Sie das folgende Verfahren an, um die Eigenschaften eines Wartungsplans zu ändern. 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>So ändern Sie die Eigenschaften eines Wartungsplans

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.

1. Klappen Sie im Arbeitsbereich „Softwarebibliothek“ **Windows 10-Wartung** auf, klicken Sie auf **Wartungspläne**, und wählen Sie dann den Wartungsplan aus, den Sie ändern möchten.

1. Klicken Sie auf der Registerkarte **Startseite** auf **Eigenschaften** , um Eigenschaften für den ausgewählten Wartungsplan zu öffnen.

    In den Eigenschaften für den Wartungsplan sind folgende Einstellungen verfügbar, die im Assistenten nicht konfiguriert wurden:

    **Bereitstellungseinstellungen**: Konfigurieren Sie auf der Registerkarte „Bereitstellungseinstellungen“ die folgenden Einstellungen:

    - **Wake-on-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren**: Geben Sie an, ob am Stichtag Wake-On-LAN aktiviert werden soll, damit Aktivierungspakete an Computer gesendet werden, für die mindestens eines der Softwareupdates in der Bereitstellung erforderlich ist. Alle Computer, die sich am Installationsstichtag im Energiesparmodus befinden, werden aktiviert, damit die Softwareupdateinstallation initiiert werden kann. Clients, die sich im Energiesparmodus befinden und für die keine der in der Bereitstellung enthaltenen Softwareupdates erforderlich sind, werden nicht gestartet. Diese Einstellung ist standardmäßig deaktiviert.

        > [!WARNING]
        > Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind.

    - **Detailstufe**: Geben Sie die Detailstufe für die von den Clientcomputern zurückgegebenen Zustandsmeldungen an.

    **Downloadeinstellungen**: Konfigurieren Sie auf der Registerkarte „Downloadeinstellungen“ die folgenden Einstellungen:

    - Geben Sie an, ob die Softwareupdates vom Client heruntergeladen und installiert werden, wenn ein Client mit einer langsamen Netzwerkverbindung oder einer Fallbackinhaltsquelle vorliegt.

    - Geben Sie an, ob die Softwareupdates vom Client von einem Fallbackverteilungspunkt heruntergeladen und installiert werden sollen, wenn der Inhalt für die Softwareupdates an einem bevorzugten Verteilungspunkt nicht verfügbar ist.

    - **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob beim Download von Inhalten BranchCache verwendet werden soll. Weitere Informationen zu BranchCache finden Sie unter [Grundlegende Konzepte für die Inhaltsverwaltung in Configuration Manager](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).

    - Geben Sie an, ob von Clients Softwareupdates von Microsoft Update heruntergeladen werden sollen, wenn keine Softwareupdates an Verteilungspunkten verfügbar sind.
        > [!IMPORTANT]
        > Verwenden Sie diese Einstellung nicht für Windows 10-Wartungsupdates. Configuration Manager kann (zumindest bis Version 1610) keine Windows 10-Wartungsupdates von Microsoft Update herunterladen.

    - Geben Sie an, ob es Clients mit einer getakteten Internetverbindung möglich sein soll, Inhalt nach dem Installationsstichtag herunterzuladen. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.

    **Warnungen**: Geben Sie auf der Seite „Warnungen“ an, wie Configuration Manager und System Center Operations Manager Warnungen für diese Bereitstellung generieren sollen.
    - Sie können die letzten Warnungen zu Softwareupdates im Arbeitsbereich **Softwarebibliothek** im Knoten **Softwareupdates** prüfen.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie unter [Grundlagen zu Configuration Manager-as-a-Service und Windows-as-a-Service](../../core/understand/configuration-manager-and-windows-as-service.md).
