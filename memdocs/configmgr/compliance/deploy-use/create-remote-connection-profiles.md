---
title: Erstellen von Remoteverbindungsprofilen
titleSuffix: Configuration Manager
description: Verwenden Sie Remoteverbindungsprofile für Configuration Manager, um Ihren Benutzern das Herstellen einer Remoteverbindung zu Ihren Arbeitscomputern zu ermöglichen.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: f9f4e1ffe8b28efda0f59e6a252f39c95e2b7749
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240115"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Remoteverbindungsprofile in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Configuration Manager-Remoteverbindungsprofile, um Ihren Benutzern das Herstellen einer Remoteverbindung zu ihrem Arbeitscomputer zu ermöglichen. Mithilfe dieser Profile können Sie Remotedesktopverbindungseinstellungen für Benutzer in Ihrer Hierarchie bereitstellen. Benutzer können über Remotedesktop über eine VPN-Verbindung auf ihren primären Arbeitscomputer zugreifen.  

> [!IMPORTANT]  
> Wenn Sie Remoteverbindungsprofileinstellungen mithilfe von Configuration Manager angeben, speichert der Client die Einstellungen in der lokalen Windows-Richtlinie. Durch diese Einstellungen können die mithilfe einer anderen Anwendung konfigurierten Remotedesktopeinstellungen überschrieben werden. Wenn Sie die Remotedesktopeinstellungen mit der Windows-Gruppenrichtlinie konfigurieren, werden mit den in der Gruppenrichtlinie angegebenen Einstellungen außerdem die Configuration Manager-Einstellungen überschrieben.

Configuration Manager erstellt eine Sicherheitsgruppe auf Clients: **Remote PC Connect**. Wenn Sie ein Remoteverbindungsprofil bereitstellen, fügt der Client die primären Benutzer des Computers dieser Gruppe hinzu. Ein lokaler Administrator kann dieser Gruppe Benutzer manuell hinzufügen oder sie aus ihr entfernen. Configuration Manager aktualisiert die Mitgliedschaft jedoch erst bei der nächsten Auswertung der Konformität des Profils.

> [!IMPORTANT]  
> Wenn sich die Affinitätsbeziehung zwischen Benutzer und Gerät ändert, deaktiviert Configuration Manager das Remoteverbindungsprofil und die Windows-Firewalleinstellungen, um Verbindungen mit dem Computer zu verhindern.

## <a name="prerequisites"></a>Voraussetzungen  

### <a name="external-dependencies"></a>Externe Abhängigkeiten  

- Wenn Sie Benutzern das Herstellen einer Verbindung über das Internet ermöglichen möchten, installieren und konfigurieren Sie einen Remotedesktop-Gatewayserver. Weitere Informationen zum Installieren und Konfigurieren eines Remotedesktop-Gatewayservers finden Sie unter [Remotedesktopdienste – ortsunabhängiger Zugriff](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere).

- Wenn auf Clients eine hostbasierte Firewall ausgeführt wird, muss die Ausführung von „mstsc.exe“ zugelassen sein. Beim Konfigurieren eines Remoteverbindungsprofils müssen Sie die Einstellung **Windows-Firewallausnahme für Verbindungen in Windows-Domänen und privaten Netzwerken zulassen** aktivieren. Mit dieser Einstellung kann Configuration Manager die Windows-Firewall automatisch konfigurieren.

    > [!TIP]
    > Durch die Gruppenrichtlinieneinstellungen für die Konfiguration der Windows-Firewall kann die in Configuration Manager eingerichtete Konfiguration außer Kraft gesetzt werden. Wenn Sie zum Konfigurieren der Windows-Firewall eine Gruppenrichtlinie verwenden, sollten Sie sicherstellen, dass die entsprechenden Einstellungen die Ausführung von „mstsc.exe“ nicht blockieren.

    Wird auf den Clients eine andere hostbasierte Firewall ausgeführt, müssen Sie die betreffende Firewallabhängigkeit manuell konfigurieren.  

