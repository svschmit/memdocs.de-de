---
title: Sicherheit und Datenschutz für Content Management
titleSuffix: Configuration Manager
description: Optimieren Sie die Sicherheit und den Datenschutz für die Inhaltsverwaltung in Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704478"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Sicherheit und Datenschutz für die Inhaltsverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel enthält Sicherheits- und Datenschutzinformationen für die Inhaltsverwaltung in Configuration Manager. 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> Bewährte Sicherheitsmethoden für die Inhaltsverwaltung  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Vor- und Nachteile von HTTPS und HTTP für Verteilungspunkte im Intranet
Berücksichtigen Sie für Verteilungspunkte im Intranet die Vor- und Nachteile bei der Verwendung von HTTPS und HTTP. In den meisten Situationen bietet die Verwendung von HTTP und Paketzugriffskonten zur Autorisierung mehr Sicherheit als die Verwendung von HTTPS mit Verschlüsselung, aber ohne Autorisierung. Wenn die Inhalte allerdings vertrauliche Daten umfassen, die bei der Übertragung verschlüsselt werden sollen, verwenden Sie HTTPS.  

-   **Wenn Sie für einen Verteilungspunkt HTTPS verwenden**, werden in Configuration Manager keine Paketzugriffskonten verwendet, um den Zugriff auf die Inhalte zu autorisieren. Stattdessen werden die Inhalte bei der Übermittlung über das Netzwerk verschlüsselt.  

-   **Wenn Sie für einen Verteilungspunkt HTTP verwenden**, können Sie Paketzugriffskonten zur Autorisierung verwenden. Allerdings werden die Inhalte bei der Übermittlung über das Netzwerk nicht verschlüsselt.  

Ab Version 1806 sollten Sie **Erweitertes HTTP** für den Standort aktivieren. Durch dieses Feature können Clients die Azure Active Directory-Authentifizierung verwenden, um sicher mit einem HTTP-Verteilungspunkt zu kommunizieren. Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](enhanced-http.md).

#### <a name="protect-the-client-authentication-certificate-file"></a>Schützen der Zertifikatdatei für die Clientauthentifizierung
Wenn Sie für den Verteilungspunkt anstelle eines selbstsignierten Zertifikats ein PKI-Clientauthentifizierungszertifikat verwenden, schützen Sie die Zertifikatdatei (.pfx) mit einem sicheren Kennwort. Wenn Sie die Datei im Netzwerk speichern, verwenden Sie beim Importieren der Datei in Configuration Manager einen sicheren Netzwerkkanal.

Wenn für das Importieren des Clientauthentifizierungszertifikats, das der Verteilungspunkt verwendet, um mit Verwaltungspunkten zu kommunizieren, ein Kennwort erforderlich ist, ist das Zertifikat durch diese Konfiguration vor Angriffen geschützt. Verwenden Sie Server Message Block (SMB)-Signaturen oder IPsec zwischen Netzwerkspeicherort und Standortserver, um einen Angreifer an der Manipulation der Zertifikatdatei zu hindern.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Entfernen der Verteilungspunktrolle vom Standortserver
Standardmäßig installiert das Setup für Configuration Manager einen Verteilungspunkt auf dem Standortserver. Clients müssen nicht direkt mit dem Standortserver kommunizieren. Weisen Sie die Rolle „Verteilungspunkt“ einem anderen Standortsystem zu, und entfernen Sie diese vom Standortserver, um die Angriffsfläche zu verringern.  

