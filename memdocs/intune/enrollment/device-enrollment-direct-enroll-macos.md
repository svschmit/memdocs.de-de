---
title: Verwenden der direkten Registrierung für macOS-Geräte
titleSuffix: Microsoft Intune
description: Hier erfahren Sie, wie Sie macOS-Geräte mithilfe der direkten Registrierung registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f12b90dd49dc9a9783a39fb78d74c40c6838b1e
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819967"
---
# <a name="use-direct-enrollment-for-macos-devices"></a>Verwenden der direkten Registrierung für macOS-Geräte

Intune unterstützt die Registrierung von macOS-Geräten mithilfe der direkten Registrierung (Direct Enrollment, DE) für Unternehmensgeräte. Durch die direkte Registrierung wird das Gerät nicht gelöscht. Das Gerät wird über die macOS-Einstellungen registriert. Diese Methode wird nur von Geräten **ohne Benutzeraffinität** unterstützt.

## <a name="prerequisites"></a>Voraussetzungen

- physischer Zugriff auf macOS-Geräte
- [Festlegen der Autorität für die Verwaltung mobiler Geräte](../fundamentals/mdm-authority-set.md)
- [Ein Apple-MDM-Push-Zertifikat](apple-mdm-push-certificate-get.md)
 - Administratorrechte auf den zu registrierenden macOS-Geräten

## <a name="create-an-apple-configurator-profile-for-devices"></a>Erstellen eines Apple Configurator-Profils für Geräte

Ein Registrierungsprofil für Geräte definiert die Einstellungen, die während der Registrierung angewandt werden. Diese Einstellungen werden nur einmal angewendet. Führen Sie folgende Schritte aus, um ein Registrierungsprofil zu erstellen, mit dem macOS-Geräte mit der direkten Registrierung registriert werden.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Geräte registrieren** > **Apple-Registrierung** > **Apple Configurator**.

2. Klicken Sie auf **Profile** > **Erstellen**.

3. Geben Sie zu administrativen Zwecken unter **Registrierungsprofil erstellen** einen **Namen** und eine **Beschreibung** für das Profil ein. Benutzer können diese Informationen nicht sehen. Sie können das Feld „Name“ zum Erstellen einer dynamischen Gruppe in Azure Active Directory verwenden. Verwenden Sie den Profilnamen, um den Parameter „enrollmentProfileName“ zu definieren, um Geräte mit diesem Registrierungsprofil zuzuweisen. Erfahren Sie mehr über dynamische Gruppen in Azure Active Directory.

4. Wählen Sie für **Benutzeraffinität** die Option **Ohne Benutzeraffinität registrieren** aus. Verwenden Sie diese Option für Geräte, die keinem einzelnen Benutzer zugeordnet sind. Verwenden Sie diese Option für Geräte, die Aufgaben ohne den Zugriff auf lokale Benutzerdaten ausführen. Apps, die eine Benutzerzugehörigkeit erfordern (einschließlich der Unternehmensportal-App, die für die Installation branchenspezifischer Apps verwendet wird), funktionieren nicht. Dies ist für die direkte Registrierung erforderlich.

     > [!NOTE]
     > Die Option **Mit Benutzeraffinität registrieren** wird unter macOS bei Verwendung der direkten Registrierung nicht unterstützt. Bei Geräten, die Benutzeraffinität erfordern, verwenden Sie die automatische Geräteregistrierung.

6. Wählen Sie **Erstellen** aus, um das Profil zu speichern.

## <a name="direct-enrollment"></a>Direkte Anmeldung
Da die direkte Registrierung nur die Registrierung ohne Benutzeraffinität unterstützt, kann das Unternehmensportal nicht zum Installieren verfügbarer Anwendungen verwendet werden.

### <a name="export-the-profile-and-install-on-macos-devices"></a>Exportieren des Profils und Installieren auf macOS-Geräten

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Geräteregistrierung** > **Apple-Registrierung** > **Apple Configurator** > **Profile**, wählen Sie das zu exportierende Profil aus, und klicken Sie dann auf **Profil exportieren**.
2. Wählen Sie unter **Direkte Registrierung** die Option **Profil herunterladen** aus, und speichern Sie die Datei. 

     > [!NOTE]
     > Ein heruntergeladenes Registrierungsprofil ist nach dem Download zwei Wochen gültig. Sie können mithilfe dieses Links beliebig viele Registrierungsprofile herunterladen. Wenn ein neues Profil heruntergeladen wird, wird das vorherige nicht ungültig, die Ablaufzeit der zuvor heruntergeladene Datei wird jedoch nicht verlängert.
         
3. Übertragen Sie die Datei auf einen macOS-Computer, um sie direkt zu installieren.
4. Doppelklicken Sie auf die gespeicherte **MOBILECONFIG**-Datei, um sie unter „Profile“ zu öffnen.
5. Wenn Sie aufgefordert werden, das Verwaltungsprofil zu installieren, klicken Sie auf **Installieren**.
6. Bestätigen Sie bei der nächsten Aufforderung, dass Sie das Verwaltungsprofil installieren möchten, indem Sie auf **Installieren** klicken.
7. Geben Sie die Anmeldeinformationen für ein Administratorkonto auf dem macOS-Gerät ein, und klicken Sie auf **OK**.
8. Das macOS-Gerät ist jetzt bei Intune registriert und wird dort verwaltet. Die Zielprofile werden nun heruntergeladen.

## <a name="next-steps"></a>Nächste Schritte

Sie können macOS-Geräte [verwalten](../remote-actions/device-management.md), nachdem Sie sie registriert haben.