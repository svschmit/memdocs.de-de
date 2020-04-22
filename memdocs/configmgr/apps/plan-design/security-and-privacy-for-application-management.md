---
title: Sicherheit und Datenschutz für Apps
titleSuffix: Configuration Manager
description: Anleitungen und Empfehlungen für Sicherheit und Datenschutz bei der Anwendungsverwaltung in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f7085b7ee6f0f723c9bcf9d10cb85b03f990a44
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689068"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Sicherheit und Datenschutz für die Anwendungsverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

## <a name="security-guidance-for-application-management"></a>Sicherheitsempfehlungen für die Anwendungsverwaltung  

### <a name="use-the-software-center-without-the-application-catalog"></a>Verwenden des Softwarecenters ohne den Anwendungskatalog

<!--1358309-->

Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Mit dieser Konfiguration können Sie die Serverinfrastruktur reduzieren, die zum Bereitstellen von Anwendungen für Benutzer erforderlich ist.

Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Das Vereinfachen der Serverinfrastruktur verringert außerdem die Angriffsfläche.

Verwenden Sie Azure Active Directory und Cloud Management Gateway, um eine konsistente und sichere Anwendungsumgebung für internetbasierte Clients zu gewährleisten.

Weitere Informationen finden Sie unter [Konfigurieren des Softwarecenters](plan-for-software-center.md#bkmk_userex).

### <a name="use-https-with-the-application-catalog"></a>Verwenden von HTTPS mit dem Anwendungskatalog

> [!Important]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Konfigurieren Sie den Anwendungskatalog-Websitepunkt und den Anwendungskatalog-Webdienstpunkt so, dass diese HTTPS-Verbindungen akzeptieren. Mit dieser Konfiguration wird der Server für Benutzer authentifiziert. Die übertragenen Daten sind geschützt, sodass sie weder manipuliert noch angezeigt werden können.

Sie können Social Engineering-Angriffen vorbeugen, indem Sie die Benutzer dazu anhalten, nur Verbindungen mit vertrauenswürdigen Websites herzustellen. Informieren Sie Ihre Benutzer über die Gefahren schädlicher Websites.

Wenn Sie HTTPS nicht verwenden, nutzen Sie nicht die Konfigurationsoptionen für das Branding. Diese Einstellungen zeigen den Namen Ihrer Organisation im Anwendungskatalog als Identitätsnachweis an.  


### <a name="use-role-separation"></a>Verwenden der Rollentrennung

> [!Important]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Installieren Sie den Anwendungskatalog-Websitepunkt und den Anwendungskatalog-Webdienstpunkt auf unterschiedlichen Servern. Wenn der Websitepunkt kompromittiert ist, ist der Webdienstpunkt dann nicht davon betroffen. Diese Vorgehensweise trägt zum Schutz der Konfigurations-Manager-Clients und der Infrastruktur bei. Diese Konfiguration ist vor allem dann wichtig, wenn der Websitepunkt Clientverbindungen aus dem Internet akzeptiert. Das macht den Server anfällig für Angriffe.  

### <a name="close-browser-windows"></a>Schließen des Browserfensters

> [!Important]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Halten Sie die Benutzer dazu an, nach Verwendung des Anwendungskatalogs das Browserfenster zu schließen. Wenn Benutzer eine externe Website in dem gleichen Browserfenster aufrufen wie zuvor den Anwendungskatalog, werden die Sicherheitseinstellungen für vertrauenswürdige Orte im Intranet vom Browser beibehalten.  

### <a name="centrally-specify-user-device-affinity"></a>Zentrales Angeben der Affinität zwischen Benutzer und Gerät

Geben Sie die Affinität zwischen Benutzer und Gerät manuell an, anstatt zuzulassen, dass Benutzer ihr primäres Gerät selbst angeben. Aktivieren Sie nicht die nutzungsbasierte Konfiguration.

Betrachten Sie Informationen, die von Benutzern oder Geräten erfasst werden, nicht als maßgeblich. Wenn Sie Software mithilfe der Affinität zwischen Benutzer und Gerät bereitstellen, die nicht von einem vertrauenswürdigen Administrator angegeben wurde, ist eine Installation der Software auf Computern und für Benutzer möglich, die nicht zum Erhalt der Software autorisiert sind.  

### <a name="dont-run-deployments-from-distribution-points"></a>Kein Bereitstellen über Verteilungspunkte

Konfigurieren Sie Bereitstellungen stets so, dass Inhalt nicht auf den Verteilungspunkten ausgeführt, sondern nur von ihnen heruntergeladen wird. Wenn Sie Bereitstellungen so konfigurieren, dass Inhalt von Verteilungspunkten heruntergeladen und lokal ausgeführt wird, wird der Hashwert des Pakets nach dem Herunterladen zunächst auf dem Configuration Manager-Client überprüft. Wenn der Hash nicht mit dem Hash in der Richtlinie übereinstimmt, verwirft der Client das Paket.

Wenn Sie die Bereitstellung so konfigurieren, dass sie direkt auf einem Verteilungspunkt ausgeführt wird, wird der Pakethash nicht vom Konfigurations-Manager-Client überprüft. Dadurch kann der Konfigurations-Manager-Client manipulierte Software installieren.

Wenn Sie Bereitstellungen direkt auf Verteilungspunkten ausführen müssen, verwenden Sie die niedrigsten NTFS-Berechtigungen für die Pakete auf den Verteilungspunkten. Sichern Sie den Kanal zwischen dem Client und den Verteilungspunkten sowie zwischen den Verteilungspunkten und dem Standortserver zudem mithilfe von IPsec (Internetprotokollsicherheit).

### <a name="dont-let-users-interact-with-elevated-processes"></a><a name="bkmk_interact"></a> Vermeiden der Interaktion zwischen Benutzern und Prozessen mit erhöhten Rechten
  
Wenn Sie die Option **Mit Administratorrechten ausführen** oder **Für System installieren** aktivieren, lassen Sie Benutzer nicht mit diesen Anwendungen interagieren. Beim Konfigurieren einer Anwendung können Sie als Option **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren** festlegen. Mit dieser Einstellung können Benutzer auf alle Aufforderungen reagieren, die auf der Benutzeroberfläche angezeigt werden. Wenn Sie außerdem als Anwendungskonfiguration **Mit Administratorrechten ausführen** festlegen oder ab Version 1802 die Einstellung **Für System installieren** verwenden, kann ein Angreifer auf dem Computer, auf dem das Programm ausgeführt wird, die Benutzeroberfläche verwenden, um die Berechtigungen für den Clientcomputer auszuweiten.

Verwenden Sie für Softwarebereitstellungen, für die Administratoranmeldeinformationen erforderlich sind, Programme, die Windows Installer für das Setup und benutzerbezogen erhöhte Rechte verwenden. Das Setup muss im Kontext eines Benutzers ausgeführt werden, der über keine Administratoranmeldeinformationen verfügt. Die Verwendung von benutzerspezifisch erhöhten Windows Installer-Rechten stellt die sicherste Möglichkeit dar, Anwendungen mit dieser Anforderung bereitzustellen.

### <a name="restrict-whether-users-can-install-software-interactively"></a>Einschränken von Benutzertypen zur interaktiven Installation von Software

Konfigurieren Sie in der Gruppe **Computer-Agent** die Clienteinstellung **Installationsberechtigungen**. Mit dieser Einstellung schränken Sie die Benutzertypen ein, die Software im Softwarecenter installieren dürfen.

Erstellen Sie beispielsweise eine benutzerdefinierte Clienteinstellung, indem Sie für **Installationsberechtigungen** die Einstellung **Nur Administratoren**festlegen. Wenden Sie diese Clienteinstellung auf eine Auflistung von Servern an. Diese Konfiguration verhindert, dass Benutzer ohne Administratorrechte Software auf diesen Servern installieren.  

### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>Stellen Sie für mobile Geräte nur Anwendungen bereit, die signiert sind.

Stellen Sie Anwendungen für mobile Geräte nur bereit, wenn diese über eine Codesignatur von einer Zertifizierungsstelle (ZS) verfügen, die das jeweilige Gerät als vertrauenswürdig einstuft.

Beispiel:

- Eine Anwendung eines Anbieters, die von einer bekannten Zertifizierungsstelle wie VeriSign signiert ist  

- Eine interne Anwendung, die Sie unabhängig von Configuration Manager von einer eigenen Zertifizierungsstelle signieren lassen  

- Eine interne Anwendung, die Sie mithilfe von Configuration Manager signieren, wenn Sie den Anwendungstyp erstellen und ein Signaturzertifikat verwenden

### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>Sichern des Speicherorts des Signaturzertifikats der mobilen App

Wenn Sie Anwendungen für mobile Geräte mithilfe des **Assistenten zum Erstellen von Anwendungen** in Configuration Manager signieren, sichern Sie den Speicherort der Signaturzertifikatdatei sowie den Kommunikationskanal. Speichern Sie als Schutz vor Rechteerweiterungen sowie Man-in-the-Middle-Angriffen die Signaturzertifikatdatei in einem gesicherten Ordner.

Verwenden Sie IPsec für die folgenden Computer:

- Computer, auf dem die Configuration Manager-Konsole ausgeführt wird
- Computer, auf dem die Signaturzertifikatsdatei gespeichert ist
- Computer, auf dem die Quelldateien der Anwendung gespeichert sind

Signieren Sie die Anwendung alternativ unabhängig von Configuration Manager, bevor Sie den **Assistenten zum Erstellen von Anwendungen** ausführen.

### <a name="implement-access-controls"></a>Implementieren von Zugriffssteuerungen

Implementieren Sie Zugriffssteuerungen zum Schutz von Referenzcomputern. Stellen Sie sicher, dass der Referenzcomputer, auf den Sie zum Konfigurieren der Erkennungsmethode in einem Bereitstellungstyp zugreifen, nicht gefährdet ist.

### <a name="restrict-and-monitor-administrative-users"></a>Einschränken und Überwachen von Administratoren

Schränken Sie den Zugriff für Administratoren ein und überwachen Sie diese mit den folgenden Sicherheitsrollen für die Anwendungsverwaltung:

- **Anwendungsadministrator**
- **Anwendungsautor**
- **Anwendungsbereitstellungs-Manager**

Selbst wenn Sie eine rollenbasierte Verwaltung festgelegt haben, verfügen Administratoren, die Anwendungen erstellen und bereitstellen, möglicherweise über mehr Berechtigungen, als Ihnen bewusst ist. Administratoren, die beispielsweise eine Anwendung erstellen oder ändern, können abhängige Anwendungen auch außerhalb ihres Sicherheitsbereichs auswählen.

### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>Konfigurieren von App-V-Apps in virtuellen Umgebungen mit derselben Vertrauensebene

Wenn Sie virtuelle App-V-Umgebungen (Microsoft Application Virtualization) konfigurieren, wählen Sie Anwendungen aus, die dieselbe Vertrauensebene in der virtuellen Umgebung aufweisen. Da Anwendungen in einer virtuellen App-V-Umgebung Ressourcen wie die Zwischenablage gemeinsam verwenden können, konfigurieren Sie die virtuelle Umgebung so, dass die ausgewählten Anwendungen dieselbe Vertrauensebene aufweisen.

Weitere Informationen finden Sie unter [Erstellen von virtuellen App-V-Umgebungen](../deploy-use/create-app-v-virtual-environments.md).

### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>Sicherstellen, dass macOS-Apps aus einer vertrauenswürdigen Quelle stammen

Stellen Sie beim Bereitstellen von Anwendungen für macOS-Geräte sicher, dass die Quelldateien aus einer vertrauenswürdigen Quelle stammen. Das CMAppUtil-Tool überprüft nicht die Signatur des Quellpakets. Überprüfen Sie, ob das Paket aus einer Quelle stammt, der Sie vertrauen. Das CMAppUtil-Tool erkennt nicht, ob die Dateien manipuliert wurden.

### <a name="secure-the-cmmac-file-for-macos-apps"></a>Sichern der CMMAC-Datei für macOS-Apps

Wenn Sie Anwendungen für macOS-Computer bereitstellen, sichern Sie den Speicherort der **CMMAC**-Datei. Das CMAppUtil-Tool generiert diese Datei, die Sie dann in Configuration Manager importieren. Diese Datei wurde weder signiert noch überprüft.

Sichern Sie den Kommunikationskanal, wenn Sie diese Datei in Configuration Manager importieren. Um Manipulationen an dieser Datei zu vermeiden, speichern Sie sie in einem gesicherten Ordner. Verwenden Sie IPsec für die folgenden Computer:

- Computer, auf dem die Configuration Manager-Konsole ausgeführt wird  
- Computer, auf dem die **CMMAC**-Datei gespeichert wird  

### <a name="use-https-for-web-applications"></a>Verwenden von HTTPS für Webanwendungen

Wenn Sie einen Bereitstellungstyp für Webanwendungen konfigurieren, verwenden Sie HTTPS, um die Verbindung zu schützen. Wenn Sie eine Webanwendung nicht über einen HTTPS-Link, sondern über einen HTTP-Link bereitstellen, könnte die Geräteverbindung zu einem nicht autorisierten Server umgeleitet werden. Daten, die zwischen dem Gerät und dem Server ausgetauscht werden, könnten in diesem Fall manipuliert werden.


## <a name="security-issues-for-application-management"></a>Sicherheitsprobleme bei der Anwendungsverwaltung  

- Benutzer mit geringsten Rechten können Dateien aus dem Cache des Clientcomputers kopieren.  

     Benutzer können den Clientcache zwar lesen, aber nicht in ihn schreiben. Mit Leseberechtigungen können Benutzer Anwendungsinstallationsdateien von einem Computer auf einen anderen kopieren.  

- Benutzer mit geringen Rechten können Dateien ändern, die den Softwarebereitstellungsverlauf auf dem Clientcomputer aufzeichnen.  

     Benutzer können Dateien ändern, die Informationen über den Installationszustand von Anwendungen enthalten, da Informationen zum Anwendungsverlauf nicht geschützt sind.  

- App-V-Pakete sind nicht signiert.  

     Die Signierung von App-V-Paketen wird in Configuration Manager nicht unterstützt. Mit einer vertrauenswürdigen Quelle wird überprüft, ob Inhalte aus einer vertrauenswürdigen Quelle stammen und während der Übertragung nicht verändert wurden. Risiken für dieses Sicherheitsproblem können nicht eingeschränkt werden. Wenden Sie auf jeden Fall die bewährte Sicherheitsmethode für das Herunterladen von Inhalten aus einer vertrauenswürdigen Quelle und von einem sicheren Speicherort an.  

- Veröffentlichte App-V-Anwendungen können von allen Benutzern auf dem Computer installiert werden.  

     Wenn eine App-V-Anwendung auf einem Computer veröffentlicht wird, können alle Benutzer, die sich auf diesem Computer anmelden, diese Anwendung installieren. Sie können nicht einschränken, welche Benutzer die Anwendung nach der Veröffentlichung installieren können.  


## <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a> Zertifikate für Microsoft Silverlight 5 und für den Anwendungskatalog erforderlicher Modus mit höherer Vertrauensstellung  

> [!Important]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Konfigurations-Manager-Clients bis einschließlich Version 1710 erfordern Microsoft Silverlight 5, das im Modus mit höherer Vertrauensstellung ausgeführt werden muss, damit Benutzer Software aus dem Anwendungskatalog installieren können. Standardmäßig werden Silverlight-Anwendungen im Modus mit teilweiser Vertrauensstellung ausgeführt, um den Zugriff von Anwendungen auf Benutzerdaten zu verhindern. Microsoft Silverlight 5 wird von Configuration Manager automatisch auf Clients installiert, wenn es noch nicht installiert ist. Standardmäßig wird die Computer-Agent-Clienteinstellung **Ausführen von Silverlight-Anwendungen im Modus mit höherer Vertrauensstellung zulassen** von Configuration Manager auf **Ja** festgelegt. Mit dieser Einstellung können signierte und vertrauenswürdige Silverlight-Anwendungen den Modus mit höherer Vertrauensstellung anfordern.  

Wenn Sie die Standortsystemrolle des Anwendungskatalog-Websitepunkts installieren, wird im Computer-Zertifikatspeicher für vertrauenswürdige Herausgeber auf jedem Configuration Manager-Clientcomputer ein Microsoft-Signaturzertifikat installiert. Silverlight-Anwendungen, die mit diesem Zertifikat signiert sind, werden im Modus mit höherer Vertrauensstellung ausgeführt, der für Computer erforderlich ist, um Software aus dem Anwendungskatalog zu installieren. Configuration Manager verwaltet das Signaturzertifikat automatisch. Um die Dienstkontinuität zu erhöhen, löschen oder verschieben Sie dieses Microsoft-Signaturzertifikat nicht manuell.  

> [!WARNING]  
> Bei aktivierter Clienteinstellung **Ausführen von Silverlight-Anwendungen im Modus mit höherer Vertrauensstellung zulassen** können alle Silverlight-Anwendungen, die mit Zertifikaten aus dem Zertifikatspeicher für vertrauenswürdige Herausgeber im Computerspeicher oder im Benutzerspeicher signiert sind, im Modus mit erhöhter Vertrauensstellung ausgeführt werden. Über die Clienteinstellung kann der Modus mit höherer Vertrauensstellung nicht speziell für den Configuration Manager-Anwendungskatalog oder den Zertifikatspeicher für vertrauenswürdige Herausgeber im Computerspeicher aktiviert werden. Wenn dem Speicher für vertrauenswürdige Herausgeber durch Schadsoftware ein nicht vertrauenswürdiges Zertifikat hinzugefügt wird, kann Schadsoftware, von der eine eigene Silverlight-Anwendung verwendet wird, nun auch im Modus mit erhöhter Vertrauensstellung ausgeführt werden.  

Wenn Sie die Einstellung **Allow Silverlight applications to run in elevated trust mode** (Ausführen von Silverlight-Anwendungen im Modus mit höherer Vertrauensstellung zulassen) auf **Nein** festlegen, wird das Microsoft-Signaturzertifikat nicht von den Clients entfernt.  

Weitere Informationen zu vertrauenswürdigen Anwendungen in Silverlight finden Sie unter [Trusted Applications ](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\)) (Vertrauenswürdige Anwendungen).  


