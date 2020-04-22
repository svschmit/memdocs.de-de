---
title: Funktionen in Technical Preview 1606
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1606 zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 05e7bbe6373ed91de5a2bb8e99a8425e733274f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705568"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Funktionen in der Technical Preview 1606 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1606 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen.      Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    

**Bekannte Probleme in dieser Technical Preview:**  
*  Wenn Sie Technical Preview 1604 auf 1605, und dann auf Version 1606 aktualisieren, schlägt das Update möglicherweise fehl, und ein Fehler ähnlich dem folgenden in der Datei **cmupdate.log** wird protokolliert:

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    In diesem Fall, klicken Sie im Knoten **Updates und Wartung** auf **Nach Updates suchen**, und **Wiederholen** Sie dann die Installation des Updates.
    ***

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a> Automatisches Kategorisieren von Geräten in Sammlungen
Sie können Gerätekategorien erstellen, mit denen Geräte automatisch in Gerätesammlungen platziert werden, wenn Sie Configuration Manager mit Microsoft Intune verwenden. Benutzer müssen eine Gerätekategorie auswählen, wenn sie ein Gerät in Intune registrieren. Sie können außerdem die Kategorie eines Geräts in der Configuration Manager-Konsole ändern.

**Wichtig:** Diese Funktion arbeitet mit dem **Juni 2016**-Release von Microsoft Intune. Stellen Sie sicher, dass Sie auf dieses Release aktualisiert haben, bevor Sie die Verfahren ausprobieren.

### <a name="try-it-out"></a>Probieren Sie es aus!

### <a name="create-a-set-of-device-categories"></a>Erstellen Sie einen Satz von Gerätekategorien
1.  Erweitern Sie **Überblick** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole, und klicken Sie dann auf **Gerätesammlungen**.
2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Kategorien** auf **Gerätekategorien verwalten**.
3.  Im Dialogfeld **Gerätekategorien verwalten** können Sie Kategorien erstellen, bearbeiten oder entfernen. Versuchen Sie, eine neue Kategorie zu erstellen.

### <a name="associate-a-collection-with-a-device-category"></a>Ordnen Sie eine Sammlung einer Gerätekategorie zu
Wenn Sie eine Sammlung zu einer Gerätekategorie zuordnen, werden alle Geräte in der von Ihnen angegebenen Kategorie zu dieser Sammlung hinzugefügt.
1.  Klicken Sie auf dem Dialogfeld für eine Gerätesammlung **Eigenschaften** auf **Regel hinzufügen** > **Gerätekategorieregel**.
2.  Wählen Sie im Dialogfeld **Mitgliedschaftsregel für die Gerätekategorie erstellen** die Kategorie aus, die auf alle Geräte in der Sammlung angewendet wird.
3.  Schließen Sie das Dialogfeld **Mitgliedschaftsregel für die Gerätekategorie auswählen** sowie das Dialogfeld Sammlungseigenschaften.

### <a name="change-the-category-of-a-device"></a>Ändern der Gerätekategorie
1.  Erweitern Sie den **Überblick** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole, und klicken Sie dann auf **Geräte**.
2.  Wählen Sie ein Gerät in der Liste **Geräte** aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Gerät** auf **Kategorie ändern**.
3.  Wählen Sie im Dialogfeld **Gerätekategorie bearbeiten** die Kategorie aus, die auf dieses Gerät angewendet werden soll, und klicken Sie dann auf **OK**.

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a> Erzwingung der Karenzzeit für erforderliche Anwendungen und Bereitstellungen von Softwareupdates

In einigen Fällen empfiehlt es sich, Benutzern mehr Zeit zum Installieren von erforderlichen Anwendungsbereitstellungen oder Softwareupdates, über die von Ihnen konfigurierten Fristen hinaus, zu geben. Dies kann erforderlich sein, wenn ein Computer für einen längeren Zeitraum ausgeschaltet war und eine große Anzahl von Anwendungs- oder Updatebereitstellungen installieren muss.
Wenn z.B. ein Benutzer gerade aus dem Urlaub zurückgekehrt ist, muss er möglicherweise sehr lange warten, bis überfällige Anwendungsbereitstellungen installiert sind.
Sie können jetzt eine zwingende Toleranzperiode definieren, um dieses Problem zu lösen. Dafür müssen Sie die Configuration Manager-Clienteinstellungen für eine Sammlung bereitstellen.

