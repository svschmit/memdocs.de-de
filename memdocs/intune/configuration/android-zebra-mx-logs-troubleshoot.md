---
title: Verwenden von StageNow-Protokollen auf Android Zebra-Geräten in Microsoft Intune – Azure | Microsoft-Dokumentation
description: In diesem Artikel werden gängige Probleme und ihre Lösungen bei der Verwendung von StageNow auf Android-Geräten mit Microsoft Intune. Außerdem erfahren Sie, wie Sie Protokolle abrufen, und erhalten Beispiele zum Prüfen von Protokollen auf Fehler.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 607e2303cbec9ec7fc069db602d51684b71e6575
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083844"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>Problembehandlung und Ermitteln potenzieller Fehler auf Android Zebra-Geräten in Microsoft Intune



In Microsoft Intune können Sie [Zebra MX (Mobility Extensions) zum Verwalten von Android Zebra-Geräten](android-zebra-mx-overview.md) verwenden. Bei der Verwendung von Zebra-Geräten erstellen Sie Profile in StageNow, um Einstellungen zu verwalten und in Intune hochzuladen. Intune verwendet die StageNow-App, um die Anwendungen auf die Geräte anzuwenden. Die StageNow-App erstellt außerdem eine ausführliche Protokolldatei auf dem Gerät, die für die Problembehandlung verwendet wird.

Diese Funktion gilt für:

- Android

Angenommen Sie erstellen ein Profil in StageNow, um ein Gerät zu konfigurieren. Wenn Sie das StageNow-Profil erstellen, wird mit dem letzten Schritt eine Datei erstellt, mit der Sie das Profil testen können. Sie nutzen diese Datei mit der StageNow-App auf dem Gerät.

Angenommen, Sie erstellen ein Profil in StageNow und testen es. Sie fügen das StageNow-Profil in Intune hinzu und weisen es dann Ihren Zebra-Geräten zu. Beim Überprüfen des Status des zugewiesenen Profils zeigt das Profil einen allgemeinen Status an.

In beiden dieser Beispiele können Sie weitere Informationen aus der StageNow-Protokolldatei erhalten, die jedes Mal auf dem Gerät gespeichert wird, wenn ein StageNow-Profil angewendet wird.

Einige Probleme stehen nicht im Zusammenhang mit den Inhalten des StageNow-Profils, und werden nicht in den Protokollen widergespiegelt.

In diesem Artikel erfahren Sie, wie Sie die StageNow-Protokolle lesen. Außerdem werden einige weitere potenzielle Probleme mit Zebra-Geräten aufgeführt, die möglicherweise nicht in der Protokollen widergespiegelt werden.

Weitere Informationen zu diesem Feature finden Sie unter [Verwenden und Verwalten von Zebra-Geräten mit Zebra Mobility Extensions](android-zebra-mx-overview.md).

## <a name="get-the-logs"></a>Abrufen der Protokolle

### <a name="use-the-stagenow-app-on-the-device"></a>Verwenden der StageNow-App auf dem Gerät
Wenn Sie ein Profil direkt mit StageNow auf Ihrem Computer testen, anstatt [Intune zum Bereitstellen des Profils](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow) zu verwenden, speichert die StageNow-App auf dem Gerät die Protokolle des Tests. Verwenden Sie die Option **More (...)** (Mehr...) in der StageNow-App auf dem Gerät, um die Protokolldatei abzurufen.

### <a name="get-logs-using-android-debug-bridge"></a>Abrufen der Protokolle mit Android Debug Bridge
Stellen Sie mit [Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb) (dieser Link führt zu einer Android-Website) eine Verbindung zwischen dem Gerät und einem Computer her, um die Protokolle abzurufen, nachdem das Profil mit Intune bereitgestellt wurde.

Die Protokolle werden auf dem Gerät unter `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files` gespeichert.

### <a name="get-logs-from-email"></a>Abrufen von Protokollen per E-Mail
Endbenutzer können Ihnen die Protokolle mithilfe einer E-Mail-App auf dem Gerät senden, damit Sie nach der Bereitstellung mit Intune auf die Protokolle zugreifen können. Öffnen Sie die Unternehmensportal-App auf dem Zebra-Gerät, und [senden Sie die Protokolle](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android). Beim Verwenden des Features zum Senden von Protokollen wird auch eine PowerLift-Incident-ID erstellt, die Sie referenzieren können, wenn Sie sich an den Microsoft-Support wenden.

