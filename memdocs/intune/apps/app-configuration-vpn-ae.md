---
title: Konfigurieren eines VPN oder Pro-App-VPN für Android Enterprise-Geräte in Microsoft Intune – Microsoft-Dokumentation
titleSuffix: Microsoft Intune
description: Verwenden Sie eine App-Konfigurationsrichtlinie, um ein VPN- oder Pro-App-VPN-Profil für Android Enterprise-Geräte in Microsoft Intune hinzuzufügen oder zu erstellen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e869ad933e86d9330dbb8d6a26b1886a71cee07
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262896"
---
# <a name="use-a-vpn-and-per-app-vpn-policy-on-android-enterprise-devices-in-microsoft-intune"></a>Verwenden einer VPN- oder Pro-App-VPN-Richtlinie auf Android Enterprise-Geräten in Microsoft Intune

Virtuelle private Netzwerke (VPNs) ermöglichen es Benutzern, remote auf Organisationsressourcen zuzugreifen, beispielsweise zu Hause, im Hotel, im Café oder an anderen Orten. In Microsoft Intune können Sie VPN-Client-Apps auf Android Enterprise-Geräten mithilfe einer App-Konfigurationsrichtlinie konfigurieren. Diese Richtlinie können Sie dann zusammen mit der VPN-Konfiguration auf Geräten in Ihrer Organisation bereitstellen.

Sie können auch VPN-Richtlinien erstellen, die von bestimmten Apps verwendet werden. Dieses Feature wird als „Pro-App-VPN“ bezeichnet. Wenn Sie App aktiv ist, kann sie eine Verbindung zum VPN herstellen und über das VPN auf Ressourcen zugreifen. Wenn die App nicht aktiv ist, wird das VPN nicht verwendet.

Diese Funktion gilt für:

- Android Enterprise

Es gibt zwei Möglichkeiten, eine App-Konfigurationsrichtlinie für Ihre VPN-Client-App zu erstellen:

- Konfigurations-Designer
- JSON-Daten

In diesem Artikel werden beide Optionen zum Erstellen eines Pro-App-VPN und einer VPN-Konfigurationsrichtlinie beschrieben.

> [!NOTE]
> Viele der Konfigurationsparameter für VPN-Clients sind ähnlich. Jede App verfügt jedoch über eindeutige Schlüssel und Optionen. Wenden Sie sich an Ihren VPN-Anbieter, wenn Sie Fragen dazu haben.

## <a name="before-you-begin"></a>Vorbereitung

- Android löst beim Öffnen einer App nicht automatisch eine VPN-Clientverbindung aus. Die VPN-Verbindung muss manuell gestartet werden. Alternativ dazu können Sie auch [Always-On-VPN](../configuration/vpn-settings-android-enterprise.md) verwenden, um die Verbindung zu starten.

- Die folgenden VPN-Clients unterstützen Intune-App-Konfigurationsrichtlinien:

  - Cisco AnyConnect
  - Citrix SSO
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - SonicWall Mobile Connect

- Wenn Sie die VPN-Richtlinie in Intune erstellen, wählen Sie verschiedene zu konfigurierende Schlüssel aus. Die Namen dieser Schlüssel unterscheiden sich bei den verschiedenen VPN-Client-Apps. Daher finden Sie in Ihrer Umgebung möglicherweise andere Schlüsselnamen als in den Beispielen in diesem Artikel.

- Sowohl Konfigurations-Designer als auch JSON-Daten können erfolgreich die zertifikatbasierte Authentifizierung verwenden. Wenn die VPN-Authentifizierung Clientzertifikate erfordert, erstellen Sie zuerst die Zertifikatprofile, bevor Sie die VPN-Richtlinie erstellen. Die VPN-App-Konfigurationsrichtlinien verwenden die Werte aus den Zertifikatprofilen.

  Android Enterprise-Arbeitsprofilgeräte unterstützen SCEP- und PKCS-Zertifikate. Vollständig verwaltete, dedizierte und unternehmenseigene Android Enterprise-Arbeitsprofilgeräte unterstützen nur SCEP-Zertifikate. Weitere Informationen finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung in Microsoft Intune](../protect/certificates-configure.md).

## <a name="per-app-vpn-overview"></a>Pro-App-VPN – Übersicht

Das Erstellen und Testen eines Pro-App-VPN umfasst die folgenden grundlegenden Schritte:

