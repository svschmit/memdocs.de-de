---
title: Zertifikate für lokales MDM
titleSuffix: Configuration Manager
description: Richten Sie Zertifikate für die vertrauenswürdige Kommunikation mit der lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager ein.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc63a21970bb522407c86d027690b83894b3cb99
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724664"
---
# <a name="set-up-certificates-for-trusted-communications-with-on-premises-mdm"></a>Einrichten von Zertifikaten für vertrauenswürdige Kommunikation mit lokalem MDM

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) erfordert, dass Sie die Standortsystem Rollen für die vertrauenswürdige Kommunikation mit verwalteten Geräten konfigurieren. Sie benötigen zwei Arten von Zertifikaten:

- Ein **Webserver Zertifikat** in IIS auf den Servern, auf denen die erforderlichen Standortsystem Rollen gehostet werden. Wenn ein Server mehrere Standortsystem Rollen hostet, benötigen Sie nur ein Zertifikat für diesen Server. Wenn sich jede Rolle auf einem separaten Server befindet, benötigt jeder Server ein separates Zertifikat.

- Das **Vertrauenswürdige Stamm Zertifikat** der Zertifizierungsstelle (Certificate Authority, ca), von der die Webserver Zertifikate ausgestellt werden. Installieren Sie dieses Stamm Zertifikat auf allen Geräten, von denen eine Verbindung mit den Standortsystem Rollen hergestellt werden muss.

Wenn Sie für in die Domäne eingebundenen Geräten Active Directory Zertifikat Dienste verwenden, können diese Zertifikate automatisch auf allen Geräten installiert werden. Installieren Sie das vertrauenswürdige Stamm Zertifikat für Geräte, die keiner Domäne beigetreten sind, auf andere Weise.

Für Massen registrierte Geräte können Sie das Zertifikat in das Registrierungspaket einschließen. Für von Benutzern registrierte Geräte müssen Sie das Zertifikat per E-Mail, Download aus dem Internet oder anderer Methode hinzufügen.

Wenn Sie eine bekannte öffentliche Zertifizierungsstelle wie VeriSign oder GoDaddy zum Ausstellen der Server Zertifikate verwenden, können Sie das vertrauenswürdige Stamm Zertifikat auf jedem Gerät nicht manuell installieren. Die meisten Geräte Vertrauen diesen öffentlichen Behörden nativ. Diese Methode ist eine nützliche Alternative für Benutzer registrierte Geräte, anstatt das Zertifikat auf andere Weise zu installieren.

> [!IMPORTANT]  
> Es gibt viele Methoden zum Einrichten der Zertifikate für die vertrauenswürdige Kommunikation zwischen Geräten und den Standortsystem Servern für lokale MDM. Die Informationen in diesem Artikel sind ein Beispiel für eine Möglichkeit. Diese Methode erfordert Active Directory Zertifikat Dienste mit einer Zertifizierungsstelle und der Rolle "Zertifizierungsstellen-Webregistrierung". Weitere Informationen finden Sie unter [Active Directory Certificate Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740\(v=ws.11\)).

## <a name="publish-the-crl"></a><a name="bkmk_configCa"></a>Veröffentlichen der CRL

Standardmäßig verwendet die Active Directory Zertifizierungsstelle LDAP-basierte Zertifikat Sperr Listen (CRLs). Sie ermöglicht Verbindungen mit der CRL für in die Domäne eingebundenen Geräten. Fügen Sie eine HTTP-basierte CRL hinzu, um zuzulassen, dass nicht in die Domäne eingebundenen Geräten von der Zertifizierungsstelle ausgegebene Zertifikate vertraut werden.

1. Wechseln Sie auf dem Server, auf dem die Zertifizierungsstelle für Ihren Standort ausgeführt wird, zum **Startmenü** , wählen Sie **Verwaltung**, und wählen Sie dann **Zertifizierungs**Stelle aus.

1. Klicken Sie in der Zertifizierungsstellen Konsole mit der rechten Maustaste auf **CertificateAuthority**, und wählen Sie dann **Eigenschaften**aus.

