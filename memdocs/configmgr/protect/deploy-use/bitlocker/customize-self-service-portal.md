---
title: Anpassen des Self-Service-Portals
titleSuffix: Configuration Manager
description: Hinzufügen benutzerdefinierter organisationsspezifischer Informationen zum Self-Service-Portal für die BitLocker-Verwaltung
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 220ebb558a0e01f701cab621381ad951a8fd0738
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88123900"
---
# <a name="customize-the-self-service-portal"></a>Anpassen des Self-Service-Portals

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

Nachdem Sie das [Self-Service-Portal von BitLocker installiert](setup-websites.md) haben, können Sie es für Ihre Organisation anpassen. Fügen Sie einen benutzerdefinierten Hinweis, den Namen Ihrer Organisation und andere organisationsspezifische Informationen hinzu.

## <a name="branding"></a>Branding

Kennzeichnen Sie das Self-Service-Portal mit dem Namen Ihrer Organisation, der Helpdesk-URL und dem Hinweistext.

1. Melden Sie sich auf dem Webserver, der das Self-Service-Portal hostet, als Administrator an.

1. Starten Sie den **Internetinformationsdienste-Manager (IIS)** (führen Sie **inetmgr.exe** aus).

1. Erweitern Sie **Sites**, erweitern Sie **Standardwebsite**, und wählen Sie den Knoten **SelfService** aus. Öffnen Sie in der Detailansicht in der Gruppe **ASP.NET** die Option **Anwendungseinstellungen**.

    [![Screenshot der Einstellungen der Selfservice-Anwendung im IIS-Manager Beispiel](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. Wählen Sie das zu ändernde Element und dann im Bereich **Aktionen** die Option **Bearbeiten** aus. Ändern Sie den **Wert** in den neuen Namen, den Sie verwenden möchten.

    > [!CAUTION]
    > Ändern Sie nicht die Werte für **Name**. Ändern Sie z. B. nicht `CompanyName`, sondern `Contoso IT`. Wenn Sie die Werte für **Name** ändern, funktioniert das Self-Service-Portal nicht mehr.

Die Änderungen werden sofort wirksam.

### <a name="supported-branding-values"></a>Unterstützte Branding-Werte

In der folgenden Tabelle finden Sie die Werte, die Sie festlegen können:

|Name|Beschreibung|Default&nbsp;value|
|--- |--- |--- |
|CompanyName|Der Organisationsname, den das Self-Service-Portal als Kopfzeile oben auf jeder Seite anzeigt.|`Contoso IT`|
|DisplayNotice|Zeigen Sie einen anfänglichen Hinweis an, den der Benutzer bestätigen muss.|`true`|
|HelpdeskText|Die Zeichenfolge im rechten Bereich unter „Für alle anderen verwandten Themen“.|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|Der Link für die HelpdeskText-Zeichenfolge.|(leer)|
|NoticeTextPath|Der Text des anfänglichen Hinweises, den der Benutzer bestätigen muss. Standardmäßig lautet der vollständige Dateipfad auf dem Webserver `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`. Bearbeiten und speichern Sie die Datei in einem einfachen Text-Editor. Dieser Pfadwert ist relativ zur SelfService-Anwendung.|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

Einen Screenshot des Self-Service-Standardportals finden Sie unter [BitLocker-Self-Service-Portal](self-service-portal.md).

> [!TIP]
> Bei Bedarf können Sie einige dieser Zeichenfolgen für die Anzeige in verschiedenen Sprachen lokalisieren. Weitere Informationen finden Sie unter [Lokalisierung](#bkmk_localize).

## <a name="session-time-out"></a>Sitzungstimeout

Damit die Sitzung des Benutzers nach einer bestimmten Zeit der Inaktivität abläuft, können Sie die Einstellung des Sitzungstimeouts für das Self-Service-Portal ändern.

1. Melden Sie sich auf dem Webserver, der das Self-Service-Portal hostet, als Administrator an.

1. Starten Sie den **Internetinformationsdienste-Manager (IIS)** (führen Sie **inetmgr.exe** aus).

1. Erweitern Sie **Sites**, erweitern Sie **Standardwebsite**, und wählen Sie den Knoten **SelfService** aus. Öffnen Sie im Detailbereich in der Gruppe **ASP.NET** die Option **Sitzungsstatus**.

1. Ändern Sie in der Gruppe **Cookieeinstellungen** den Wert **Timeout (in Minuten)** . Dies ist die Anzahl der Minuten, nach denen die Sitzung des Benutzers abläuft. Der Standardwert lautet `5`. Zum Deaktivieren der Einstellung, sodass kein Timeout erfolgt, legen Sie den Wert auf `0` fest.

1. Klicken Sie im Bereich **Aktionen** auf **Übernehmen**.

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a> Lokalisieren von Helpdesktext und -URL

Sie können lokalisierte Versionen der `HelpdeskText`-Anweisung und des `HelpdeskUrl`-Links des Self-Service-Portals konfigurieren. Diese Zeichenfolge informiert Benutzer darüber, wie sie zusätzliche Hilfe erhalten, wenn sie das Portal benutzen. Wenn Sie lokalisierten Text konfigurieren, zeigt das Portal die lokalisierte Version für Webbrowser in dieser Sprache an. Wenn es keine lokalisierte Version findet, zeigt es den Standardwert in den Einstellungen `HelpdeskText` und `HelpdeskUrl` an.

1. Melden Sie sich auf dem Webserver, der das Self-Service-Portal hostet, als Administrator an.

1. Starten Sie den **Internetinformationsdienste-Manager (IIS)** (führen Sie **inetmgr.exe** aus).

1. Erweitern Sie **Sites**, erweitern Sie **Standardwebsite**, und wählen Sie den Knoten **SelfService** aus. Öffnen Sie in der Detailansicht in der Gruppe **ASP.NET** die Option **Anwendungseinstellungen**.

1. Klicken Sie im Bereich **Aktionen** auf **Hinzufügen**.

1. Konfigurieren Sie im Fenster **Anwendungseinstellung hinzufügen** die folgenden Werte:

    - **Name**: Geben Sie `HelpdeskText_<language>` ein, wobei `<language>` der Sprachcode für den Text ist.

      Wenn Sie z. B. eine lokalisierte `HelpdeskText`-Anweisung in Spanisch (Spanien) erstellen möchten, lautet der Name `HelpdeskText_es-es`.

    - **Wert**: Die lokalisierte Zeichenfolge, die im rechten Bereich des Self-Service-Portals unter „Für alle anderen verwandten Themen“ angezeigt werden soll.

1. Wählen Sie **OK** aus, um die neue Einstellung zu speichern.

1. Wiederholen Sie diesen Vorgang, um eine neue Anwendungseinstellung für `HelpdeskUrl_<language>` hinzuzufügen, die mit der zugehörigen Einstellung `HelpdeskText_<language>` übereinstimmt.

Wiederholen Sie diesen Vorgang, um ein Einstellungspaar für alle Sprachen hinzuzufügen, die Sie in Ihrer Organisation unterstützen.

## <a name="localize-the-notice-file"></a>Lokalisieren der Hinweisdatei

Sie können lokalisierte Versionen des anfänglichen Hinweises konfigurieren, den der Benutzer im Self-Service-Portal bestätigen muss. Standardmäßig lautet der vollständige Dateipfad auf dem Webserver `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`.

Erstellen Sie eine lokalisierte notice.txt-Datei, um lokalisierten Hinweistext anzuzeigen. Speichern Sie sie dann unter einem bestimmten Sprachordner. Beispiel: `Self Service Website\es-es\Notice.txt` für Spanisch (Spanien).

Das Self-Service-Portal zeigt den Hinweistext auf der Grundlage der folgenden Regeln an:

- Wenn die Standardhinweisdatei fehlt, zeigt das Portal eine Meldung an, dass die Standarddatei fehlt.

- Wenn Sie eine lokalisierte Hinweisdatei im entsprechenden Sprachordner erstellen, zeigt diese den lokalisierten Hinweistext an.

- Wenn der Webserver keine lokalisierte Version der Hinweisdatei findet, zeigt er den Standardhinweis an.

- Wenn der Benutzer seinen Browser auf eine Sprache einstellt, für die es keinen lokalisierten Hinweis gibt, zeigt das Portal den Standardhinweis an.

### <a name="create-a-localized-notice-file"></a>Erstellen einer lokalisierten Hinweisdatei

1. Melden Sie sich auf dem Webserver, der das Self-Service-Portal hostet, als Administrator an.

1. Erstellen Sie einen Ordner `<language>` für jede unterstützte Sprache im `Self Service Website`-Anwendungspfad. Beispiel: `es-es` für Spanisch (Spanien). Standardmäßig ist der vollständige Pfad `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es`.

    Eine Liste der gültigen Sprachcodes, die Sie verwenden können, finden Sie unter [Referenz zur NLS-API (Unterstützung von Landessprachen)](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers).

    > [!TIP]
    > Der Name des Sprachordners kann auch der sprachneutrale Name sein. Beispiel: **es** für Spanisch, statt **es-es** für Spanisch (Spanien) und **es-ar** für Spanisch (Argentinien). Wenn der Benutzer seinen Browser auf **es-es** einstellt und dieser Sprachordner nicht existiert, überprüft der Webserver rekursiv den übergeordneten Gebietsschemaordner (**es**). (Die übergeordneten Gebietsschemas sind in .NET definiert.) Beispiel: `Self Service Website\es\Notice.txt`. Dieses rekursive Fallback imitiert die Laderegeln für .NET-Ressourcen.

1. Erstellen Sie eine Kopie Ihrer Standardhinweisdatei mit dem lokalisierten Text. Speichern Sie sie im Ordner für den Sprachcode. Für Spanisch (Spanien) lautet der vollständige Pfad z. B. standardmäßig `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt`.

Wiederholen Sie diesen Vorgang für eine lokalisierte Hinweisdatei für alle Sprachen, die Sie in Ihrer Organisation unterstützen.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie das Self-Service-Portal installiert und angepasst haben, probieren Sie es aus! Weitere Informationen finden Sie unter [BitLocker-Self-Service-Portal](self-service-portal.md).
