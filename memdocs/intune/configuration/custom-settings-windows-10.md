---
title: 'Hinzufügen von benutzerdefinierten Einstellungen für Windows 10-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Fügen Sie ein benutzerdefiniertes Profil zur Verwendung der OMA-URI-Einstellungen für Windows 10 in Microsoft Intune hinzu, oder erstellen Sie ein solches Profil. Verwenden Sie ein benutzerdefiniertes Profil, um benutzerdefinierte Einstellung hinzuzufügen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28a867c735a05cfa4a4765534d200b806711f9b5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913017"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Verwenden von benutzerdefinierten Einstellungen für Windows 10-Geräte in Intune

In diesem Artikel werden die verschiedenen benutzerdefinierten Einstellungen aufgeführt und beschrieben, die Sie auf Geräten mit Windows 10 und höher festlegen können. Verwenden Sie diese Einstellungen im Rahmen Ihrer MDM-Lösung (mobile Geräteverwaltung), um Einstellungen zu konfigurieren, die nicht in Intune integriert sind.

Weitere Informationen über benutzerdefinierte Profile finden Sie unter [Erstellen eines Profils mit benutzerdefinierten Einstellungen](custom-settings-configure.md).

Diese Einstellungen werden erst einem Gerätekonfigurationsprofil in Intune hinzugefügt und dann Ihren Windows 10-Geräten zugewiesen oder für diese bereitgestellt.

Diese Funktion gilt für:

- Windows 10 und höher

Benutzerdefinierte Windows 10-Profile verwenden die OMA-URI-Einstellungen (Open Mobile Alliance Uniform Resource Identifier) zum Konfigurieren verschiedener Features auf Android-Geräten. Diese Einstellungen werden in der Regel von den Herstellern der Geräte verwendet, um die Features auf dem Gerät zu steuern.

Windows 10 stellt viele CSP-Einstellungen zur Verfügung, z.B. den [Richtlinienkonfigurationsdienst-Anbieter (Policy Configuration Service Provider, Policy CSP)](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).

Wenn Sie nach einer bestimmten Einstellung suchen, beachten Sie, dass das [Geräteeinschränkungsprofil von Windows 10](device-restrictions-windows-10.md) viele integrierte Einstellungen enthält. Sie müssen also möglicherweise keine benutzerdefinierten Werte eingeben.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein benutzerdefiniertes Windows 10-Profil.](custom-settings-configure.md#create-the-profile)

## <a name="oma-uri-settings"></a>OMA-URI-Einstellungen

**Hinzufügen**: Legen Sie folgende Einstellungen fest:

- **Name:** Geben Sie einen eindeutigen Namen für die OMA-URI-Einstellung ein, damit Sie sie in der Liste der Einstellungen leichter identifizieren können.
- **Beschreibung:** Geben Sie eine Beschreibung ein, die einen Überblick über die Einstellung und andere wichtige Details bietet.
- **OMA-URI** (Groß-/Kleinschreibung beachten): Geben Sie den OMA-URI ein, für den Sie eine Einstellung bereitstellen möchten.
- **Datentyp:** Wählen Sie den Datentyp aus, den Sie für diese OMA-URI-Einstellung verwenden möchten. Folgende Optionen sind verfügbar:

  - Base64 (Datei)
  - Boolesch
  - Zeichenfolge (XML-Datei)
  - Datum und Uhrzeit
  - Zeichenfolge
  - Gleitkomma
  - Ganze Zahl

- **Wert:** Geben Sie den gewünschten Datenwert an, der dem von Ihnen eingegebenen OMA-URI zugeordnet werden soll. Der Wert hängt vom ausgewählten Datentyp ab. Beim Datentyp **Datum und Uhrzeit** wählen Sie den Wert beispielsweise aus einer Datumsauswahl aus.

Wenn Sie einige Einstellungen hinzugefügt haben, können Sie auf **Exportieren** klicken. Wenn Sie auf **Exportieren** klicken, wird eine Liste aller hinzugefügten Werte in einer Datei mit durch Trennzeichen getrennten Werten (CSV) erstellt.

## <a name="find-the-policies-you-can-configure"></a>Suchen konfigurierbarer Richtlinien

Eine vollständige Liste aller Konfigurationsdienstanbieter (CSP), die von Windows 10 unterstützt werden, finden Sie in der [Referenz zum Konfigurationsdienstanbieter](/windows/client-management/mdm/configuration-service-provider-reference).

Nicht alle Einstellungen sind mit allen Windows 10-Versionen kompatibel. Über die [Konfigurationsdienstanbieter-Referenz](/windows/client-management/mdm/configuration-service-provider-reference) erfahren Sie, welche Versionen für die einzelnen Konfigurationsdienstanbieter unterstützt werden.

Außerdem unterstützt Intune nicht alle Einstellungen, die in der [Referenz zum Konfigurationsdienstanbieter](/windows/client-management/mdm/configuration-service-provider-reference) aufgeführt sind. Öffnen Sie den Artikel für die jeweilige Einstellung, um herauszufinden, ob die gewünschte Einstellung von Intune unterstützt wird. Auf jeder Einstellungsseite wird angezeigt, welcher Vorgang jeweils unterstützt wird. Damit die Einstellung mit Intune funktioniert, muss sie die Vorgänge **Hinzufügen**, **Ersetzen** und **Abrufen** unterstützen. Wenn der vom Vorgang **Abrufen** zurückgegebene Wert nicht mit dem vom Vorgang **Hinzufügen** oder **Ersetzen** zurückgegebenen Wert übereinstimmt, meldet Intune einen Konformitätsfehler.

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie dessen Status](device-profile-monitor.md).

Weitere Informationen zu [benutzerdefinierten Profilen in Intune](custom-settings-configure.md).