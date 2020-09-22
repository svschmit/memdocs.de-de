---
title: Apps im Unternehmensportal
titleSuffix: Configuration Manager
description: Stellen Sie für gemeinsam verwaltete Geräte eine einheitliche Benutzererfahrung zur Nutzung der Unternehmensportal-App bereit.
ms.date: 09/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: 26456bb7-f46b-4d8d-bb0b-e3fd9a52fe14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d44116ee022f2f01fb8b84244fb903fa6d440345
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076157"
---
# <a name="use-the-company-portal-app-on-co-managed-devices"></a>Verwenden der Unternehmensportal-App auf gemeinsam verwalteten Geräten

*Gilt für: Configuration Manager (Current Branch)*

<!--CMADO-3601237,INADO-4297660-->

Ab Version 2006 ist das Unternehmensportal nun das plattformübergreifende App-Portal für Microsoft Endpoint Manager. Indem Sie gemeinsam verwaltete Geräte so konfigurieren, dass sie auch das Unternehmensportal nutzen, können Sie auf allen Geräten eine einheitliche Benutzererfahrung bieten.

Da Unternehmensportal unterstützt die folgenden Aktionen:

- Starten der Unternehmensportal-App auf gemeinsam verwalteten Geräten und einmaliges Anmelden (Single Sign-On, SSO) mithilfe von Azure Active Directory (Azure AD)
- Anzeigen verfügbarer und installierter Configuration Manager-Apps im Unternehmensportal neben Intune-Apps
- Installieren verfügbarer Configuration Manager-Apps im Unternehmensportal und Empfangen von Informationen zum Installationsstatus

:::image type="content" source="media/3601237-company-portal.png" alt-text="Unternehmensportal mit App aus Configuration Manager" lightbox="media/3601237-company-portal.png":::

Das Verhalten des Unternehmensportals hängt von der Konfiguration Ihrer Workload für die Co-Verwaltung ab:

