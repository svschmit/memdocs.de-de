---
title: Konfigurieren eines VPN für Android Enterprise-Geräte
titleSuffix: Microsoft Intune
description: In diesem Artikel erfahren Sie, wie Sie mit einer App-Schutzrichtlinie ein VPN für Android Enterprise-Geräte konfigurieren.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
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
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347417"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>Konfigurieren eines VPN für Android Enterprise-Geräte

In diesem Thema wird beschrieben, wie Sie eine App-Konfigurationsrichtlinie erstellen, die zusammen mit einem VPN-Client auf Android Enterprise-Geräten bereitgestellt werden kann. Mit dieser Konfiguration kann der Netzwerkdatenverkehr für ausgewählte Anwendungen auf Unternehmensressourcen zugreifen.

> [!NOTE]
> Das automatische Auslösen von VPN-Clientverbindungen beim Öffnen einer ausgewählten Anwendung wird für die Android-Plattform derzeit nicht unterstützt. Die VPN-Verbindung muss zuerst manuell initiiert werden. Alternativ können Sie auch [Always On-VPN-Verbindungen](../configuration/vpn-settings-android-enterprise.md) verwenden.

Zu den Voraussetzungen für das Erstellen einer Konfigurationsrichtlinie, die einen erfolgreichen VPN-Zugriff ermöglicht, zählt, dass der ausgewählte VPN-Client Konfigurationsprofile für verwaltete Anwendungen unterstützt. Die VPN-Clients, die die Intune-App-Konfigurationsrichtlinien unterstützen, sind momentan:
- Cisco AnyConnect
- Citrix SSO
- F5 Access
- Global Connect von Palo Alto
- Pulse Secure
- SonicWall Mobile Connect

Wenn die Methode für den Authentifizierungszugriff auf den VPN-Endpunkt Clientzertifikate erfordert, sollten die Zertifikatprofile vorab erstellt werden, damit die erforderlichen Werte für die App-Konfigurationsrichtlinie aufgefüllt werden können.

> [!NOTE]
> Während Android Enterprise-Arbeitsprofile sowohl SCEP- als auch PKCS-Zertifikate unterstützen, werden in Szenarios für Android Enterprise-Gerätebesitzer derzeit nur SCEP-Zertifikate unterstützt. 

Die grundlegenden Schritte für das Erstellen und Testen des App-spezifischen VPN-Profils lauten wie folgt:
1.  Wählen Sie die angemessene VPN-Clientanwendung für Ihre Infrastruktur aus.
2.  Ermitteln Sie die Anwendungspaket-IDs der Produktivitäts-Apps, die Sie mit der VPN-Verbindung verbinden möchten.
3.  Stellen Sie alle Zertifikatprofile bereit, die laut den Authentifizierungsanforderungen der VPN-Verbindung erforderlich sind. Überprüfen Sie, ob die Bereitstellung erfolgreich war.
4.  Stellen Sie die VPN-Clientanwendung bereit.
5.  Bereiten Sie das auf der App-Konfiguration basierende VPN-Profil mithilfe der Informationen vor, die während der vorherigen Schritte erfasst wurden
6.  Stellen Sie das neu erstellte VPN-Profil bereit.
7.  Überprüfen Sie, ob die VPN-Client-App erfolgreich eine Verbindung mit der VPN-Serverinfrastruktur herstellt.
8.  Überprüfen Sie, ob der Datenverkehr von Ihren ausgewählten Produktivitäts-Apps erfolgreich über das VPN übertragen wird, wenn es aktiv ist.

## <a name="get-the-app-package-id"></a>Ermitteln der App-Paket-ID

Bestimmen Sie für jede Anwendung, der Sie VPN-Zugriff erteilen möchte, die Paket-ID. Für öffentlich verfügbare Anwendungen können Sie die Paket-IDs über den Google Play Store ermitteln. Die URL der einzelnen Anwendungen enthält die Paket-ID. Die Paket-ID für die Android-Version des Microsoft Edge-Browsers lautet z. B. `com.microsoft.emmx`. Die Paket-ID ist ein Teil der URL.

