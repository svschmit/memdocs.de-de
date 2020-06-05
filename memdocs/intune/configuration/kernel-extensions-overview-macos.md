---
title: 'Azure: Erstellen von macOS-System- und -Kernelerweiterungen mit Microsoft Intune | Microsoft-Dokumentation'
titleSuffix: ''
description: Hier erfahren Sie, wie Sie ein macOS-Geräteprofil hinzufügen oder erstellen, das Systemerweiterungen oder Kernelerweiterungen konfiguriert, um die Benutzerüberschreibung zuzulassen, und Team-IDs sowie ein Bündel und eine Team-ID in Microsoft Intune hinzufügt.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fce8218c9f8fb8757f0aef892f0854f1c386a8bd
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990305"
---
# <a name="add-macos-system-and-kernel-extensions-in-intune"></a>Hinzufügen von macOS-System- und Kernelerweiterungen in Intune

> [!NOTE]
> macOS-Kernelerweiterungen werden durch Systemerweiterungen ersetzt. Weitere Informationen finden Sie unter [Tipp zur Unterstützung: Verwenden von Systemerweiterungen anstelle von Kernelerweiterungen für macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Auf macOS-Geräten können Sie Kernel- und Systemerweiterungen hinzufügen. Sowohl Kernel- als auch Systemerweiterungen ermöglichen den Benutzern das Installieren von App-Erweiterungen, die die nativen Funktionen des Betriebssystems erweitern. Der Code von Kernelerweiterungen wird auf der Kernelebene ausgeführt. Systemerweiterungen werden in einem streng kontrollierten Benutzerbereich ausgeführt.

Verwenden Sie Microsoft Intune, um Erweiterungen hinzuzufügen, die auf Ihren Geräten immer geladen werden dürfen. Intune verwendet „Konfigurationsprofile“ zum Erstellen und Anpassen dieser Einstellungen für die Anforderungen Ihrer Organisation. Nachdem Sie diese Features zu einem Profil hinzugefügt haben, stellen Sie das Profil auf macOS-Geräten in Ihrer Organisation bereit.

In diesem Artikel werden Systemerweiterungen und Kernelerweiterungen behandelt. Außerdem erfahren Sie, wie Sie ein Gerätekonfigurationsprofil mithilfe von Erweiterungen in Intune erstellen.

## <a name="system-extensions"></a>Systemerweiterungen

Systemerweiterungen werden im Benutzerbereich ausgeführt und greifen nicht auf den Kernel zu. Das Ziel besteht darin, die Sicherheit zu erhöhen, Endbenutzern mehr Kontrolle zu ermöglichen und Angriffe auf Kernelebene einzuschränken. Folgende Erweiterungen sind möglich:

- Treibererweiterungen, einschließlich Treiber für USB, Netzwerkkarten (NIC), serielle Controller und Eingabegeräte (HID, Human Interface Devices)
- Netzwerkerweiterung, einschließlich Inhaltsfilter, DNS-Proxys und VPN-Clients
- Endpunktsicherheitserweiterungen, einschließlich Endpunkterkennung, Endpunktreaktion und Antivirus

Systemerweiterungen sind im Paket einer App enthalten und werden über die App installiert.

Weitere Informationen zu Systemerweiterungen finden Sie unter [Systemerweiterungen](https://developer.apple.com/documentation/systemextensions) (Apple-Website).

## <a name="kernel-extensions"></a>Kernelerweiterungen

Kernelerweiterungen fügen Features auf der Kernelebene hinzu. Diese Features greifen auf Teile des Betriebssystems zu, auf die reguläre Programme nicht zugreifen können. In Ihrer Organisation gibt es möglicherweise bestimmte Bedürfnisse oder Anforderungen, die von einer App oder einem Gerätefeature nicht erfüllt werden können.

Angenommen, Sie haben ein Virenerkennungsprogramm, das Ihr Gerät auf schädliche Inhalte überprüft. In diesem Fall können Sie die Kernelerweiterung dieses Virenerkennungsprogramms als zulässige Kernelerweiterung in Intune hinzufügen. Weisen Sie die Erweiterung anschließend Ihren macOS-Geräten zu.

Mithilfe dieses Features können Administratoren Benutzer dazu berechtigen, Kernelerweiterungen zu überschreiben sowie Team-IDs und bestimmte Kernelerweiterungen in Intune hinzuzufügen.

Weitere Informationen zu Kernelerweiterungen finden Sie unter [Kernelerweiterungen](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (Apple-Website).

## <a name="prerequisites"></a>Voraussetzungen

- Diese Funktion gilt für:

  - macOS 10.13.2 und höher (Kernelerweiterungen)
  - macOS 10.15 und höher (Systemerweiterungen)

  Für macOS 10.15 bis 10.15.4 können Kernelerweiterungen und Systemerweiterungen parallel ausgeführt werden.

- Wenn Sie dieses Feature verwenden möchten, muss Folgendes auf Ihre Geräte zutreffen:

  - Ihre Geräte sind über das Programm zur Geräteregistrierung von Apple (DEP) bei Intune registriert. Weitere Informationen finden Sie unter [Automatisches Registrieren von macOS-Geräten mit dem Programm zur Geräteregistrierung oder Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md).

    ODER

  - Ihre Geräte sind über sogenanntes „user approved enrollment“ (Registrierung mit Benutzereinwilligung; Apple-Begriff) bei Intune registriert. Weitere Informationen finden Sie auf der Apple-Website [Auf Änderungen an Kernel-Erweiterungen in macOS High Sierra vorbereiten](https://support.apple.com/en-us/HT208019).

## <a name="what-you-need-to-know"></a>Was Sie wissen müssen

- Nicht signierte Vorgängerversionen von Kernelerweiterungen und Systemerweiterungen können hinzugefügt werden.
- Stellen Sie sicher, dass Sie die korrekte Team-ID und Paket-ID der Erweiterung eingeben. Intune überprüft die eingegebenen Werte nicht. Wenn Sie falsche Informationen eingeben, funktioniert die Erweiterung auf dem Gerät nicht. Eine Team-ID ist genau zehn alphanumerische Zeichen lang.

> [!NOTE]
> Bei Apple stehen Informationen zum Signieren und zur Notarisierung sämtlicher Software zur Verfügung. Ab macOS 10.14.5 müssen Kernelerweiterungen, die über Intune bereitgestellt werden, nicht mehr der Notarisierungsrichtlinie von Apple entsprechen.
>
> Informationen zu dieser Notarisierungsrichtlinie sowie sämtliche Aktualisierungen oder Änderungen finden Sie auf den folgenden Apple-Websites:
>
> - [Notarizing your app before distribution (Notarisierung Ihrer App vor der Verteilung)](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) 
> - [Auf Änderungen an Kernel-Erweiterungen in macOS High Sierra vorbereiten](https://support.apple.com/en-us/HT208019)

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie **macOS** aus.
    - **Profil**: Wählen Sie **Erweiterungen** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname ist beispielsweise **macOS: Hinzufügen von Antivirenscans zu Kernelerweiterungen auf Geräten**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Konfigurieren Sie Ihre Einstellungen in den **Konfigurationseinstellungen**:

    - [macOS](kernel-extensions-settings-macos.md)

8. Wählen Sie **Weiter** aus.
9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="next-steps"></a>Nächste Schritte

Nachdem das Profil erstellt wurde, kann es zugewiesen werden. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).
