---
title: Hinzufügen branchenspezifischer Windows-Apps zu Microsoft Intune
titleSuffix: ''
description: Erfahren Sie, wie Sie branchenspezifische Windows-Apps mithilfe von Microsoft Intune hinzufügen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f81c5f82-5cfa-4b97-9f73-d6cf77c06896
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b70f36873200d0adbbc356d9a482cf13cc2ea49
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913323"
---
# <a name="add-a-windows-line-of-business-app-to-microsoft-intune"></a>Hinzufügen branchenspezifischer Windows-Apps zu Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Branchenspezifische Apps werden über eine App-Installationsdatei hinzugefügt. Diese Art von App wird in der Regel intern geschrieben. Die folgenden Schritte enthaltenen Informationen zum Hinzufügen einer LOB-Windows-App mit Microsoft Intune.

> [!IMPORTANT]
> Wenn Sie Win32-Apps mithilfe einer Installationsdatei mit der Erweiterung „.msi“ bereitstellen (mithilfe des Content Prep Tools in eine .intunewin-Datei gepackt), sollten Sie die Verwendung der [Intune-Verwaltungserweiterung](../apps/intune-management-extension.md) in Erwägung ziehen. Wenn Sie die Installation von Win32- und branchenspezifischen Apps während der Autopilot-Registrierung kombinieren, kann die App-Installation fehlschlagen.  

## <a name="select-the-app-type"></a>Auswählen des App-Typs

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Alle Apps** > **Hinzufügen** aus.
3. Wählen Sie im Bereich **App-Typ auswählen** unter den App-Typen **Sonstige** die Option **Branchenspezifische App** aus.
4. Klicken Sie auf **Auswählen**. Die **App hinzufügen**-Schritte werden angezeigt.

## <a name="step-1---app-information"></a>Schritt 1: App-Informationen

### <a name="select-the-app-package-file"></a>Auswählen der App-Paketdatei

1. Klicken Sie im Bereich **App hinzufügen** auf **App-Paketdatei auswählen**. 
2. Wählen Sie im Bereich **App-Paketdatei** die Schaltfläche zum Durchsuchen. Wählen Sie dann eine Windows-Installationsdatei mit der Erweiterung **MSI**, **APPX** oder **APPXBUNDLE** aus.
   Die App-Details werden angezeigt.

    > [!NOTE]
    > Zu den Dateierweiterungen für Windows-Apps gehören **.msi**, **.appx**, **.appxbundle**, **.msix** und **.msixbundle**. Weitere Informationen zu **.msix** finden Sie in der [MSIX-Dokumentation](/windows/msix/) und unter [MSIX-App-Verteilung](/windows/msix/desktop/managing-your-msix-deployment-enterprise).

3. Wenn Sie fertig sind, wählen Sie im Bereich **App-Paketdatei** die Option **OK** aus, um die App hinzuzufügen.

### <a name="set-app-information"></a>Festlegen von App-Informationen

1. Fügen Sie auf der Seite **App-Informationen** die Details zu Ihrer App hinzu. Abhängig von der ausgewählten App wurden einige der Werte in diesem Bereich möglicherweise automatisch ausgefüllt.
    - **Name:** Geben Sie den Namen der App so ein, wie er im Unternehmensportal angezeigt wird. Stellen Sie sicher, dass alle App-Namen eindeutig sind. Wenn ein App-Name zweimal vergeben wird, wird im Unternehmensportal nur eine der Apps angezeigt.
    - **Beschreibung:** Geben Sie eine Beschreibung für die App ein. Die Beschreibung wird im Unternehmensportal angezeigt.
    - **Herausgeber**: Geben Sie den Namen des Herausgebers der App ein.
    - **App-Installationskontext**: Wählen Sie den Installationskontext aus, der dieser App zugeordnet werden soll. Wählen Sie für Apps mit dualem Modus den gewünschten Kontext aus. Für alle weiteren Apps wird diese Einstellung basierend auf dem Paket vorausgewählt und kann nicht geändert werden.
    - **App-Version ignorieren**: Legen Sie diese Option auf **Ja** fest, wenn der App-Entwickler die App automatisch aktualisiert. Diese Option gilt nur für mobile MSI-Apps.
    - **Befehlszeilenargumente**: Geben Sie optional Befehlszeilenargumente ein, die bei Ausführung auf die MSI-Datei angewendet werden sollen.  Ein Beispiel ist **/q**. Schließen Sie den Befehl „msiexec“ und Argumente wie **/i** oder **/x** nicht ein, da diese automatisch verwendet werden. Weitere Informationen finden Sie unter [Befehlszeilenoptionen](/windows/desktop/Msi/command-line-options). Wenn die MSI-Datei zusätzliche Befehlszeilenoptionen benötigt, verwenden Sie [Win32-App-Verwaltung](app-management.md).
    - **Kategorie**: Wählen Sie eine oder mehrere der integrierten oder von Ihnen erstellten App-Kategorien aus. Kategorien erleichtern es dem Benutzer, die App über das Unternehmensportal zu finden.
    - **Diese App als ausgewählte App im Unternehmensportal anzeigen**: Präsentieren Sie die App herausgehoben auf der Hauptseite des Unternehmensportals, wenn die Benutzer nach Apps suchen.
    - **Informations-URL**: Geben Sie optional eine URL zu einer Website ein, die Informationen über diese App enthält. Die URL wird im Unternehmensportal angezeigt.
    - **URL der Datenschutzrichtlinien:** Geben Sie optional eine URL zu einer Website ein, die Datenschutzinformationen für diese App enthält. Die URL wird im Unternehmensportal angezeigt.
    - **Entwickler**: Geben Sie optional den Namen des App-Entwicklers ein.
    - **Besitzer**: Geben Sie optional einen Namen für den Besitzer dieser App ein. Ein Beispiel ist **Personalabteilung**.
    - **Anmerkungen**: Geben Sie Hinweise zu dieser App ein.
    - **Logo**: Laden Sie ein Symbol hoch, das der App zugeordnet wird. Dieses Symbol wird mit der App angezeigt, wenn Benutzer das Unternehmensportal durchsuchen.
