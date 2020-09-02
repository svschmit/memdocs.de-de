---
title: Registrieren von dedizierten oder vollständig verwalteten Android Enterprise-Geräten oder unternehmenseigenen Android Enterprise-Geräten mit einem Arbeitsprofil in Intune
titleSuffix: Microsoft Intune
description: In diesem Artikel erfahren Sie, wie Sie dedizierte oder vollständig verwaltete Android Enterprise-Geräte oder unternehmenseigene Android Enterprise-Geräte mit einem Arbeitsprofil in Intune registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9fafc6a48e933fbcce692c560532736808cbf7c4
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915244"
---
# <a name="enroll-your-android-enterprise-dedicated-fully-managed-or-corporate-owned-with-work-profile-devices"></a>Registrieren eines dedizierten oder vollständig verwalteten Android Enterprise-Geräts oder eines unternehmenseigenen Android Enterprise-Geräts mit einem Arbeitsprofil

Nachdem Sie Ihre [dedizierten](android-kiosk-enroll.md), [vollständig verwalteten](android-fully-managed-enroll.md) oder [unternehmenseigenen Android Enterprise-Geräte mit einem Arbeitsprofil](android-corporate-owned-work-profile-enroll.md) in Intune eingerichtet haben, können Sie diese registrieren. Die Intune-Registrierung für dedizierte Geräte und vollständig verwaltete Geräte beginnt mit dem Zurücksetzen auf die Werkseinstellungen. Wie Sie Ihre Android Enterprise-Geräte registrieren, hängt vom Betriebssystem ab.

| Registrierungsmethode | Mindestversion des Android-Betriebssystems für dedizierte und vollständig verwaltete Geräte |
| ----- | ----- |
| Near Field Communication | 6.0 |
| Token-Eingabe | 6.0 |
| QR-Code | 7.0 |
| Zero-Touch  | 8.0<br><br> Bei beteiligten Herstellern |
| [Registrierung mobiler Geräte für Knox](./android-samsung-knox-mobile-enroll.md)  | 6.0<br><br> Nur auf Geräten mit Samsung Knox 2.8 oder höher. |

## <a name="enroll-by-using-near-field-communication-nfc"></a>Registrieren mit NFC (Near Field Communication)

