---
title: Ihr Android-Gerät ist offenbar verschlüsselt | Microsoft-Dokumentation
description: Aufheben des Verschlüsselungsstatus im Unternehmensportal und in Microsoft Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/14/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a7ce95d5c28b1b85f27fdd0aee74e3148abfb554
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83882275"
---
# <a name="device-encrypted-but-apps-say-otherwise"></a>Verschlüsseltes Gerät entgegen der Angabe der App

Wenn das Unternehmensportal oder die Microsoft Intune-App angeben, dass Ihr Gerät nicht verschlüsselt ist, Sie aber sicher sind, dass es verschlüsselt ist, können die Schritte in diesem Artikel behilflich sein.  

## <a name="add-a-startup-pin"></a>Hinzufügen einer Start-PIN

Bei bestimmten Android-Geräten müssen Sie eine Start-PIN erstellen, um die Sicherheit Ihres Geräts zu gewährleisten. Diese Einstellung wird auf Ihrem Gerät unter **Einstellungen** gespeichert. Der Name und der Menüpfad der Einstellung können variieren. Beispielsweise wird die Einstellung auf Samsung Galaxy S7 als **Sicherer Start** bezeichnet. Sie können diese aktivieren und einen Passcode erstellen, indem Sie zu **Einstellungen** > **Sperrbildschirm** > **Sicherer Start** navigieren.  

## <a name="encrypt-the-entire-device"></a>Verschlüsseln des gesamten Geräts

Dieser Abschnitt gilt nur für die Unternehmensportal-App. Bei einigen Geräten haben Sie die Wahl: Sie können entweder das gesamte Gerät verschlüsseln oder nur den tatsächlich belegten Speicherplatz. Wählen Sie die Option zum Verschlüsseln des gesamten Geräts aus. Wenn Sie ausgewählt haben, dass nur der verwendete Speicherplatz verschlüsselt werden soll:

1. [Entfernen Sie dieses Geräts aus dem Unternehmensportal](unenroll-your-device-from-intune-android.md).
2. Entschlüsseln Sie den belegten Speicherplatz.  
3. Verschlüsseln Sie das gesamte Gerät.  
4. Registrieren Sie das Gerät erneut.  

## <a name="downgrade-your-version-of-android"></a>Herabstufen Ihrer Android-Version

Dieser Abschnitt gilt nur für die Unternehmensportal-App. Falls Ihr Gerät Ihnen die Option gibt, auf Android 6.0 downzugraden, tun Sie dies. Falls Sie versuchen, Ihr Gerät downzugraden, besteht die Gefahr, dass Daten verloren gehen. Wenden Sie sich andernfalls an die Supportabteilung Ihres Unternehmens, um dieses Problem zu beheben. Die Kontaktinformationen für die Supportabteilung Ihres Unternehmens finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="specific-manufacturer-issues"></a>Spezifische Herstellerprobleme

Einige Android-Geräte mit Version 7.0 und höher verschlüsseln Daten so, dass sie mit gewissen Android-Plattformstandards nicht kompatibel sind. Mit diesen Verschlüsselungsmethoden werden Geräteinformationen gefährdet. Dadurch können diese Geräte nicht unterstützt werden.

Eine nicht vollständige Liste der unterstützten Android-Geräte finden Sie im Artikel [In Intune unterstützte Betriebssysteme und Browser](https://docs.microsoft.com/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices). Wenn Ihr Gerät nicht aufgeführt ist, wenden Sie sich an den Gerätehersteller oder an den Support.

> [!Note]
> Microsoft arbeitet mit Herstellern zusammen, um Probleme zu beheben, die wir beim Testen finden oder die Benutzer uns melden. Dieser Artikel wird aktualisiert, sobald neue Informationen verfügbar sind.

## <a name="update-devices"></a>Aktualisieren von Geräten

Wenn Sie Ihr Gerät nicht auf die neueste Version von Android aktualisiert haben, können Sie die **Einstellungen** Ihres Geräts aufrufen und ein **Update** durchführen.  

## <a name="next-steps"></a>Nächste Schritte

Benötigen Sie weitere Unterstützung? Wenden Sie sich an die Supportabteilung Ihres Unternehmens (suchen Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980) nach Kontaktinformationen) oder an das <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">Android-Team von Microsoft</a>.  
