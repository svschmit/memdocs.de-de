---
title: Benutzerfunktionen für die Betriebssystembereitstellung
titleSuffix: Configuration Manager
description: Hier erfahren Sie mehr über die Funktionen für Benutzer wie beispielsweise den Tasksequenzstatus und Medien-Assistent für die Betriebssystembereitstellung in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f92e76047a70f6d86406b1a364603163d902e62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703218"
---
# <a name="user-experiences-for-os-deployment"></a>Benutzerfunktionen für die Betriebssystembereitstellung

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie eine [Tasksequenz bereitgestellt haben](../deploy-use/deploy-a-task-sequence.md), gibt es je nach Szenario verschiedene Möglichkeiten für Benutzer, mit der Bereitstellung zu interagieren. In diesem Artikel werden die wichtigsten Benutzerfunktionen für Betriebssystembereitstellungen und deren Konfiguration erläutert:

- Benutzerbenachrichtigung des Softwarecenters für eine Bereitstellung mit hohem Einfluss
- Beispiel für PXE-Startfunktion
- Tasksequenz-Assistent für Medien
- Statusfenster beim Ausführen der Tasksequenz
- Fenster zum Anzeigen von Fehlern bei fehlerhafter Ausführung der Tasksequenz

## <a name="software-center"></a>Software Center

Bei einer Bereitstellung mit hohem Einfluss können Sie die im Softwarecenter angezeigte Nachricht anpassen. Wenn der Benutzer die Betriebssystembereitstellung im Softwarecenter öffnet, wird eine Meldung ähnlich der folgenden angezeigt:

![Benutzerdefinierte Tasksequenzbenachrichtigung für den Endbenutzer im Softwarecenter](../media/user-notification-enduser.png)

Weitere Informationen zum Anpassen der Nachricht in diesem Fenster finden Sie unter [Erstellen einer benutzerdefinierten Benachrichtigung für risikoreiche Bereitstellungen](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments).

Sie können den Organisationsnamen auch am oberen Rand des Fensters anpassen. (Das obige Beispiel zeigt den Standardwert `IT Organization`). Ändern Sie die Clienteinstellung **Organisationsname** in der Gruppe **Computer-Agent**. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../core/clients/deploy/about-client-settings.md#computer-agent).

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

Weitere Informationen finden Sie unter [Verwenden von Softwarecenter zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md).

## <a name="pxe"></a>PXE

Verschiedene Hardwaremodelle bieten unterschiedliche Funktionen für PXE. UEFI-basierte Geräte verwenden für den Netzwerkstart in der Regel den `Enter`-Schlüssel und BIOS-basierte Geräte den `F12`-Schlüssel.

Das folgende Beispiel zeigt die PXE-Funktion Hyper-V Gen1 (BIOS):

![BIOS-PXE-Beispielbildschirm eines virtuellen Hyper-V-Computers](media/hyperv-pxe.png)

