---
title: Registrieren von Geräten durch Benutzer
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Benutzer Geräte bei der lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager registrieren.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724884"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Wie Benutzer Geräte mit lokalem MDM in Configuration Manager registrieren

*Gilt für: Configuration Manager (Current Branch)*

Mit Configuration Manager lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) können Benutzer ihre Geräte registrieren. Dafür gibt es zwei Voraussetzungen:

- Mit den Client Einstellungen erteilen Sie dem Benutzer die Berechtigung, sich anzumelden.

- Sie installieren das erforderliche vertrauenswürdige Stamm Zertifikat auf dem Gerät.

Weitere Informationen zum Einrichten der Registrierung finden Sie unter [Einrichten der Geräteregistrierung für die lokale Verwaltung mobiler Geräte (MDM](../get-started/set-up-device-enrollment-on-premises-mdm.md)).

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>Registrieren von Windows 10

1. Wechseln Sie auf einem Computer mit Windows 10 zu **Einstellungen**.

1. Wählen Sie Konten, und klicken Sie dann auf **Arbeits-oder Schul** **Konto**zugreifen.

1. Wählen Sie **verbinden**aus, geben Sie Ihren Benutzer Prinzipal Namen (UPN) ein, und klicken Sie auf **weiter**. Der UPN kann mit Ihrer e-Mail-Adresse identisch sein, z jdoe@contoso.com. b..

1. Geben Sie den voll qualifizierten Domänen Namen (FQDN) des anmeldungsproxy-Punkts ein, und klicken Sie auf **weiter**.

1. Geben Sie Ihr Kennwort ein, und wählen Sie **Anmelden aus**.

1. Windows muss die Anmelde Informationen für diese Aktion nicht merken. Wählen Sie daher über **springen**aus.

Nach kurzer Zeit wird das Gerät mit Configuration Manager registriert.

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>Registrieren von Windows 10 Mobile

1. Wechseln Sie auf einem Windows 10 Mobile-Gerät zu **Einstellungen**.

1. Wählen Sie **Konten**aus, und wählen Sie dann **Arbeitsplatz Zugriff**aus.

1. Wählen Sie **Verbinden**.

1. Geben Sie Ihren UPN und den voll qualifizierten Namen des anmeldungsproxy-Punkts ein. Wählen Sie dann **verbinden**aus.

1. Geben Sie auf dem nächsten Bildschirm ihren UPN und Ihr Kennwort ein, und wählen Sie dann **Anmelden aus**.

Nach kurzer Zeit wird das Gerät mit Configuration Manager registriert. Wählen Sie **Fertig**aus.

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>Überprüfen der Registrierung

Verwenden Sie die Configuration Manager Konsole, um zu überprüfen, ob Geräte erfolgreich registriert wurden. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie **Geräte** aus. Suchen Sie in der Liste der Geräte nach dem registrierten Gerät, oder suchen Sie nach diesem.
