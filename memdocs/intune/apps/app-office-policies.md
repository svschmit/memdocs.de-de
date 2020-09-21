---
title: Richtlinien für Office-Apps
titleSuffix: Microsoft Intune
description: Lernen Sie die für Office-Apps verfügbaren Richtlinien kennen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca558b40ad3d006aa764819a0fbccc16a03fd0e2
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89644026"
---
# <a name="policies-for-office-apps"></a>Richtlinien für Office-Apps

Intune bietet Richtlinien speziell für Microsoft Office-Apps. Sie können bestimmte Optionen auswählen, um Verwaltungsrichtlinien für mobile Office-Apps zu erstellen, die eine Verbindung mit Microsoft 365-Diensten herstellen. Es gibt eine Vielzahl von Richtlinien für Office-Apps, die Sie Microsoft Intune hinzufügen und auf Endbenutzergruppen anwenden können.

Hier nur einige Beispiele für diese Office-App-Richtlinien:
- Microsoft Word: *Geschützte Ansicht für aus Outlook geöffnete Anlagen deaktivieren*
- Microsoft Visio: *Ausführung von Makros in Office-Dateien aus dem Internet blockieren*
- Microsoft Project: *Vertrauenswürdige Speicherorte im Netzwerk zulassen*
- Microsoft Publisher: *Publisher-Automatisierungssicherheitsstufe*
- Microsoft PowerPoint: *Geschützte Ansicht für aus Outlook geöffnete Anlagen deaktivieren*

> [!NOTE]
> Wenn Sie die Option zum Konfigurieren der jeweiligen App-Richtlinie auswählen, werden zusätzliche Richtliniendetails bereitgestellt. Sie können die Liste der Office-Richtlinien filtern, um schnell die empfohlenen Richtlinien der **Sicherheitsbaseline** auszuwählen.

Außerdem können Sie den Zugriff auf lokale Exchange-Postfächer schützen, indem Sie Intune-App-Schutzrichtlinien für Outlook für iOS/iPadOS und Android erstellen, die mit hybrider moderner Authentifizierung aktiviert wurden. Bevor Sie dieses Feature verwenden, müssen die Voraussetzungen für die Nutzung des Office-Cloudrichtliniendiensts erfüllt sein. App-Schutzrichtlinien werden nicht für andere Apps unterstützt, die eine Verbindung mit lokalen Exchange- oder SharePoint-Diensten herstellen. Verwandte Informationen finden Sie unter [Übersicht über den Office-Cloudrichtliniendienst für Microsoft 365-Apps für Unternehmen](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service).

## <a name="prerequisites"></a>Voraussetzungen

Sie müssen die Anforderungen für die Verwendung von Richtlinien für Office-Apps erfüllen. Weitere Informationen finden Sie unter [Voraussetzungen für die Verwendung des Office-Cloudrichtliniendiensts](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service).

## <a name="to-add-an-office-app-policy"></a>So fügen Sie eine Office-App-Richtlinie hinzu

Nachdem Sie Intune für Ihre Organisation eingerichtet haben, können Sie eine Office-App-Richtlinie erstellen.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Richtlinien für Office-Apps** > **Erstellen** aus.
3. Fügen Sie die folgenden Werte hinzu:
    - **Name:** Geben Sie einen Namen für Ihre neue Richtlinie ein (erforderlich).
    - **Beschreibung:** Geben Sie eine Beschreibung ein (optional).
    - **Typ auswählen**: Wählen Sie aus, wie diese Richtlinienkonfiguration angewendet wird.
    - **Gruppe auswählen**: Wählen Sie die Gruppe für diese Richtlinienkonfiguration aus.
    - **Richtlinien konfigurieren**: Wählen Sie die Office-Richtlinie aus, das Sie anwenden möchten. Sie können die Liste nach Richtlinie, Plattform, Anwendung, Empfehlung und Status sortieren.
4. Klicken Sie auf **Erstellen**. Die Richtlinie wird erstellt und im Bereich **Richtlinienkonfiguration** in der Tabelle angezeigt.

   > [!TIP]
   > Der Bereich **Richtlinienkonfiguration** zeigt den **Integritätsstatus** für jede Richtlinie an.

## <a name="additional-information"></a>Zusätzliche Informationen

- [Übersicht über den Office-Cloudrichtliniendienst für Microsoft 365-Apps für Unternehmen](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)
- [Verwenden von Richtlinien zum Verwalten von Datenschutzsteuerelementen für Microsoft 365-Apps für Unternehmen](https://docs.microsoft.com/deployoffice/privacy/manage-privacy-controls)
- [Verwenden von Einstellungen zum Verwalten von Datenschutzsteuerelementen für Office für Mac](https://docs.microsoft.com/deployoffice/privacy/mac-privacy-preferences)
- [Verwenden von Einstellungen zum Verwalten von Datenschutzsteuerelementen für Office auf iOS-Geräten](https://docs.microsoft.com/deployoffice/privacy/ios-privacy-preferences)
- [Verwenden von Richtlinieneinstellungen zum Verwalten von Datenschutzsteuerelementen für Office auf Android-Geräten](https://docs.microsoft.com/deployoffice/privacy/android-privacy-controls)

## <a name="next-steps"></a>Nächste Schritte

- [Überwachen von App-Informationen und -Zuweisungen mit Microsoft Intune](apps-monitor.md)