### <a name="try-it-out"></a>Probieren Sie es aus!

Führen Sie folgende Aktionen aus, um die Karenzzeit zu konfigurieren:

1.  Auf der Seite **Computer-Agent** der Clienteinstellungen müssen Sie die neue Eigenschaft **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** mit einem Wert zwischen **1** und **120** Stunden konfigurieren.
2.  Aktivieren Sie in einer neuen erforderlichen Anwendungsbereitstellung oder in den Eigenschaften einer vorhandenen Bereitstellung auf der Seite **Planung** das Kontrollkästchen **Erzwingung dieser Bereitstellung entsprechend den Benutzervoreinstellungen verzögern**, bis zu der Toleranzperiode, die in den Clienteinstellungen definiert ist.
Alle Bereitstellungen, für die dieses Kontrollkästchen ausgewählt ist, und die für Geräte vorgesehen sind, für die Sie ebenfalls die Clienteinstellungen bereitgestellt haben, werden die Toleranzperiode verwenden.

Wenn Sie eine Toleranzperiode konfigurieren und das Kontrollkästchen aktivieren, wird die Anwendung im ersten, nicht geschäftlichen Fenster installiert werden, das der Benutzer nach Ablauf der Frist konfiguriert. Der Benutzer kann jedoch weiterhin das Software Center öffnen und die Anwendung zu einem beliebigen Zeitpunkt installieren. Nach Ablauf der Toleranzperiode wird die Erzwingung auf normales Verhalten für überfällige Bereitstellungen zurückgesetzt.
Ähnliche Optionen wurden zum Bereitstellungsassistenten für Softwareupdates, zum Assistenten für automatische Bereitstellungsregeln und den Eigenschaftenseiten hinzugefügt.

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a>Verwendung von Configuration Manager als verwalteter Installer mit Device Guard

Device Guard ist ein Windows 10-Feature, das Hardware- und Software-Features verwendet, um genau zu kontrollieren, was zur Ausführung auf dem Gerät zulässig ist.

Eine ausführliche Übersicht über die Funktionsweise und die Aktionen von Device Guard finden Sie in diesem [Technet-Artikel](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview).

In diesem Release kann Configuration Manager mit Device Guard und [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) zusammenarbeiten, damit ausführbare und DLL-Dateien, die mit Configuration Manager bereitgestellt werden, automatisch als vertrauenswürdig eingestuft werden, da sie aus einem verwalteten Installationsprogramm stammen, d.h., sie können auf dem Zielgerät ausgeführt werden und andere Software nicht, außer wenn es durch andere AppLocker-Regeln zulässig gemacht wird.  

Diese Funktion kann derzeit nicht über die Configuration Manager-Konsole konfiguriert werden. Zum Konfigurieren der Richtlinie müssen Sie einen Registrierungsschlüssel auf jedem Client und Windows-Dienste auf dem Client konfigurieren.
Sobald dies geschehen ist, konfigurieren Sie die AppLocker-Richtliniendatei. Nachdem Sie die Richtliniendatei konfiguriert haben, können Sie sie auf allen kompatiblen Clientgeräten bereitstellen.


Wie alle AppLocker-Richtlinien können Richtlinien mit Manager Installer-Regeln in zwei Modi ausgeführt werden:

- Überwachungsmodus – Die Ausführung von Apps wird nicht verhindert, aber jede Anwendung, die blockiert worden wäre, wird in einer Protokolldatei gemeldet (Dies wird in einer späteren Release von Configuration Manager unterstützt).
- Erzwingung aktiviert – Die Ausführung von Anwendungen wird blockiert.