#### <a name="secure-content-at-the-package-access-level"></a>Schützen von Inhalten auf Paketzugriffsebene
Die Verteilungspunktfreigabe gewährt allen Benutzern den Lesezugriff. Verwenden Sie Paketzugriffskonten, wenn der Verteilungspunkt für HTTP konfiguriert ist, um festzulegen, welche Benutzer auf den Inhalt zugreifen können. Diese Konfiguration gilt nicht für Cloudverteilungspunkte, die Paketzugriffskonten nicht unterstützten. Weitere Informationen finden Sie unter [Paketzugriffskonten](accounts.md#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Konfigurieren von IIS für die Rolle „Verteilungspunkt“
Wenn beim Hinzufügen der Standortsystemrolle „Verteilungspunkt“ IIS von Configuration Manager installiert wird, entfernen Sie die HTTP-Umleitung bzw. die IIS-Verwaltungsskripts und -tools, sobald die Installation des Verteilungspunkts abgeschlossen ist. Für den Verteilungspunkt sind die HTTP-Umleitung bzw. die IIS-Verwaltungsskripts und -tools nicht erforderlich. Entfernen Sie diese Rollendienste für die Webserverrolle, um die Angriffsfläche zu verringern.  Weitere Informationen zu den Rollendiensten für die Webserverrolle für Verteilungspunkte finden Sie unter [Voraussetzungen für Standorte und Standortsysteme](../configs/site-and-site-system-prerequisites.md).  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Legen Sie beim Erstellen des Pakets Paketzugriffsberechtigungen fest.
Änderungen der Zugriffskonten für die Paketdateien treten erst nach dem erneuten Bereitstellen des Pakets in Kraft. Gehen Sie daher beim Festlegen der Zugriffsberechtigungen für ein neu erstelltes Paket mit großer Sorgfalt vor. Diese Konfiguration ist wichtig, wenn das Paket groß ist oder an viele Verteilungspunkte verteilt wird und wenn die Netzwerkbandbreite zur Verteilung von Inhalten beschränkt ist.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implementieren Sie Zugriffssteuerungen zum Schutz von Medien, die vorab bereitgestellte Inhalte enthalten.
Vorab bereitgestellte Inhalte werden komprimiert, aber nicht verschlüsselt. Ein Angreifer könnte die Dateien lesen und ändern, die auf die Geräte heruntergeladen werden. Manipulierte Inhalte werden von Konfigurations-Manager-Clients abgelehnt, aber dennoch heruntergeladen.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Importieren von vorab bereitgestelltem Inhalt mit ExtractContent
Importieren Sie vorab bereitgestellten Inhalt nur über das Befehlszeilentool „ExtractContent.exe“. Verwenden Sie nur das in Configuration Manager enthaltene autorisierte Befehlszeilentool, um Manipulationen und Rechteerweiterungen zu vermeiden.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Sichern Sie den Kommunikationskanal zwischen Standortserver und Paketquellspeicherort.
Verwenden Sie zum Erstellen von Anwendungen und Paketen IPsec oder SMB-Signaturen zwischen Standortserver und Paketquellspeicherort. Durch diese Konfiguration verhindern Sie die Manipulation der Quelldateien durch einen Angreifer.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Entfernen der virtuellen Standardverzeichnisse für benutzerdefinierte Websites mit der Rolle „Verteilungspunkt“
Wenn Sie die Standortkonfigurationsoption von der Standardwebsite in eine benutzerdefinierte Website ändern, nachdem die Rolle „Verteilungspunkt“ installiert wurde, entfernen Sie die virtuellen Standardverzeichnisse. Wenn Sie von der Standardwebsite zu einer benutzerdefinierten Website wechseln, werden die alten virtuellen Verzeichnisse von Configuration Manager nicht entfernt. Entfernen Sie folgende virtuelle Verzeichnisse, die ursprünglich von Configuration Manager unter der Standardwebsite erstellt wurden:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Cloudverteilungspunkte: Schützen von Abonnementdetails und Zertifikaten
Schützen Sie die folgenden wichtigen Elemente, wenn Sie Cloudverteilungspunkte verwenden:
- Den Benutzernamen und das Kennwort für das Azure-Abonnement
- Das Azure-Verwaltungszertifikat 
- Das Dienstzertifikat für den Cloudverteilungspunkt

Speichern Sie die Zertifikate an einem sicheren Ort. Verwenden Sie IPsec oder SMB-Signaturen zwischen dem Standortsystemserver und dem Quellspeicherort, wenn Sie beim Konfigurieren des Cloudverteilungspunkts über das Netzwerk auf die Zertifikate zugreifen.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Überwachen Sie aus Gründen der Dienstkontinuität das Ablaufdatum der Zertifikate des Cloudverteilungspunkts.
Configuration Manager zeigt keine Warnung an, wenn das Ablaufdatum der importierten Zertifikate für den Cloudverteilungspunkt bald erreicht ist. Überwachen Sie das Ablaufdatum unabhängig von Configuration Manager. Stellen Sie sicher, dass Sie Zertifikate vor dem Ablaufdatum erneuern und neu importieren. Dieser Vorgang ist wichtig, wenn Sie ein Serverauthentifizierungszertifikat von einem externen, öffentlichen Anbieter beziehen, da es in diesem Fall mehr Zeit erfordern kann, ein Zertifikat zu erneuern.  

 Wenn ein Zertifikat abläuft, generiert der Cloud Services-Manager eine Statusmeldung mit der ID **9425**. Die Datei „CloudMgr.log“ enthält einen Eintrag, der angibt, dass das Zertifikat **abgelaufen ist**. Das Ablaufdatum wird dabei im UTC-Format protokolliert.  



## <a name="security-considerations-for-content-management"></a>Sicherheitsüberlegungen für Content Management  

Bei der Planung von Content Management sollten Sie Folgendes berücksichtigen:  

-   Clients überprüfen Inhalte erst nach dem Herunterladen.  

     Konfigurations-Manager-Clients überprüfen den Hashwert von Inhalten erst nach dem Herunterladen in ihren Clientcache. Wenn ein Angreifer die Liste der herunterzuladenden Dateien oder die Inhalte selbst manipuliert, kann für das Herunterladen auf den Client eine erhebliche Netzwerkbandbreite erforderlich sein, jedoch müssen die Inhalte dann aufgrund des ungültigen Hashwerts verworfen werden.  

-   Wenn Sie Cloudverteilungspunkte verwenden, ist der Zugriff auf den Inhalt automatisch auf Ihr Unternehmen beschränkt. Sie können diesen nicht auf ausgewählte Benutzer oder Gruppen einschränken.  

-   Wenn Sie Cloudverteilungspunkte verwenden, werden Clients vom Verwaltungspunkt authentifiziert. Anschließend können Sie über ein Configuration Manager-Token auf die Cloudverteilungspunkte zugreifen. Das Token ist acht Stunden lang gültig. Wenn Sie einen Client sperren, weil er nicht mehr vertrauenswürdig ist, kann dieser also noch so lange Inhalte von einem Cloudverteilungspunkt herunterladen, bis der Gültigkeitszeitraum des Tokens abgelaufen ist. Vom Verwaltungspunkt wird dann kein weiteres Token für den Client ausgegeben, weil der Client gesperrt ist.  

     Beenden Sie den Clouddienst, um zu verhindern, dass ein gesperrter Client Inhalte innerhalb dieser acht Stunden herunterlädt. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Cloud Services**, und wählen Sie den Knoten **Cloudverteilungspunkte** aus.  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Datenschutzinformationen zur Inhaltsverwaltung  

 Configuration Manager speichert keine Benutzerdaten in Inhaltsdateien, für einen Administrator wäre dies jedoch möglich.  



## <a name="see-also"></a>Weitere Informationen:

- [Grundlegende Konzepte für das Content Management](fundamental-concepts-for-content-management.md)  

- [Sicherheit und Datenschutz für die Anwendungsverwaltung](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [Sicherheit und Datenschutz für die Softwareupdates](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [Sicherheit und Datenschutz für die Betriebssystembereitstellung](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