1. Wechseln Sie in den Eigenschaften von CertificateAuthority zur Registerkarte **Erweiterungen** . Stellen Sie sicher, dass die Option **Erweiterung auswählen** auf **CRL-Verteilungs Punkt (CDP)** festgelegt ist.

1. Wählen Sie `http://<ServerDNSName>/CertEnroll/<CAName><CRLNameSuffix><DeltaCRLAllowed>.crl`aus. Wählen Sie dann die folgenden Optionen aus:

    - **In CRLs einschließen. Diese werden von Clients verwendet, um Speicherorte für Delta-CRLs zu suchen.**

    - **In CDP-Erweiterung des ausgestellten Zertifikats einbeziehen.**

    - **In die IDP-Erweiterung der ausgestellten CRLs einbeziehen**

1. Wechseln Sie zur Registerkarte Beendigungs **Modul** . Wählen Sie **Eigenschaften**aus, und wählen Sie dann **das Veröffentlichen von Zertifikaten im Dateisystem zulassen**aus. Es wird ein Hinweis angezeigt, Active Directory Zertifikat Dienste neu zu starten.

1. Klicken Sie mit der rechten Maustaste auf gesperrte **Zertifikate**, wählen Sie **Alle Tasks**und dann **veröffentlichen**aus.

1. Wählen Sie im Fenster "CRL veröffentlichen" **nur Delta**Sperr Liste aus, und klicken Sie dann auf **OK** , um das Fenster zu schließen.

## <a name="create-the-certificate-template"></a><a name="bkmk_certTempl"></a>Erstellen der Zertifikat Vorlage

Die Zertifizierungsstelle verwendet die Webserver-Zertifikat Vorlage zum Ausstellen von Zertifikaten für die Server, auf denen die Standortsystem Rollen gehostet werden. Diese Server sind SSL-Endpunkte für die vertrauenswürdige Kommunikation zwischen den Standortsystem Rollen und registrierten Geräten.

1. Erstellen Sie eine Domänen Sicherheitsgruppe mit dem Namen **ConfigMgr-MDM-Server**. Fügen Sie die Computer Konten der Standortsystem Server zur Gruppe hinzu.

1. Klicken Sie in der Zertifizierungsstellen Konsole mit der rechten Maustaste auf **Zertifikat Vorlagen**, und wählen Sie **Verwalten**aus. Mit dieser Aktion wird die Zertifikat Vorlagen Konsole geladen.

1. Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagen Anzeige Name der Name** **Webserver** angezeigt wird, und wählen Sie dann **Doppelte Vorlage**aus.

1. Wählen Sie im Fenster **Doppelte Vorlage** die Option **Windows 2003 Server, Enterprise Edition** oder **Windows 2008 Server, Enterprise Edition**aus, und klicken Sie dann auf **OK**.

    > [!TIP]
    > Configuration Manager unterstützt Windows 2008-Server Zertifikat Vorlagen, die auch als V3-oder CNG-Zertifikate (Cryptography: Next Generation) bezeichnet werden. Weitere Informationen finden Sie in der [Übersicht über CNG-Zertifikate](../../core/plan-design/network/cng-certificates-overview.md).

    Wenn die Zertifizierungsstelle unter Windows Server 2012 oder höher ausgeführt wird, wird in diesem Fenster nicht die Option für die Zertifikat Vorlagen Version angezeigt. Nachdem Sie die Vorlage dupliziert haben, wählen Sie die Version auf der Registerkarte **Kompatibilität** der Vorlagen Eigenschaften aus.

1. Geben Sie im Fenster **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagen Namen ein. Die Zertifizierungsstelle verwendet diesen Namen, um die Webzertifikate zu generieren, die auf Configuration Manager Standort Systemen verwendet werden. Geben Sie z. b. **ConfigMgr-MDM-Webserver**ein.

1. Wechseln Sie zur Registerkarte Antragsteller **Name** , und wählen Sie **aus Active Directory Informationen erstellen aus**. Geben Sie unter Format des Antragsteller namens den **DNS-Namen**an. Wenn **Benutzer Prinzipal Name (User Principal Name, UPN)** ausgewählt ist, deaktivieren Sie die Option für den alternativen Antragsteller Namen.

