---
title: Einrichten der Registrierung für die lokale Verwaltung mobiler Geräte
titleSuffix: Configuration Manager
description: Erteilen Sie Benutzern die Berechtigung zum Registrieren Ihrer Geräte für die lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724684"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>Einrichten der Geräteregistrierung für die lokale Verwaltung mobiler Geräte (MDM) in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Der letzte Schritt zum Einrichten der lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) besteht darin, Benutzern das Registrieren Ihrer Geräte zu ermöglichen. Verwenden Sie Configuration Manager-Client Einstellungen, um Benutzern die Berechtigung zum Registrieren von Geräten in der lokalen MDM zu erteilen.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a> Erstellen eines Anmeldungsprofils

Fügen Sie ein neues Registrierungs Profil zu den Standard Client Einstellungen hinzu, um die Einstellungen zu übertragen, die erforderlich sind, damit Benutzer Mobile Geräte anmelden können. Dieses Profil gilt dann für alle Benutzer am Configuration Manager Website.

> [!NOTE]
> Bei diesem Prozess werden die **Client Standardeinstellungen**verwendet, die automatisch für alle Geräte und Benutzer gelten. Alternativ dazu können Sie auch benutzerdefinierte Client Einstellungen erstellen und diese dann in Sammlungen Ihrer Wahl bereitstellen. Diese alternative Methode erfordert mindestens zwei benutzerdefinierte Client Einstellungen, eine für *Geräte* Einstellungen und eine für die *Benutzer* Einstellungen. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md).

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich **Verwaltung** , und wählen Sie den Knoten **Client Einstellungen** aus. Öffnen **Sie die** **Client Standardeinstellungen** , und wählen Sie die Registrierungs Gruppe aus.

1. Geben Sie unter Geräteeinstellungen das Abruf **Intervall für moderne Geräte (Minuten) an**. Standardmäßig beträgt dieses Intervall 60 Minuten.

1. Aktivieren Sie unter Benutzereinstellungen die Option, um **Benutzern das Anmelden moderner Geräte zu gestatten**.

1. Wählen Sie für das Registrierungs **Profil für moderne Geräte**die Option **Profil festlegen**aus. Wählen Sie im Fenster Registrierungs Profil die Option **Erstellen**aus.

1. Geben Sie im Fenster Registrierungs Profil erstellen die folgenden Informationen an:

    - Einen eindeutigen und beschreibenden **Namen** für das Registrierungs Profil.

    - Eine optionale **Beschreibung** , um zusätzliche Informationen zum Profil bereitzustellen.

    - Wählen Sie den **Verwaltungsstandort Code** aus, der den Geräte Verwaltungspunkt enthält. Wählen Sie **OK** aus, um zu speichern und zu schließen.

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>Zusätzliche Client Einstellungen konfigurieren

Es gibt zusätzliche Client Einstellungen zum Konfigurieren von Geräten, nachdem Sie registriert wurden. Weitere allgemeine Informationen finden Sie unter [Konfigurieren von Client Einstellungen](../../core/clients/deploy/configure-client-settings.md).

Configuration Manager unterstützt die folgenden Client Einstellungen für lokales MDM:

- **Client Richtlinie**: Diese Einstellungen geben die Häufigkeit für das Herunterladen der Client Richtlinie auf das Gerät an. Sie können auch die Einstellungen für die Benutzer Richtlinie aktivieren. Weitere Informationen finden Sie unter Informationen [zu Client Einstellungen-Client Richtlinie](../../core/clients/deploy/about-client-settings.md#client-policy).

- **Software Bereitstellung**: Legen Sie das Intervall für die Evaluierung von Software Bereitstellungen fest. Weitere Informationen finden Sie unter Informationen [zu Client Einstellungen-Software Bereitstellung](../../core/clients/deploy/about-client-settings.md#software-deployment).

    > [!NOTE]
    > Für die lokale Verwaltung mobiler Geräte können die Einstellungen für die Software Bereitstellung nur als Standard Client Einstellungen verwendet werden.

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>Benutzer ermitteln

Damit Benutzer die Client Einstellungen mit dem Registrierungs Profil für die lokale Verwaltung mobiler Geräte (MDM) erhalten können, wird Ihr Benutzerkonto von dem Standort in Active Directory ermittelt. Führen Sie die Ermittlung für Active Directory-Benutzer aus, um sicherzustellen, dass alle erforderlichen Personen das Anmeldungsprofil erhalten. Weitere Informationen finden Sie unter [Active Directory Benutzer](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)Ermittlung.

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>Installieren des vertrauenswürdigen Stamm Zertifikats

In die Domäne eingebundenen Geräten wird das Vertrauens Stamm Zertifikat für die vertrauenswürdige Kommunikation mit den Servern, auf denen die Standortsystem Rollen gehostet werden, Active Directory Zertifikat Dienste verteilt das vertrauenswürdige Stamm Zertifikat automatisch. Für Computer und mobile Geräte, die nicht der Domäne beigetreten sind, muss dieses Zertifikat auf andere Weise installiert werden, um die Registrierung zuzulassen.

> [!NOTE]
> Wenn die Webserver Zertifikate von einer öffentlichen Zertifizierungsstelle ausgestellt werden, werden diese Zertifizierungsstellen von den meisten Geräten bereits als vertrauenswürdig eingestuft. Wenn Ihr Entwurf die Verwendung einer dieser öffentlichen Zertifizierungsstellen einschließt, müssen Sie diesen Schritt nicht durchführen.

Nachdem Sie [das vertrauenswürdige Stamm Zertifikat exportiert](set-up-certificates-on-premises-mdm.md#bkmk_exportCert)haben, müssen Sie es auf Geräten installieren, die es für die Registrierung benötigen. Beispielsweise Geräte, die nicht der Domäne beigetreten sind und nicht automatisch aus Active Directory erhalten werden können. Der Prozess, den Sie verwenden, hängt von den folgenden Faktoren ab:

- Bestimmte Gerätetypen und technische Funktionen
- Betriebssystemversion
- Anforderungen an die Geschäfts-, Sicherheits-und Benutzer Leistung

Die folgende Liste enthält einige Beispiel Methoden zum übermitteln und Installieren des vertrauenswürdigen Stamm Zertifikats auf Geräten:

- Dateifreigabe

- E-Mail-Anlage

- Speicherkarte

- Verbundenes Gerät

- Cloudspeicher (z. B. OneDrive)

- NFC-Verbindung (Near Field Communication)

- Barcodescanner

- Out-of-Box-Experience (OOBE) des bereitstellenden Pakets

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>Manuelles Installieren des vertrauenswürdigen Stamm Zertifikats in Windows

1. Navigieren Sie auf dem zu registrierenden Gerät im Datei-Explorer zur vertrauenswürdigen Stamm Zertifikatsdatei (CER-Datei), und **Öffnen** Sie Sie.

1. Klicken Sie im Zertifikat Fenster auf **Zertifikat installieren**.

1. Wählen Sie im Zertifikat Import-Assistenten die Option **lokaler Computer**aus, und klicken Sie dann **auf Weiter, um als** Administrator fortzufahren.

1. Wählen Sie auf der Seite Zertifikat Speicher die Option **alle Zertifikate in folgendem Speicher speichern aus**, und klicken Sie dann auf **Durchsuchen**.

1. Wählen Sie im Fenster Zertifikat Speicher auswählen die Option **Vertrauenswürdige Stamm Zertifizierungs**stellen aus, und klicken Sie dann auf **OK**.

1. Vervollständigen Sie den Assistenten.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Geräte registrieren](../deploy-use/enroll-devices-on-premises-mdm.md)
