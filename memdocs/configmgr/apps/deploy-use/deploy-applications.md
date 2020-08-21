---
title: Bereitstellen von Anwendungen
titleSuffix: Configuration Manager
description: Erstellen oder Simulieren der Bereitstellung einer Anwendung für ein Gerät oder eine Benutzersammlung
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a4afb066a5f07ff2347bc64b7811c2f09f3bd548
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88590933"
---
# <a name="deploy-applications-with-configuration-manager"></a>Bereitstellen von Anwendungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Erstellen oder simulieren Sie in Configuration Manager die Bereitstellung einer Anwendung für ein Gerät oder eine Benutzersammlung. Diese Bereitstellung enthält Anweisungen für den Configuration Manager-Client zur Vorgehensweise und zum Zeitpunkt der Installation der Software.

Bevor Sie eine Anwendung bereitstellen können, müssen Sie mindestens einen Bereitstellungstyp für die Anwendung erstellen. Weitere Informationen finden Sie unter [Erstellen von Anwendungen](create-applications.md).

Ab Version 1906 können Sie eine Gruppe von Anwendungen erstellen, die Sie als einzelne Bereitstellung an eine Benutzer- oder Gerätesammlung senden können. Weitere Informationen finden Sie unter [Create application groups](create-app-groups.md) (Erstellen von Anwendungsgruppen).

Sie können eine Anwendungsbereitstellung auch simulieren. Diese Simulation testet die Anwendbarkeit einer Bereitstellung ohne eine Installation oder Deinstallation der Anwendung. Bei einer simulierten Bereitstellung werden die Erkennungsmethode, Anforderungen und Abhängigkeiten für einen Bereitstellungstyp ausgewertet. Anschließend wird ein Bericht mit den Ergebnissen im Arbeitsbereich **Überwachung** unter dem Knoten **Bereitstellungen** ausgegeben. Weitere Informationen finden Sie unter [Simulate application deployments (Simulieren von Anwendungsbereitstellungen)](simulate-application-deployments.md).

> [!NOTE]
> Sie können nur die Bereitstellung erforderlicher Anwendungen simulieren, jedoch nicht die Bereitstellung von Paketen oder Softwareupdates.
>
> MDM-registrierte Geräte unterstützen keine simulierten Bereitstellungen, Einstellungen für Benutzerfreundlichkeit oder Zeitplanung.

## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a> Bereitstellen einer Anwendung

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungen** oder **Anwendungsgruppen** aus.

1. Wählen Sie aus der Liste eine Anwendung oder eine Anwendungsgruppe aus, die Sie bereitstellen möchten. Klicken Sie im Menüband auf **Bereitstellen**.  