## <a name="read-the-logs"></a>Lesen der Protokolle

Wenn Sie sich die Protokolle ansehen, finden Sie überall dort, wo Sie das `<characteristic-error>`-Tag finden, einen Fehler. Fehlerdetails werden in die `desc`-Eigenschaft des `<parm-error>`-Tags geschrieben.

## <a name="error-types"></a>Fehlertypen

Zebra-Geräte verfügen über verschiedene Stufen für die Fehlerberichterstattung:

- Die CSP wird auf dem Gerät nicht unterstützt. Zum Beispiel, wenn es sich bei dem Gerät nicht um ein Mobilfunkgerät handelt, das über keinen Mobilfunk-Manager verfügt.
- Die MX- oder OSX-Version stimmt nicht überein. Jede CSP wird versioniert. Eine vollständige Unterstützungsmatrix finden Sie in der [Zebra-Dokumentation](http://techdocs.zebra.com/mx/) (dieser Link führt zu einer Zebra-Website).
- Das Gerät meldet ein weiteres Problem bzw. einen weiteren Fehler.

## <a name="examples"></a>Beispiele

Angenommen, Sie verfügen über das folgende Eingabeprofil:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

Der XML-Code im Protokoll stimmt mit der Eingabe überein. Diese übereinstimmende Ausgabe bedeutet, dass das Profil erfolgreich und ohne Fehler auf das Gerät angewendet wurde:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

Angenommen, Sie verfügen über die folgende Eingabe:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

Das Protokoll zeigt einen Fehler an, da es ein `<characteristic-error>`-Tag enthält. In diesem Szenario hat das Profil versucht, ein Android-Paket (APK) zu installieren, das nicht im angegebenen Pfad vorhanden ist:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Andere potenzielle Probleme mit Zebra-Geräten

In diesem Abschnitt werden weitere mögliche Probleme aufgeführt, die bei der Verwendung von Zebra-Geräten mit Geräteadministrator auftreten können. Diese Probleme werden nicht in den StageNow-Protokollen gemeldet.

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView ist veraltet

Wenn ältere Geräte mit der Unternehmensportal-App angemeldet werden, wird dem Benutzer möglicherweise eine Meldung angezeigt, die besagt, dass die System WebView-Komponente veraltet ist und aktualisiert werden muss. Wenn Google Play auf dem Gerät installiert ist, stellen Sie eine Verbindung mit dem Internet her, und suchen Sie nach Updates. Wenn Google Play nicht auf dem Gerät installiert ist, rufen Sie die aktualisierte Version der Komponente ab, und wenden Sie sie auf die Geräte an. Alternativ können Sie ein Update auf die neueste Version des Betriebssystems für Zebra-Geräte durchführen.

### <a name="management-actions-take-a-long-time"></a>Verwaltungsaktionen nehmen viel Zeit in Anspruch

Wenn Google Play-Dienste nicht verfügbar sind, können einige Aufgaben bis zu 8 Stunden dauern. Bei diesem Problem finden Sie möglicherweise hilfreiche Informationen unter [Einschränkungen der Intune-Unternehmensportal-App für Android](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (dieser Link führt zu einer anderen Microsoft-Website).

### <a name="device-spoofing-suspected-shows-in-intune"></a>Die Meldung „Device spoofing suspected“ (Verdacht auf Gerätespoofing) wird in Intune angezeigt

Bei diesem Fehler vermutet Intune, dass ein nicht von Zebra stammendes Android-System sich für ein Zebra-Gerät ausgibt (Modell und Hersteller).

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>Die Unternehmensportal-App ist älter als die erforderliche Mindestversion

Intune kann ein Update auf die erforderliche Mindestversion der Unternehmensportal-App durchführen. Wenn Google Play nicht auf dem Gerät installiert ist, wird die Unternehmensportal-App nicht automatisch aktualisiert. Wenn die erforderliche Mindestversion neuer als die installierte Version ist, funktioniert die Unternehmensportal-App nicht mehr. Führen Sie ein Update auf die neueste Unternehmensportal-App [per Sideloading auf Zebra-Geräten](android-zebra-mx-overview.md#sideload-the-company-portal-app) durch.

## <a name="next-steps"></a>Nächste Schritte

[Zebra-Diskussionsforen](https://developer.zebra.com/community/home/discussions) (dieser Link führt zu einer Zebra-Website)

[Verwenden und Verwalten von Zebra-Geräten mit Zebra Mobility Extensions in Intune](android-zebra-mx-overview.md)