### <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

- Benutzer können nur dann eine Verbindung mit einem Arbeitscomputer herstellen, wenn es sich bei dem betreffenden Computer um das primäre Gerät des Benutzers handelt. Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

- Zum Verwalten von Remoteverbindungsprofilen benötigt das Benutzerkonto bestimmte Berechtigungen in Configuration Manager. Die integrierte Rolle **Konformitätseinstellungs-Manager**  verfügt über die Berechtigungen, die zum Verwalten dieser Profile erforderlich sind. Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="security-and-privacy-considerations"></a>Überlegungen zu Sicherheit und Datenschutz

### <a name="security-considerations"></a>Sicherheitsüberlegungen  

- Geben Sie manuell die Affinität zwischen Benutzer und Gerät an, statt zuzulassen, dass die Benutzer das primäre Gerät selbst bestimmen. Aktivieren Sie nicht die nutzungsbasierte Konfiguration.

  - Bevor Sie ein Remoteverbindungsprofil bereitstellen können, müssen Sie die Option **Allen primären Benutzern des Arbeitscomputers Remoteverbindungen gestatten** aktivieren. Für diese Konfiguration sollten Sie die Affinität zwischen Benutzer und Gerät immer manuell angeben. Betrachten Sie Informationen, die Configuration Manager von Benutzern oder Geräten erfasst, nicht als maßgeblich. Wenn Sie ein Profil bereitstellen und ein vertrauenswürdiger Administrator nicht die Affinität zwischen Benutzer und Gerät angibt, erhalten nicht autorisierte Benutzer möglicherweise erhöhte Berechtigungen und können eine Remoteverbindung zu Computern herstellen.

  - Configuration Manager sammelt nutzungsbasierte Informationen über Zustandsmeldungen, bei denen es sich um einen schnellen, aber unsicheren Kommunikationskanal handelt. Sie können diese Bedrohung durch SMB-Signaturen (Server Message Block) oder IPsec (Internet Protocol Security) zwischen Clientcomputern und dem Verwaltungspunkt verringern.

- Schränken Sie lokale Administratorrechte auf dem Standortservercomputer ein. Ein lokaler Administrator für den Standortserver kann der Sicherheitsgruppe **Remote PC Connect**, die von Configuration Manager automatisch erstellt und verwaltet wird, manuell Mitglieder hinzufügen. Diese Aktion kann zu einer Erhöhung von Berechtigungen führen, da Mitglieder Remotedesktopberechtigungen erhalten.

### <a name="privacy-considerations"></a>Überlegungen zum Datenschutz  

Wenn ein Benutzer eine Remoteverbindung zu einem Arbeitscomputer herstellt, wird eine WSRDP-Datei heruntergeladen. Diese Datei enthält den Gerätenamen und den Namen des Remotedesktop-Gatewayservers. Diese Werte sind erforderlich, um die Remotedesktopsitzung zu erstellen. Die WSRDP-Datei wird heruntergeladen und automatisch lokal gespeichert. Bei der nächsten Ausführung einer Remotedesktopverbindung wird die Datei überschrieben.  

## <a name="create-a-profile"></a>Erstellen eines Profils

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, erweitern Sie **Konformitätseinstellungen**, und wählen Sie **Remoteverbindungsprofile** aus.  

1. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Remoteverbindungsprofil erstellen** aus.  

1. Geben Sie im **Assistenten zum Erstellen von Remoteverbindungsprofilen** auf der Seite **Allgemein** einen Namen und optional eine Beschreibung für das Profil ein. Beide Werte dürfen 256 Zeichen nicht überschreiten.  