Weitere Informationen zur Verwendung von Device Guard mit Configuration Manager finden Sie auf dem [Enterprise Mobility und Security-Blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10).

Weitere Informationen:

- [Einführung zu Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Device Guard-Zertifizierung und -Kompatibilität](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Device Guard-Bereitstellungshandbuch](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a> Verschiedene Geräteverwaltungspunkte für die lokale Verwaltung mobiler Geräte  
  Mit Technical Preview 1606 unterstützt die lokale Verwaltung mobiler Geräte (MDM) jetzt eine neue Funktion im Windows 10 Anniversary Update, die ein registriertes Gerät automatisch konfiguriert, um mehr als einen Geräteverwaltungspunkt zur Verwendung zur Verfügung zu haben. Diese Funktion lässt Fallbacks des Geräts auf einen anderen Geräteverwaltungspunkt zu, wenn der normalerweise verwendete Punkt nicht verfügbar ist. Diese Funktion ist nur auf PCs verfügbar, auf denen das Windows 10 Anniversary Update installiert ist.  

### <a name="try-it-out"></a>Probieren Sie es aus!  

1.  Installieren Sie mehr als einen Geräteverwaltungspunkt in Ihrer Hierarchie.  

2.  Registrieren Sie ein Gerät mit einem Windows 10 Anniversary Update für die lokale Verwaltung mobiler Geräte.  

Informationen zum Vorbereiten Ihres Standorts und zur Registrierung von Geräten für die lokale Verwaltung mobiler Geräte, finden Sie unter [Lokale Verwaltung mobiler Geräte (MDM)](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a>Cloudproxydienst für die Verwaltung von Clients im Internet

Der Cloudproxydienst bietet eine einfache Möglichkeit zum Verwalten von Configuration Manager-Clients im Internet. Der Dienst, der in Microsoft Azure bereitgestellt wird und ein Azure-Abonnement erfordert, stellt mithilfe einer neuen Rolle namens Cloudproxy-Connectorpunkt eine Verbindung mit Ihrer lokalen Configuration Manager-Infrastruktur her. Nachdem er bereitgestellt und konfiguriert wurde, können Clients auf lokale Configuration Manager-Standortsystemrollen zugreifen, unabhängig davon, ob sie mit dem internen, privaten Netzwerk oder über das Internet verbunden sind.

Sie verwenden die Configuration Manager-Konsole zum Bereitstellen des Diensts in Azure, fügen die Cloudproxy-Connectorpunktrolle hinzu und konfigurieren Standortsystemrollen, damit sie den Cloudproxy-Datenverkehr zulassen. Der Cloudproxydienst unterstützt derzeit nur den Verwaltungspunkt, den Verteilungspunkt und Softwareupdatepunktrollen.

Client-Zertifikate und Zertifikate für Secure Socket Layer (SSL) sind erforderlich, um Computer zu authentifizieren und die Kommunikation zwischen den verschiedenen Ebenen des Diensts verschlüsseln. In der Regel erhalten die Clientcomputer ein Clientzertifikat über das Durchsetzen von Gruppenrichtlinien. Zum Verschlüsseln des Datenverkehrs zwischen Clients und Standortsystemserver, der die Rollen hostet, müssen Sie ein benutzerdefiniertes SSL-Zertifikat von der Zertifizierungsstelle erstellen. Zusätzlich zu diesen beiden Zertifikattypen müssen Sie auch ein Verwaltungszertifikat in Azure einrichten, mit dem Configuration Manager den Cloudproxydienst bereitstellen kann.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Anforderungen für den Cloudproxydienst in TP 1606
- Clientcomputer und der Standortsystemserver führen den Cloudproxy-Connectorpunkt aus.
- Benutzerdefinierte SSL-Zertifikate von der internen Zertifizierungsstelle ‒ Werden zum Verschlüsseln der Kommunikation der Clientcomputer und zum Authentifizieren der Identität des Clouddiensts verwendet.
- Azure-Abonnement für Clouddienste.
- Azure-Verwaltungszertifikat ‒ Wird zur Authentifizierung von Configuration Manager mit Azure verwendet.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Einschränkungen des Cloudproxydiensts in TP 1606

- Unterstützt nur den Verwaltungspunkt, den Verteilungspunkt und Softwareupdatepunktrollen.
- Benutzerrichtlinien werden nicht unterstützt.
- Kann nicht mit [Lokale Verwaltung mobiler Geräte](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) in Configuration Manager verwendet werden.
- Nur auf der öffentlichen Cloudplattform von Azure unterstützt.


### <a name="try-it-out"></a>Probieren Sie es aus!

Der Prozess für die Bereitstellung des Cloudproxydienstes umfasst die folgenden Schritte:

1. Erstellen Sie ein benutzerdefiniertes SSL-Zertifikat und stellen Sie es für den Cloudproxydienst zur Verfügung.
1. Exportieren Sie den Stamm des Clientzertifikats.
2. Laden Sie das Verwaltungszertifikat in Azure hoch.
3. Richten Sie den Cloudproxydienst in der Configuration Manager-Konsole ein.
4. Konfigurieren Sie den primären Standort für die Nutzung der Clientzertifikatauthentifizierung.
5. Fügen Sie den Cloudproxy-Connectorpunkt zu Ihrem Standort hinzu.
6. Konfigurieren Sie die Standortsystemrollen, damit sie Cloudproxy-Datenverkehr akzeptieren.

Die folgenden Abschnitte enthalten weitere Informationen zu diesen Schritten.

#### <a name="create-a-custom-ssl-certificate"></a>Erstellen Sie ein benutzerdefiniertes SSL-Zertifikat

Sie können ein benutzerdefiniertes SSL-Zertifikat für den Cloudproxydienst auf die gleiche Weise erstellen, wie Sie bei einem cloudbasierten Verteilungspunkt vorgehen würden. Führen Sie die Anweisungen zum [Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) durch, tun Sie jedoch folgende Dinge anders:

* Geben Sie beim Einrichten der Zertifikatvorlage die Berechtigungen **Lesen** und **Registrieren** für die Sicherheitsgruppe an, die Sie für Configuration Manager-Server einrichten.

#### <a name="export-the-client-certificates-root"></a>Exportieren Sie das Clientstammzertifikat

Die einfachste Möglichkeit zum Export der Clientstammzertifikate im Netzwerk ist, ein Clientzertifikat auf einem Computer zu öffnen und zu kopieren, der einer Domäne angehört, und der über eines verfügt.

>[!NOTE]
>Clientzertifikate sind auf jedem Computer erforderlich, den Sie mit dem Cloudproxydienst verwalten möchten und auf jedem Standortsystemserver, der den Cloudproxy-Connectorpunkt hostet. Wenn Sie jedem dieser Computer ein Clientzertifikat hinzufügen müssen, finden Sie mehr Informationen unter [Bereitstellen des Clientzertifikats für Windows-Computer](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).

1. Geben Sie im Ausführungsfenster **Mmc** ein, und drücken Sie die Eingabetaste.
2. Klicken Sie in der Verwaltungskonsole im Menü „Datei“ auf **Snap-In hinzufügen/entfernen…** .
3. Klicken Sie im Dialogfeld „Snap-Ins hinzufügen bzw. entfernen“ auf **Zertifikate**, auf **Hinzufügen >** , klicken Sie auf **Computerkonto**, klicken Sie auf **Weiter**, klicken Sie auf **Lokaler Computer**, und klicken Sie dann auf **Fertig stellen**. Klicken Sie auf **OK** , um das Dialogfeld zu schließen.
4. Wechseln Sie zu **Zertifikate > Privat > Zertifikate**.
5. Doppelklicken Sie auf das Zertifikat zur Clientauthentifizierung auf dem Computer, klicken Sie auf die Registerkarte „Zertifizierungspfad“, und doppelklicken Sie auf die Stammzertifizierungsstelle (am Anfang des Pfades).
6.  Klicken Sie auf der Registerkarte „Details“, und klicken Sie auf **In Datei kopieren...** .
7. Schließen Sie den Zertifikatexportassistenten ab, indem Sie das Standardzertifikatformat verwenden. Notieren Sie sich den Namen und den Speicherort des Stammzertifikats, das Sie erstellen. Sie benötigen es zum Konfigurieren des Cloudproxydiensts in einem späteren Schritt.

#### <a name="upload-the-management-certificate-to-azure"></a>Laden Sie das Verwaltungszertifikat in Azure hoch

Ein Azure-Verwaltungszertifikat ist für Configuration Manager erforderlich, um auf die Azure-API zugreifen und den Cloudproxydienst zu konfigurieren. Weitere Informationen und Anweisungen zum Hochladen eines Verwaltungszertifikats finden Sie unter den folgenden Artikeln in der Azure-Dokumentation:
- [Übersicht über Zertifikate für Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Hochladen eines Verwaltungszertifikats für die Azure-Verwaltung-API](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Stellen Sie sicher, dass Sie die Abonnement-ID kopieren, die dem Verwaltungszertifikat zugeordnet ist. Sie werden Sie zum Konfigurieren des Cloudproxydiensts in der Configuration Manager-Konsole benötigen.

#### <a name="set-up-cloud-proxy-service"></a>Einrichten des Cloudproxydiensts

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung > Clouddienste > Cloudproxydienst**.
2. Klicken Sie auf **Cloudproxydienst erstellen** .
3. Geben Sie im Assistenten zur Erstellung von Cloudproxydiensten Ihre Azure-Abonnement-ID (aus dem Azure-Verwaltungsportal kopiert) ein, klicken Sie auf „Durchsuchen“, und wählen Sie die Zertifikatdatei aus, die Sie als Azure-Verwaltungszertifikat hochgeladen haben. Klicken Sie auf **Weiter**. Warten Sie einige Augenblicke, bis sich die Konsole mit Azure verbindet.
4. Füllen Sie die zusätzlichen Details im Assistenten aus:
    - Geben Sie den privaten Schlüssel (PFX-Datei) an, den Sie aus dem benutzerdefinierten SSL-Zertifikat exportiert haben.
    - Geben Sie das aus dem Clientzertifikat exportierte Stammzertifikat an.
    - Geben Sie den gleichen FQDN-Dienstnamen an, den Sie bei der Erstellung der neuen Zertifikatvorlage verwendet haben.
    - Deaktivieren Sie das Kontrollkästchen **Clientzertifikatsperre überprüfen** (es sei denn, Sie veröffentlichen Ihre CRL-Informationen).
    - Klicken Sie auf **Weiter**, wenn Sie fertig sind.
5. Überprüfen Sie die Einstellungen, und klicken Sie auf **Weiter**. Configuration Manager beginnt mit der Einrichtung des Diensts. Wenn der Assistent abgeschlossen ist, können Sie auf **Schließen** klicken, aber es wird 5 bis 15 Minuten dauern, um den Dienst vollständig in Azure bereitzustellen. Überprüfen Sie die Spalte **Status** für den neu eingerichteten Cloudproxydienst, um zu bestimmen, wann der Dienst bereit ist.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Konfigurieren des primären Standorts für die Clientzertifikatauthentifizierung

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung > Standortkonfiguration > Standorte**.
2. Wählen Sie den primären Standort für die Clients aus, die Sie über den Cloudproxydienst verwalten möchten, und klicken Sie auf **Eigenschaften**.
3. Aktivieren Sie das Kontrollkästchen neben **Use PKI client certificate (client authentication) when available**  (PKI-Clientzertifikat (Clientauthentifizierung) verwenden, sofern verfügbar) auf der Registerkarte Clientcomputerkommunikation im Eigenschaftenblatt für den primären Standort.
4. Stellen Sie sicher, dass Sie das Kontrollkästchen neben **Die Zertifikatsperrliste für Standortsysteme wird von Clients überprüft**  deaktivieren. Diese Option wäre nur erforderlich, wenn Sie Ihre CRL veröffentlichen würden.
5. Klicken Sie auf **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Hinzufügen des Cloudproxy-Connectorpunkts

Der Verbindungspunkt für den Cloudproxy-Connectorpunkt ist eine neue Standortsystemrolle für die Kommunikation mit dem Cloudproxydienst. Wenn Sie den Cloudproxy-Connectorpunkt hinzufügen möchten, führen Sie die Anweisungen unter [Hinzufügen von Standortsystemrollen für Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md) aus.

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Konfigurieren von Rollen für Cloudproxy-Datenverkehr

Der letzte Schritt bei der Einrichtung des Cloudproxydiensts ist das Konfigurieren der Standortsystemrollen zum Akzeptieren des Cloudproxy-Datenverkehrs. Für Tech Preview 1606 werden nur der Verwaltungspunkt, der Verteilungspunkt und Softwareupdatepunktrollen für den Cloudproxydienst unterstützt. Sie müssen jede Rolle einzeln konfigurieren.

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung > Standortkonfiguration > Server und Standortsystemrollen**.
2. Klicken Sie auf dem Standortsystemserver auf die Rolle, die Sie für den Cloudproxy-Datenverkehr konfigurieren möchten.
3. Klicken Sie auf die Rolle und danach auf **Eigenschaften**.
4. Wählen Sie auf der Eigenschaftenseite der Rolle unter „Clientverbindungen“ **HTTPS** aus, aktivieren Sie das Kontrollkästchen neben **Datenverkehr über Configuration Manager-Cloudproxy zulassen**, und klicken Sie dann auf **OK**. Wiederholen Sie diese Schritte für die übrigen Rollen.

#### <a name="check-status-on-a-client-on-the-internet"></a>Überprüfen des Status auf einem Client im Internet

Nachdem der Dienst und die Rollen vollständig konfiguriert sind, erhalten interne Clients den Speicherort des Cloudproxydiensts bei der nächsten Speicherortanfrage. Clients mit aktualisierten Speicherortinformationen können dann mit Configuration Manager über das Internet kommunizieren. Der Abfragezyklus für Standortanfragen beträgt 24 Stunden. Wenn Sie nicht auf die normal geplante Standortanfragen warten möchten, können Sie sie erzwingen, indem Sie den SMS-Agent-Hostdienst (ccmexec.exe) auf dem Computer neustarten.

Nachdem Clients die neue Speicherortinformationen für Cloudproxydienst haben, überprüfen Sie den Status der Clients, die nicht mehr auf dem internen privaten Netzwerk sind, aber Zugriff auf das Internet haben. Sie können Datenverkehr auf dem Cloudproxydienst auch überwachen, indem Sie auf **Verwaltung > Clouddienste > Cloudproxydienst** den Dienst im Listenbereich auswählen und die Informationen zum Datenverkehr im Detailbereich anzeigen.   

## <a name="manage-the-office-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a>Verwaltung des Office 365-Client-Agents in Configuration Manager  

Ab Technical Preview 1606 können Sie eine Configuration Manager-Client-Agenteinstellung anstatt der Gruppenrichtlinie verwenden, um Office 365-Clients zum Empfangen von Updates von Configuration Manager zu aktivieren. Nachdem Sie diese Einstellung konfiguriert und Updates für Office 365 bereitgestellt haben, kommuniziert der Configuration Manager-Client-Agent mit dem Office 365-Client-Agent, um Office 365-Updates von einem Verteilungspunkt herunterzuladen und zu installieren. Configuration Manager macht auch eine Bestandsaufnahme der Client-Agenteinstellungen.

Weitere Informationen finden Sie unter [Verwalten von Office 365 ProPlus-Updates](https://technet.microsoft.com/library/mt741983.aspx).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Einrichten der Configuration Manager-Clienteinstellung, zum Verwalten des Office 365-Client-Agents
1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Übersicht** > **Clienteinstellungen**.
2. Öffnen Sie die entsprechenden Geräteeinstellungen zum Aktivieren des Client-Agents. Weitere Informationen zum Konfigurieren von Standard- und benutzerdefinierten Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md).
3. Klicken Sie auf **Softwareupdates** und wählen Sie **Ja** für die Einstellung **Verwaltung des Office 365-Client-Agents aktivieren** aus.  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a>Die Tasksequenzvariable „OSDPreserveDriveLetter“ wurde als veraltet markiert.
Die Tasksequenzvariable „OSDPreverveDriveLetter“ bestimmt, ob die Tasksequenz bei der Anwendung des Images auf einen Zielcomputer den in der WIM-Datei des Betriebssystemimages erfassten Laufwerkbuchstaben verwendet.
- Die Tasksequenzvariable wurde in Technical Preview 1606 als veraltet markiert.

Während einer standardmäßigen Betriebssystembereitstellung bestimmt Windows Setup den Laufwerkbuchstaben, der am besten zur Verwendung geeignet ist (in der Regel C:). Wenn Sie ein anderes Laufwerk zur Verwendung angeben möchten, können Sie den Speicherort im Tasksequenzschritt „Betriebssystem anwenden“ ändern. Wechseln Sie zur Einstellung **Wählen Sie den Standort aus, an dem Sie dieses Betriebssystem anwenden möchten.** , wählen Sie **Bestimmter Buchstabe für logisches Laufwerk**  aus und wählen Sie das Laufwerk aus, das Sie verwenden möchten. Sie müssen dem gewählten Buchstaben auf dem Zielcomputer ein Laufwerk zuordnen. 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a>Änderungen am Knoten „Updates und Wartung“
Mit Technical Preview 1606 wurden mehrere Änderungen eingeführt, die für Updates und Wartung in der Configuration Manager-Konsole gelten:
- **Änderung des Knotennamen:**

    Im Arbeitsbereich **Überwachung** wurde der Knoten **Wartungsstatus des Standorts** in **Update- und Wartungsstatus** umbenannt.
- **Erweiterung des Installationsstatus:**

    Wenn Sie den Updateinstallationsstatus für einen Standort anzeigen, zeigt die Konsole nun die Details zu den folgenden Aktionen getrennt an:
    - **Herunterladen** (Dies gilt nur für den Standort der obersten Ebene, auf dem die Standortsystemrolle des Dienstverbindungspunkts installiert ist)
    - **Replikation**
    - **Prüfung der erforderlichen Komponenten**
    - **Installation**

  Darüber hinaus stehen jetzt detailliertere Informationen zu jedem Schritt zur Verfügung, z.B. in welcher Protokolldatei Sie weitere Informationen finden.  
-   **Neue Option zum Wiederholen von Fehlern der erforderlichen Komponente:**

    In den Arbeitsbereichen **Verwaltung** und **Überwachung** enthält der Knoten **Updates und Wartung** eine neue Schaltfläche auf dem Menüband mit der Bezeichnung **Warnungen der erforderlichen Komponente ignorieren**.

    Wenn Sie Updates installieren, ohne die Option „Warnungen der erforderlichen Komponente ignorieren“ (innerhalb des Update-Assistenten) zu verwenden, und diese Updateinstallation im Status der **Warnung der erforderlichen Komponente** stoppt, können Sie **Warnungen der erforderlichen Komponente ignorieren** aus dem Menüband auswählen, um eine automatische Fortsetzung dieser Updateinstallation auszulösen, bei der die Warnungen der erforderlichen Komponente ignoriert werden.  



- **Übersichtlichere Ansicht der Updates:**

    Wenn Sie den Knoten **Updates und Wartung** anzeigen, sehen Sie jetzt nur noch die zuletzt installierten Updates, und alle neuen Updates, die zur Installation für Sie bereitstehen. Wenn Sie bereits installierte Updates anzeigen möchten, klicken Sie auf die neue Schaltfläche **Verlauf**, die im Menüband erscheint.  

-   **Umbenannte Option für die Präproduktion:**

    Auf dem Knoten „Updates und Wartung“ wurde die Schaltfläche **Clientoptionen** in **Präproduktionsclient höher stufen** umbenannt.