![Ein Beispiel für die Suche nach der ID eines App-Pakets](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

Bitten Sie bei branchenspezifischen Apps den Anbieter oder das Anwendungsentwicklungsteam, Ihnen die relevante Paket-ID zu übermitteln.

## <a name="certificates"></a>Zertifikate

In diesem Thema wird davon ausgegangen, dass Ihre VPN-Verbindung auf einer zertifikatbasierten Authentifizierung beruht und dass Sie alle Zertifikate, die für eine erfolgreiche Clientauthentifizierung erforderlich sind, erfolgreich in der Kette bereitgestellt haben. In der Regel handelt es sich dabei um das Clientzertifikat, etwaige Zwischenzertifikate und das Stammzertifikat.
Weitere Informationen zur Bereitstellung von Zertifikaten für Android Enterprise finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung in Microsoft Intune](../protect/certificates-configure.md).

Nachdem Ihr Zertifikatprofil für die Clientauthentifizierung bereitgestellt wurde, benötigen Sie einige Informationen zu diesem Profil, um die Konfigurationsrichtlinie für VPN-Apps zu erstellen.
Wenn Sie mit dem Erstellen von App-Konfigurationsprofilen nicht vertraut sind, lesen Sie den Artikel [Hinzufügen von App-Konfigurationsrichtlinien für verwaltete Android Enterprise-Geräte](../apps/app-configuration-policies-use-android.md).
 

## <a name="build-the-vpn-profile"></a>Erstellen des VPN-Profils

Es gibt zwei Möglichkeiten, die App-Konfigurationsrichtlinie für Ihre VPN-App zu erstellen. Sie können den **Konfigurations-Designer** oder die Option **JSON-Daten** verwenden. Die Option **JSON-Daten** muss verwendet werden, wenn im **Konfigurations-Designer** nicht alle erforderlichen VPN-Einstellungen verfügbar sind. Wenn Sie feststellen, dass Sie für die JSON-Option benötigen, wenden Sie sich an Ihren VPN-Anbieter. In diesem Thema werden Beispiele für beide Methoden gezeigt. Beide Methoden, die Option **JSON-Daten** sowie der **Konfigurations-Designer**, unterstützen die zertifikatbasierte Authentifizierung. Wenn Sie die Methode **JSON-Daten** wählen, können Sie mit dem **Konfigurations-Designer** zunächst die erforderlichen Profilwerte extrahieren.

> [!NOTE]
> Obwohl viele sich der Konfigurationsparameter des VPN-Clients ähneln, verfügt jede App über einen eindeutigen Schlüssel und eindeutige Optionen. Wenden Sie sich an Ihren VPN-Anbieter, wenn Fragen auftreten. 

## <a name="use-the-configuration-designer-flow"></a>Verwenden des Konfigurations-Designers