1. Wechseln Sie zur Registerkarte **Sicherheit** .

    1. Entfernen Sie die Berechtigung **Anmelden** aus den Sicherheitsgruppen **Domänen-Admins** und Organisations- **Admins** .

    1. Wählen Sie **Hinzufügen**aus, und geben Sie den Namen der Sicherheitsgruppe ein. Beispielsweise **ConfigMgr-MDM-Server**. Wählen Sie **OK** aus, um das Fenster zu schließen.

    1. Wählen Sie die Berechtigung **registrieren** für diese Gruppe aus. Entfernen Sie die Berechtigung **Lesen** nicht.

1. Wählen Sie **OK** aus, um die Änderungen zu speichern, und schließen Sie die Konsole Zertifikat Vorlagen.

1. Klicken Sie in der Zertifizierungsstellen Konsole mit der rechten Maustaste auf **Zertifikat Vorlagen**, wählen Sie **neu**und dann auszustellende **Zertifikat Vorlage**aus.

1. Wählen Sie im Fenster **Zertifikat Vorlagen aktivieren** die neue Vorlage aus. Beispiel: **ConfigMgr-MDM-Webserver**. Wählen Sie dann **OK** aus, um das Fenster zu speichern und zu schließen.

## <a name="request-the-certificate"></a><a name="bkmk_requestCert"></a>Anfordern des Zertifikats

In diesem Verfahren wird beschrieben, wie Sie das Webserver Zertifikat für IIS anfordern. Führen Sie diesen Vorgang für jeden Standortsystem Server aus, der eine der Rollen für die lokale Verwaltung mobiler Geräte (MDM) hostet.

1. Öffnen Sie auf dem Standortsystem Server, auf dem eine der Rollen gehostet wird, eine Eingabeaufforderung als Administrator. Geben `mmc` Sie ein, um eine leere Microsoft Management Console zu öffnen.

1. Wechseln Sie im Konsolenfenster zum Menü **Datei** , und klicken Sie auf **Snap-in hinzufügen/entfernen**.

    1. Wählen Sie **Zertifikate** aus der Liste der verfügbaren Snap-Ins aus, und wählen Sie **Hinzufügen**.

    1. Wählen Sie im Fenster Zertifikate-Snap-in die Option **Computer Konto**aus. Wählen Sie **weiter**, und wählen Sie dann **Fertig** stellen aus, um den lokalen Computer zu verwalten.

    1. Wählen Sie **OK** aus, um das Snap-in-Fenster hinzufügen oder entfernen zu schließen.

1. Erweitern Sie **Zertifikate (lokaler Computer)**, und wählen Sie den **persönlichen** Speicher aus. Klicken Sie im Menü **Aktion** auf **Alle Tasks**, und wählen Sie **Neues Zertifikat anfordern**aus. Diese Aktion kommuniziert mit Active Directory Zertifikat Diensten, um mithilfe der zuvor erstellten Vorlage ein neues Zertifikat zu erstellen.

    1. Wählen Sie im Assistenten für die Zertifikat Registrierung auf der Seite Vorbereitung die Option **weiter**aus.

    1. Wählen Sie auf der Seite Zertifikat Registrierungs Richtlinie auswählen **Active Directory Registrierungs Richtlinie**aus, und klicken Sie dann auf **weiter**.

    1. Wählen Sie Ihre Webserver-Zertifikat Vorlage (**ConfigMgr-MDM-Webserver**) aus, und klicken Sie dann auf **registrieren**.

    1. Nachdem Sie das Zertifikat angefordert haben, klicken Sie auf **Fertig**stellen.

Jeder Server benötigt ein eindeutiges Webserver Zertifikat. Wiederholen Sie diesen Vorgang für jeden Server, auf dem eine der erforderlichen Standortsystem Rollen gehostet wird. Wenn ein Server alle Standortsystemrollen hostet, müssen Sie nur ein Webserverzertifikat anfordern.

## <a name="bind-the-certificate"></a><a name="bkmk_bindCert"></a>Binden des Zertifikats