Bei Geräten der Version 6 oder höher, die NFC unterstützen, können Sie Ihre Geräte bereitstellen, indem Sie ein speziell formatiertes NFC-Tag erstellen. Sie können Ihre eigene App oder ein beliebiges NFC-Tagerstellungstool verwenden. Weitere Informationen finden Sie im Blogbeitrag [NFC-based Android Enterprise device enrollment with Microsoft Intune (NFC-basierte Android Enterprise-Geräteregistrierung mit Microsoft Intune)](/archive/blogs/cbernier/nfc-based-android-enterprise-device-enrollment-with-microsoft-intune) und in der Google-Dokumentation zur [Android Management API](https://developers.google.com/android/management/provision-device#nfc_method).

## <a name="enroll-by-using-a-token"></a>Registrieren mithilfe eines Tokens

Für Android 6-Geräte und höher können Sie das Token zum Registrieren des Geräts verwenden. Bei Android 6.1 und höheren Versionen kann bei Verwendung der Registrierungsmethode **afw#setup** auch der QR-Code-Scan genutzt werden.

1. Schalten Sie das zurückgesetzte Gerät ein.
2. Wählen Sie auf dem **Willkommenssbildschirm** Ihre Sprache aus.
3. Stellen Sie eine **WLAN**-Verbindung her, und tippen Sie dann auf **WEITER**.
4. Akzeptieren Sie Nutzungsbedingungen von Google, und tippen Sie dann auf **WEITER**.
5. Geben Sie auf dem Google-Anmeldebildschirm anstelle eines Gmail-Kontos **afw#setup** ein, und tippen Sie dann auf **WEITER**.
6. Tippen Sie bei der **Android-Geräterichtlinien**-App auf **INSTALLIEREN**.
7. Fahren Sie mit der Installation dieser Richtlinie fort.  Einige Geräte erfordern möglicherweise, dass zusätzliche Lizenzbedingungen akzeptiert werden.
8. Lassen Sie auf dem Bildschirm **Dieses Gerät registrieren** zu, dass Ihr Gerät den QR-Code scannen kann, oder geben Sie das Token manuell ein.
9. Führen Sie die angezeigten Eingabeaufforderungen durch, um die Registrierung abzuschließen.

## <a name="enroll-by-using-a-qr-code"></a>Registrieren mithilfe eines QR-Codes

Auf Android 7-Geräten und höher können Sie den QR-Code aus dem Registrierungsprofil scannen, um das Gerät zu registrieren.

> [!Note]
> Bei bestimmten Zoomeinstellungen des Browsers können Geräte möglicherweise keine QR-Codes scannen. Dieses Problem lässt sich durch die Erhöhung des Zooms beheben.

1. Tippen Sie mehrmals auf den ersten Bildschirm, der nach einer Zurücksetzung angezeigt wird, um einen QR-Scanner auf dem Android-Gerät zu starten.
2. Auf Android 7- und 8-Geräten werden Sie dazu aufgefordert, einen QR-Scanner zu installieren. Auf Android 9-Geräten und höher ist bereits ein QR-Scanner installiert.
3. Verwenden Sie den QR-Scanner zum Scannen des QR-Codes vom Registrierungsprofil, und führen Sie anschließend die angezeigten Eingabeaufforderungen aus, um die Registrierung durchzuführen.

## <a name="enroll-by-using-google-zero-touch"></a>Registrieren mithilfe von Google Zero-Touch

Das Gerät muss das Zero-Touch-System von Google unterstützen und einem Lieferanten zugeordnet sein, der Teil des Diensts ist, damit das System verwendet werden kann.  Weitere Informationen finden Sie auf der [Website zum Zero-Touch-Programm von Google](https://www.android.com/enterprise/management/zero-touch/).

1. Erstellen Sie eine neue Konfiguration in der Zero-Touch-Konsole.
2. Wählen Sie in der EMM DPC-Dropdownliste **Microsoft Intune** aus.
3. Kopieren Sie den folgenden JSON-Code, und fügen Sie ihn in der Zero-Touch-Konsole von Google in das Feld „DPC-Extras“ ein. Ersetzen Sie die Zeichenfolge *YourEnrollmentToken* mit dem Registrierungstoken, das Sie als Teil Ihres Registrierungsprofils erstellt haben. Stellen Sie sicher, dass das Registrierungstoken mit doppelten Anführungszeichen umgeben ist.

    ```json
    {
        "android.app.extra.PROVISIONING_DEVICE_ADMIN_COMPONENT_NAME": "com.google.android.apps.work.clouddpc/.receivers.CloudDeviceAdminReceiver",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_SIGNATURE_CHECKSUM": "I5YvS0O5hXY46mb01BlRjq4oJJGs2kuUcHvVkAPEXlg",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION": "https://play.google.com/managed/downloadManagingApp?identifier=setup",

        "android.app.extra.PROVISIONING_ADMIN_EXTRAS_BUNDLE": {
            "com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "YourEnrollmentToken"
        }
    }
    ```

4. Wählen Sie **Anwenden** aus.

## <a name="enroll-by-using-knox-mobile-enrollment"></a>Registrierung mithilfe der Registrierung mobiler Geräte für Knox
Wenn Sie die Registrierung mobiler Geräte für Samsung Knox (Knox Mobile Enrollment, KME) verwenden möchten, muss das Gerät die Betriebssystemversion Android 6 oder höher und Knox 2.8 oder höher besitzen. Weitere Informationen finden Sie unter [Automatisches Registrieren von Android-Geräten mit Samsung Knox Mobile Enrollment](./android-samsung-knox-mobile-enroll.md).

## <a name="next-steps"></a>Nächste Schritte
- [Bereitstellen von Android-Apps](../apps/apps-deploy.md)
- [Hinzufügen von Android-Konfigurationsrichtlinien](../configuration/device-profiles.md)