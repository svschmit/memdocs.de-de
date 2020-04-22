---
title: 'Schnellstart: Erstellen eines E-Mail-Geräteprofils für iOS/iPadOS-Geräte'
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie mit Microsoft Intune ein E-Mail-Geräteprofil erstellen können, damit iOS/-Geräte sicher auf Unternehmens-E-Mails zugreifen können.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af7657eb89df14e8429a81616e76d81a5a9ac5c1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327423"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>Schnellstart: Erstellen eines E-Mail-Geräteprofils für iOS/iPadOS

In diesem Schnellstart erfahren Sie, wie Sie ein E-Mail-Geräteprofil für iOS/iPadOS-Geräte erstellen. Dieses Profil gibt die Einstellungen an, die für die integrierte E-Mail-App auf dem iOS/iPadOS-Gerät erforderlich sind, um auf Unternehmens-E-Mails zugreifen zu können. E-Mail-Geräteprofile helfen beim geräteübergreifenden Standardisieren von Einstellungen und ermöglichen Endbenutzern den Zugriff auf Unternehmens-E-Mails auf ihren persönlichen Geräten, ohne dass ihrerseits eine Konfiguration erforderlich wäre. Um Ihre E-Mails noch besser zu schützen, können Sie mit einem E-Mail-Profil bestimmen, ob Geräte konform sind, und dann den bedingten Zugriff so einrichten, dass nur konforme Geräte auf E-Mails zugreifen können. Weitere Informationen zu E-Mail-Profilen finden Sie unter [Konfigurieren von E-Mail-Einstellungen in Microsoft Intune](email-settings-configure.md).

Wenn Sie über kein Intune-Abonnement verfügen, [registrieren Sie sich für eine kostenlose Testversion](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Anmelden bei Intune

Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) als globaler Administrator oder Intune-Dienstadministrator an. Wenn Sie ein Testabonnement für Intune erstellt haben, besitzt das Konto, mit dem Sie das Abonnement erstellt haben, die Rolle des globalen Administrators.

## <a name="create-an-iosipados-email-profile"></a>Erstellen eines iOS/iPadOS-E-Mail-Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
   ![Erstellen eines E-Mail-Profils für iOS/iPadOS in Intune](./media/quickstart-email-profile/ios-create-profile.png)

3. Geben Sie die folgenden Eigenschaften ein:
   - **Plattform**: Wählen Sie **iOS/iPadOS** aus.
   - **Profil**: Wählen Sie **E-Mail** aus.
  
4. Wählen Sie **Erstellen** aus.

5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:
   - **Name:** Geben Sie einen aussagekräftigen Namen für das neue Profil ein. Geben Sie für dieses Beispiel **iOS require work email** (Für iOS geschäftliche E-Mail erfordern) ein.
   - **Beschreibung:** Geben Sie **Voraussetzen, dass iOS/iPadOS-Geräte geschäftliche E-Mail verwenden** ein.


        ![Erstellen eines E-Mail-Profils zur Verwendung mit iOS/iPadOS-Geräten in Intune](./media/quickstart-email-profile/ios-email-profile-name.png)

6. Wählen Sie **Weiter** aus.

7. Wählen Sie **Konfigurationseinstellungen** aus, und geben Sie die folgenden Einstellungen ein (behalten Sie bei den anderen Einstellungen die Standardwerte bei):
   - **E-Mail-Server**: Geben Sie im Rahmen dieses Schnellstarts **outlook.office365.com** ein. Diese Einstellung gibt den Exchange-Speicherort (URL) des E-Mail-Servers an, den die iOS/iPadOS-Mail-App verwendet, um auf E-Mails zuzugreifen.
   - **Kontoname**: Geben Sie **Unternehmens-E-Mail-Adresse** ein.
   - **Benutzernamensattribut aus AAD**: Dieser Name ist das Attribut, das Intune aus Azure Active Directory (Azure AD) abruft. Intune generiert mit diesem Namen dynamisch den Benutzernamen für dieses Profil. Für diese Schnellstartanleitung soll angenommen werden, dass der **Benutzerprinzipalname** als Benutzername für das Profil verwenden werden soll (zum Beispiel user1@contoso.com).
   - **Attribut für E-Mail-Adresse aus AAD**: Diese Einstellung ist die E-Mail-Adresse aus Azure AD, die für die Anmeldung bei Exchange verwendet wird. Wählen Sie für diese Schnellstartanleitung **Benutzerprinzipalname** aus.
   - **Authentifizierungsmethode**: Wählen Sie im Rahmen dieses Schnellstarts **Benutzername und Kennwort** aus. (Sie können auch **Zertifikat** auswählen, wenn Sie bereits ein Zertifikat für Intune eingerichtet haben.)

8. Wählen Sie **Weiter** aus.

9. Wählen Sie in **Bereichsmarkierungen** (optional) **Weiter** aus. Wir verwenden für dieses Profil keine Bereichsmarkierungen.

10. Verwenden Sie in **Zuweisungen** die Dropdownliste für **Zuweisen zu**, und wählen Sie **Alle Benutzer und alle Geräte** aus.  Wählen Sie anschließend **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. 

## <a name="clean-up-resources"></a>Bereinigen der Ressourcen

Wenn Sie das erstellte Profil nicht für weitere Tutorials oder Tests verwenden möchten, können Sie es jetzt löschen.

1. Wählen Sie in Intune **Geräte** > **Gerätekonfiguration** aus.
2. Wählen Sie das erstellte Testprofil **Voraussetzen, dass iOS/iPadOS-Geräte geschäftliche E-Mail verwenden**, und dann **Löschen** aus. 

## <a name="next-steps"></a>Nächste Schritte

In diesem Schnellstart haben Sie ein E-Mail-Profil für iOS/iPadOS-Geräte erstellt. Jetzt können Sie mit diesem Profil bestimmen, ob ein iOS/iPadOS-Gerät konform ist, indem Sie eine Konformitätsrichtlinie erstellen, die alle nicht dem Profil entsprechenden iOS/iPadOS-Geräte als nicht konform markiert. Für noch besseren Schutz können Sie eine Richtlinie für bedingten Zugriff erstellen, die verhindert, dass nicht konforme iOS/iPadOS-Geräte auf E-Mails zugreifen. Weitere Informationen über Gerätekonformitätsrichtlinien finden Sie unter [Erste Schritte bei der Gerätekonformität in Intune](../protect/device-compliance-get-started.md).

> [!div class="nextstepaction"]
> [Tutorial: Schützen des Exchange Online-E-Mail-Diensts auf verwalteten Geräten](../protect/tutorial-protect-email-on-enrolled-devices.md)