1. Geben Sie auf der Seite **Profileinstellungen** die folgenden Einstellungen an:  

    - **Vollständiger Name und Port des Remotedesktop-Gatewayservers (optional):** Geben Sie den Namen des Remotedesktop-Gatewayservers an, der für Verbindungen verwendet werden soll. Für diesen Wert bestehen die folgenden Anforderungen:

        - Der Servername darf nicht länger als 256 Zeichen sein.
        - Er kann Großbuchstaben, Kleinbuchstaben und numerische Zeichen enthalten.
        - Abgesehen von den Punkten (`.`) zwischen Segmenten und einem Doppelpunkt (`:`) vor dem Port sind die einzigen Sonderzeichen Bindestriche (`–`) und Unterstriche (`_`).
        - Configuration Manager unterstützt nicht die Verwendung von internationalisierten Domänennamen für diesen Wert.

    - **Verbindungen nur von Computern zulassen, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebene ausgeführt wird**: Diese Einstellung ist standardmäßig aktiviert und bietet eine zusätzliche Sicherheitsebene für die Verbindung. Weitere Informationen finden Sie unter [Sollte ich Remotedesktop aktivieren?](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication)

    - Aktivieren Sie die folgenden Verbindungseinstellungen:

        - **Remoteverbindungen mit Arbeitscomputern zulassen**

        - **Allen primären Benutzern des Arbeitscomputers Remoteverbindungen gestatten**

        - **Windows-Firewallausnahme für Verbindungen in Windows-Domänen und privaten Netzwerken zulassen**

        > [!IMPORTANT]  
        > Alle drei Einstellungen müssen identisch sein, bevor Sie fortfahren können.

        Deaktivieren Sie diese Einstellungen nur bei der Bereitstellung eines Profil, um Remoteverbindungen zu deaktivieren.

1. Schließen Sie den Assistenten ab.

Das neue Profil wird im Arbeitsbereich **Bestand und Konformität** im Knoten **Remoteverbindungsprofile** angezeigt.  

## <a name="deploy"></a>Bereitstellen

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, erweitern Sie **Konformitätseinstellungen**, und wählen Sie **Remoteverbindungsprofile** aus.

1. Wählen Sie in der Liste **Remoteverbindungsprofile** das Profil aus, das Sie bereitstellen möchten. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Bereitstellung** die Option **Bereitstellen** aus.  

1. Geben Sie im Fenster **Remoteverbindungsprofil bereitstellen** die folgenden Informationen an:

    - **Sammlung:** Wählen Sie die Gerätesammlung aus, in der Sie das Profil bereitstellen möchten.

    - **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird:** Aktivieren Sie diese Einstellung, damit die Profileinstellungen automatisch wiederhergestellt werden, wenn sie nicht mit einem Gerät konform sind. Das Profil kann z. B. nicht konform sein, wenn es nicht vorhanden ist.

    - **Wiederherstellung außerhalb des Wartungsfensters zulassen:** Wenn Sie ein Wartungsfenster für die Sammlung konfigurieren, in der Sie das Profil bereitstellen, aktivieren Sie diese Option, damit Configuration Manager das Profil außerhalb des Wartungsfensters wiederherstellen kann. Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).

    - **Warnung generieren:** Aktivieren Sie diese Option, um eine Konformitätswarnung zu konfigurieren.

    - **Geben Sie den Zeitplan für die Kompatibilitätsauswertung dieser Konfigurationsbasislinie an**: Geben Sie einen einfachen oder benutzerdefinierten Zeitplan an, nach dem der Client das Profil auswertet.

1. Wählen Sie **OK** aus, um das Fenster zu schließen und die Bereitstellung zu erstellen.

### <a name="client-evaluation"></a>Clientauswertung

Der Client wertet das Profil aus, wenn sich ein Benutzer anmeldet.

Wenn ein Gerät aus einer Sammlung entfernt wird, in der Sie ein Remoteverbindungsprofil bereitstellen, deaktiviert Configuration Manager die Einstellungen auf dem Gerät. Dieser Vorgang kann jedoch nur dann ordnungsgemäß ausgeführt werden, wenn Sie zuvor wenigstens ein Konfigurationselement oder eine Konfigurationsbasislinie bereitgestellt haben, die ein Konfigurationselement von Ihrem Standort enthält.