## <a name="privacy-information-for-application-management"></a>Datenschutzinformationen zur Anwendungsverwaltung  

Mit der Anwendungsverwaltung können Sie Anwendungen, Programme oder Skripts auf jedem Client in der Hierarchie ausführen. Welche Typen von Anwendungen, Programmen oder Skripts Sie ausführen und welche Informationen übertragen werden, kann von Configuration Manager nicht gesteuert werden. Beim Anwendungsbereitstellungsprozess werden von Configuration Manager möglicherweise Informationen übertragen, anhand derer die Geräte- und Anmeldekonten zwischen Clients und Servern identifiziert werden können.  

In Configuration Manager werden Statusinformationen zum Softwarebereitstellungsprozess verwaltet. Diese Statusinformationen zum Softwarebereitstellungsprozess werden bei der Übertragung nicht verschlüsselt, wenn vom Client kein HTTPS zur Kommunikation verwendet wird. In der Datenbank werden die Statusinformationen unverschlüsselt gespeichert.  

Für das Verwenden der Configuration Manager-Installation zur interaktiven, unbeaufsichtigten oder Remoteinstallation von Software auf Clients gelten möglicherweise die Lizenzbedingungen der Software. Diese unterscheiden sich von den Softwarelizenzbedingungen für Configuration Manager. Bevor Sie Software mit Configuration Manager bereitstellen, müssen Sie stets die Softwarelizenzbedingungen lesen und akzeptieren.  