| Workload | Einstellung | Verhalten |
|----------|---------|----------|
| Client-Apps | **Configuration Manager** | Es werden nur Configuration Manager-Client-Apps angezeigt. |
| Client-Apps | **Intune-Pilot** oder **Intune** | Es werden sowohl Configuration Manager- als auch Intune-Client-Apps angezeigt. |
| Office-Klick-und-Los-Apps | **Configuration Manager** | Es werden nur Office-Klick-und-Los-Apps aus Configuration Manager angezeigt. |
| Office-Klick-und-Los-Apps | **Intune-Pilot** oder **Intune** | Es werden nur Office-Klick-und-Los-Apps aus Intune angezeigt. |

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Diagramm zu App-Workloads](workloads.md#diagram-for-app-workloads)

- [Umstellen von Configuration Manager-Workloads auf Intune](how-to-switch-workloads.md)

## <a name="prerequisites"></a>Voraussetzungen

- Configuration Manager Current Branch, ab Version 2006 <sup>([Siehe FAQ](#bkmk_ver-prereq))</sup>

- Unternehmensportal-App, Version 11.0.8980.0 oder höher

- Windows 10 ab Version 1803:

  - Für [Co-Verwaltung](how-to-enable.md) registriert

  - Zugriff auf [Endpunkte im Internet für Intune](../../intune/fundamentals/intune-endpoints.md)

- Die Benutzerkonten, die sich bei diesen Geräten anmelden, benötigen Folgendes:

  - Eine Azure AD-Identität

  - Eine zugewiesene Intune-Lizenz

## <a name="configure-and-deploy"></a>Konfigurieren und Bereitstellen

### <a name="configuration-manager-client-settings"></a>Clienteinstellungen von Configuration Manager

Um sicherzustellen, dass Benutzer nur Benachrichtigungen vom Unternehmensportal empfangen, konfigurieren Sie die Clienteinstellungen von Configuration Manager. Ändern Sie in der Gruppe **Softwarecenter** der Geräteeinstellungen **Wählen Sie das Benutzerportal aus** in **Unternehmensportal**.

Weitere Informationen zu Clienteinstellungen finden Sie in den folgenden Artikeln:

- [Konfigurieren von Clienteinstellungen](../core/clients/deploy/configure-client-settings.md)
- [Informationen zu Clienteinstellungen](../core/clients/deploy/about-client-settings.md#software-center)

### <a name="deploy-the-company-portal-app"></a>Bereitstellen der Unternehmensportal-App

- Benutzer können die Unternehmensportal-App über den [Microsoft Store](https://www.microsoft.com/p/company-portal/9wzdncrfj3pz?activetab=pivot:overviewtab) manuell installieren.

- Um die App auf gemeinsam verwalteten Geräten vorzuschreiben, hängt der Bereitstellungsprozess vom Status des Co-Verwaltungsworkloads [Client-Apps](workloads.md#client-apps) ab:

  - Wenn die Workload „Client-Apps“ zu Configuration Manager gehört, [müssen Sie eine Anwendung mit Configuration Manager erstellen und bereitstellen](../apps/get-started/create-and-deploy-an-application.md). Laden Sie die Unternehmensportal-App für die Offlinenutzung aus dem [Microsoft Store für Unternehmen](https://www.microsoft.com/business-store) herunter.

  - Wenn die Workload „Client-Apps“ zu Intune gehört, können Sie sie über Configuration Manager bereitstellen oder [die Unternehmensportal-App für Windows 10 mithilfe von Microsoft Intune hinzufügen](../../intune/apps/store-apps-company-portal-app.md).

Weitere Informationen zum Branding des Unternehmensportals für Ihre Organisation finden Sie unter [Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../../intune/apps/company-portal-app.md).

## <a name="use-the-company-portal"></a>Verwenden des Unternehmensportals

1. Starten Sie das Unternehmensportal im Startmenü. Der derzeit angemeldete Benutzer wird auf Grundlage seiner Azure AD-Identität automatisch beim Unternehmensportal angemeldet.

1. Wählen Sie die Seite **Apps** aus. Sie sollten Configuration Manager-Apps in der Liste sehen.

1. Wählen Sie eine der vom Configuration Manager bereitgestellten Apps aus.

    - Die Registerkarte **Übersicht** zeigt Details zur App, wie z. B. Größe, Version und Veröffentlichungsdatum.

    - Um zu prüfen, ob Configuration Manager der Verwaltungsdienst für diese App ist, wechseln Sie zur Registerkarte **Zusätzliche Informationen**.

    - Wählen Sie **Installieren** aus, um die App zu installieren. Das Unternehmensportal zeigt den Installationsstatus. Nach Abschluss der Installation erhalten Sie eine Benachrichtigung.

    - Wenn die App bereits installiert ist, wählen Sie **Deinstallieren** aus, um die App zu entfernen.

    - Wählen Sie für weitere Aktionen, z. B. **Reparieren** und **Freigeben**, die Auslassungspunkte (`...`) aus.

        :::image type="content" source="media/3601237-company-portal-app-details.png" alt-text="Configuration Manager-App mit Details im Unternehmensportal" lightbox="media/3601237-company-portal-app-details.png":::

    - Nachdem Sie eine Configuration Manager-Web-App installiert haben, wählen Sie das Menü mit den Auslassungspunkten und dann **Im Browser öffnen** aus, um die Web-App zu starten.

    - Wenn eine Configuration Manager-Anwendung mit einem bekannten Fehlercode fehlschlägt, wählen Sie den entsprechenden Link aus, um nach dem Fehlercode zu suchen.

Wenn Sie die Clienteinstellung für das Unternehmensportal ändern, startet ein Benutzer beim Auswählen einer Configuration Manager-Benachrichtigung das Unternehmensportal. Wenn sich die Benachrichtigung auf ein Szenario bezieht, das das Unternehmensportal nicht unterstützt, wird durch Auswählen der Benachrichtigung das Softwarecenter gestartet.

Um Hilfe bei Installationsproblemen mit Configuration Manager-Apps zu erhalten, besuchen Sie im Unternehmensportal den Abschnitt **Hilfe und Support**. Wenn Sie die Option **Hilfe anfordern** wählen, können Sie als Teil der Anforderung Configuration Manager-Protokolldateien senden.

## <a name="frequently-asked-questions-faq"></a>Häufig gestellte Fragen (FAQ)

### <a name="im-using-configuration-manager-version-2002-why-is-the-new-company-portal-showing-configuration-manager-apps"></a><a name="bkmk_ver-prereq"></a> Ich verwende Configuration Manager, Version 2002. Warum zeigt das neue Unternehmensportal Configuration Manager-Apps an?

Unternehmensportal, Version 11.0.8980.0 oder höher, zeigt von Configuration Manager bereitgestellte Anwendungen für alle gemeinsam verwalteten Clients an, die es verwenden. Configuration Manager, Version 2006, ist die Voraussetzung, da es die Clienteinstellung zur Steuerung von Benachrichtigungen hinzufügt. Wenn Sie das Unternehmensportal auf einem gemeinsam verwalteten Gerät einer früheren Version installieren oder die Clienteinstellung nicht konfigurieren, verursacht dies ein Verhalten, das für Benutzer verwirrend sein kann. Benachrichtigungen von Configuration Manager starten das Software Center, während Benachrichtigungen von Intune das Unternehmensportal starten.

Microsoft-Empfehlung:

- Verwenden Sie das Unternehmensportal, Version 11.0.8980.0 oder höher, auf gemeinsam verwalteten Clients, auf denen Configuration Manager, Version 2006 oder höher, ausgeführt wird.
- Konfigurieren Sie die Clienteinstellung **Wählen Sie das Benutzerportal aus** auf **Unternehmensportal**.

### <a name="does-company-portal-support-applications-deployed-as-software-updates-from-configuration-manager"></a>Unterstützt das Unternehmensportal Anwendungen, die als Softwareupdates über Configuration Manager bereitgestellt werden?

Ja. Wenn Sie eine App mit dem Feature „Softwareupdates“ bereitstellen, wird sie vom Client unabhängig davon, ob es sich bei der Benutzerumgebung um das Unternehmensportal oder Softwarecenter handelt, gleich behandelt.

### <a name="can-users-repair-uninstall-and-update-configuration-manager-apps-in-company-portal"></a>Können Benutzer Configuration Manager-Apps im Unternehmensportal reparieren, deinstallieren und aktualisieren?

Ja. Wenn Sie die Configuration Manager-App so konfigurieren, dass diese zusätzlichen Aktionen unterstützt werden, unterstützt das Unternehmensportal das Reparieren, Deinstallieren und Aktualisieren.

## <a name="known-issues"></a>Bekannte Probleme

Die folgenden Features des Softwarecenters sind derzeit nicht im Unternehmensportal verfügbar:

- Einige Informationen zu Apps, z. B. ob ein Neustart erforderlich ist oder die geschätzte Zeit für die Installation

- [App-Gruppen](../apps/deploy-use/create-app-groups.md)

Andere bekannte Probleme:

- Wenn Sie dieselbe App sowohl über Configuration Manager als auch über Intune bereitstellen, wird sie im Unternehmensportal zweimal angezeigt.

- Wenn Sie das Unternehmensportal durchsuchen, werden Intune-Apps immer vor Configuration Manager-Apps angezeigt.

## <a name="next-steps"></a>Nächste Schritte

[Umstellen von Configuration Manager-Workloads auf Intune](how-to-switch-workloads.md)

[Anpassen der App „Intune-Unternehmensportal“](../../intune/apps/company-portal-app.md)