1.  Fügen Sie als Erstes eine neue App-Konfigurationsrichtlinie für **verwaltete Geräte** hinzu.
2.  Geben Sie einen angemessenen Namen ein.
3.  Wählen Sie **Android Enterprise** als Plattform aus.
4.  Wählen Sie als Profiltyp entweder **Nur Arbeitsprofil** oder **Nur Gerätebesitzer** aus, wenn die zertifikatbasierte Authentifizierung erforderlich ist. Das **Profil für Arbeits- und Gerätebesitzer** ist nicht mit der zertifikatbasierten Authentifizierung kompatibel.
5.  Wählen Sie für die Ziel-App den VPN-Client aus, den Sie bereitgestellt haben. In diesem Beispiel verwenden Sie den zuvor bereitgestellten VPN-Client „Cisco AnyConnect“.

  ![Beispiel für das Erstellen einer App-Konfigurationsrichtlinie: Grundlagen](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. Wählen Sie auf der nächsten Seite in der Dropdownliste der Konfigurationseinstellungen die Option **Konfigurations-Designer verwenden** aus.

  ![Beispiel für die Verwendung des Konfigurations-Designer-Flows: Einstellungen](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. Klicken Sie auf **Hinzufügen**, um die Liste mit den Konfigurationsschlüsseln aufzurufen.
8.  Wählen Sie alle Konfigurationsschlüssel aus, die Sie für die ausgewählte Konfiguration benötigen. In diesem Beispiel verwenden Sie eine minimale Liste, um eine AnyConnect-VPN-Verbindung mit zertifikatbasierter Authentifizierung und App-spezifischen VPN-Profilen einzurichten.
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. Geben Sie für die Schlüssel **Verbindungsname**, **Host** und **Protokoll** die entsprechenden Werte ein.

  ![Beispiel für die Verwendung des Konfigurations-Designer-Flows: Auswahl der Konfigurationsschlüssel](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > Je nach der VPN-Clientanwendung, für die Sie die Richtlinie erstellen, können die Namen dieser Schlüssel variieren.

10. Geben Sie die Anwendungspaket-ID(s) ein, die Sie zuvor im Schlüssel **Per App VPN Allowed Apps** (Apps mit zugelassenem App-spezifischen Profil) erfasst haben.

  ![Beispiel für die Verwendung des Konfigurations-Designer-Flows: App-Paket-IDs](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. Ändern Sie im Schlüssel **KeyChain Certificate Alias** (KeyChain-Zertifikatalias) (optional) den **Werttyp** von **Zeichenfolge** in **Zertifikat**. Nun können Sie das richtige Clientzertifikatprofil auswählen, das für die VPN-Authentifizierung verwendet werden soll.

  ![Beispiel für die Verwendung des Konfigurations-Designer-Flows: Aktualisieren des KeyChain-Zertifikatalias](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. Wählen Sie auf der nächsten Seite alle entsprechenden Bereichstags aus.
13. Geben Sie auf der nächsten Seite die entsprechenden Gruppen ein, für die Sie die App-Konfigurationsrichtlinie bereitstellen möchten.
14. Klicken Sie auf **Erstellen**, um die Erstellung und Bereitstellung der Richtlinie abzuschließen.

  ![Beispiel für die Verwendung des Konfigurations-Designer-Flows: Überprüfung](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>Verwenden des JSON-Flows

Erstellen Sie ein temporäres Profil:
1.  Fügen Sie als Erstes eine neue App-Konfigurationsrichtlinie für **verwaltete Geräte** hinzu.
2.  Geben Sie einen geeigneten Namen ein (dieses Profil wird nur vorübergehend verwendet und daher NICHT gespeichert).
3.  Wählen Sie **Android Enterprise** als Plattform aus.
4.  Wählen Sie als Ziel-App den VPN-Client aus, den Sie bereitgestellt haben.
5.  Wählen Sie als Profiltyp entweder **Nur Arbeitsprofil** oder **Nur Gerätebesitzer** aus, wenn die zertifikatbasierte Authentifizierung erforderlich ist. Das **Profil für Arbeits- und Gerätebesitzer** ist nicht mit der zertifikatbasierten Authentifizierung kompatibel.

  ![Beispiel für die Verwendung des JSON-Flows: Grundlagen](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  Wählen Sie auf der nächsten Seite in der Dropdownliste **Konfigurationseinstellungen** die Option **Konfigurations-Designer verwenden** aus.

  ![Beispiel für die Verwendung des JSON-Flows: Konfigurationseinstellungen-Formats.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  Klicken Sie auf **Hinzufügen**, um die Liste mit den Konfigurationsschlüsseln aufzurufen.
8.  Wählen Sie einen der Schlüssel aus, für die als **Werttyp** die Option **Zeichenfolge** konfiguriert ist, und klicken Sie auf **OK**.

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  Ändern Sie nun den **Werttyp** von **Zeichenfolge** in **Zertifikat**. Nun können Sie das richtige Clientzertifikatprofil auswählen, das für die VPN-Authentifizierung verwendet werden soll.

  ![Beispiel für die Verwendung des JSON-Flows: Verbindungsname](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. Ändern Sie den **Werttyp** gleich wieder zurück in **Zeichenfolge**. Beachten Sie, dass der **Konfigurationswert** in ein Token des Formats `{{cert:GUID}}` geändert wird.
11. Wählen Sie die Tokendarstellung des Zertifikats aus, und kopieren Sie diese an einen alternativen Speicherort, z. B. in einen Text-Editor

  ![Beispiel für die Verwendung des JSON-Flows: Konfigurationswert](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. Verwerfen Sie das Profil, das erstellt wird. Der einzige Zweck der vorherigen Schritte war das Ermitteln des Zertifikattokens.

### <a name="create-the-vpn-profile"></a>Erstellen des VPN-Profils

1.  Fügen Sie als Erstes ein neues Anwendungskonfigurationsprofil für **verwaltete Geräte** hinzu.
2.  Geben Sie einen angemessenen Namen ein.
3.  Wählen Sie **Android Enterprise** als Plattform aus.
4.  Wählen Sie als Ziel-App den VPN-Client aus, den Sie bereitgestellt haben.
5.  Wählen Sie als Profiltyp entweder **Nur Arbeitsprofil** oder **Nur Gerätebesitzer** aus, wenn die zertifikatbasierte Authentifizierung erforderlich ist. Das **Profil für Arbeits- und Gerätebesitzer** ist nicht mit der zertifikatbasierten Authentifizierung kompatibel.
6.  Wählen Sie in der Dropdownliste **Konfigurationseinstellungen** die Option **JSON-Daten eingeben** aus.
7.  Sie können die JSON-Daten direkt bearbeiten. Wenn Sie dies bevorzugen, können Sie auch eine Vorlage über die Schaltfläche **JSON-Vorlage herunterladen** in einen externen Editor Ihrer Wahl herunterladen und diese dort bearbeiten. Seien Sie vorsichtig bei Text-Editoren, in denen **typografische Anführungszeichen** verwendet werden können: Durch Einfügen solcher Anführungszeichen wird JSON-Code ungültig.

  ![Beispiel für die Verwendung des JSON-Flows: JSON bearbeiten](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  Nachdem Sie die Werte aufgefüllt haben, die Sie für die gewünschte Konfiguration benötigen, müssen alle verbleibenden Einstellungen mit "STRING_VALUE" oder einem STRING_VALUE-Wert aus dem gesamten JSON-Code entfernt werden – unabhängig von der Methode, für die Sie sich entscheiden.

#### <a name="example-json-for-f5-access-vpn"></a>JSON-Beispiel für eine F5 Access-VPN-Verbindung

Nachstehend finden Sie ein Beispiel für JSON-Daten für eine F5 Access-VPN-Verbindung.

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

## <a name="summary"></a>Zusammenfassung

Mithilfe einer App-Konfigurationsrichtlinie für bei Android Enterprise registrierte Geräte können Sie App-spezifisches VPN-Verhalten einrichten, ohne dass dies direkt von der Plattform unterstützt wird. 

## <a name="additional-information"></a>Zusätzliche Informationen

Weitere Informationen finden Sie in den folgenden Themen:
- [Hinzufügen von App-Konfigurationsrichtlinien für verwaltete Android Enterprise-Geräte](../apps/app-configuration-policies-use-android.md)
- [Android Enterprise-Geräteeinstellungen zur VPN-Konfiguration in Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Nächste Schritte

- [Erstellen von VPN-Profilen zum Herstellen einer Verbindung mit VPN-Servern in Intune](../configuration/vpn-settings-configure.md)