Configuration Manager sammelt Diagnose- und Nutzungsdaten über Anwendungen, die Microsoft zur Verbesserung künftiger Releases verwendet. Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

Die Anwendungsbereitstellung wird nicht standardmäßig ausgeführt. Zur Ausführung sind mehrere Konfigurationsschritte erforderlich.  

Die folgenden Funktionen unterstützen eine effiziente Softwarebereitstellung:

- Die **Affinität zwischen Benutzer und Gerät** ordnet einen Benutzer Geräten zu. Ein Configuration Manager-Administrator stellt Software den Benutzer bereit. Der Client installiert die Software automatisch auf den Computern, die der Benutzer am häufigsten verwendet.  

- **Softwarecenter** wird automatisch auf einem Gerät installiert, wenn Sie den Konfigurations-Manager-Client installieren. Benutzer können im Softwarecenter Einstellungen ändern, nach Software suchen und diese installieren.  

- Der **Anwendungskatalog** ist eine Website, über die Benutzer Softwareinstallationen anfordern können.  

    > [!Important]  
    > Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

### <a name="user-device-affinity-privacy-information"></a><a name="bkmk_privacy-uda"></a> Informationen zur Affinität zwischen Benutzer und Gerät

- Von Configuration Manager werden möglicherweise Informationen zwischen Clients und Verwaltungspunkt-Standortsystemen übertragen. Anhand der Informationen können unter Umständen die Computer und Anmeldekonten sowie die Verwendungszusammenfassung zu den Anmeldekonten identifiziert werden.  