> [!NOTE]
> Bei der Anzeige der Eigenschaften einer vorhandenen Bereitstellung entsprechen die folgenden Abschnitte den jeweiligen Registerkarten im Fenster mit den Eigenschaften der Bereitstellung:  
>
> - [Allgemein](#bkmk_deploy-general)
> - [Inhalt](#bkmk_deploy-content)
> - [Bereitstellungseinstellungen](#bkmk_deploy-settings)
> - [Zeitplanung](#bkmk_deploy-sched)
> - [Benutzerfreundlichkeit](#bkmk_deploy-ux)
> - [Warnungen](#bkmk_deploy-alerts)

### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a> Allgemeine Informationen zur **Bereitstellung**

Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Allgemein** die folgenden Informationen an:  

- **Software**: Dieser Wert zeigt die Anwendung an, die bereitgestellt werden soll. Wählen Sie **Durchsuchen** aus, um eine andere Anwendung auszuwählen.  

- **Sammlung:** Wählen Sie **Durchsuchen** aus, um die Zielsammlung für diese Anwendungsbereitstellung auszuwählen.

- **Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind**: Speichern Sie den Anwendungsinhalt in der Standard-Verteilungspunktgruppe der Sammlung. Wenn die ausgewählte Sammlung keiner Verteilungspunktgruppe zugeordnet ist, ist diese Option ausgegraut.  

- **Inhalt automatisch für Abhängigkeiten bereitstellen**: Wenn Bereitstellungstypen in der Anwendung Abhängigkeiten enthalten, sendet der Standort den Inhalt der abhängigen Anwendung auch an Verteilungspunkte.  

    >[!NOTE]
    > Wenn Sie die abhängige Anwendung aktualisieren, nachdem die primäre Anwendung bereitgestellt wurde, verteilt der Standort nicht automatisch neue Inhalte für die Abhängigkeit.

- **Kommentare (optional)** : Geben Sie bei Bedarf eine Beschreibung für diese Bereitstellung ein.

### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a> Optionen für den **Inhalt** der Bereitstellung

Wählen Sie auf der **Inhaltsseite** die Option **Hinzufügen** aus, um den Inhalt für diese Anwendung an einen Verteilungspunkt oder eine Verteilungspunktgruppe zu verteilen.

Wenn Sie auf der Seite „Allgemein“ die Option **Use default distribution points associated to this collection** (Dieser Sammlung zugeordnete Standardverteilungspunkte verwenden) ausgewählt haben, wird diese Option automatisch aufgefüllt. Nur ein Mitglied der Sicherheitsrolle **Anwendungsadministrator** kann dies ändern.

Wenn der Anwendungsinhalt bereits verteilt ist, erscheint dieses Mitglied hier.

### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a> **Bereitstellungseinstellungen**

Geben Sie auf der Seite **Bereitstellungseinstellungen** die folgenden Informationen an:  

- **Aktion**: Wählen Sie in der Dropdownliste aus, ob diese Bereitstellung zum **Installieren** oder **Deinstallieren** der Anwendung dienen soll.  

    > [!NOTE]  
    > Wenn Sie eine Bereitstellung zum **Installieren** einer App und eine andere Bereitstellung zum **Deinstallieren** derselben App auf dem selben Gerät erstellen, hat die **Installationsbereitstellung** Priorität.  

    Sie können die Aktion einer Bereitstellung nicht mehr ändern, nachdem sie erstellt wurde.  

- **Zweck**: Wählen Sie in der Dropdownliste eine der folgenden Optionen aus:  

  - **Verfügbar**: Dem Benutzer wird die Anwendung im Softwarecenter angezeigt. Er kann sie bei Bedarf installieren.  

  - **Erforderlich**: Der Client installiert automatisch die App gemäß des von Ihnen festgelegten Zeitplans. Wenn die Anwendung nicht ausgeblendet ist, kann ein Benutzer deren Bereitstellungsstatus nachverfolgen. Der Benutzer kann auch das Softwarecenter verwenden, um die Anwendung vor Ablauf der Frist zu installieren.  

    > [!NOTE]  
    > Wenn als Bereitstellungsaktion **Deinstallieren** festgelegt wurde, wird als Bereitstellungszweck automatisch **Erforderlich** festgelegt. Dieses Verhalten kann nicht geändert werden.  

- **Endbenutzern den Versuch zum Reparieren dieser Anwendung gestatten**: Aktivieren Sie diese Option ab Version 1810, wenn Sie die Anwendung mit einer Reparaturbefehlszeile erstellt haben. Benutzern wird im Softwarecenter eine Option zum **Reparieren** der Anwendung angezeigt.<!--1357866-->  

- **Software vorab auf dem primären Gerät des Benutzers bereitstellen**: Wählen Sie diese Option bei der Bereitstellung für einen Benutzer aus, um die Anwendung für die primären Geräte des Benutzers bereitzustellen. Bei dieser Einstellung ist es nicht erforderlich, dass sich der Benutzer vor der Ausführung der Bereitstellung anmeldet. Wählen Sie diese Option nicht aus, wenn der Benutzer mit der Installation interagieren muss. Diese Option ist nur verfügbar, wenn die Bereitstellung auf **Erforderlich** festgelegt ist.  

- **Aktivierungspakete senden**: Wenn die Bereitstellung auf **Erforderlich** festgelegt ist, sendet Configuration Manager ein Aktivierungspaket an die Computer, bevor der Client die Bereitstellung ausführt. Dieses Paket aktiviert den Computer zum Installationsstichtag. Bevor Sie diese Option verwenden, müssen Computer und Netzwerke für Wake-On-LAN konfiguriert sein. Weitere Informationen finden Sie unter [Planen der Clientaktivierung](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

- **Clients mit einer getakteten Internetverbindung dürfen den Inhalt nach dem Installationsstichtag herunterladen (Zusatzkosten können anfallen)** : Diese Option ist nur für Bereitstellungen mit dem Zweck **Erforderlich** verfügbar.  

- **Automatisch ein Upgrade aller abgelösten Versionen dieser Anwendung ausführen**: Der Client aktualisiert jede abgelöste Version der Anwendung auf die neuere Anwendung.

    > [!NOTE]
    > Diese Option funktioniert auch ohne Administratorgenehmigung. Wenn ein Administrator die ersetzte Version bereits genehmigt hat, muss die ersetzende Version nicht auch noch genehmigt werden. Die Genehmigung gilt nur für neue Anforderungen, nicht für ersetzende Upgrades.<!--515824-->  
    >
    > Wenn der Installationszweck **Verfügbar** lautet, können Sie diese Option aktivieren oder deaktivieren. <!--1351266-->

#### <a name="approval-settings"></a><a name="bkmk_approval"></a> Genehmigungseinstellungen

Das Verhalten bei der Anwendungsgenehmigung hängt davon ab, ob Sie die empfohlene optionale Funktion **Anwendungsanforderungen für Benutzer pro Gerät genehmigen** aktivieren.

- **Ein Administrator muss eine Anforderung für diese Anwendung auf dem Gerät genehmigen**: Wenn Sie das optionale Feature aktivieren, genehmigt der Administrator Anforderungen für die Anwendung, bevor der Benutzer sie auf dem Gerät installieren kann, für das er die Anforderung gestellt hat. Wenn ein Administrator die Anforderung genehmigt, kann der Benutzer die Anwendung nur auf diesem spezifischen Gerät installieren. Der Benutzer muss eine weitere Anforderung senden, um die Anwendung auf einem anderen Gerät installieren zu können. Diese Option ist ausgegraut, wenn der Zweck der Bereitstellung **Erforderlich** lautet, oder wenn die Anwendung für eine Gerätesammlung bereitgestellt wird.

- **Genehmigung durch Administrator erforderlich, wenn Benutzer diese Anwendung anfordern**: Wenn Sie das optionale Feature nicht aktivieren, genehmigt der Administrator Anforderungen für die Anwendung, bevor der Benutzer sie installieren kann. Diese Option ist ausgegraut, wenn der Zweck der Bereitstellung **Erforderlich** lautet, oder wenn die Anwendung für eine Gerätesammlung bereitgestellt wird.  

Weitere Informationen finden Sie im Artikel zum [Genehmigen von Anwendungen](app-approval.md).

#### <a name="deployment-properties-deployment-settings"></a>Bereitstellungseigenschaften **Bereitstellungseinstellungen**

Wenn Sie die Eigenschaften einer Bereitstellung anzeigen, werden die folgenden Optionen auf der Registerkarte **Bereitstellungseinstellungen** angezeigt, sofern von der Technologie des Bereitstellungstyps unterstützt:

**Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box** (Alle ausgeführten Dateien, die Sie auf der Registerkarte „Installationsverhalten“ im Dialogfeld zu den Bereitstellungstypeigenschaften angegeben haben, werden automatisch beendet). Weitere Informationen finden Sie unter [So prüfen Sie auf ausgeführte ausführbare Dateien, bevor Sie eine Anwendung installieren](#bkmk_exe-check).

### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a> Einstellungen für die **Zeitplanung** der Bereitstellung

Stellen Sie auf der Seite **Zeitplanung** die Zeit ein, wann diese Anwendung für Clientgeräte bereitgestellt oder verfügbar gemacht werden soll.

In der Standardeinstellung stellt Configuration Manager die Bereitstellungsrichtlinie für Clients sofort zur Verfügung. Wenn Sie die Bereitstellung erstellen, diese jedoch für Clients bis zu einem späteren Zeitpunkt nicht zur Verfügung stellen möchten, konfigurieren Sie die Option **Schedule the application to be available** (Zeitpunkt der Verfügbarkeit der Anwendung festlegen). Wählen Sie anschließend Datum und Uhrzeit und ob es sich um UTC oder um die Ortszeit des Clients handelt.

Wenn die Bereitstellung **Erforderlich** ist, geben Sie dazu noch den **Installationsstichtag** an. Standardmäßig ist dieser so bald wie möglich.

Angenommen, Sie müssen eine neue branchenspezifische Anwendung bereitstellen. Alle Benutzer müssen diese zu einem bestimmten Zeitpunkt installiert haben. Sie möchten ihnen jedoch die Möglichkeit geben, sie bereits vor dem Stichtag zu installieren. Sie müssen ebenso sicherstellen, dass der Standort den Inhalt an alle Verteilungspunkte verteilt hat. Sie legen fest, dass die Anwendung ab heute in fünf Tagen verfügbar sein soll. Dieser Zeitplan gibt Ihnen die nötige Zeit, den Inhalt zu verteilen und dessen Status zu bestätigen. Sie legen den Installationsstichtag auf heute in einem Monat fest. Benutzern wird die Anwendung im Softwarecenter angezeigt, wenn sie in fünf Tagen verfügbar ist. Wenn diese nichts tun, wird die Anwendung automatisch vom Client am Installationsstichtag installiert.

Wenn die bereitgestellte Anwendung eine andere Anwendung ablöst, legen Sie den Installationsstichtag fest, an dem bei Benutzern die neue Anwendung installiert wird. Legen Sie den **Installationsstichtag** fest, um für Benutzer mit der abgelösten Anwendung ein Upgrade auszuführen.

#### <a name="delay-enforcement-with-a-grace-period"></a>Verzögerung der Erzwingung mit Karenzzeit

Sie sollten Benutzern mehr Zeit für die Installation erforderlicher Anwendungen *über die von Ihnen konfigurierten Fristen hinaus* gewähren. Dieses Verhalten ist in der Regel erforderlich, wenn ein Computer für lange Zeit ausgeschaltet ist und viele Anwendungen installiert werden müssen. Dieser Fall kann eintreten, wenn ein Benutzer beispielsweise aus dem Urlaub zurückkehrt und lange warten muss, während der Client überfällige Bereitstellungen installiert. Definieren Sie eine Toleranzperiode, um dieses Problem zu beheben.

- Konfigurieren Sie zunächst diese Karenzzeit mit der Eigenschaft **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** in den Clienteinstellungen. Weitere Informationen finden Sie in der [Computer-Agent](../../core/clients/deploy/about-client-settings.md#computer-agent)-Gruppe. Geben Sie einen Wert zwischen **1** und **120** Stunden an.  

- Aktivieren Sie auf der Seite **Zeitplanung** in einer neuen erforderlichen Anwendungsbereitstellung die Option **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings** (Erzwingen dieser Bereitstellung entsprechend den Benutzervoreinstellungen bis zur Karenzzeit verzögern, die in den Clienteinstellungen definiert ist) aus. Die Karenzzeit für die Erzwingung gilt für alle Bereitstellungen, für die diese Option aktiviert wird, und die für Geräte vorgesehen sind, für die Sie ebenfalls die Clienteinstellungen bereitgestellt haben.

Nach Ablauf der Frist installiert der Client die Anwendung im ersten nicht geschäftlichen Fenster, das der Benutzer in der Karenzzeit konfiguriert hat. Der Benutzer kann jedoch weiterhin das Softwarecenter öffnen und die Anwendung zu einem beliebigen Zeitpunkt installieren. Nach Ablauf der Toleranzperiode wird die Erzwingung auf normales Verhalten für überfällige Bereitstellungen zurückgesetzt.

:::image type="content" source="media/grace-period.svg" alt-text="Diagramm zur Toleranzperiode":::

<!-- SCCMDocs issue #1599 -->

> [!NOTE]
> Diese Funktion wird meist für das Szenario verwendet, dass ein Gerät lange ausgeschaltet war, weil der Benutzer nicht im Büro war. Technisch gesehen beginnt die Toleranzperiode, wenn der Client nach dem Bereitstellungsstichtag eine Richtlinie erhält. Das gleiche Verhalten tritt auf, wenn Sie den Configuration Manager-Clientdienst (CcmExec) stoppen und ihn zu einem späteren Zeitpunkt, nach dem Bereitstellungsstichtag, neu starten.

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a> Einstellungen für die **Benutzerfreundlichkeit** der Bereitstellung

Geben Sie auf der Seite **Benutzerfreundlichkeit** an, wie Benutzer mit der Anwendungsinstallation interagieren können.

- **Benutzerbenachrichtigungen**: Geben Sie an, ob die Benachrichtigung im Softwarecenter zum konfigurierten Zeitpunkt der Verfügbarkeit angezeigt werden soll. Mit dieser Einstellung wird auch gesteuert, ob Benutzer auf den Clientcomputern benachrichtigt werden sollen. Für verfügbare Bereitstellungen können Sie die Option **In Softwarecenter und allen Benachrichtigungen ausblenden** nicht auswählen.  

  - **Wenn Softwareänderungen erforderlich sind, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen**<!--3555947-->: Wählen Sie ab Version 1902 diese Option aus, um die Benutzeroberfläche deutlicher zu gestalten. Dies gilt nur für erforderliche Bereitstellungen. Weitere Informationen finden Sie unter [Planen für Software Center](../plan-design/plan-for-software-center.md#bkmk_impact).

- **Softwareinstallation** und **Systemneustart**: Konfigurieren Sie diese Einstellungen nur für erforderliche Bereitstellungen. Sie geben das jeweilige Verhalten an, wenn die Bereitstellung den Ablauf der Frist außerhalb von definierten Wartungsfenstern erreicht. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

- **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Diese Einstellung steuert das Installationsverhalten auf Windows Embedded-Geräten, auf denen ein Schreibfilter aktiviert ist. Wählen Sie diese Option aus, um Änderungen am Installationsstichtag oder während eines Wartungsfensters vorzunehmen. Die Auswahl dieser Option erfordert auch einen Neustart. Die Änderungen werden auf dem Gerät beibehalten. Andernfalls wird die Anwendung auf der temporären Überlagerung installiert und später übergeben.  

  - Stellen Sie beim Bereitstellen eines Softwareupdates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert wurde. Weitere Informationen zu Wartungsfenstern und Windows Embedded-Geräten finden Sie unter [Create Windows Embedded applications (Erstellen von Windows Embedded-Geräten)](../get-started/creating-windows-embedded-applications.md).  

### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a>**Bereitstellungswarnungen**

Konfigurieren Sie auf der Seite **Warnungen**, wie Configuration Manager Warnungen für diese Bereitstellung generiert. Wenn Sie auch System Center Operations Manager verwenden, konfigurieren Sie diese Warnungen ebenso. Sie können nur einige Warnungen für erforderliche Bereitstellungen konfigurieren.

## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a> Erstellen einer Bereitstellung in Phasen

<!--1358147-->
Mithilfe von Bereitstellungen in Phasen können Sie einen koordinierten, sequenzierten Softwarerollout basierend auf anpassbaren Kriterien und Gruppen orchestrieren. Sie können die Anwendung beispielsweise für eine Pilotsammlung bereitstellen, und anschließend wird der Rollout basierend auf Erfolgskriterien automatisch fortgesetzt.

Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Erstellen einer Bereitstellung in Phasen](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  

- [Verwalten und Überwachen von Bereitstellungen in Phasen](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  

## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a> Bereitstellung löschen

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungen** oder **Anwendungsgruppen** aus.  

1. Wählen Sie die Anwendung oder Anwendungsgruppe aus, die die Bereitstellung enthält, die Sie löschen möchten.  

1. Wechseln Sie im Detailbereich zur Registerkarte **Bereitstellungen**, und wählen Sie die Bereitstellung aus.  

1. Wählen Sie auf dem Menüband auf der Registerkarte **Bereitstellung** in der Gruppe **Bereitstellung** die Option **Löschen** aus.  

Wenn Sie eine Anwendungsbereitstellung löschen, werden bereits vom Client installierte Instanzen der Anwendung nicht entfernt. Stellen Sie die Anwendungen mit **Deinstallieren** auf Computern bereit, um diese Anwendungen zu entfernen. Wenn Sie eine Anwendungsbereitstellung löschen, ist die Anwendung nicht mehr im Software Center sichtbar. Das gleiche Verhalten tritt auf, wenn Sie eine Ressource aus der Zielsammlung für die Bereitstellung entfernen.

## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a> Benutzerbenachrichtigungen für erforderliche Bereitstellungen

Wenn Benutzer die erforderliche Software erhalten und die Einstellung **Snooze and remind me** (Erneut erinnern) auswählen, können sie aus folgenden Optionen wählen:  

- **Später**: Gibt an, dass Benachrichtigungen basierend auf den in den Clienteinstellungen konfigurierten Benachrichtigungseinstellungen geplant sind.  

- **Feste Zeit**: Gibt an, dass die Benachrichtigung nach der ausgewählten Zeit erneut angezeigt wird. Wenn Sie z.B. 30 Minuten auswählen, wird die Benachrichtigung in 30 Minuten erneut angezeigt.  

:::image type="content" source="media/ComputerAgentSettings.png" alt-text="Gruppe „Computer-Agent“ in Clientstandardeinstellungen":::

Die maximale Erinnerungszeit basiert immer auf den Benachrichtigungswerten, die in den Clienteinstellungen zu jedem Zeitpunkt der Bereitstellung konfiguriert sind. Beispiel:  

- Sie konfigurieren die Einstellung **Deployment deadline greater than 24 hours, remind users every (hours)** (Bereitstellungsstichtag größer als 24 Stunden, Benutzer alle (Stunden) erinnern) auf der Seite **Computer-Agent** für 10 Stunden.  

- Der Client zeigt das Benachrichtigungsdialogfeld mehr als 24 Stunden vor dem Bereitstellungsstichtag an.  

- Im Dialogfeld werden Erinnerungsoptionen von bis zu maximal 10 Stunden angezeigt.  

- Wenn der Bereitstellungsstichtag näher rückt, werden im Dialogfeld weniger Optionen angezeigt. Diese Optionen stimmen mit den entsprechenden Clienteinstellungen für jede Komponente der Bereitstellungszeit überein.  

Bei Bereitstellungen mit hohem Risiko, z. B. einer Tasksequenz, die ein Betriebssystem bereitstellen, fällt die Benachrichtigung des Benutzers deutlicher aus. Immer wenn Sie benachrichtigt werden, dass eine wichtige Softwarewartung erforderlich ist, wird anstatt einer vorübergehenden Benachrichtigung in der Taskleiste ein Dialogfeld wie das folgende angezeigt:

:::image type="content" source="media/client-toast-notification.png" alt-text="Erforderlicher Softwaredialog, der Sie über wichtige Softwarewartung benachrichtigt":::

## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a> Überprüfen auf ausführbare Dateien, die ausgeführt werden

Konfigurieren Sie eine Bereitstellung, um zu überprüfen, ob bestimmte ausführbare Dateien auf dem Client ausgeführt werden. Verwenden Sie diese Option, um Prozesse zu suchen, die womöglich die Installation der Anwendung stören. Wenn eine dieser ausführbaren Dateien auf dem Client ausgeführt wird, blockiert diese die Installation des Bereitstellungstyps. Der Benutzer muss die ausgeführte ausführbare Datei schließen, bevor der Client den Bereitstellungstyp installieren kann. Für Bereitstellungen mit dem Zweck „Erforderlich“ kann der Client die ausgeführte ausführbare Datei automatisch schließen.

1. Öffnen Sie die **Eigenschaften** für den Bereitstellungstyp.

1. Wechseln Sie zur Registerkarte **Installationsverhalten**, und wählen Sie **Hinzufügen** aus.

1. Geben Sie im Fenster **Ausführbare Datei hinzufügen** den Namen der ausführbaren Zieldatei ein. Geben Sie optional einen Anzeigenamen für die Anwendung ein, damit Sie sie leichter identifizieren können.

1. Wählen Sie **OK** aus, um zu speichern und das Fenster der Eigenschaften des Bereitstellungstyps zu schließen.

1. Wenn Sie die Anwendung bereitstellen, wählen Sie die Option **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box** (Alle ausgeführten Dateien, die Sie in der Registerkarte „Installationsverhalten“ im Dialogfeld zu den Bereitstellungstypeigenschaften angegeben haben, werden automatisch beendet) aus. Diese Option befindet sich auf der Registerkarte **Bereitstellungseinstellungen** der Bereitstellungseigenschaften.  

> [!NOTE]
> Eine Anwendung kann von der Tasksequenz nicht installiert werden, wenn Sie sie so konfiguriert haben, dass eine Prüfung auf laufende ausführbare Dateien erfolgt, und Sie sie in den Tasksequenzschritt [Anwendung installieren](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) aufgenommen haben. Wenn Sie diesen Tasksequenzschritt nicht so konfigurieren, dass er auch bei einem Fehler fortgesetzt wird, schlägt die gesamte Tasksequenz fehl.

### <a name="client-behaviors-and-user-notifications"></a>Clientverhalten und Benutzerbenachrichtigungen

Nachdem Clients die Bereitstellung empfangen haben, wird folgendes Verhalten angewendet:  

- Wenn Sie die Anwendung als **Verfügbar** bereitgestellt haben und ein Benutzer versucht, sie zu installieren, fordert der Client ihn dazu auf, die ausgeführten ausführbaren Dateien zu schließen, bevor er mit der Installation fortfahren kann.  

- Wenn Sie die Anwendung als **Erforderlich** bereitgestellt haben und die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte „Installationsverhalten“ angegeben wurden** ausgewählt ist, wird vom Client eine Benachrichtigung angezeigt. Der Benutzer wird so informiert, dass die angegebenen ausführbaren Dateien automatisch geschlossen werden, sobald der Stichtag der Anwendungsinstallation erreicht ist.  

  - Planen Sie diese Dialogfelder in der Gruppe **Computer-Agent** in den Clienteinstellungen. Weitere Informationen finden Sie unter [Computer-Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

  - Wenn Sie nicht möchten, dass der Benutzer diese Meldungen sieht, wählen Sie auf der Registerkarte **User Experience** (Benutzerfreundlichkeit) der Bereitstellungseigenschaften **In Softwarecenter und allen Benachrichtigungen ausblenden** aus. Weitere Informationen finden Sie unter [Deployment User Experience settings (Einstellungen für die Benutzerfreundlichkeit der Bereitstellung)](#bkmk_deploy-ux).  

- Wenn Sie die Anwendung als **Erforderlich** bereitgestellt haben, und die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte „Installationsverhalten“ angegeben wurden** nicht ausgewählt ist, schlägt die Installation der App fehl, wenn mindestens eine der angegebenen Anwendungen ausgeführt wird.  

## <a name="deploy-user-available-applications"></a>Bereitstellen von für Benutzer verfügbaren Anwendungen

Wenn Sie Anwendungen als **Verfügbar** in Benutzersammlungen bereitstellen, können Benutzer das Softwarecenter durchsuchen und die benötigten Apps installieren. Für lokale in die Domäne eingebundene Clients verwendet das Softwarecenter die Domänenanmeldeinformationen des Benutzers, um die Liste der verfügbaren Anwendungen vom Verwaltungspunkt abzurufen.

Es gibt zusätzliche Anforderungen für Clients, die internetbasiert, in Azure Active Directory (Azure AD) eingebunden oder beides sind.

### <a name="azure-ad-joined-devices"></a>In Azure AD eingebundene Geräte
<!-- 1322613 -->

Wenn Sie Anwendungen als für Benutzer verfügbar bereitstellen, können diese die Anwendungen über das Softwarecenter durchsuchen und auf Azure AD-Geräten installieren. Konfigurieren Sie die folgenden Voraussetzungen, um dieses Szenario zu aktivieren:

- Aktivieren Sie HTTPS auf dem Verwaltungspunkt.  

- Integrieren Sie den Standort in [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) für die **Cloudverwaltung**.  

  - Konfigurieren Sie die [Azure AD-Benutzerermittlung](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc).  

- Stellen Sie über Azure AD eine Anwendung als für eine Benutzersammlung verfügbar bereit.  

- Aktivieren Sie die Clienteinstellung **Neues Softwarecenter verwenden** in der Gruppe [Computer-Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

- Als Clientbetriebssystem muss Windows 10 verwendet werden, und es muss in Azure AD eingebunden sein. Eine einfache Einbindung in die Clouddomäne oder eine Einbindung in Hybrid-Azure AD  

- Zur Unterstützung internetbasierter Clients:  

  - [Cloudverwaltungsgateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (Cloud Management Gateway, CMG)

  - Verteilen Sie Anwendungsinhalte an ein inhaltsfähiges CMG oder einen [Cloudverteilungspunkt](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  

  - Aktivieren Sie die Clienteinstellung: **Benutzerrichtlinienanforderungen von Internetclients aktivieren** in der Gruppe [Clientrichtlinie](../../core/clients/deploy/about-client-settings.md#client-policy).  

- So unterstützen Sie Clients im Intranet:  

  - Fügen Sie das inhaltsfähige CMG oder den Cloudverteilungspunkt einer Begrenzungsgruppe hinzu, die von den Clients verwendet wird.  

  - Clients müssen den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des HTTPS-fähigen Verwaltungspunkts auflösen.  

  > [!NOTE]
  > Für einen Client, der als im Intranet befindlich erkannt wurde, aber über das Cloudverwaltungsgateway (Cloud Management Gateway, CMG) in Configuration Manager Version 2002 und früher kommuniziert, verwendet das Softwarecenter die Windows-Authentifizierung. Beim Versuch, die Liste der für Benutzer verfügbaren Apps über das CMG abzurufen, trat ein Fehler auf. Ab Version 2006 wird Azure AD-Identität (Azure Active Directory) für Geräte verwendet, die mit Azure AD verknüpft sind. Diese Geräte können mit der Cloud verbunden oder hybrid eingebunden sein.<!--6935376-->

## <a name="next-steps"></a>Nächste Schritte

- [Überwachen von Anwendungen](monitor-applications-from-the-console.md)
- [Troubleshoot application deployments (Problembehandlung bei Anwendungsbereitstellungen)](troubleshoot-application-deployment.md)
- [Verwaltungstasks für Anwendungen](management-tasks-applications.md)
- [Benutzerleitfaden des Softwarecenters](../../core/understand/software-center.md)
