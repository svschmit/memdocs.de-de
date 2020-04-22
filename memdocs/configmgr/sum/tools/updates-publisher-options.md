---
title: Konfigurieren von Optionen
titleSuffix: Configuration Manager
description: Konfigurieren der Optionen für die Verwendung von System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b6578e32d5ae5a003c485960b556f3b87e8d557
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700068"
---
# <a name="configure-options-for-updates-publisher"></a>Konfigurieren der Optionen für Updates Publisher

*Gilt für: System Center Updates Publisher*

Überprüfen und konfigurieren Sie die Optionen und zugehörigen Einstellungen, die Auswirkungen auf den Einsatz von Updates Publisher haben.

Klicken Sie zum Zugriff auf die Updates Publisher-Optionen in der oberen linken Ecke der Konsole auf die Registerkarte **Eigenschaften** von **Updates Publisher**, und wählen Sie dann **Optionen** aus.

![Optionen](media/properties1.png)   


Die Optionen sind folgendermaßen unterteilt:

-   -Updateserver
-   ConfigMgr-Server
-   Proxyeinstellungen
-   Vertrauenswürdige Herausgeber
-   Erweitert
-   Updates
-   Protokollierung

## <a name="update-server"></a>-Updateserver
Sie müssen Updates Publisher für den Einsatz mit Updateservern wie Windows Server Update Services (WSUS) konfigurieren, bevor Sie [Updates veröffentlichen](manage-updates-with-updates-publisher.md#publish-updates-and-bundles-from-the-updates-workspace) können. Dies umfasst die Angabe des Servers sowie von Methoden zum Herstellen der Verbindung mit diesem Server, wenn er sich auf einem anderen Computer als die Konsole befindet, und eines Zertifikats zum digitalen Signieren von Updates, die Sie veröffentlichen.

- **Konfigurieren eines Updateservers**. Wenn Sie einen Updateserver konfigurieren, wählen Sie den WSUS-Server (Updateserver) auf oberster Ebene in Ihrer Configuration Manager-Hierarchie aus, sodass alle untergeordneten Standorte auf die Updates zugreifen können, die Sie veröffentlichen.

  Wenn Ihr Updateserver sich auf einem anderen Computer als Ihr Updates Publisher-Server befindet, geben Sie den vollständig qualifizierten Domänennamen (FQDN) des Servers ein, und ob Sie SSL zum Herstellen der Verbindung verwenden. Beim Herstellen der Verbindung mit SSL ändert sich der Standardport von 8530 in 8531. Stellen Sie sicher, dass der Port, den Sie festlegen, dem entspricht, was von Ihrem Updateserver verwendet wird.

  > [!TIP]  
  > Wenn Sie keinen Updateserver konfigurieren, können Sie Updates Publisher dennoch zum Erstellen von Softwareupdates verwenden.

- **Konfigurieren Sie das Signaturzertifikat**. Sie müssen einen Updateserver konfigurieren und erfolgreich eine Verbindung mit ihm herstellen, bevor Sie das Signaturzertifikat konfigurieren können.

  Updates Publisher verwendet das Signaturzertifikat, um die Softwareupdates zu signieren, die auf dem Updateserver veröffentlicht werden. Bei der Veröffentlichung tritt ein Fehler auf, wenn das digitale Zertifikat nicht im Zertifikatspeicher des Updateservers oder des Computers, der Updates Publisher ausführt, verfügbar ist.

  Weitere Informationen zum Hinzufügen des Zertifikats zum Zertifikatspeicher finden Sie unter [Certificates and security for Updates Publisher](updates-publisher-security.md) (Zertifikate und Sicherheit für Updates Publisher).

  Wenn ein digitales Zertifikat nicht automatisch für den Updateserver erkannt wird, wählen Sie eine der folgenden Optionen:

  -   **Durchsuchen**: Diese Option ist nur verfügbar, wenn der Updateserver auf dem Server installiert ist, auf dem Sie die Konsole ausführen. Nach Auswahl eines Zertifikats müssen Sie **Erstellen** auswählen, um dieses Zertifikat dem WSUS-Zertifikatspeicher auf dem Updateserver hinzuzufügen. Sie müssen das **PFX**-Dateikennwort für Zertifikate eingeben, die Sie mit dieser Methode auswählen.

  -   **Erstellen**: Erstellen Sie mit dieser Option ein neues Zertifikat. Hiermit wird das Zertifikat auch dem WSUS-Zertifikatspeicher auf dem Updateserver hinzugefügt.

  **Wenn Sie Ihr eigenes Signaturzertifikat erstellen**, konfigurieren Sie Folgendes:

  -   Aktivieren Sie die Option **Exportieren von privatem Schlüssel zulassen**.

  -   Legen Sie für **Schlüsselverwendung** die digitale Signatur fest.

  -   Legen Sie für **Minimale Schlüsselgröße** einen Wert von mindestens 2.048 Bit fest.

  Verwenden Sie die Option **Entfernen** zum Entfernen eines Zertifikats aus dem WSUS-Zertifikatspeicher. Diese Option ist verfügbar, wenn Updateserver und Updates Publisher-Konsole auf dem lokalen Computer installiert sind, oder wenn Sie **SSL** zum Herstellen der Verbindung mit einem Remoteupdateserver verwendet haben.

## <a name="configmgr-server"></a>ConfigMgr-Server
Verwenden Sie diese Optionen, wenn Sie Configuration Manager mit Updates Publisher verwenden.

-   **Specify the Configuration Manager server** (Festlegen des Configuration Manager-Servers): Geben Sie nach dem Aktivieren der Unterstützung von Configuration Manager den Standort des Servers der obersten Ebene in Ihrer Configuration Manager-Hierarchie an. Wenn dieser Server sich auf einem anderen Computer als die Updates Publisher-Installation befindet, geben Sie den FQDN des Standortservers ein. Wählen Sie **Verbindung testen**, um sicherzustellen, dass Sie eine Verbindung mit dem Standortserver herstellen können.

-   **Konfigurieren von Schwellenwerten**: Schwellenwerte werden beim Veröffentlichen von Updates mit dem Veröffentlichungstyp „Automatisch“ verwendet. Mit den Schwellenwerten können Sie bestimmen, wann der vollständige Inhalt für ein Update und nicht nur die Metadaten veröffentlicht werden. Informationen über weitere Veröffentlichungstypen finden Sie unter [Assign updates to a publication](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) (Zuweisen von Updates zu einer Veröffentlichung).

    Sie können einen oder beide der folgenden Schwellenwerte festlegen:

    -   **Requested client count threshold** (Angeforderter Schwellenwert für die Clientanzahl): Dieser Wert definiert, wie viele Clients ein Update anfordern müssen, bevor Updates Publisher automatisch den vollständigen Satz von Inhalten für das Update veröffentlichen kann. Bis die angegebene Anzahl von Clients das Update anfordert, werden nur die Metadaten veröffentlicht.

    -   **Package source size threshold Paket** (Paketquellengrößen-Schwellenwert [MB]): Dies verhindert die automatische Veröffentlichung von Updates, die die von Ihnen angegebene Größe überschreiten. Wenn die Größe der Updates diesen Wert überschreitet, werden nur die Metadaten veröffentlicht. Bei Updates, die die angegebene Größe unterschreiten, kann der vollständige Inhalt veröffentlicht werden.

## <a name="proxy-settings"></a>Proxyeinstellungen
Updates Publisher verwendet die Proxyeinstellungen beim Importieren von Softwarekatalogen aus dem Internet oder Veröffentlichen von Updates im Internet.

-   Geben Sie den FQDN oder die IP-Adresse eines Proxyservers an. IPv4 und IPv6 werden unterstützt.

-   Wenn der Proxyserver Benutzer für den Internetzugriff authentifiziert, müssen Sie den Windows-Namen angeben. Ein Universal Principle Name (UPN) wird nicht unterstützt.

## <a name="trusted-publishers"></a>Vertrauenswürdige Herausgeber
Beim Importieren eines Updatekatalogs wird die Quelle des betreffenden Katalogs (basierend auf seinem Zertifikat) als vertrauenswürdiger Herausgeber hinzugefügt. Ebenso wird beim Veröffentlichen eines Updates die Quelle des Updatezertifikats als vertrauenswürdiger Herausgeber hinzugefügt.

Sie können Zertifikatdetails für jeden Herausgeber anzeigen und einen Herausgeber aus der Liste der vertrauenswürdigen Herausgeber entfernen.

Inhalte von Herausgebern, die nicht vertrauenswürdig sind, können potenziell Clientcomputer bei der Überprüfung auf Updates beschädigen. Akzeptieren Sie nur Inhalte von Herausgebern, denen Sie vertrauen.

## <a name="advanced"></a>Erweitert
Zu den erweiterten Optionen zählen:

-   **Repository location** (Repository-Speicherort): Anzeigen und Ändern des Speicherorts der Datenbankdatei **scupdb.sdf**. Diese Datei ist das Repository für Updates Publisher.

-   **Zeitstempel**: Bei Aktivierung wird den Updates, die Sie signieren, ein Zeitstempel hinzugefügt, der den Zeitpunkt der Signierung angibt. Ein Update, das signiert wurde, während ein Zertifikat gültig war, kann verwendet werden, nachdem das Signaturzertifikat abgelaufen ist. Standardmäßig können Softwareupdates nicht bereitgestellt werden, nachdem ihr Signaturzertifikat abgelaufen ist.

-   **Check for updates to subscribed catalogs** (Nach Updates abonnierter Kataloge suchen): Bei jedem Start kann Updates Publisher automatisch nach Updates von Katalogen suchen, die Sie abonniert haben. Wenn ein Katalog gefunden wird, werden Details wie **Letzte Warnungen** im Fenster **Übersicht** des **Arbeitsbereichs „Updates“** bereitgestellt.

-   **Certificate revocation** (Sperren von Zertifikaten): Wählen Sie diese Option, um Überprüfungen bezüglich des Sperrens von Zertifikaten zu ermöglichen.

-   **Local source publishing** (Veröffentlichen aus lokaler Quelle): Updates Publisher kann eine lokale Kopie eines Updates verwenden, die Sie veröffentlichen, bevor Sie das Update aus dem Internet herunterladen. Der Speicherort muss ein Ordner auf dem Computer sein, der Updates Publisher ausführt. Dieser Speicherort ist standardmäßig **Eigene Dokumente\LocalSourcePublishing**. Verwenden Sie diese Option, wenn Sie zuvor ein oder mehrere Updates heruntergeladen haben, oder Änderungen an einem Update vorgenommen haben, das Sie bereitstellen möchten.

-   **Software Updates Cleanup Wizard** (Assistent zum Bereinigen von Softwareupdates): Starten des Assistenten zum Bereinigen von Updates. Der Assistent lässt Updates ablaufen, die sich auf dem Updateserver, aber nicht im Updates Publisher-Repository befinden. Weitere Informationen finden Sie unter [Ablaufen nicht referenzierter Softwareupdates](#expire-unreferenced-software-updates).

## <a name="updates"></a>Updates
 Updates Publisher kann bei jedem Öffnen automatisch nach neuen Updates suchen. Wahlweise können Sie auch Vorschaubuilds von Updates Publisher empfangen.

Um manuell nach Updates zu suchen, klicken Sie in der Updates Publisher-Konsole auf ![Eigenschaften](media/properties2.png),  
um die **Updates Publisher-Eigenschaften** zu öffnen, und wählen Sie dann **Nach Update suchen**.

Wenn Update Publisher ein neues Update findet, wird das Fenster **Update verfügbar** angezeigt, und Sie können es dann zur Installation auswählen. Wenn Sie das Update nicht installieren möchten, wird es Ihnen beim nächsten Öffnen der Konsole angeboten.

## <a name="logging"></a>Protokollierung
Updates Publisher protokolliert grundlegende Informationen zu Updates Publisher unter **%WINDIR%\Temp\UpdatesPublisher.log**.

Verwenden Sie den Editor oder **CMTrace** zum Anzeigen des Protokolls. Das Configuration Manager-Protokollanzeigetool CMTrace finden Sie im Ordner **\SMSSetup\Tools** der Configuration Manager-Quellmedien.

Sie können die Größe des Protokolls und seinen Detaillierungsgrad ändern.

Wenn Sie die Datenbankprotokollierung aktivieren, werden Informationen zu den Abfragen einbezogen, die an die Updates Publisher-Datenbank gerichtet werden. Die Verwendung der Datenbankprotokollierung kann die Leistung des Updates Publisher-Computers beeinträchtigen.

Klicken Sie zur Anzeige der Protokolldatei in der Konsole auf ![Eigenschaften](media/properties2.png), um die **Updates Publisher-Eigenschaften** zu öffnen, und wählen Sie dann **Protokolldatei anzeigen**.

## <a name="expire-unreferenced-software-updates"></a>Ablaufen nicht referenzierter Softwareupdates
Sie können den **Software Update Cleanup Wizard** (Assistenten zum Bereinigen von Softwareupdates) ausführen, um Updates auslaufen zu lassen, die sich auf Ihrem Updateserver, aber nicht im Updates Publisher-Repository befinden. Dies benachrichtigt Configuration Manager, worauf diese Updates aus zukünftigen Bereitstellungen entfernt werden.

Das Ablaufen eines Updates kann nicht rückgängig gemacht werden. Führen Sie diese Aufgabe nur aus, wenn Sie sicher sind, dass die ausgewählten Softwareupdates nicht mehr in Ihrer Organisation erforderlich sind.

### <a name="to-remove-expired-software-updates"></a>So entfernen Sie abgelaufene Softwareupdates
1.  Klicken Sie in der Updates Publisher-Konsole auf ![Eigenschaften](media/properties2.png), um die **Updates Publisher-Eigenschaften** zu öffnen, und wählen Sie dann **Optionen**.

2.  Wählen Sie **Erweitert** und dann unter **Software Update Clean Wizard** (Softwareupdatebereinigungs-Assistent) **Starten**.

3.  Wählen Sie die Softwareupdates aus, die Sie ablaufen lassen möchten, und dann **Weiter**.

4.  Wählen Sie nach Überprüfen Ihrer Auswahl **Weiter**, um die Auswahl zu akzeptieren und diese Updates ablaufen zu lassen.

5.  Wählen Sie nach der Ausführung durch den Assistenten **Schließen**, um den Assistenten abzuschließen.