1. Wählen Sie die VPN-Clientanwendung aus. Im Abschnitt [Vorbereitung](#before-you-begin) in diesem Artikel sind die unterstützten Apps aufgeführt.
2. Rufen Sie die Anwendungspaket-IDs der Apps ab, die die VPN-Verbindung verwenden. Unter [Ermitteln der App-Paket-ID](#get-the-app-package-id) in diesem Artikel erfahren Sie, wie Sie dabei vorgehen.
3. Wenn Sie Zertifikate zum Authentifizieren der VPN-Verbindung verwenden, müssen Sie die Zertifikatprofile erstellen und bereitstellen, bevor Sie die VPN-Richtlinie bereitstellen. Stellen Sie sicher, dass die Bereitstellung der Zertifikatprofile erfolgreich verläuft. Weitere Informationen finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung in Microsoft Intune](../protect/certificates-configure.md).
4. Fügen Sie die [VPN-Clientanwendung](apps-add-android-for-work.md) zu Intune hinzu, und stellen Sie sie für Ihre Benutzer und Geräte bereit.
5. Erstellen Sie die VPN-App-Konfigurationsrichtlinie. Verwenden Sie in der Richtlinie die App-Paket-IDs und Zertifikatinformationen.
6. Stellen Sie die neue VPN-Richtlinie bereit.
7. Bestätigen Sie, dass die VPN-Client-App erfolgreich eine Verbindung mit Ihrem VPN-Server herstellen kann.
8. Wenn die App aktiv ist, vergewissern Sie sich, dass Datenverkehr von der App erfolgreich über das VPN geleitet wird.

## <a name="get-the-app-package-id"></a>Ermitteln der App-Paket-ID

Ermitteln Sie die Paket-ID für jede Anwendung ab, die das VPN verwenden soll. Bei öffentlich verfügbaren Anwendungen können Sie die App-Paket-ID im Google Play Store ermitteln. Die URL der einzelnen Anwendungen enthält die Paket-ID.

Im folgenden Beispiel lautet die Paket-ID der Microsoft Edge-Browser-App `com.microsoft.emmx`. Die Paket-ID ist ein Teil der URL:

:::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png" alt-text="Ermitteln der App-Paket-ID in der URL im Google Play Store":::

Bei branchenspezifischen Apps erhalten Sie die Paket-ID vom Anbieter oder Anwendungsentwickler.

## <a name="certificates"></a>Zertifikate

In diesem Artikel wird davon ausgegangen, dass Ihre VPN-Verbindung die zertifikatbasierte Authentifizierung verwendet. Es wird ebenfalls vorausgesetzt, dass alle Zertifikate in der Kette, die für eine erfolgreiche Authentifizierung der Clients erforderlich sind, erfolgreich bereitgestellt wurden. In der Regel umfasst die Zertifikatkette das Clientzertifikat, etwaige Zwischenzertifikate und das Stammzertifikat.

Weitere Informationen zu Zertifikaten finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung in Microsoft Intune](../protect/certificates-configure.md).

Wenn das Zertifikatprofil für die Clientauthentifizierung bereitgestellt ist, wird im Profil ein Zertifikattoken erstellt. Dieses Token wird zum Erstellen der VPN-App-Konfigurationsrichtlinie verwendet.

Wenn Sie mit dem Erstellen von App-Konfigurationsrichtlinien nicht vertraut sind, finden Sie weitere Informationen unter [Hinzufügen von App-Konfigurationsrichtlinien für verwaltete Android Enterprise-Geräte](app-configuration-policies-use-android.md).

## <a name="use-the-configuration-designer"></a>Verwenden des Konfigurations-Designers

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen** > **Verwaltete Geräte** aus.
3. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname wäre beispielsweise **App-Konfigurationsrichtlinie: Cisco AnyConnect VPN-Richtlinie für Android Enterprise-Arbeitsprofilgeräte**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **Plattform**: Wählen Sie **Android Enterprise** aus.
    - **Profiltyp**: Folgende Optionen sind verfügbar:
      - **Alle Profiltypen**: Diese Option unterstützt die Authentifizierung per Benutzername und Kennwort. Wenn Sie die zertifikatbasierte Authentifizierung verwenden, nutzen Sie diese Option nicht.
      - **Nur vollständig verwaltetes, dediziertes und unternehmenseigenes Arbeitsprofil**: Diese Option unterstützt die zertifikatbasierte Authentifizierung und die Authentifizierung per Benutzername und Kennwort.
      - **Nur Arbeitsprofil**: Diese Option unterstützt die zertifikatbasierte Authentifizierung und die Authentifizierung per Benutzername und Kennwort.
    - **Ziel-App:** Wählen Sie die VPN-Client-App aus, die Sie zuvor hinzugefügt haben. Im folgenden Beispiel wird die Cisco AnyConnect-VPN-Client-App verwendet:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png" alt-text="Erstellen einer App-Konfigurationsrichtlinie zum Konfigurieren eines VPN oder Pro-App-VPN in Microsoft Intune":::

