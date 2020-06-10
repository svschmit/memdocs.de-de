---
title: Bereitstellen mehrerer OEMConfig-Profile für Zebra Geräte mit Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie Microsoft Intune zum Erstellen und Bereitstellen mehrerer OEMConfig-Gerätekonfigurationsprofile auf Zebra Geräten, auf denen Android Enterprise ausgeführt wird. Verwenden Sie Zebra-Aktionen und -Schritte, um Ihre Profile zu sortieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a38c445018200d9fe80db19142f123aba783b60
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311159"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Bereitstellen mehrerer OEMConfig-Profile für Zebra-Geräte in Microsoft Intune

In Microsoft Intune können Sie mithilfe von OEMConfig OEM-spezifische Einstellungen für Android Enterprise-Geräte anpassen. Diese Einstellungen gelten speziell für den Gerätehersteller und werden mithilfe von Konfigurationsprofilen in Intune bereitgestellt.

Auf Zebra-Geräten können Sie dem gleichen Gerät mehrere Profile bereitstellen oder zuweisen. Vorhandene OEMConfig-Profile können diese Funktion verwenden, wenn die Geräte das nächste Mal mit Intune synchronisiert werden.

Diese Funktion gilt für:

- Zebra-Geräte, auf denen Android Enterprise ausgeführt wird

Weitere Informationen zu OEMConfig, einschließlich der Funktionsweise und seiner Verwendung, finden Sie unter [OEMConfig-Konfigurationsprofil](android-oem-configuration-overview.md).

In diesem Artikel wird beschrieben, wie mehrere OEMConfig-Profile für Zebra-Geräte bereitgestellt werden, wie die Sortierung erfolgt und wie die Berichtsfunktionen in Microsoft Intune verwendet werden.

## <a name="prerequisites"></a>Voraussetzungen

Erstellen Sie ein [OEMConfig-Konfigurationsprofil](android-oem-configuration-overview.md).

## <a name="use-multiple-profiles"></a>Verwenden mehrerer Profile

Bei Zebra-Geräten können auf jedem Gerät mehrere Profile gleichzeitig vorhanden sein. Mit dieser Funktion können Sie Ihre Zebra-OEMConfig-Einstellungen in kleinere Profile aufteilen. Erstellen Sie z. B. ein Basisprofil, das sich auf alle Geräte auswirkt. Erstellen Sie dann weitere Profile, mit denen Einstellungen speziell für ein Gerät konfiguriert werden.

