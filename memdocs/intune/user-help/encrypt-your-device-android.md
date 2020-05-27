---
title: Verschlüsseln eines Android-Geräts für Intune | Microsoft-Dokumentation
description: Hier finden Sie Schritte zum Aktivieren der Android-Geräteverschlüsselung, wenn diese für Intune erforderlich ist.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 268e1ab9b76cc214b7e755763ada6a2bd09ed80e
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880587"
---
# <a name="encrypting-your-android-device"></a>Verschlüsseln Ihres Android-Geräts

Die Geräteverschlüsselung schützt Ihre Dateien und Ordner vor nicht autorisiertem Zugriff, wenn Ihr Gerät verloren geht oder gestohlen wird. Sie verhindert den Zugriff auf die Daten, die auf Ihrem Gerät gespeichert sind, und macht sie unlesbar für Personen, die nicht über den Passcode verfügen. 

Bevor Sie auf Schul-, Geschäfts- oder Uniressourcen zugreifen können, fordert Ihre Organisation möglicherweise Folgendes von Ihnen:

* [Verschlüsseln Ihres Geräts](#encrypt-device)
* [Aktivieren des sicheren Starts](#enable-secure-startup)
* [Einrichten von Startpasscode, PIN oder einer anderen Authentifizierungsmethode](#set-startup-passcode)  

> [!Note]
> Bestimmte Android-Geräte von Huawei, Vivo und OPPO können nicht verschlüsselt werden. Weitere Informationen finden Sie unter [Verschlüsseltes Gerät entgegen der Angabe der App
](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

## <a name="encrypt-device"></a>Verschlüsseln des Geräts

Führen Sie diese Schritte aus, um Ihr Gerät zu verschlüsseln. Ihr Gerät kann mehrmals neu gestartet werden. 

Name und Speicherort der Verschlüsselungsoption variieren je nach Gerätehersteller und Android-Version. 

1. Öffnen Sie die App **Einstellungen**.
2. Geben Sie **Sicherheit** oder **Verschlüsseln** in der Suchleiste der App ein, um verwandte Einstellungen zu suchen.
3. Tippen Sie auf die Option zum Verschlüsseln Ihres Geräts. Folgen Sie den Anweisungen auf dem Bildschirm.  
4. Wenn Sie dazu aufgefordert werden, legen Sie ein Kennwort für den Sperrbildschirm, eine PIN oder eine andere Authentifizierungsmethode fest (sofern von Ihrer Organisation zugelassen). 
5. Um die Einstellungen erneut zu überprüfen, öffnen Sie das Unternehmensportal oder die Microsoft Intune-App.
    * Unternehmensportalbenutzer: Wählen Sie Ihr Gerät aus, und tippen Sie auf **Geräteeinstellungen überprüfen**. 
    * Microsoft Intune-Benutzer: Sie müssen warten, bis die Seite aktualisiert wird. Sobald sie aktualisiert wurde, sollte der Verschlüsselungsstatus jedoch in „konform“ geändert werden. 

## <a name="enable-secure-startup"></a>Aktivieren des sicheren Starts

In Ihrer Organisation ist es möglicherweise erforderlich, dass Sie im Rahmen der Verschlüsselungsrichtlinie den sicheren Start aktivieren. Mit dieser Funktion wird das Gerät weiter geschützt, indem vor dem Start des Telefons ein Kennwort oder eine PIN eingegeben werden muss. Abhängig davon, was Ihre Organisation zulässt, können Ihnen viele zusätzliche Authentifizierungsoptionen zur Verfügung stehen. 

Name und Speicherort der sicheren Startoption variieren je nach Gerätehersteller und Android-Version. Auf einigen Geräten wird diese Einstellung möglicherweise als **starker Schutz** bezeichnet. 

1. Öffnen Sie die App **Einstellungen**.
2. Geben Sie **sicheren Start** in der Suchleiste der App ein.
3. Tippen Sie auf **Sicherer Start** > **PIN beim Einschalten des Geräts anfordern**.
4. Geben Sie bei entsprechender Aufforderung Ihre Geräte-PIN ein.   
5. Um die Einstellungen erneut zu überprüfen, öffnen Sie das Unternehmensportal oder die Microsoft Intune-App.
    * Unternehmensportalbenutzer: Wählen Sie Ihr Gerät aus, und tippen Sie auf **Geräteeinstellungen überprüfen**. 
    * Microsoft Intune-Benutzer: Sie müssen warten, bis die Seite aktualisiert wird. Sobald sie aktualisiert wurde, sollte der Verschlüsselungsstatus jedoch in „konform“ geändert werden.  


## <a name="set-startup-passcode"></a>Festlegen des Startpasscodes   
Wenn Sie [Ihr Gerät verschlüsseln](#encrypt-device) und [sicheren Start aktivieren](#enable-secure-startup), werden Sie aufgefordert, Ihre Geräte-PIN, das Kennwort oder eine andere Authentifizierungsmethode (sofern von Ihrer Organisation zugelassen) festzulegen. Es sind keine weiteren Schritte erforderlich. 

So können Sie den Sperrbildschirmtyp auswählen oder ändern:

1. Öffnen Sie die App **Einstellungen**.
2. Geben Sie **Bildschirmsperre** in der Suchleiste der App ein.
3. Tippen Sie auf **Bildschirmsperrentyp**.
4. Tippen Sie auf den zu verwendenden Bildschirmsperrentyp, und befolgen Sie zum Bestätigen die Anweisungen auf dem Bildschirm.  

## <a name="troubleshoot"></a>Problembehandlung    
**Problem:** Die Schaltfläche „Verschlüsselung“ ist deaktiviert.   

**Versuchen Sie Folgendes**: 
* Stellen Sie sicher, dass das Gerät vollständig aufgeladen und angeschlossen ist. Die Verschlüsselung kann einige Zeit in Anspruch nehmen und erfordert einen vollständig aufgeladenen Akku.   

**Problem:** Eine Meldung wird angezeigt, dass die Verschlüsselung Ihres Geräts noch ausgeführt werden muss.  

**Versuchen Sie Folgendes**:
   *  [Legen Sie einen Sperrbildschirm](#set-startup-passcode) auf Ihrem Gerät fest. 
   * [Aktivieren Sie den sicheren Start](#enable-secure-startup).

Benötigen Sie weitere Unterstützung? Wenden Sie sich an den Support Ihres Unternehmens (suchen Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980) nach Kontaktinformationen) oder an das <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android-Team</a>.  