### <a name="conflict-resolution"></a>Konfliktauflösung

Stellen Sie nicht mehr als ein Remoteverbindungsprofil mit in Konflikt stehenden Einstellungen auf demselben Gerät bereit. Beispielsweise können Sie zwei Profile mit unterschiedlichen Einstellungen für dieselbe Sammlung bereitstellen. Sie aktivieren die Einstellung **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird** nur für eine Profilbereitstellung. Diese Bereitstellung kann die Einstellungen im anderen Profil überschreiben. Diese Art der Bereitstellung eines Remoteverbindungsprofils wird von Configuration Manager nicht unterstützt.

## <a name="monitor"></a>Überwachen

Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie **Bereitstellungen** aus. Wählen Sie in der Liste **Bereitstellungen** die Remoteverbindungsprofilbereitstellung aus.

Zusammenfassende Informationen zur Kompatibilität der Bereitstellung der Remoteverbindungsprofile finden Sie auf der Hauptseite. Klicken Sie auf die Profilbereitstellung, wenn weitere Informationen angezeigt werden sollen. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Bereitstellung** dann die Option **Status anzeigen** aus. Mit dieser Aktion wird die Seite **Bereitstellungsstatus** geöffnet.  

Auf der Seite **Bereitstellungsstatus** sind die folgenden Registerkarten enthalten:  

- **Konform**: Hiermit wird die Kompatibilität des Remoteverbindungsprofils basierend auf der Anzahl der betroffenen Bestände angezeigt.

    > [!IMPORTANT]  
    > Der Client wertet ein Remoteverbindungsprofil nur aus, wenn es zulässig ist. Es wird jedoch dennoch als konform gekennzeichnet.

- **Fehler**: Hiermit wird eine Liste aller Fehler für die ausgewählte Bereitstellung des Remoteverbindungsprofils basierend auf der Anzahl der betroffenen Bestände angezeigt.

- **Nicht konform**: Hiermit wird eine Liste aller nicht kompatiblen Regeln im Remoteverbindungsprofil basierend auf der Anzahl der betroffenen Bestände angezeigt.

- **Unbekannt**: Hiermit wird eine Liste aller Geräte angezeigt, von denen keine Konformität der ausgewählten Bereitstellung des Remoteverbindungsprofils gemeldet wurde, zusammen mit dem aktuellen Clientstatus der Geräte.

Öffnen Sie in einer beliebigen Registerkarte eine Regel, um im Arbeitsbereich **Bestand und Konformität** einen temporären Unterknoten unter dem Knoten **Benutzer** zu erstellen. Dieser Unterknoten enthält alle Geräte der ausgewählten Registerkarte mit dem jeweiligen Konformitätszustand.

Im Bereich **Bestandsdetails** werden die Geräte mit dem ausgewählten Konformitätszustand für das Profil angezeigt. Öffnen Sie ein Gerät in der Liste, damit weitere Informationen angezeigt werden.

## <a name="reports"></a>Berichte

Configuration Manager enthält integrierte Berichte, mit deren Hilfe Sie Informationen zu Remoteverbindungsprofilen überwachen können. Diese Berichte verfügen über die Berichtskategorie **Kompatibilitäts- und Einstellungsverwaltung**.  

> [!IMPORTANT]  
> Verwenden Sie ein Platzhalterzeichen (`%`), wenn Sie in den Berichten zu Konformitätseinstellungen die Parameter **Gerätefilter** und **Benutzerfilter** eingestellt haben.  

Weitere Informationen zum Konfigurieren der Berichterstellung in Configuration Manager finden Sie unter [Einführung in die Berichterstellung](../../core/servers/manage/introduction-to-reporting.md).  
