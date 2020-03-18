---
title: Android-Geräteadministratorregistrierung in Microsoft Intune
titleSuffix: ''
description: Registrieren Sie Android-Geräte bei Intune mithilfe der Geräteadministratorregistrierung.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebe011c5549762c865eacdc2719e5ec28fdbed8c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339708"
---
# <a name="android-device-administrator-enrollment"></a>Android-Geräteadministratorregistrierung

Der Android-Geräteadministrator (mit Android 2.2 veröffentlicht und manchmal auch als „Legacy“-Android-Verwaltung bezeichnet) ist eine Möglichkeit zum Verwalten von Android-Geräten. [Android Enterprise](https://www.android.com/enterprise/management/) (veröffentlicht mit Android 5.0) bietet jetzt jedoch eine verbesserte Verwaltungsfunktionalität. In dem Bestreben, auf eine moderne, umfassendere und sicherere Geräteverwaltung umzusteigen, reduziert Google die Geräteadministratorunterstützung in neuen Android-Releases.

Um eine solche Einschränkung der Funktionalität zu vermeiden, empfehlen wir daher, neue Geräte nicht mit dem im Folgenden beschriebenen Geräteadministratorprozess zu registrieren.

Aus den gleichen Gründen empfehlen wir auch, dass Sie Geräte aus der Geräteadministratorverwaltung migrieren, wenn die Geräte auf Android 10 aktualisiert werden sollen. 

Weitere Informationen zur Intune-Unterstützung für den Android-Geräteadministrator finden Sie im Abschnitt [Hinweise](../fundamentals/whats-new.md#decreasing-support-for-android-device-administrator).

Wenn Sie sich dennoch dafür entscheiden, dass Benutzer ihre Android-Geräte mit der Geräteadministratorverwaltung registrieren lassen, fahren Sie mit dem nächsten Abschnitt fort.  

Weitere Informationen zu den Android Enterprise-Features von Google finden Sie in den folgenden Artikeln:
- [Google-Leitfaden für die Migration vom Geräteadministrator zu Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google-Dokumentation zum Plan, die Geräteadministrator-API als veraltet zu kennzeichnen](https://developers.google.com/android/work/device-admin-deprecation)

## <a name="set-up-device-administrator-enrollment"></a>Einrichten der Geräteadministratorregistrierung

1. Um auf die Verwaltung von mobilen Geräten vorzubereiten, müssen Sie die MDM-Autorität (Mobile Device Management, Verwaltung mobiler Geräte) auf **Microsoft Intune** festlegen. Anweisungen finden Sie unter [Festlegen der MDM-Autorität](../fundamentals/mdm-authority-set.md). Sie legen dieses Element nur einmal fest, wenn Sie die Ersteinrichtung von Intune für die Verwaltung mobiler Geräte durchführen.
2. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, und wählen Sie **Geräte** > **Android** > **Android-Registrierung** > **Persönliche und unternehmenseigene Geräte mit Geräteverwaltungsrechten** > **Geräteadministrator zum Verwalten von Geräten verwenden**.
3. [Informieren Sie Ihre Benutzer darüber, wie sie ihre Geräte registrieren sollen.](../user-help/enroll-device-android-company-portal.md)  

Nachdem ein Benutzer sich registriert hat, können Sie damit anfangen, die Geräte in Intune zu verwalten, dies umfasst das [Zuweisen von Gerätekonformitätsrichtlinien](../protect/compliance-policy-create-android.md), das [Verwalten von Apps](../apps/app-management.md) und mehr.

Informationen zu anderen Benutzeraufgaben finden Sie in den folgenden Artikeln:
- [Ressourcen zu Endbenutzerszenarios in Microsoft Intune](../fundamentals/end-user-educate.md)
- [Verwenden Ihres Android-Geräts mit Intune](https://docs.microsoft.com/user-help/using-your-android-device-with-intune)


## <a name="block-device-administrator-enrollment"></a>Blockieren der Geräteadministratorregistrierung
Um Android-Geräteadministratorgeräte oder nur die Registrierung von persönlichen Android-Geräteadministratorgeräten zu blockieren, lesen Sie [Festlegen von Gerätetypbeschränkungen](enrollment-restrictions-set.md).


## <a name="next-steps"></a>Nächste Schritte
- [Zuweisen von Konformitätsrichtlinien für Geräte](../protect/compliance-policy-create-android.md)
- [Verwalten von Apps](../apps/app-management.md)