Nachdem das Gerät erfolgreich über PXE gestartet wurde, verhält es sich ähnlich wie startbare Medien. Weitere Informationen finden Sie im nächsten Abschnitt über den [Tasksequenz-Assistenten](#task-sequence-wizard).

Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

> [!WARNING]
> Wenn Sie PXE-Bereitstellungen verwenden und Gerätehardware mit dem Netzwerkadapter als erstes Startgerät konfigurieren, können diese Geräte automatisch und ohne Benutzerinteraktion eine Tasksequenz für die Betriebssystembereitstellung starten. Diese Konfiguration wird nicht durch die Bereitstellungsüberprüfung verwaltet. Während diese Konfiguration möglicherweise den Prozess vereinfachen und die Benutzerinteraktion reduzieren kann, erhöht sie das Risiko, dass für das Gerät versehentlich ein Reimaging durchgeführt wird.

## <a name="task-sequence-wizard"></a>Tasksequenz-Assistent

Wenn Sie [Tasksequenzmedien](../deploy-use/create-task-sequence-media.md) verwenden, wird der Tasksequenz-Assistent ausgeführt, um den Prozess zu steuern.

### <a name="welcome-to-the-task-sequence-wizard"></a>Willkommen beim Tasksequenz-Assistenten

![Screenshot: Hauptseite des Tasksequenz-Assistenten](media/welcome-task-sequence-wizard.png)

- Wenn Sie Medien mit Kennwörtern schützen, muss der Benutzer auf dieser Willkommensseite das Kennwort eingeben.

- Klicken Sie auf **Netzwerkeinstellungen konfigurieren**, um eine statische IP-Adresse oder andere benutzerdefinierte Netzwerkeinstellungen anzugeben. Andernfalls verwendet das Gerät standardmäßig ein DHCP.

- Klicken Sie auf **Proxyeinstellungen konfigurieren**, wenn Ihr Netzwerk einen Proxy erfordert.

### <a name="select-a-task-sequence-to-run"></a>Auswählen einer auszuführenden Tasksequenz

Wenn Sie mehr als eine Tasksequenz auf dem Gerät bereitstellen, wird diese Seite angezeigt, um eine Tasksequenz auszuwählen. Stellen Sie sicher, dass Sie einen Namen und eine Beschreibung für die Tasksequenz verwenden, die von Benutzern verstanden werden können.

![Screenshot: Seite zum Auswählen der Tasksequenz im Tasksequenz-Assistenten](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>Bearbeiten von Tasksequenzvariablen

Wenn Tasksequenzvariablen leere Werte aufweisen, zeigt der Assistent eine Seite an, auf der die Variablenwerte bearbeitet werden können.

![Screenshot: Seite zum Bearbeiten von Tasksequenzvariablen im Tasksequenz-Assistenten](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>Prestart-Befehle

Sie können Tasksequenzmedien oder Startimages anpassen, um einen Prestart-Befehl auszuführen. Ein Prestart-Befehl wird vor dem Starten der Tasksequenz ausgeführt. Dies sind häufig verwendete Aktionen:

- Auffordern des Benutzers, dynamische Werte wie den Computernamen einzugeben
- Angeben der Netzwerkkonfiguration
- Festlegen einer Benutzeraffinität

Beim Prestart-Befehl handelt es sich um eine Befehlszeile, die Sie mit einem Skript oder Programm angeben. Die Benutzerfunktion ist für das Skript oder Programm eindeutig.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Prestart-Befehle für Tasksequenzmedien](prestart-commands-for-task-sequence-media.md)
- [Verwalten von Startimages](../get-started/manage-boot-images.md#customization)
- [Tasksequenzmedien](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>Tasksequenzstatus

Wenn die Tasksequenz ausgeführt wird, wird das Fenster **Installationsstatus** angezeigt:

![Beispiel für Fenster zum Tasksequenzstatus](media/task-sequence-progress.png)

- Dieses Fenster befindet sich immer im Vordergrund. Sie können es zwar verschieben, allerdings nicht schließen oder minimieren.

- Sie können den Organisationsnamen am oberen Rand des Fensters anpassen. (Das obige Beispiel zeigt den Standardwert `IT Organization`). Ändern Sie die Clienteinstellung **Organisationsname** in der Gruppe **Computer-Agent**. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../core/clients/deploy/about-client-settings.md#computer-agent).

    > [!TIP]
    > Die Tasksequenz speichert diesen Wert in der schreibgeschützten Variablen [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName).

- Sie können die Unterüberschrift anpassen. (Das obige Beispiel zeigt den Standardwert `Running: <task sequence name>`). Klicken Sie für den Statusbenachrichtigungstext in den Eigenschaften der Tasksequenz auf die Option **Benutzerdefinierten Text verwenden**. Sie können maximal 255 Zeichen verwenden.

- **Aktion wird ausgeführt:** In der ersten Zeile wird der Name des aktuellen Tasksequenzschritts angezeigt. Die Statusanzeige darunter zeigt den Gesamtstatus der Tasksequenz an.

- In der zweiten Zeile werden nur einige Schritte mit detaillierteren Informationen zum Status angezeigt.

- Verwenden Sie die Tasksequenzvariable [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI), um zu steuern, wann die Tasksequenz den Status anzeigt.

    Deaktivieren Sie die Option **Tasksequenzstatus anzeigen** auf der Seite **Benutzerfreundlichkeit** der Tasksequenzbereitstellung, um das Statusfenster vollständig zu deaktivieren.

Ab Version 2002 weist das Fenster für den Tasksequenzstatus die folgenden Verbesserungen auf:<!--5932692-->

- Es werden die aktuelle Schrittnummer, die Gesamtzahl der Schritte und der Fortschritt in Prozent angezeigt.

- Vergrößern der Breite des Fensters, um mehr Platz zu schaffen, damit der Name der Organisation in einer einzelnen Zeile besser angezeigt werden kann

![Beispiel für Fenster zum Tasksequenzstatus](media/2356386-task-sequence-progress.png)

Standardmäßig wird im Fenster zum Tasksequenzstatus der vorhandene Text verwendet. Wenn Sie keine Änderungen vornehmen, funktioniert dies weiterhin wie in Version 1910 bzw. vorherigen Versionen. Geben Sie die Tasksequenzvariable [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel) an, um die neuen Statusinformationen anzuzeigen.

Die Anzahl der abgeschlossenen Aktionen und der Fortschritt in Prozent sind nur als allgemeiner Leitfaden gedacht. Diese Werte basieren auf der Gesamtanzahl der Schritte in der Tasksequenz. Bei einer komplexeren Tasksequenz mit Schritten, die basierend auf der Logik der Tasksequenz ausgeführt werden, ist der Fortschritt möglicherweise nicht linear.

Die Gesamtanzahl von Schritten enthält keine der folgenden Elemente in der Tasksequenz:

- Gruppen. Dieses Element ist selbst kein Schritt, sondern ein Container für andere Schritte.

- Instanzen des Schritts **Tasksequenz ausführen**. Dieser Schritt ist ein Container für andere Schritte.

- Schritte, die von Ihnen explizit deaktiviert werden. Ein deaktivierter Schritt wird während der Tasksequenz nicht ausgeführt.

    > [!NOTE]
    > Aktivierte Schritte in einer deaktivierten Gruppe sind in der Gesamtanzahl weiterhin enthalten.

## <a name="task-sequence-error"></a>Tasksequenzfehler

Wenn bei der Tasksequenz ein Fehler auftritt, wird das Fenster **Tasksequenzfehler** angezeigt.

![Beispiel eines Fensters für einen Tasksequenzfehler](media/task-sequence-error.png)

- Sie passen die Headerinformationen genauso an wie das Fenster zum Tasksequenzstatus.

- Es zeigt den Namen der Tasksequenz, einen Fehlercode und eine allgemeine Meldung für Benutzer an. Beispiel: `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- Das Fenster wird nach einem Timeoutzeitraum automatisch geschlossen. Der Standardwert für Timeouts beträgt 15 Minuten. Sie können diesen Wert mit der Tasksequenzvariablen [SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout) anpassen.
