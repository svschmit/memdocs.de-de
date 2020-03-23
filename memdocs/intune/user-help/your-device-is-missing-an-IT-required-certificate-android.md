---
title: Auf Ihrem Gerät ist ein Zertifikat nicht vorhanden | Microsoft-Dokumentation
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/29/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f0ba4cbb-ef0a-4335-86bf-f1d006867fa2
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b4a16204afc99169183e02eb269ab24d7f63cc49
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79346052"
---
# <a name="install-missing-certificate-required-by-your-organization"></a>Installieren des fehlenden Zertifikats, das Ihre Organisation vorschreibt  

Wenn Ihr Gerät nicht bei Intune registriert ist und ein erforderliches Zertifikat fehlt, können Sie sich nicht bei der Unternehmensportal-App anmelden. Wenn Sie versuchen, sich anzumelden, sehen Sie die folgende Meldung:

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

Es gibt zwei Möglichkeiten, das erforderliche Zertifikat herunterzuladen und Ihr Gerät zu registrieren. 

- Aktivieren Sie den Browserzugriff in der Unternehmensportal-App.
- Identifizieren Sie das fehlende Zertifikat auf einem Unternehmens- oder Schul-PC. Suchen Sie dann im Internet danach, und laden Sie es auf Ihr Gerät herunter. 

Schließen Sie zunächst die Schritte für das Aktivieren des Browserzugriffs ab. Wenn Sie Ihr Gerät anschließend immer noch nicht registrieren können, führen Sie die Schritte für die Internetsuche nach dem Zertifikat aus. 

## <a name="enable-browser-access"></a>Aktivieren des Browserzugriffs
Führen Sie die folgenden Schritte durch, um den Browserzugriff zu aktivieren. Nachdem Sie den Zugriff aktiviert haben, wird das richtige Zertifikat über das Unternehmensportal installiert und die Registrierung fortgesetzt.    

1. Tippen Sie in der Unternehmensportal-App in der rechten Ecke auf das Menü.  
2. Wählen Sie **Einstellungen** aus.  
3. Wählen Sie neben **Browser Zugriff aktivieren** die Option **aktivieren aus**.  
4. Tippen Sie auf dem Bildschirm „Geräteadministrator“ auf **AKTIVIEREN**. 

## <a name="identify-and-download-the-missing-certificate-through-web-search"></a>Ermitteln und Herunterladen des fehlenden Zertifikats über eine Websuche
Schließen Sie diese Schritte ab, um das Zertifikat manuell zu ermitteln und es auf Ihrem Gerät zu installieren.  

1. Öffnen Sie auf einem PC den Internet Explorer. Wenn Ihnen dafür kein PC zur Verfügung steht, wenden Sie sich an die Supportabteilung Ihres Unternehmens. Die Kontaktinformationen für die Supportabteilung Ihres Unternehmens finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).

2. Öffnen Sie die [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980), und melden Sie sich mit Ihren Geschäfts- oder Schulanmeldeinformationen an.

3. Wählen Sie ganz rechts in der Adressleiste des Browsers das Symbol aus, das wie ein Vorhängeschloss aussieht, wie im nachstehenden Screenshot dargestellt.

    ![screenshot-internet-explorer-address-bar-padlock-symbol](./media/andr-missing-cert-ie-padlock-symbol.png)

    Wenn das Vorhängeschlosssymbol nicht angezeigt wird, beenden Sie den Vorgang, und wenden Sie sich an die Supportabteilung Ihres Unternehmens. Das Vorhängeschlosssymbol bedeutet, dass Sie sicher angemeldet sind, Sie sollten also nicht fortfahren, solange dieses Symbol nicht angezeigt wird.

4. Wählen Sie **Zertifikate anzeigen** aus.

    ![screenshot-internet-explorer-view-certificates-button-on-website-identification-dialog](./media/andr-missg-cert-ie-view-cert-button.png)

5. Wählen Sie die Registerkarte **Zertifizierungspfad** aus, und identifizieren Sie das Zertifikat, das Sie aus dem Internet abrufen müssen. Der Name des Zertifikats, das Sie benötigen, befindet sich an der gleichen Position wie der, der im vorherigen Beispielscreenshot hervorgehoben ist.

6. Suchen Sie mithilfe einer Suchmaschine wie Bing oder Google nach dem Namen des fehlenden Zertifikats, das Sie im vorherigen Abschnitt angegeben haben. Das Zertifikat kann mit verschiedenen Erweiterungen wie CRT oder PEM usw. enden.

7. Laden Sie das Stammzertifikat von der Website herunter.

8. Ziehen Sie nach dem Herunterladen des Zertifikats vom oberen Rand Ihres Geräts nach unten, um Ihre Benachrichtigungen zu öffnen, und tippen Sie dann in der Liste der Benachrichtigungen auf den Namen des Zertifikats.

4. Übernehmen Sie im Dialogfeld **Name the Certificate** (Zertifikat benennen), das im folgenden Screenshot angezeigt wird, den Standardzertifikatnamen.

5. Stellen Sie sicher, dass **Verwendung von Anmeldeinformationen** auf **Für VPN und Apps** festgelegt ist, und tippen Sie dann auf **OK**.

    ![screenshot-certificate-name-dialog-showing-certificate-name](./media/andr-missing-cert-cert-name.png)

6. Schließen Sie die Unternehmensportal-App.

7. Öffnen Sie die Unternehmensportal-App erneut. Sie sollten sich jetzt bei der Unternehmensportal-App anmelden können. Wenn Sie Hilfe benötigen, wenden Sie sich an die Supportabteilung Ihres Unternehmens.

Wenn Ihnen die gleiche „Zertifikat fehlt“-Meldung wie in der Abbildung oben angezeigt wird, und Sie den oben beschriebenen Vorgang bereits ausgeführt haben, benötigt die Supportabteilung Ihres Unternehmens wahrscheinlich noch ein anderes Zertifikat, um Ihnen bei der Installation helfen zu können. Verwenden Sie die Kontaktinformationen auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980), wenn Sie sich an die Supportabteilung Ihres Unternehmens wenden möchten.

## <a name="next-steps"></a>Nächste Schritte  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  
