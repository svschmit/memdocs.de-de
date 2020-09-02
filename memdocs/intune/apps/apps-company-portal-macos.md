---
title: Hinzufügen der Unternehmensportal-App für macOS
titleSuffix: Microsoft Intune
description: Fügen Sie die Unternehmensportal-App für macOS-Geräte hinzu.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1eb64f8ed2bc67b4800a4583010dea150ade421d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914156"
---
# <a name="add-the-macos-company-portal-app"></a>Hinzufügen der Unternehmensportal-App für macOS

Installieren Sie zum Verwalten von Geräten optionale Apps. Benutzer müssen die Unternehmensportal-App installieren und sich bei dieser anmelden, um Zugriff auf Ressourcen zu erhalten, die auf macOS-Geräten mit Benutzeraffinität durch den bedingten Zugriff geschützt sind. Sie können den Benutzern Anweisungen für die Installation der Unternehmensportal-App für macOS bereitstellen oder die App auf Geräten installieren, die bereits direkt in Intune registriert sind.

Sie können eine der folgenden Optionen verwenden, um die Unternehmensportal-App für macOS zu installieren:
- [Benutzeranweisungen zum Herunterladen und Installieren der Unternehmensportal-App](#instruct-users-to-download-and-install-company-portal)
- [Installieren der Unternehmensportal-App für macOS als branchenspezifische macOS-App](#install-company-portal-for-macos-as-a-macos-lob-app)
- [Installieren der Unternehmensportal-App für macOS mithilfe eines macOS-Shellskripts](#install-company-portal-for-macos-by-using-a-macos-shell-script)

Die Unternehmensportal-App ist auch im Lieferumfang von Microsoft AutoUpdate (MAU) enthalten, um die Apps sicherer und auf dem neuesten Stand zu halten.

> [!NOTE]
> Die Unternehmensportal-App kann nur automatisch mit Intune auf Geräten installiert werden, die bereits über die direkte Registrierung oder die automatische Geräteregistrierung registriert sind. Bei persönlichen Geräten oder der manuellen Registrierung muss die Unternehmensportal-App heruntergeladen und installiert werden, um die Registrierung zu initiieren. Weitere Informationen finden Sie unter [Benutzeranweisungen zum Herunterladen und Installieren der Unternehmensportal-App](#instruct-users-to-download-and-install-company-portal).
## <a name="instruct-users-to-download-and-install-company-portal"></a>Benutzeranweisungen zum Herunterladen und Installieren der Unternehmensportal-App

Sie können Benutzer anweisen, die Unternehmensportal-App für macOS herunterzuladen, zu installieren und sich bei dieser anzumelden. Anwendungen zum Herunterladen, Installieren und Anmelden bei der Unternehmensportal-App finden Sie unter [Registrieren eines macOS-Geräts mithilfe der Unternehmensportal-App](../user-help/enroll-your-device-in-intune-macos-cp.md).

##  <a name="install-company-portal-for-macos-as-a-macos-lob-app"></a>Installieren der Unternehmensportal-App für macOS als branchenspezifische macOS-App

Die Unternehmensportal-App für macOS kann mithilfe des Features für [branchenspezifische macOS-Apps](lob-apps-macos.md) heruntergeladen und installiert werden. Die heruntergeladene Version ist immer die Version, die installiert wird und möglicherweise in regelmäßigen Abständen aktualisiert werden muss, um sicherzustellen, dass den Benutzern die anfängliche Registrierung möglichst einfach gemacht wird.

1. Laden Sie die Unternehmensportal-App für macOS von https://go.microsoft.com/fwlink/?linkid=853070 herunter. 

2. Befolgen Sie die Anweisungen unter [Hinzufügen von branchenspezifischen (Line-of-Business, LOB) macOS-Apps zu Microsoft Intune](lob-apps-macos.md), um eine branchenspezifische macOS-App zu erstellen.

> [!NOTE]
> Nach der Installation wird die Unternehmensportal-App für macOS mithilfe von MAU (Microsoft AutoUpdate) automatisch aktualisiert.
## <a name="install-company-portal-for-macos-by-using-a-macos-shell-script"></a>Installieren der Unternehmensportal-App für macOS mithilfe eines macOS-Shellskripts

Die Unternehmensportal-App für macOS kann mithilfe des Features für [Shellskripts für macOS-Geräte](macos-shell-scripts.md) heruntergeladen und installiert werden. Mit dieser Option wird immer die aktuelle Version der Unternehmensportal-App für macOS installiert, aber es werden keine Anwendungsinstallationsberichte bereitgestellt, die Sie beim Bereitstellen von Anwendungen mithilfe von [branchenspezifischen macOS-Apps](lob-apps-macos.md) verwenden können.

1. Laden Sie ein Beispielskript herunter, um die Unternehmensportal-App für macOS aus den [Intune-Shellskriptbeispielen für Unternehmensportal-Apps](https://github.com/microsoft/shell-intune-samples/tree/master/Apps/Company%20Portal) herunterzuladen.

2. Führen Sie die Anweisungen unter [Verwenden von Shellskripts auf macOS-Geräten in Intune](macos-shell-scripts.md) aus, um das macOS-Shellskript bereitzustellen. 
    - Legen Sie **Skript als angemeldeter Benutzer ausführen** auf **Nein** fest (für die Ausführung im Systemkontext).
    - Legen Sie **Maximum number of retries if script fails** (Maximale Anzahl von Wiederholungsversuchen bei Skriptfehlern) auf **3** fest.

> [!NOTE]
> Das Skript erfordert Internetzugriff, wenn es ausgeführt wird, um die aktuelle Version der Unternehmensportal-App für macOS herunterzuladen. 
## <a name="next-steps"></a>Nächste Schritte
- Weitere Informationen zum Zuweisen von Apps finden Sie unter [Zuweisen von Apps zu Gruppen mit Microsoft Intune](apps-deploy.md).
- Weitere Informationen zum Konfigurieren der automatischen Geräteregistrierung finden Sie unter [Automatisches Registrieren von macOS-Geräten mit Apple Business Manager oder Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md).
- Unter [Mac-Updates](/windows/security/threat-protection/microsoft-defender-atp/mac-updates) erfahren Sie mehr über das Konfigurieren der Microsoft AutoUpdate-Einstellungen auf macOS-Geräten.