Das OEMConfig-Schema von Zebra verwendet auch **Aktionen**. Aktionen sind Vorgänge, die auf dem Gerät ausgeführt werden. Sie konfigurieren keine Einstellungen. Mit diesen Aktionen können Sie einen Dateidownload auslösen, die Zwischenablage löschen und vieles mehr. Eine vollständige Liste der unterstützten Aktionen finden Sie in der [Zebra-Dokumentation](https://techdocs.zebra.com/oemconfig/10-0/about/) (öffnet die Zebra-Website).

Ein Beispiel: Sie erstellen ein Zebra-OEMConfig-Profil, mit dem einige Einstellungen auf das Gerät angewendet werden. Ein weiteres Zebra-OEMConfig-Profil enthält eine Aktion zum Löschen der Zwischenablage. Sie weisen das erste Profil einer Zebra-Gerätegruppe zu. Später müssen Sie die Zwischenablage auf diesen Geräten löschen. Sie weisen das zweite Profil der gleichen Gerätegruppe zu, ohne das erste Profil zu ändern. Die Gerätezwischenablage wird gelöscht, ohne dass die im ersten Profil erstellten Konfigurationseinstellungen erneut gesendet oder beeinträchtigt werden.

Ein weiteres Beispiel: Sie haben ein OEMConfig-Profil zugewiesen, mit dem einige Zebra-Geräteeinstellungen konfiguriert wurden. In letzter Zeit melden Benutzer Probleme mit einer bestimmten App, und Sie möchten den Cache der App löschen. Erstellen Sie dazu ein neues OEMConfig-Profil, das nur die Aktion „Cache löschen“ enthält. Dann weisen Sie das Profil den Geräten zu, die es benötigen.

## <a name="ordering"></a>Sortieren

Beim Vorhandensein von mehreren Profilen auf jedem Gerät ist die Reihenfolge, in der die Profile bereitgestellt werden, nicht garantiert. Dieses Verhalten ist eine Google Play-Einschränkung. Zum Ausführen von Vorgängen in einer bestimmten Sequenz können Sie die [Transaktionsschritt-Funktion von Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/) verwenden (öffnet die Zebra-Website). 

Zusammenfassend gilt: Wenn die Reihenfolge wichtig ist, verwenden Sie die [Transaktionsschritt-Funktion von Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/) (öffnet die Website von Zebra). Wenn die Reihenfolge keine Rolle spielt, verwenden Sie mehrere Intune-Profile. 

Sehen wir uns einige Beispiele an:

- Sie möchten Bluetooth für alle neu registrierten Zebra Geräte aktivieren, bevor Sie andere Einstellungen auf diesen Geräten konfigurieren. Verwenden Sie zum Ausführen von Vorgängen in einer bestimmten Sequenz die Funktion **Schritte** im Zebra-Schema.

  Erstellen Sie ein Intune-Profil, das zwei Transaktionsschritte umfasst. Der erste Schritt umfasst die Bluetooth-Einstellungen, während im zweiten Schritt die andere Einstellung konfiguriert wird. Wenn die OEMConfig-App von Zebra das Profil empfängt, führt sie die Schritte in der angegebenen Reihenfolge aus.

  Weitere Informationen finden Sie unter [Transaktionsschritte von Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/) (öffnet die Zebra-Website).

- Sie möchten, dass auf allen Zebra-Geräten die Uhrzeit im 24-Stunden-Format angezeigt wird. Für einige dieser Geräte möchten Sie die Kamera deaktivieren. Die Uhrzeit- und Kameraeinstellungen sind nicht voneinander abhängig.

  Erstellen Sie zwei Intune-Profile:

  - **Profil 1**: Zeigt die Uhrzeit im 24-Stunden-Format an. Am Montag wird dieses Profil der Gruppe **Alle Zebra-AE-Geräte** zugewiesen.
  - **Profil 2**: Deaktiviert die Kamera. Am Dienstag wird dieses Profil der Gruppe **Zebra AE-Factory-Geräte** zugewiesen.

  Am Mittwoch registrieren Sie 10 neue Zebra-Geräte bei Intune. Profil 1 und Profil 2 werden zugewiesen. Nachdem die neuen Geräte mit Intune synchronisiert wurden, erhalten sie die Profile. Die Geräte erhalten möglicherweise das Profil 2, bevor sie das Profil 1 erhalten.

## <a name="enhanced-reporting"></a>Erweiterte Berichterstellung

Sie stellen ein Profil bereit, das von der OEMConfig-App von Zebra auf dem Gerät ausgeführt wird. Die OEMConfig-App von Zebra meldet den Profil Status an Intune. Im Endpunkt-Manager Admin Center sehen Sie den Status der bereitgestellten OEMConfig-Profile sowie alle Fehler oder Warnungen.

1. Öffnen Sie das [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Wählen Sie Ihr Zebra-OEMConfig-Profil aus, dann **Überwachen** > **Gerätestatus**. Diese Option zeigt die Geräte an, denen Ihr OEMConfig-Profil zugewiesen ist.
3. Wählen Sie ein Gerät aus, dann **Gerätekonfiguration**, dann wählen Sie Ihr Zebra-OEMConfig-Profil aus. Diese Option zeigt die Profileinstellungen an, die erfolgreich waren oder fehlgeschlagen sind.

    Wählen Sie eine fehlerhafte Zeile aus. Details werden angezeigt, die weitere Informationen zur Fehlerursache enthalten.

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zu [OEMConfig-Konfigurationsprofilen](android-oem-configuration-overview.md).
- Konfigurieren von [Mobility Extensions(MX)](android-zebra-mx-overview.md) auf dem Android-Geräteadministrator.
- [Überwachen des Profilstatus](device-profile-monitor.md)