4. Wählen Sie **Weiter** aus.
5. Geben Sie in **Einstellungen** die folgenden Eigenschaften ein:

    - **Format der Konfigurationseinstellungen**: Wählen Sie **Konfigurations-Designer verwenden** aus:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png" alt-text="Erstellen einer VPN-Richtlinie für die App-Konfiguration in Microsoft Intune mit dem Konfigurations-Designer: Beispiel":::

    - **Hinzufügen**: Zeigt die Liste der Konfigurationsschlüssel an. Wählen Sie alle Konfigurationsschlüssel aus, die Sie für Ihre Konfiguration benötigen, und klicken Sie auf **OK**.

      Im folgenden Beispiel wurde ein minimale Liste für ein AnyConnect-VPN ausgewählt, einschließlich zertifikatbasierter Authentifizierung und Pro-App-VPN:
  
      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" alt-text="Hinzufügen von Konfigurationsschlüsseln zu einer VPN-App-Konfigurationsrichtlinie in Microsoft Intune mithilfe des Konfigurations-Designers: Beispiel":::

    - **Konfigurationswert**: Geben Sie die Werte für die ausgewählten Konfigurationsschlüssel ein. Denken Sie daran, dass sich die Schlüsselnamen je nach verwendeter VPN-Client-App unterscheiden. In unserem Beispiel wurden folgende Schlüssel ausgewählt:

      - **Apps mit zugelassenem Pro-App-VPN**: Geben Sie die Anwendungspaket-ID(s) ein, die Sie zuvor erfasst haben. Beispiel:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png" alt-text="Eingeben der Paket-IDs zugelassener Apps zu einer VPN-App-Konfigurationsrichtlinie in Microsoft Intune mithilfe des Konfigurations-Designers: Beispiel":::

      - **Schlüsselkettenzertifikat-Alias** (optional): Ändern Sie den **Werttyp** von **Zeichenfolge** in **Zertifikat**. Wählen Sie das Clientzertifikatprofil aus, das mit der VPN-Authentifizierung verwendet werden soll. Beispiel:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png" alt-text="Ändern des Schlüsselkettenzertifikat-Alias in einer VPN-App-Konfigurationsrichtlinie in Microsoft Intune mithilfe des Konfigurations-Designers: Beispiel":::

      - **Protokoll:** Wählen Sie das Tunnelprotokoll **SSL** oder **IPsec** des VPN aus.
      - **Verbindungsname**: Geben Sie einen benutzerfreundlichen Anzeigenamen für die VPN-Verbindung ein. Benutzer sehen diesen Verbindungsnamen auf ihren Geräten. Geben Sie beispielsweise `ContosoVPN` ein.
      - **Host:** Geben Sie die Hostnamen-URL zum Head-End-Router ein. Geben Sie beispielsweise `vpn.contoso.com` ein.

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png" alt-text="Beispiele zur Angabe von Protokoll, Verbindungsname und Hostname in einer VPN-App-Konfigurationsrichtlinie in Microsoft Intune mithilfe des Konfigurations-Designers":::

6. Wählen Sie **Weiter** aus.
7. Wählen Sie unter **Zuweisungen** die Gruppen aus, denen die VPN-App-Konfigurationsrichtlinie zugewiesen werden soll.

    Wählen Sie **Weiter** aus.

8. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und die Richtlinie wird in den Gruppen bereitgestellt. Die Richtlinie wird auch in der Liste der App-Konfigurationsrichtlinien angezeigt.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png" alt-text="Überprüfen der App-Konfigurationsrichtlinie mit dem Konfigurations-Designer-Flow in Microsoft Intune: Beispiel":::

## <a name="use-json"></a>Verwenden von JSON

Verwenden Sie diese Option, wenn Sie nicht alle erforderlichen VPN-Einstellungen für den **Konfigurations-Designer** kennen. Wenn Sie Hilfe benötigen, wenden Sie sich an Ihren VPN-Anbieter.

### <a name="get-the-certificate-token"></a>Ermitteln des Zertifikattokens

In diesen Schritten erstellen Sie eine temporäre Richtlinie. Diese Richtlinie wird nicht gespeichert. Sie dient nur dazu, das Zertifikattoken zu kopieren. Dieses Token verwenden Sie beim Erstellen der VPN-Richtlinie mit JSON (nächster Abschnitt).

1. Wechseln Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), und wählen Sie **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen** > **Verwaltete Geräte** aus.
2. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen beliebigen Namen ein. Diese Richtlinie ist temporär und wird nicht gespeichert.
    - **Plattform**: Wählen Sie **Android Enterprise** aus.
    - **Profiltyp**: Wählen Sie die Option **Nur Arbeitsprofil** aus.
    - **Ziel-App:** Wählen Sie die VPN-Client-App aus, die Sie zuvor hinzugefügt haben.

