---
title: Verwenden von Intune in Umgebungen ohne Google Mobile Services
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie Intune in Umgebungen ohne Google Mobile Services verwenden.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce61f7af7c11fb579e34890700231ca2e59fb5cd
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81267682"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>Verwenden von Intune in Umgebungen ohne Google Mobile Services

Microsoft Intune verwendet Google Mobile Services (GMS) für die Kommunikation mit dem Microsoft Intune-Unternehmensportal bei der Verwaltung von Android-Geräten. In einigen Fällen können Geräte vorübergehend oder dauerhaft keinen Zugriff auf die GMS haben. Ein Gerät könnte z. B. ohne GMS ausgeliefert werden, oder das Gerät stellt eine Verbindung mit einem geschlossenen Netzwerk her, in dem GMS nicht verfügbar ist. In diesem Dokument werden die Unterschiede und Einschränkungen zusammengefasst, die Ihnen bei der Installation und Verwendung von Intune für die Verwaltung von Android-Geräten ohne GMS auffallen könnten.

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>Installieren der Intune-Unternehmensportal-App ohne Zugriff auf den Google Play Store 

### <a name="for-users-outside-of-mainland-china"></a>Für Benutzer außerhalb des chinesischen Festlands 

Wenn Google Play nicht verfügbar ist, können Android-Geräte das  [Microsoft Intune-Unternehmensportal für Android](https://www.microsoft.com/en-us/download/details.aspx?id=49140) herunterladen und die App querladen. Bei dieser Installation erhält die App nicht Updates oder Korrekturen automatisch. Sie müssen die App regelmäßig manuell aktualisieren und patchen. 

### <a name="for-users-in-mainland-china"></a>Für Benutzer auf dem chinesischen Festland 

Da der Google Play Store derzeit nicht auf dem chinesischen Festland zur Verfügung steht, müssen Apps für Android-Geräte von chinesischen App-Marktplätzen abgerufen werden. Weitere Informationen finden Sie unter [Installieren der Unternehmensportal-App auf dem chinesischen Festland](../user-help/install-company-portal-android-china.md).

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>Einschränkungen der Administratorverwaltung von Intune-Geräten, wenn GMS nicht verfügbar sind 

### <a name="unavailable-intune-features"></a>Nicht verfügbare Intune-Features

Einige Intune-Features sind von GMS-Komponenten wie dem Google Play Store oder Google Play-Diensten abhängig. Da diese Komponenten nicht in Umgebungen ohne GMS verfügbar sind, sind möglicherweise die folgenden Features in der Intune-Administratorkonsole nicht verfügbar.  

| Szenario  | Features  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Gerätekompatibilitätsrichtlinien  | Beim Erstellen oder Bearbeiten von Kompatibilitätsrichtlinien für Android-Geräteadministratoren sind alle unter **Google Play Protect** aufgeführten Optionen nicht verfügbar.  |
| App-Schutzrichtlinien (bedingter Start)  | **SafetyNet-Gerätenachweis** und **Bedrohungsüberprüfung für Apps erzwingen**-Gerätebedingungen können nicht für den bedingten Start verwendet werden.  |
| Client-Apps  | Apps vom Typ **Android** sind nicht verfügbar. Verwenden Sie stattdessen zum Bereitstellen und Verwalten von Apps **branchenspezifische App-** .  |
| Mobile Threat Defense  | Arbeiten Sie mit dem MTD-Anbieter zusammen, um zu verstehen, ob seine Lösung in Intune integriert ist, ob sie in der betreffenden Region verfügbar ist und ob sie auf GMS basiert.  |

### <a name="some-tasks-may-be-delayed"></a>Einige Aufgaben sind möglicherweise verzögert. 

In Umgebungen, in denen GMS verfügbar ist, sendet Intune Pushbenachrichtigungen, um die Beendigung von Aufgaben zu beschleunigen. Wenn Sie z. B. versuchen, das Gerät remote zu löschen, werden Benachrichtigungen in der Regel innerhalb weniger Sekunden an das Gerät gesendet. Falls GMS nicht verfügbar ist, sind möglicherweise auch keine Pushbenachrichtigungen verfügbar. Daher muss Intune auf die nächste Geräteeincheckzeit warten, um die Aufgaben abzuschließen.  

Registrierte Android-Geräte senden alle 8 Stunden einen Bericht an Intune. Wenn ein Gerät beispielsweise um 13.00 Uhr an Intune berichtet und die Remoteaufgaben um 13:05 Uhr ausgegeben werden, kontaktiert Intune das Gerät um 21:00 Uhr, um die Aufgaben abzuschließen. 

Die folgenden Aufgaben können bis zu 8 Stunden dauern: 

**Intune-Konsole**:
- Vollständiges Zurücksetzen
- Selektives Zurücksetzen
- Neue oder aktualisierte App-Bereitstellungen
- Remotesperre
- Zurücksetzen der Kennung

**Intune-Unternehmensportal-App für Android**:
- Remoteentfernung von Geräten
- Gerät zurücksetzen
- Installieren verfügbarer branchenspezifischer Apps

**Intune-Unternehmensportalwebsite**:
- Entfernen eines Geräts (lokal und remote)
- Gerät zurücksetzen
- Zurücksetzen der Gerätekennung

Wenn das Gerät erst kürzlich registriert wurde, wird das Einchecken wg. Konformität, Nichtkonformität und Konfiguration häufiger durchgeführt. Weitere Informationen zum Einchecken von Geräten finden Sie unter [Häufige Fragen, Probleme und entsprechende Behebungen mit Geräterichtlinien und -profilen in Microsoft Intune](../configuration/device-profile-troubleshoot.md). 

## <a name="next-steps"></a>Nächste Schritte

- [Zuweisen von Apps zu Gruppen mit Microsoft Intune](../apps/apps-deploy.md)