2. Klicken Sie auf **Weiter**, um die Seite **Bereichsmarkierungen** anzuzeigen.

## <a name="step-2---select-scope-tags-optional"></a>Schritt 2: Auswählen von Bereichsmarkierungen (optional)

Sie können Bereichsmarkierungen verwenden, um zu bestimmen, wer Client-App-Informationen in Intune anzeigen kann. Ausführliche Informationen zu Bereichsmarkierungen finden Sie unter [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Verwenden der rollenbasierten Zugriffssteuerung und von Bereichsmarkierungen für verteilte IT).

1. Klicken Sie auf **Bereichstags auswählen**, um optional Bereichsmarkierungen für die App hinzuzufügen. 
2. Klicken Sie auf **Weiter**, um die Seite **Zuweisungen** anzuzeigen.

## <a name="step-3---assignments"></a>Schritt 3: Zuweisungen

1. Wählen Sie die Gruppenzuweisungen **Erforderlich**, **Für registrierte Geräte verfügbar** oder **Deinstallieren** für die App aus. Weitere Informationen finden Sie unter [Hinzufügen von Gruppen zum Organisieren von Benutzern und Geräten](../fundamentals/groups-add.md) und [Zuweisen von Apps zu Gruppen mit Microsoft Intune](apps-deploy.md).
2. Klicken Sie auf **Weiter**, um die Seite **Überprüfen + erstellen** anzuzeigen.

## <a name="step-4---review--create"></a>Schritt 4: Überprüfen und Erstellen

1. Überprüfen Sie die Werte und Einstellungen, die Sie für die App eingegeben haben.
2. Klicken Sie abschließend auf **Erstellen**, um Intune die App hinzuzufügen.

    Das Blatt **Übersicht** für die branchenspezifische App wird angezeigt.

Die von Ihnen erstellte App wird nun in der Liste der Apps angezeigt. Sie können die App über die Liste den von Ihnen ausgewählten Gruppen zuweisen. Hilfe finden Sie unter [Zuweisen von Apps zu Gruppen](apps-deploy.md).

## <a name="update-a-line-of-business-app"></a>Aktualisieren einer branchenspezifischen App

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

   > [!NOTE]
   > Damit der Intune-Dienst eine neue APPX-Datei erfolgreich auf dem Gerät bereitstellt, müssen Sie die Zeichenfolge `Version` in der Datei „AndroidManifest.xml“ in Ihrem APPX-Paket erhöhen.

## <a name="configure-a-self-updating-mobile-msi-app-to-ignore-the-version-check-process"></a>Konfigurieren Sie eine mobile MSI-App, die sich selbst aktualisiert, um den Prozess der Versionsüberprüfung zu ignorieren.

Sie können eine bekannte mobile MSI-App konfigurieren, die sich selbst aktualisiert, um den Prozess der Versionsüberprüfung zu ignorieren.

Einige MSI-basierte Apps werden automatisch vom App-Entwickler oder durch eine andere Aktualisierungsmethode aktualisiert. Für diese automatisch aktualisierten MSI-Apps können Sie die Einstellung **App-Version ignorieren** im Bereich **App-Informationen** konfigurieren. Wenn diese Einstellung auf **Ja** festgelegt wird, erzwingt Microsoft Intune keine App-Version, die auf dem Windows-Client installiert ist.

Diese Einstellung ist nützlich, um Racebedingungen zu vermeiden. Beispielsweise kann eine Racebedingung auftreten, wenn die App automatisch vom App-Entwickler und von Intune aktualisiert wird. Beide könnten dann eine Version der App auf dem Windows-Client erzwingen, was einen Konflikt auslösen kann.

## <a name="next-steps"></a>Nächste Schritte

- Die von Ihnen erstellte App wird in der Liste der Apps angezeigt. Sie können sie jetzt den ausgewählten Gruppen zuweisen. Hilfe finden Sie unter [Zuweisen von Apps zu Gruppen](apps-deploy.md).

- Erfahren Sie mehr darüber, wie Sie die Eigenschaften und Zuweisungen Ihrer App überwachen können. Siehe [Überwachen von App-Informationen und -Zuweisungen](apps-monitor.md).

- Erfahren Sie mehr über den Kontext Ihrer App in Intune. Weitere Informationen erhalten Sie unter [Übersicht über den App-Lebenszyklus in Microsoft Intune](app-lifecycle.md).

- Erfahren Sie mehr über Win32-Apps. Siehe [Win32-App-Verwaltung](apps-win32-app-management.md).