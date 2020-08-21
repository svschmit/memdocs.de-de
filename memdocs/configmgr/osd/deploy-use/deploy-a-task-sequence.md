---
title: Bereitstellen einer Tasksequenz
titleSuffix: Configuration Manager
description: Verwenden Sie diese Informationen, um eine Tasksequenz auf Computern in einer Sammlung bereitzustellen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fea9088a11310aedc95d2fdbeacdb98650eef361
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125201"
---
# <a name="deploy-a-task-sequence"></a>Bereitstellen einer Tasksequenz

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie eine Tasksequenz erstellt und die referenzierten Inhalte verteilt haben, können Sie sie für eine Gerätesammlung bereitstellen. Dadurch kann die Tasksequenz auf einem Gerät ausgeführt werden. Eine bereitgestellte Tasksequenz kann entweder automatisch ausgeführt werden oder wenn sie von einem Benutzer des Geräts installiert wird.

> [!WARNING]  
> Sie können das Verhalten für Tasksequenzbereitstellungen mit hohem Risiko verwalten. Bei einer Bereitstellung mit hohem Risiko handelt es sich um eine Bereitstellung, die automatisch installiert wird und zu unerwünschten Ergebnissen führen kann. Beispielsweise wird eine Tasksequenz, die als Zweck **Erforderlich** aufweist und ein Betriebssystem bereitstellt, als eine Bereitstellung mit hohem Risiko betrachtet. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments (Einstellungen zum Verwalten risikoreicher Bereitstellungen)](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

## <a name="process"></a>Prozess

Mithilfe der folgenden Vorgehensweise können Sie eine Tasksequenz auf Computern in einer Sammlung bereitstellen.  

> [!NOTE]  
> Die Statusmeldungen für die Tasksequenzbereitstellung werden in einem Meldungsfenster an einem primären Standort, nicht jedoch an einem Standort der zentralen Verwaltung angezeigt.  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie in der Liste **Tasksequenz** die Tasksequenz aus, die Sie bereitstellen möchten.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Bereitstellung** die Option **Bereitstellen** aus.  

    > [!NOTE]  
    > Wenn **Bereitstellen** nicht verfügbar ist, weist die Tasksequenz eine ungültige Referenz auf. Korrigieren Sie die Referenz, und versuchen Sie dann erneut, die Tasksequenz bereitzustellen.  

4. Geben Sie auf der Seite **Allgemein** die folgenden Informationen an.  

    - **Tasksequenz**: Geben Sie die bereitzustellende Tasksequenz an. In diesem Feld wird standardmäßig die ausgewählte Tasksequenz angezeigt.  

    - **Sammlung:** Wählen Sie die Sammlung aus, die die Computer enthält, auf denen die Tasksequenz ausgeführt werden soll.  

        Stellen Sie keine Tasksequenz bereit, mit der ein Betriebssystem in ungeeigneten Sammlungen installiert wird, wie beispielsweise in einer Sammlung mit all Ihren Rechenzentrumsservern. Achten Sie darauf, dass die ausgewählte Sammlung nur die Computer enthält, auf denen die Tasksequenz ausgeführt werden soll.  

        Weitere Informationen zu risikoreichen Bereitstellungen finden Sie unter [High-risk deployments](#bkmk_high-risk) (Risikoreiche Bereitstellungen).

    - **Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind**: Speichern Sie den Tasksequenzinhalt in der Standard-Verteilungspunktgruppe der Sammlung. Wenn die ausgewählte Sammlung keiner Verteilungspunktgruppe zugeordnet ist, ist diese Option ausgegraut.  

    - **Inhalt automatisch für Abhängigkeiten bereitstellen**: Wenn Inhalte, auf die verwiesen wird, Abhängigkeiten enthalten, sendet der Standort den abhängigen Inhalt auch an Verteilungspunkte.  

    - **Inhalt für diese Tasksequenz vorab herunterladen**: Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](configure-precache-content.md).  

    - **Bereitstellungsvorlage auswählen**: Speichern Sie eine Bereitstellungsvorlage für eine Tasksequenz und geben Sie sie an.<!--1357391-->  

        > [!IMPORTANT]  
        > Einige Elemente werden nicht in der Vorlage gespeichert.<!--510610--> Wenden Sie beim Ausführen des Bereitstellungs-Assistenten die folgenden Elemente an:  
        >
        > - Softwareinstallation
        > - Planung
        > - Inhalt vorab laden

    - **Kommentare (optional)** : Geben Sie zusätzliche Informationen zur Beschreibung dieser Tasksequenzbereitstellung an.  

5. Geben Sie auf der Seite **Bereitstellungseinstellungen** die folgenden Informationen an:  

    - **Zweck**: Wählen Sie in der Dropdownliste eine der folgenden Optionen aus:  

        - **Verfügbar**: Dem Benutzer wird die Tasksequenz im Softwarecenter angezeigt, und er kann sie bei Bedarf installieren.  

        - **Erforderlich**: Configuration Manager führt die Tasksequenz automatisch gemäß dem konfigurierten Plan aus. Wenn die Tasksequenz nicht ausgeblendet ist, kann der Benutzer weiterhin ihren Bereitstellungsstatus nachverfolgen. Der Benutzer kann auch das Softwarecenter verwenden, um die Tasksequenz vor Ablauf der Frist zu installieren.  

        > [!NOTE]
        > Wenn mehrere Benutzer auf dem Gerät angemeldet sind, werden Paket- und Tasksequenzbereitstellungen möglicherweise im Softwarecenter nicht angezeigt.  

    - **Verfügbar machen für**: Geben Sie an, ob die Tasksequenz für einen der folgenden Typen verfügbar sein soll:  

        - Nur Configuration Manager-Clients  
        - Configuration Manager-Clients, Medien und PXE  
        - Nur Medien und PXE  
        - Nur Medien und PXE (ausgeblendet)  

        > [!IMPORTANT]  
        > Verwenden Sie die Einstellung **Nur Medien und PXE (ausgeblendet)** für automatisierte Bereitstellungen von Tasksequenzen. Wenn der Computer bei der Bereitstellung ohne Benutzerinteraktion automatisch gestartet werden soll, wählen Sie **Unbeaufsichtigte Betriebssystembereitstellung zulassen** aus und legen die Variable **SMSTSPreferredAdvertID** als Teil der Medien fest. Weitere Informationen zu Tasksequenzvariablen finden Sie unter [Tasksequenzvariablen](../understand/task-sequence-variables.md#SMSTSPreferredAdvertID).  

    - **Aktivierungspakete senden**: Wenn die Bereitstellung auf **Erforderlich** festgelegt ist und Sie diese Option auswählen, sendet der Standort ein Aktivierungspaket an Computer, bevor der Client die Bereitstellung ausführt. Durch dieses Paket wird der Energiesparmodus des Computers am Installationsstichtag beendet, und der Computer wird aktiviert. Bevor Sie diese Option verwenden, müssen Computer und Netzwerke für Wake-On-LAN konfiguriert sein. Weitere Informationen finden Sie unter [Planen der Clientaktivierung](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    - **Clients mit einer getakteten Internetverbindung dürfen den Inhalt nach dem Installationsstichtag herunterladen (Zusatzkosten können anfallen)** : Diese Option ist nur für Bereitstellungen mit dem Status **Erforderlich** verfügbar. Bei einer benutzerdefinierten Tasksequenz, mit der eine Anwendung installiert, aber kein Betriebssystem bereitgestellt wird, können Sie angeben, ob Clients mit einer getakteten Internetverbindung Inhalt nach einem Installationsstichtag herunterladen dürfen. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie nutzen.  

        > [!NOTE]  
        > Die Verwendung einer getakteten Internetverbindung funktioniert zwar möglicherweise für Tasksequenzen, mit denen kein Betriebssystem bereitgestellt wird, aber dies wird nicht unterstützt.  

6. Geben Sie auf der Seite **Zeitplanung** folgende Informationen an:  

    > [!IMPORTANT]  
    > Wenn ein Windows PE-Client über PXE oder Startmedien gestartet wird, wertet der Client keine Bereitstellungspläne aus. Zu diesen Plänen zählen Startzeiten, Ablaufzeiten und Stichtage. Konfigurieren Sie Zeitpläne nur in Bereitstellungen auf Clients, die vom vollständigen Windows-Betriebssystem gestartet werden. Ziehen Sie die Verwendung anderer Methoden in Betracht, z. B. Wartungsfenster, um aktive Tasksequenzen für Clients zu steuern, die von Windows PE gestartet werden.  

    - **Verfügbarkeitsdatum der Bereitstellung festlegen**: Geben Sie den Zeitpunkt (Datum und Uhrzeit) an, zu dem die Tasksequenz zur Ausführung auf dem Zielcomputer verfügbar ist. Wenn Sie die Option **UTC** auswählen, ist die Tasksequenz für mehrere Computer gleichzeitig verfügbar. Andernfalls ist die Bereitstellung zu unterschiedlichen Zeiten gemäß der lokalen Zeit auf den einzelnen Computern verfügbar.  

        Wenn die Startzeit vor der erforderlichen Zeit liegt, wird der Tasksequenzinhalt vom Client zur Startzeit heruntergeladen.  

    - **Ablaufdatum der Bereitstellung festlegen**: Geben Sie den Zeitpunkt (Datum und Uhrzeit) an, zu dem die Tasksequenz auf dem Zielcomputer abläuft. Wenn Sie die Option **UTC** auswählen, läuft die Tasksequenz für mehrere Zielcomputer gleichzeitig ab. Andernfalls läuft die Bereitstellung zu unterschiedlichen Zeiten gemäß der lokalen Zeit auf den einzelnen Computern ab.  

    - **Zuweisungszeitplan**: Geben Sie für eine Bereitstellung mit dem Status **Erforderlich** den Zeitpunkt an, an dem der Client die Tasksequenz ausführt. Sie können mehrere Zeitpläne hinzufügen. Der Zuweisungszeitplan kann eine der folgenden Konfigurationen aufweisen:  

        - Ein bestimmtes Datum und eine bestimmte Uhrzeit  
        - Monatliches, wöchentliches oder benutzerdefiniertes Wiederholungsmuster  
        - So bald wie möglich  
        - Anmelde- oder Abmeldeereignisse  

        > [!NOTE]  
        > Wenn Sie eine Startzeit für eine erforderliche Bereitstellung planen, die vor dem Datum und der Uhrzeit liegt, an denen die Tasksequenz verfügbar ist, lädt der Configuration Manager-Client den Inhalt zur zugewiesenen Startzeit herunter. Dieses Verhalten tritt auch dann auf, wenn Sie geplant haben, dass die Tasksequenz zu einem späteren Zeitpunkt verfügbar sein soll.<!--SCCMDocs issue 777-->  

    - **Verhalten beim erneuten Ausführen**: Geben Sie an, wann die Tasksequenz erneut ausgeführt wird. Wählen Sie eine der folgenden Optionen aus:  

        - **Bereitgestelltes Programm nie erneut ausführen**: Wenn der Client die Tasksequenz bereits ausgeführt hat, wird sie nicht erneut ausgeführt. Die Tasksequenz wird selbst dann nicht erneut ausgeführt, wenn bei der ursprünglichen Ausführung ein Fehler aufgetreten ist oder die Tasksequenzdateien geändert wurden.  

        - **Programm immer erneut ausführen**: Die Tasksequenz wird immer erneut auf dem Client ausgeführt, wenn die Bereitstellung geplant ist. Sie wird selbst dann erneut ausgeführt, wenn die Tasksequenz bereits erfolgreich ausgeführt wurde. Diese Einstellung ist nützlich, wenn Sie wiederholte Bereitstellungen verwenden, bei denen routinemäßig ein Update der Tasksequenz ausgeführt wird.  

            > [!IMPORTANT]  
            > Diese Option ist standardmäßig ausgewählt. Sie hat jedoch erst Auswirkungen, wenn Sie eine erforderliche Bereitstellung zuweisen. Ein Benutzer kann verfügbare Bereitstellungen stets erneut ausführen.  

        - **Bei fehlgeschlagenem vorherigen Versuch erneut ausführen**: Die Tasksequenz wird bei geplanter Bereitstellung nur dann erneut ausgeführt, wenn bei der vorherigen Ausführung ein Fehler aufgetreten ist. Diese Einstellung ist nützlich für erforderliche Bereitstellungen. Wenn der letzte Ausführungsversuch nicht erfolgreich war, wird automatisch entsprechend dem Zuweisungszeitplan erneut versucht, die Bereitstellungen auszuführen.  

        - **Bei erfolgreichem vorherigen Versuch erneut ausführen**: Die Tasksequenz wird nur dann erneut ausgeführt, wenn sie auf dem Client bereits erfolgreich ausgeführt wurde. Diese Einstellung ist nützlich, wenn Sie wiederholte Bereitstellungen verwenden, bei denen routinemäßig ein Update der Tasksequenz ausgeführt wird, und jedes dieser Updates nur möglich ist, wenn das vorherige Update erfolgreich installiert wurde.  

        > [!NOTE]  
        > Ein Benutzer kann eine verfügbare Tasksequenzbereitstellung erneut ausführen. Bevor Sie eine verfügbare Tasksequenz in einer Produktionsumgebung bereitstellen, testen Sie zuerst, was geschieht, wenn ein Benutzer die Tasksequenz mehrmals erneut ausführt.  

7. Geben Sie auf der Seite **Benutzerfreundlichkeit** die folgenden Informationen an:  

    - **Benutzern zuweisungsunabhängige Programmausführung erlauben**: Geben Sie an, ob ein Benutzer eine erforderliche Bereitstellung außerhalb des Zuweisungszeitplans ausführen kann. Diese Option ist für verfügbare Bereitstellungen immer aktiviert.  

    - **Tasksequenzstatus anzeigen**: Geben Sie an, ob der Status der Tasksequenz vom Configuration Manager-Client angezeigt wird.  

    - **Softwareinstallation**: Geben Sie an, ob der Benutzer außerhalb eines konfigurierten Wartungsfensters nach dem geplanten Zeitpunkt Software installieren darf.  

    - **Systemneustart (falls dieser zum Abschluss der Installation erforderlich ist)** : Geben Sie an, ob der Benutzer den Computer im Anschluss an eine Softwareinstallation außerhalb eines konfigurierten Wartungsfensters nach dem Zuweisungszeitraum neu starten darf.  

    - **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Diese Einstellung steuert das Installationsverhalten auf Windows Embedded-Geräten, auf denen ein Schreibfilter aktiviert ist. Wählen Sie diese Option aus, um Änderungen am Installationsstichtag oder während eines Wartungsfensters vorzunehmen. Die Auswahl dieser Option erfordert auch einen Neustart. Die Änderungen werden auf dem Gerät beibehalten. Andernfalls wird die Anwendung auf der temporären Überlagerung installiert und später übergeben. Stellen Sie beim Bereitstellen einer Tasksequenz auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist.  

    - **Ausführung der Tasksequenz für internetbasierten Client zulassen**: Geben Sie an, ob die Tasksequenz auf einem internetbasierten Client ausgeführt werden darf.

        Diese Einstellung wird für Bereitstellungen von Tasksequenzen für ein direktes Upgrade von Windows 10 auf internetbasierten Clients über das Cloudverwaltungsgateway (Cloud Management Gateway, CMG) unterstützt. Weitere Informationen finden Sie unter [Bereitstellen eines direkten Upgrades für Windows 10 über das CMG](#deploy-windows-10-in-place-upgrade-via-cmg).

        Ab Version 2006 können Sie eine Tasksequenz mit einem Startimage auf einem Gerät bereitstellen, das über das CMG kommuniziert. Der Benutzer muss die Tasksequenz in Software Center starten.<!--6997525-->

        > [!NOTE]
        > Wenn ein in Azure Active Directory (Azure AD) eingebundener Client eine Tasksequenz für die Bereitstellung eines Betriebssystems ausführt, wird der Client im neuen Betriebssystem nicht automatisch in Azure AD eingebunden. Auch wenn der Client nicht in Azure AD eingebunden ist, wird er dennoch verwaltet.
        >
        > Wenn Sie eine Tasksequenz zum Bereitstellen eines Betriebssystems auf einem internetbasierten Client ausführen, der entweder in Azure AD eingebunden ist oder die tokenbasierte Authentifizierung verwendet, müssen Sie die Eigenschaft **CCMHOSTNAME** im Schritt [Windows und ConfigMgr einrichten](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) angeben.

        In Version 2002 und früher werden Vorgänge, die ein Startmedium erfordern, mit dieser Einstellung nicht unterstützt. Verwenden Sie diese Option nur für generische Softwareinstallationen oder skriptbasierte Tasksequenzen, mit denen Vorgänge im Standardbetriebssystem ausgeführt werden.

        > [!NOTE]
        > Starten Sie für alle internetbasierten Tasksequenzszenarios die Tasksequenz aus dem Softwarecenter. Windows PE, PXE oder Tasksequenzmedien werden in diesen Szenarios nicht unterstützt.

8. Geben Sie auf der Seite **Warnungen** die für diese Tasksequenzbereitstellung gewünschten Warnungseinstellungen an.  

9. Geben Sie auf der Seite **Verteilungspunkte** die folgenden Informationen an:  

    - **Bereitstellungsoptionen**: Weitere Informationen finden Sie unter[Bereitstellungsoptionen](#bkmk_deploy-options).

    - **Remoteverteilungspunkt verwenden, wenn kein lokaler Verteilungspunkt verfügbar ist**: Geben Sie an, ob Verteilungspunkte über eine benachbarte Begrenzungsgruppe von Clients zum Herunterladen des Inhalts verwendet werden können, der für die Tasksequenz erforderlich ist.  

    - **Clients die Verwendung von Verteilungspunkten aus der Standard-Standortbegrenzungsgruppe gestatten**: Geben Sie an, ob Clients Inhalte von einem Verteilungspunkt in der standardmäßig festgelegten Standortbegrenzungsgruppe herunterladen dürfen, wenn der Inhalt nicht über einen Verteilungspunkt in den aktuellen oder benachbarten Begrenzungsgruppen verfügbar ist.  

        > [!Note]  
        > Wenn ein Gerät eine Tasksequenz ausführt und Inhalt abrufen muss, verwendet es ab Version 1810 ähnlich wie der Konfigurations-Manager-Client Verhaltensweisen von Begrenzungsgruppen. Weitere Informationen finden Sie unter [Tasksequenzunterstützung für Begrenzungsgruppen](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).<!--1359025-->  

10. Wenn Sie diese Einstellungen zur erneuten Verwendung speichern möchten, wählen Sie auf der Registerkarte **Zusammenfassung** die Option **Als Vorlage speichern** aus. Benennen Sie die Vorlage, und wählen Sie die Einstellungen aus, die gespeichert werden sollen.  

11. Schließen Sie den Assistenten ab.  

### <a name="deployment-options"></a><a name="bkmk_deploy-options"></a> Bereitstellungsoptionen

<!-- MEMDocs#328, SCCMDocs#2114 -->

Diese Optionen befinden sich auf der Registerkarte **Verteilungspunkte** der Tasksequenzbereitstellung. Sie sind dynamisch und basieren auf anderen Auswahlmöglichkeiten bei der Bereitstellung und den Attributen der Tasksequenz. Möglicherweise werden nicht alle Optionen angezeigt.

> [!NOTE]  
> Wenn Sie zum Bereitstellen eines Betriebssystems einen Multicast verwenden, laden Sie den Inhalt entweder je nach Bedarf oder vor Ausführung der Tasksequenz auf die Computer herunter.  

- **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist**: Geben Sie an, dass Clients den Inhalt vom Verteilungspunkt herunterladen, wenn dieser von der Tasksequenz benötigt wird. Der Client startet die Tasksequenz. Wenn ein Schritt in der Tasksequenz Inhalte benötigt, wird es heruntergeladen, bevor der Schritt ausgeführt wird.  

- **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen**: Geben Sie an, dass Clients den gesamten Inhalt vom Verteilungspunkt herunterladen, bevor die Tasksequenz ausgeführt wird. Wenn Sie auf der Seite **Bereitstellungseinstellungen** angegeben haben, dass die Tasksequenz für die Bereitstellung per PXE und Startmedien verfügbar ist, wird diese Option nicht angezeigt.  

- **Auf Inhalt direkt von einem Verteilungspunkt aus zugreifen, wenn er von der ausgeführten Tasksequenz benötigt wird**: Geben Sie an, dass Clients den Inhalt vom Verteilungspunkt ausführen. Diese Option ist nur verfügbar, wenn Sie alle der Tasksequenz zugeordneten Pakete für die Verwendung einer Paketfreigabe auf dem Verteilungspunkt aktivieren. Verwenden Sie für ein Paket unter **Eigenschaften** jeweils die Registerkarte **Datenzugriff** , um für Inhalte die Nutzung einer Paketfreigabe zu aktivieren.  

> [!IMPORTANT]  
> Aus Sicherheitsgründen empfiehlt es sich, die Option **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist** oder **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen** auszuwählen. Wenn Sie eine dieser Optionen auswählen, erstellt Configuration Manager einen Hashwert für das Paket, um die Paketintegrität gewährleisten zu können. Wenn Sie die Option **Auf Inhalt direkt von einem Verteilungspunkt aus zugreifen, wenn er von der ausgeführten Tasksequenz benötigt wird** auswählen, wird der Hashwert des Pakets vor dem Ausführen des angegebenen Programms nicht überprüft. Da die Paketintegrität in diesem Fall nicht gewährleistet werden kann, können Benutzer mit Administratorrechten Paketinhalte ändern oder manipulieren.  

#### <a name="example-1-one-deployment-option"></a>Beispiel 1: Eine Bereitstellungsoption

Sie stellen eine Tasksequenz zur Betriebssystembereitstellung bereit, die den Datenträger zurücksetzt und ein Image löscht. Auf der Seite **Bereitstellungseinstellungen** stellen Sie sie für eine Option zur Verfügung, die Medien und PXE umfasst:

:::image type="content" source="media/deploy-setting-make-available.png" alt-text="Bereitstellen der Tasksequenz und Option „Verfügbarmachen für“":::

Auf der Seite **Verteilungspunkte** gibt es nur eine Bereitstellungsoption:

- **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist**

:::image type="content" source="media/deploy-option-1.png" alt-text="Tasksequenz bereitstellen und eine Bereitstellungsoption":::

Die Option **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen** ist nicht verfügbar, da die Bereitstellung für Medien und PXE verfügbar gemacht wird.

Die Option **Auf Inhalt direkt von einem Verteilungspunkt aus zugreifen, wenn er von der ausgeführten Tasksequenz benötigt wird** ist ebenso nicht verfügbar. Nicht für alle Inhalte, auf die verwiesen wird, wird eine Paketfreigabe verwendet.

#### <a name="example-2-two-deployment-options"></a>Beispiel 2: Zwei Bereitstellungsoptionen

Sie stellen eine Tasksequenz zur Betriebssystembereitstellung bereit, die den Datenträger zurücksetzt und ein Image löscht. Auf der Seite **Bereitstellungseinstellungen** machen Sie sie für **Nur Configuration Manager-Clients** verfügbar. Auf der Seite **Verteilungspunkte** gibt es zwei Bereitstellungsoptionen:

- **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist**
- **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen**

:::image type="content" source="media/deploy-option-2.png" alt-text="Tasksequenz bereitstellen und zwei Bereitstellungsoptionen":::

Die Option **Auf Inhalt direkt von einem Verteilungspunkt aus zugreifen, wenn er von der ausgeführten Tasksequenz benötigt wird** ist ebenso nicht verfügbar. Nicht für alle Inhalte, auf die verwiesen wird, wird eine Paketfreigabe verwendet.

#### <a name="example-3-three-deployment-options"></a>Beispiel 3: Drei Bereitstellungsoptionen

Sie verfügen über mehrere Pakete mit administrativen Skripts und zugeordneten Inhalten. Auf der Registerkarte **Datenzugriff** der Paketeigenschaften können Sie alle Pakete für folgende Option konfigurieren: **Copy the content in this package to a package share on distribution points** (Den Inhalt in diesem Paket in eine Paketfreigabe auf Verteilungspunkten kopieren).

Sie erstellen eine Tasksequenz, die nur einige Schritte zum **Installieren von Paketen** für diese Skriptpakete besitzt, und stellen sie dann bereit. Auf der Seite **Bereitstellungseinstellungen** ist die einzige Option für das Verfügbarmachen **Nur Configuration Manager-Clients**. Diese Option ist die einzige verfügbare Option. Die Tasksequenz ist nicht für die Betriebssystembereitstellung vorgesehen, da ihr kein Startimage zugeordnet ist. Auf der Seite **Verteilungspunkte** gibt es drei Bereitstellungsoptionen:

- **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist**
- **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen**
- **Auf Inhalt direkt von einem Verteilungspunkt aus zugreifen, wenn er von der ausgeführten Tasksequenz benötigt wird**

:::image type="content" source="media/deploy-option-3.png" alt-text="Tasksequenz bereitstellen und drei Bereitstellungsoptionen":::

## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Bereitstellen eines direkten Upgrades für Windows 10 über das CMG

<!-- 1357149 -->
Die Tasksequenz für ein direktes Windows 10-Upgrade unterstützt jetzt die Bereitstellung auf internetbasierten Clients, die über [Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) verwaltet werden. Mit dieser Funktion können Remotebenutzer einfacher ein Upgrade auf Windows 10 durchführen, ohne eine Verbindung mit dem Intranet herstellen zu müssen.

Stellen Sie sicher, dass alle Inhalte, auf die von der Tasksequenz für das direkte Upgrade verwiesen wird, auf ein für Inhalte aktivierte CMG bereitgestellt wurden. (Aktivieren Sie die folgende [CMG-Einstellung](../../core/clients/manage/cmg/setup-cloud-management-gateway.md#settings): **Verwendung dieses Diensts als Cloudverteilungspunkt und zum Verarbeiten von Inhalt aus Azure Storage zulassen**.) Sie können auch einen [Cloudverteilungspunkt](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) verwenden. Andernfalls können die Geräte die Tasksequenz nicht ausführen.

Wenn Sie eine Upgradetasksequenz bereitstellen, verwenden Sie folgende Einstellungen:

- **Ausführung der Tasksequenz für internetbasierten Client zulassen** auf der Registerkarte „Benutzerfreundlichkeit“ der Bereitstellung.  

- Wählen Sie eine der folgenden Optionen auf der Registerkarte „Verteilungspunkte“ der Bereitstellung aus:

  - **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist** Ab Version 1910 kann die Tasksequenz-Engine Pakete bei Bedarf von einem für Inhalte aktivierten CMG oder einem Cloudverteilungspunkt herunterladen. Diese Änderung bietet noch mehr Flexibilität für Bereitstellungen von direkten Windows 10-Upgrades auf internetbasierten Geräten.<!--3601238-->

  - **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen** In Configuration Manager, Version 1906 und früher, funktionieren andere Optionen wie **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist** in diesem Szenario nicht. Die Tasksequenzengine kann Inhalte nicht aus einer Cloudquelle herunterladen. Der Configuration Manager-Client muss die Inhalte aus der Cloudquelle herunterladen, bevor die Tasksequenz gestartet wird. Sie können diese Option in der Version 1910 immer noch verwenden, wenn dies erforderlich ist, um Ihren Anforderungen zu entsprechen.

- (*Optional*) **Inhalt für diese Tasksequenz vorab herunterladen** auf der Registerkarte „Allgemein“ der Bereitstellung. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](configure-precache-content.md).  

> [!NOTE]
> Starten Sie die Tasksequenz aus dem Softwarecenter. Windows PE, PXE und Tasksequenzmedien werden in diesem Szenario nicht unterstützt.

## <a name="high-risk-deployments"></a><a name="bkmk_high-risk"></a> Verwalten risikoreicher Bereitstellungen

Bei einer Bereitstellung mit hohem Risiko wie z.B. einem Betriebssystem werden im Fenster **Sammlung auswählen** nur die benutzerdefinierten Sammlungen angezeigt, die den in den Eigenschaften des Standorts konfigurierten Einstellungen zur Bereitstellungsüberprüfung entsprechen. Bereitstellungen mit hohem Risiko sind immer auf benutzerdefinierte Sammlungen, von Ihnen erstellte Sammlungen und die integrierte Sammlung **Unbekannte Computer** beschränkt. Beim Erstellen einer Bereitstellung mit hohem Risiko können Sie keine integrierte Sammlung auswählen, wie z.B. **Alle Systeme**. Deaktivieren Sie die Option **Sammlungen mit einer Anzahl der Mitglieder, die größer als die minimale Größenkonfiguration des Standorts ist, ausblenden**, um alle benutzerdefinierten Sammlungen anzuzeigen, die weniger Clients als die konfigurierte maximale Größe enthalten. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments (Einstellungen zum Verwalten risikoreicher Bereitstellungen)](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Die Einstellungen zur Bereitstellungsüberprüfung basieren auf der aktuellen Mitgliedschaft der Sammlung. Nach der Bereitstellung der Tasksequenz bewertet Configuration Manager nicht erneut die Sammlungsmitgliedschaft für die Einstellungen für eine Bereitstellung mit hohem Risiko.  

Angenommen, Sie legen **Standardgröße** auf 100 und **Maximale Größe** auf 1000 fest. Wenn Sie eine Bereitstellung mit hohem Risiko erstellen, werden im Fenster **Sammlung auswählen** nur die Sammlungen angezeigt, die weniger als 100 Clients enthalten. Wenn Sie die Einstellung **Sammlungen mit einer Anzahl der Mitglieder, die größer als die minimale Größenkonfiguration des Standorts ist, ausblenden** deaktivieren, werden im Fenster Sammlungen angezeigt, die weniger als 1000 Clients enthalten.  

Wenn Sie eine Sammlung auswählen, die eine Standortrolle enthält, gilt folgendes Verhalten:  

- Wenn die Sammlung einen Standortsystemserver enthält und Sie die Einstellungen zur Bereitstellungsüberprüfung so konfigurieren, dass Sammlungen mit Standortsystemservern blockiert werden, tritt ein Fehler auf. Sie können in diesem Fall nicht mit dem Erstellen der Bereitstellung fortfahren.  

- Wenn eines der folgenden Kriterien zutrifft, zeigt der Assistent zum Bereitstellen von Software eine Warnung an, die auf ein hohes Risiko hinweist. Um fortzufahren, müssen Sie dem Erstellen einer Bereitstellung mit hohem Risiko zustimmen. Der Standort gibt anschließend eine Überwachungsstatusmeldung aus.  

  - Wenn die Sammlung einen Standortsystemserver enthält und Sie die Einstellungen zur Bereitstellungsüberprüfung so konfigurieren, dass bei Sammlungen mit Standortsystemservern eine Warnung angezeigt wird.  

  - Wenn die Sammlung den Standardwert für die Größe überschreitet.

  - Wenn die Sammlung einen Server enthält.  

## <a name="see-also"></a>Weitere Informationen:

[Verwalten von Tasksequenzen zum Automatisieren von Tasks](manage-task-sequences-to-automate-tasks.md)
