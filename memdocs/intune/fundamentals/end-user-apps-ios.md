---
title: Wie Ihre iOS/iPadOS-Benutzer Apps erhalten
description: Methoden, um iOS/iPadOS-Apps für Endbenutzer verfügbar zu machen.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79344089"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>Wie Ihre iOS/iPadOS-Benutzer Apps erhalten

Verwenden Sie diese Informationen, um zu verstehen, wie und wo Ihre Endbenutzer die Apps erhalten, die Sie über Microsoft Intune verteilen.

**Erforderliche Apps:** Apps, die vom Administrator benötigt werden und auf dem Gerät (abhängig von der Plattform) mit minimalen Benutzereingriffen installiert werden.

**Verfügbare Apps:** Apps, die in der App-Liste im Unternehmensportal enthalten sind und die ein Benutzer optional installieren kann.

**Verwaltete Apps:** Apps, die mittels Richtlinien verwaltet werden können und die von Intune „umschlossen“ werden oder mit dem Software Development Kit (SDK) für die Intune-App erstellt wurden. Diese Apps können von Intune verwaltet werden, und ihnen lassen sich App-Schutzrichtlinien zuweisen.

**Nicht verwaltete Apps:** Apps, die Benutzer aus dem iOS/iPadOS App Store herunterladen können und die nicht in das Intune App SDK integriert sind. Intune bietet keinerlei Kontrolle über die Verteilung, Verwaltung oder selektive Zurücksetzung dieser Apps.  

Registrierte Benutzer erhalten ihre Apps durch Berühren der folgenden Kacheln auf dem Bildschirm „Apps“ der Unternehmensportal-App:

- **Alle Apps** verweist auf eine Liste aller Apps auf der Registerkarte „ALLE“ der [Unternehmensportal-Website](https://portal.manage.microsoft.com).

- **Ausgewählte Apps** leitet Benutzer zur Registerkarte „EMPFOHLEN“ der Unternehmensportal-Website.

- **Kategorien** verweist auf die Registerkarte „KATEGORIEN“ der Unternehmensportal-Website.

![Apps-Bildschirm des iOS-Unternehmensportals](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

Informationen zum Hinzufügen von Apps finden Sie unter [Hinzufügen von Apps zu Microsoft Intune](../apps/apps-add.md).

## <a name="app-management-takeover"></a>Übernehmen der App-Verwaltung
Wenn eine App bereits auf dem Gerät eines Endbenutzers installiert ist, zeigt das iOS/iPadOS-Gerät eine Warnung an, um die Verwaltung der App durch die Organisation zu ermöglichen. Der Endbenutzer muss der Organisation erlauben, die Verwaltung der App zu übernehmen, damit App-Konfigurationen auf ein verwaltetes Gerät angewendet werden können. Wenn der Benutzer die Warnung abbricht, wird die Warnung regelmäßig angezeigt, solange das Gerät verwaltet und die App zugewiesen wird.  


![Abbildung der Warnung zur Änderung der App-Verwaltung mit den Optionen „Abbrechen“ und „Verwalten“](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>Weitere Informationen:  

[Wie Ihre Android-Benutzer Apps erhalten](end-user-apps-android.md)

[Wie Ihre Windows-Benutzer Apps erhalten](end-user-apps-windows.md)