3. Wählen Sie **Weiter** aus.
4. Geben Sie in **Einstellungen** die folgenden Eigenschaften ein:

    - **Format der Konfigurationseinstellungen**: Wählen Sie **Konfigurations-Designer verwenden** aus.
    - **Hinzufügen**: Zeigt die Liste der Konfigurationsschlüssel an. Wählen Sie einen beliebigen Schlüssel aus, für den **Zeichenfolge** als **Werttyp** angegeben ist. Klicken Sie auf **OK**.

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" alt-text="Im Konfigurations-Designer: Auswahl eines beliebigen Schlüssels mit dem Werttyp „Zeichenfolge“ in einer Microsoft Intune-VPN-App-Konfigurationsrichtlinie":::

5. Ändern Sie den **Werttyp** von **Zeichenfolge** in **Zertifikat**. In diesem Schritt können Sie das richtige Clientzertifikatprofil auswählen, mit dem das VPN authentifiziert wird:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png" alt-text="Beispiel für die Änderung des Verbindungsnamens in einer VPN-App-Konfigurationsrichtlinie in Microsoft Intune":::

6. Ändern Sie den **Werttyp** gleich wieder zurück in **Zeichenfolge**. Beachten Sie, dass der **Konfigurationswert** in ein Token des Formats `{{cert:GUID}}` geändert wird:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png" alt-text="Der Konfigurationswert zeigt das Zertifikattoken in einer VPN-App-Konfigurationsrichtlinie in Microsoft Intune":::

7. Kopieren Sie dieses Zertifikattoken, und fügen Sie es in eine andere Datei ein, z. B. in einem Text-Editor.

8. Verwerfen Sie diese Richtlinie. Speichern Sie sie nicht. Der einzige Zweck dieser Richtlinie war es, das Zertifikattoken kopieren zu können.

### <a name="create-the-vpn-policy-using-json"></a>Erstellen der VPN-Richtlinie mit JSON

1. Wechseln Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), und wählen Sie **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen** > **Verwaltete Geräte** aus.

2. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname wäre beispielsweise **App-Konfigurationsrichtlinie: JSON-Cisco AnyConnect VPN-Richtlinie für Android Enterprise-Arbeitsprofilgeräte im gesamten Unternehmen**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **Plattform**: Wählen Sie **Android Enterprise** aus.
    - **Profiltyp**: Folgende Optionen sind verfügbar:
      - **Alle Profiltypen**: Diese Option unterstützt die Authentifizierung per Benutzername und Kennwort. Wenn Sie die zertifikatbasierte Authentifizierung verwenden, nutzen Sie diese Option nicht.
      - **Nur vollständig verwaltetes, dediziertes und unternehmenseigenes Arbeitsprofil**: Diese Option unterstützt die zertifikatbasierte Authentifizierung und die Authentifizierung per Benutzername und Kennwort.
      - **Nur Arbeitsprofil**: Diese Option unterstützt die zertifikatbasierte Authentifizierung und die Authentifizierung per Benutzername und Kennwort.
    - **Ziel-App:** Wählen Sie die VPN-Client-App aus, die Sie zuvor hinzugefügt haben. 

3. Wählen Sie **Weiter** aus.
4. Geben Sie in **Einstellungen** die folgenden Eigenschaften ein:

    - **Format der Konfigurationseinstellungen**: Wählen Sie **JSON-Daten eingeben** aus. Sie können die JSON-Datei direkt bearbeiten.
    - **JSON-Vorlage herunterladen**: Verwenden Sie diese Option, um die Vorlage herunterzuladen und in einem externen Editor zu aktualisieren. Beachten Sie, dass einige Text-Editoren **typografische Anführungszeichen** verwenden, dies könnte zu ungültigen JSON-Einträgen führen.

    Nachdem Sie die für Ihre Konfiguration erforderlichen Werte eingegeben haben, entfernen Sie alle Einstellungen, die `"STRING_VALUE"` oder `STRING_VALUE` aufweisen.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png" alt-text="Beispiel für die Verwendung des JSON-Flows: JSON bearbeiten":::

5. Wählen Sie **Weiter** aus.
6. Wählen Sie unter **Zuweisungen** die Gruppen aus, denen die VPN-App-Konfigurationsrichtlinie zugewiesen werden soll.

    Wählen Sie **Weiter** aus.

7. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und die Richtlinie wird in den Gruppen bereitgestellt. Die Richtlinie wird auch in der Liste der App-Konfigurationsrichtlinien angezeigt.

#### <a name="json-example-for-f5-access-vpn"></a>JSON-Beispiel für ein F5 Access-VPN

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="additional-information"></a>Zusätzliche Informationen

- [Hinzufügen von App-Konfigurationsrichtlinien für verwaltete Android Enterprise-Geräte](app-configuration-policies-use-android.md)
- [Android Enterprise-Geräteeinstellungen zur VPN-Konfiguration in Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Nächste Schritte

- [Erstellen von VPN-Profilen zum Herstellen einer Verbindung mit VPN-Servern in Intune](../configuration/vpn-settings-configure.md)