- Die zwischen Client und Server übertragenen Daten werden nur dann verschlüsselt, wenn aufgrund der Konfiguration des Verwaltungspunkts eine Clientkommunikation über HTTPS erforderlich ist.  

- Die Computerinformationen und Verwendungsinformationen zum Anmeldekonto, die zur Zuordnung von Benutzern und Geräten verwendet werden, werden auf den Clientcomputern gespeichert, an Verwaltungspunkte gesendet und dann in der Configuration Manager-Datenbank gespeichert. Die alten Informationen werden standardmäßig nach 90 Tagen aus der Datenbank gelöscht. Das Löschverhalten können Sie konfigurieren, indem Sie den Standortwartungstask **Veraltete Daten zur Affinität zwischen Benutzer und Gerät löschen** festlegen.  

- Configuration Manager verwaltet Statusinformationen zur Affinität zwischen Benutzer und Gerät. Statusinformationen werden beim Übertragen nur dann verschlüsselt, wenn die Clients für die Kommunikation mit Verwaltungspunkten über HTTPS konfiguriert sind. In der Datenbank werden die Statusinformationen unverschlüsselt gespeichert.  

- Computerinformationen und Nutzungsinformationen zum Anmelden, die zum Festlegen der Affinität zwischen Benutzer und Gerät verwendet werden, sind stets aktiviert. Benutzer und Administratoren können Informationen zur Affinität zwischen Benutzer und Gerät bereitstellen.  

