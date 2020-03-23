---
title: Verschlüsseln eines Android-Geräts für Intune | Microsoft-Dokumentation
description: Hier finden Sie Schritte zum Aktivieren der Android-Geräteverschlüsselung, wenn diese für Intune erforderlich ist.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ee2d220e308b406251f049e1c17422f89ee36534
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348782"
---
# <a name="encrypting-your-android-device"></a>Verschlüsseln Ihres Android-Geräts

Die Geräteverschlüsselung schützt Ihre Dateien und Ordner vor nicht autorisiertem Zugriff, wenn Ihr Gerät verloren geht oder gestohlen wird. Nachdem Sie die Geräteverschlüsselung aktiviert haben, können sich nur Personen mit dem richtigen Kennwort oder der PIN bei Ihrem Gerät anmelden. 

Bevor Sie auf Schul-, Geschäfts- oder Uniressourcen zugreifen können, erfordert Ihre Organisation möglicherweise, dass Sie Ihr Android-Gerät verschlüsseln. Einige neuere Android-Geräte sind standardmäßig verschlüsselt.  

## <a name="turn-on-encryption"></a>Aktivieren der Verschlüsselung

Wenn das Unternehmensportal oder die Microsoft Intune-App Sie zum Verschlüsseln Ihres Geräts auffordert, führen Sie die folgenden Schritte aus. 

> [!Note]
> Bestimmte Android-Geräte von Huawei, Vivo und OPPO können nicht verschlüsselt werden. [Hier](your-device-appears-encrypted-but-cp-says-otherwise-android.md) erfahren Sie mehr.  

1. Legen Sie eine Bildschirmsperre für Ihr Gerät fest.  
    a. Wechseln Sie zu **Einstellungen** > **Lock Screen and Security** > **Screen lock** (Sperrbildschirm und Sicherheit > Bildschirmsperre).  
    b. Wählen Sie eine der Optionen **PIN**, **Kennwort** oder **Muster** aus.  
    c. Führen Sie die angezeigten Anweisungen durch, um Ihre Bildschirmsperre zu konfigurieren.  

2. Kehren Sie zu **Sperrbildschirm und Sicherheit** zurück, und wählen Sie dann **Sicherer Start** aus.
3. Klicken Sie auf **Require PIN when device turns on** > **OK** (PIN beim Einschalten des Geräts erfordern > OK).
4. Geben Sie Ihre PIN zur Bestätigung und zum Verschlüsseln des Geräts ein.
5. Öffnen Sie die Unternehmensportal- oder die Microsoft Intune-App.
    * Unternehmensportalbenutzer: Wählen Sie Ihr Gerät aus, und tippen Sie auf **Geräteeinstellungen überprüfen**. 
    * Microsoft Intune-Benutzer: Sie müssen warten, bis die Seite aktualisiert wird. Sobald sie aktualisiert wurde, sollte der Verschlüsselungsstatus jedoch in „konform“ geändert werden.  

Geräte mit Android 4.4 und früher verfügen möglicherweise nicht über die Option **Sicherer Start**. Führen Sie in diesem Fall die folgenden Schritte durch, um Ihr Gerät zu verschlüsseln.

1. Navigieren Sie zu **Einstellungen** > **Sicherheit** > **Gerät verschlüsseln**. Die angezeigten Bezeichnungen können je nach Android-Gerät variieren. Wenn die Option **Gerät verschlüsseln** nicht angezeigt wird, suchen Sie unter den folgenden Kategorien nach ihr:
    * **Speicher** > **Speicherverschlüsselung**
    * **Speicher** > **Sperrbildschirm und Sicherheits** > **Weitere Sicherheitseinstellungen** 

2. Folgen Sie den Anweisungen auf dem Bildschirm. Während der Verschlüsselung startet Ihr Gerät möglicherweise mehrmals neu.
3. Öffnen Sie die Unternehmensportal- oder die Microsoft Intune-App.
    * Unternehmensportalbenutzer: Wählen Sie Ihr Gerät aus, und tippen Sie auf **Geräteeinstellungen überprüfen**.  
    * Microsoft Intune-Benutzer: Sie müssen warten, bis die Seite aktualisiert wird. Sobald sie aktualisiert wurde, sollte der Verschlüsselungsstatus jedoch in „konform“ geändert werden.

## <a name="troubleshoot"></a>Problembehandlung  
**Problem:** Sie haben Ihr Gerät bereits verschlüsselt, aber:

- Die Schaltfläche „Verschlüsselung“ ist deaktiviert.
- Eine Meldung wird angezeigt, dass die Verschlüsselung noch ausgeführt werden muss.
- Es treten Fehler auf, wenn Sie versuchen, das Unternehmensportal oder die Microsoft Intune-App zu verwenden.

**Versuchen Sie Folgendes**

- Stellen Sie sicher, dass das Gerät aufgeladen und angeschlossen ist.  
- Stellen Sie sicher, dass Sie auf Ihrem Gerät eine PIN oder ein Kennwort festgelegt haben.  

Benötigen Sie weitere Unterstützung? Wenden Sie sich an den Support Ihres Unternehmens (suchen Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980) nach Kontaktinformationen) oder an das <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android-Team</a>.  