Der nächste Schritt besteht darin, das neue Zertifikat an den Webserver zu binden. Befolgen Sie diesen Vorgang für jeden Server, der die Standortsystem Rollen "anmeldungspunkt" und "anmeldungsproxy- *Punkt* " *enrollment point* Wenn ein Server alle Standortsystem Rollen hostet, müssen Sie diesen Vorgang nur einmal ausführen.

> [!NOTE]
> Sie müssen diesen Vorgang nicht für die Standortsystem Rollen "Verteilungs Punkt" und "Geräte Verwaltungspunkt" durchführen. Sie erhalten automatisch das erforderliche Zertifikat während der Registrierung.

1. Wechseln Sie auf dem Server, auf dem der anmeldungspunkt oder der anmeldungsproxypunkt gehostet wird, zum **Startmenü** , wählen Sie **Verwaltung**und dann **IIS-Manager**aus.

1. Wählen Sie in der Liste der Verbindungen die **Standard Website**aus, und wählen Sie dann **Bindungen bearbeiten**aus.

    1. Wählen Sie im Fenster Website Bindungen die Option **https**aus, und klicken Sie dann auf **Bearbeiten**.

    1. Wählen Sie im Fenster "Site Bindung bearbeiten" das neu registrierte Zertifikat für das **SSL-Zertifikat**aus. Klicken Sie zum Speichern auf **OK** , und wählen Sie dann **Schließen**aus.

1. Wählen Sie in der IIS-Manager-Konsole in der Liste der Verbindungen den Webserver aus. Wählen Sie im Bereich Aktion auf der rechten Seite **neu starten**aus. Durch diese Aktion wird der Webserver Dienst neu gestartet.

## <a name="export-the-trusted-root-certificate"></a><a name="bkmk_exportCert"></a>Exportieren des vertrauenswürdigen Stamm Zertifikats

Active Directory Zertifikat Dienste installiert automatisch das erforderliche Zertifikat von der Zertifizierungsstelle auf allen in die Domäne eingebundenen Geräten. Um das Zertifikat zu erhalten, das für die Kommunikation mit den Standortsystem Rollen für nicht in die Domäne eingebundene Geräte erforderlich ist, exportieren Sie es aus dem Zertifikat, das an den Webserver gebunden ist.

1. Wählen Sie im IIS-Manager die **Standard Website**aus. Wählen Sie im Bereich Aktion auf der rechten Seite **Bindungen**aus.

1. Wählen Sie im Fenster Website Bindungen die Option **https**aus, und klicken Sie dann auf **Bearbeiten**.

1. Wählen Sie das Webserver Zertifikat aus, und wählen Sie **Ansicht**aus.

1. Wechseln Sie in den Eigenschaften des Webserver Zertifikats zur Registerkarte **Zertifizierungspfad** . Wählen Sie den Stamm des Zertifizierungs Pfads aus, und wählen Sie **Zertifikat anzeigen**aus.

1. Wechseln Sie in den Eigenschaften des Stamm Zertifikats zur Registerkarte **Details** , und wählen Sie dann in **Datei kopieren**aus.

1. Klicken Sie im Assistenten zum Exportieren von Zertifikaten auf der Willkommensseite auf **weiter**.

1. Wählen Sie die Option **der-codierten binären X. 509 (. CER)** als Format, und wählen Sie **weiter**aus.

1. Geben Sie einen Pfad und einen Dateinamen ein, um dieses vertrauenswürdige Stamm Zertifikat zu identifizieren. Klicken Sie für den Dateinamen auf **Durchsuchen...**, wählen Sie einen Speicherort zum Speichern der Zertifikat Datei, benennen Sie die Datei, und wählen Sie **weiter**aus.

1. Überprüfen Sie die Einstellungen, und wählen Sie **Fertig** stellen, um das Zertifikat in die Datei zu exportieren

Abhängig vom Entwurf Ihrer Zertifizierungsstelle müssen Sie möglicherweise zusätzliche Stamm Zertifikate der untergeordneten Zertifizierungsstelle exportieren. Wiederholen Sie diesen Vorgang, um die anderen Zertifikate im Zertifizierungspfad des Webserver Zertifikats zu exportieren.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Einrichten der Geräteregistrierung](set-up-device-enrollment-on-premises-mdm.md)