### <a name="software-center-privacy-information"></a><a name="bkmk_privacy-userex"></a> Datenschutzinformationen zum Software Center

- Mithilfe des Softwarecenters kann der Configuration Manager-Administrator beliebige Anwendungen, Programme und Skripts zur Ausführung durch die Benutzer veröffentlichen. Welche Typen von Programmen oder Skripts im Katalog veröffentlicht und welche Informationen übertragen werden, kann von Configuration Manager nicht gesteuert werden.  

- Von Configuration Manager werden möglicherweise Informationen zwischen Clients und Verwaltungspunkt übertragen. Anhand der Informationen können unter Umständen die Computer und die Anmeldekonten identifiziert werden. Zwischen Clients und Servern übertragene Daten werden nur dann verschlüsselt, wenn aufgrund der Konfiguration des Verwaltungspunkts Clientverbindungen über HTTPS erforderlich sind.  

- Die Informationen zu Genehmigungsanforderungen für Anwendungen werden in der Configuration Manager-Datenbank gespeichert. Abgebrochene oder abgelehnte Anforderungen und die zugehörigen Einträge zum Anforderungsverlauf werden standardmäßig nach 30 Tagen gelöscht. Sie können das Löschverhalten konfigurieren, indem Sie den Standortwartungstask **Veraltete Anwendungsanforderungsdaten löschen** einstellen. Zugelassene und ausstehende Genehmigungsanforderungen für Anwendungen werden nie gelöscht.  

- Softwarecenter wird automatisch installiert, wenn Sie den Konfigurations-Manager-Client auf einem Gerät installieren.  

### <a name="application-catalog-privacy-information"></a>Datenschutzinformationen zum Anwendungskatalog

> [!Important]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

- Der Anwendungskatalog wird nicht standardmäßig installiert. Für diese Installation sind mehrere Konfigurationsschritte erforderlich.  

- Mithilfe des Anwendungskatalogs kann der Configuration Manager-Administrator beliebige Anwendungen, Programme und Skripts zur Ausführung durch die Benutzer veröffentlichen. Welche Typen von Programmen oder Skripts im Katalog veröffentlicht und welche Informationen übertragen werden, kann von Configuration Manager nicht gesteuert werden.  

- Von Configuration Manager werden möglicherweise Informationen zwischen Clients und den Standortsystemrollen für den Anwendungskatalog übertragen. Anhand der Informationen können unter Umständen die Computer und die Anmeldekonten identifiziert werden. Zwischen Clients und Servern übertragene Daten werden nur dann verschlüsselt, wenn eine Clientverbindung über HTTPS aufgrund der Konfiguration dieser Standortsystemrollen erforderlich ist.  
