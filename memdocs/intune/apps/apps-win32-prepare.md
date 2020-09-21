---
title: Vorbereiten einer Win32-App auf den Upload in Microsoft Intune
titleSuffix: ''
description: Erfahren Sie, wie Sie eine Win32-App auf den Upload in Microsoft Intune vorbereiten.
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
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 94626b6cc7e9586ff6b9230206c3e57e6b01b86f
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083796"
---
# <a name="prepare-win32-app-content-for-upload"></a>Vorbereiten des Inhalts der Win32-App für den Upload

Bevor Sie Microsoft Intune eine Win32-App hinzufügen können, müssen Sie die App mit dem [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) vorbereiten.

## <a name="prerequisites"></a>Voraussetzungen

Stellen Sie sicher, dass die folgenden Kriterien erfüllt sind, wenn Sie die Win32-App-Verwaltung verwenden wollen:

- Verwenden Sie Windows 10 Version 1607 oder höher (Enterprise-, Pro- und Education-Editionen).
- Geräte müssen Azure Active Directory (Azure AD) beigetreten und automatisch registriert sein. Die Intune-Verwaltungserweiterung unterstützt Geräte, die Azure AD und der hybriden Domäne beigetreten und per Gruppenrichtlinie registriert sind. 
  > [!NOTE]
  > Im Szenario der Registrierung per Gruppenrichtlinie verwenden Endbenutzer das lokale Benutzerkonto zum Einbinden ihrer Windows 10-Geräte in Azure AD. Benutzer müssen sich mit ihrem Azure AD-Benutzerkonto beim Gerät anmelden und sich bei Intune registrieren. Intune installiert die Intune-Verwaltungserweiterung auf dem Gerät, wenn ein PowerShell-Skript oder eine Win32-App auf einen Benutzer oder ein Gerät ausgerichtet sind.
- Die Größe der Windows-Anwendung ist auf 8 GB pro App begrenzt.

## <a name="convert-the-win32-app-content"></a>Konvertieren des Inhalts der Win32-App

Verwenden Sie das [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) zum Vorverarbeiten von klassischen Windows-Apps (Win32). Das Tool konvertiert Anwendungsinstallationsdateien in das *INTUNEWIN*-Format. Das Tool erkennt auch einige der Attribute, die Intune benötigt, um den Installationsstatus der Anwendung zu bestimmen. Nachdem Sie dieses Tool im Installationsordner der App verwendet haben, können Sie in der Intune-Konsole eine Win32-App erstellen.

> [!IMPORTANT]
> Beim Erstellen der *.intunewin*-Datei zippt das [Microsoft Win32-Inhaltsvorbereitungstool](https://go.microsoft.com/fwlink/?linkid=2065730) alle Dateien und Unterordner. Achten Sie darauf, das Microsoft Win32-Inhaltsvorbereitungstool nicht zusammen mit den Installationsdateien und -ordnern zu speichern, damit Sie das Tool oder andere unnötige Dateien und Ordner nicht in Ihre *.intunewin*-Datei einschließen.

Sie können das [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) als ZIP-Datei von GitHub herunterladen. Die ZIP-Datei enthält einen Ordner namens *Microsoft-Win32-Content-Prep-Tool-master*. Der Ordner enthält das Vorbereitungstool, die Lizenz, eine Infodatei und die Versionshinweise. 

### <a name="process-flow-to-create-a-intunewin-file"></a>Prozessflow zum Erstellen einer .intunewin-Datei

   <img alt="Flow chart of the process to create a .intunewin file." src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### <a name="running-the-microsoft-win32-content-prep-tool"></a>Ausführen des Microsoft Win32 Content Prep Tool

Wenn Sie `IntuneWinAppUtil.exe` im Befehlsfenster ohne Parameter ausführen, leitet Sie das Tool Schritt für Schritt durch die Eingabe der erforderlichen Parameter. Sie können dem Befehl die Parameter auch basierend auf den folgenden verfügbaren Befehlszeilenparametern hinzufügen:

### <a name="available-command-line-parameters"></a>Verfügbare Befehlszeilenparameter: 

|    **Befehlszeilenparameter**    |    **Beschreibung**    |
|--------------------------------|------------------------------------------------------------|
|    `-h`     |    Hilfe    |
|    `-c <setup_folder>`     |    Ordner für alle Setupdateien. Alle Dateien in diesem Ordner werden in die *.intunewin*-Datei komprimiert.    |
|    `-s <setup_file>`     |    Setupdatei (z. B. *setup.exe* oder *setup.msi*).    |
|    `-o <output_folder>`     |    Ausgabeordner für die generierte *.intunewin*-Datei.    |
|    `-q`       |    Stiller Modus.    |

### <a name="example-commands"></a>Beispielbefehle

|    **Beispielbefehl**    |    **Beschreibung**    |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `IntuneWinAppUtil -h`    |    Dieser Befehl zeigt Nutzungsinformationen für das Tool an.    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    Dieser Befehl generiert die *.intunewin*-Datei aus dem angegebenen Quellordner und der Setupdatei. Für die MSI-Setupdatei ruft dieses Tool die erforderlichen Informationen für Intune ab. Wenn `-q` angegeben ist, wird der Befehl im stillen Modus ausgeführt. Wenn die Ausgabedatei bereits vorhanden ist, wird sie überschrieben. Wenn der Ausgabeordner nicht vorhanden ist, wird er automatisch erstellt.    |

Wenn Sie eine *.intunewin*-Datei generieren, legen Sie alle Dateien, die Sie als Referenz benötigen, in einem Unterordner des Setupordners ab. Verwenden Sie dann einen relativen Pfad, um auf die gewünschte Datei zu verweisen. Beispiel:

**Setupquellordner:** *C:\testapp\v1.0*<br>
**Lizenzdatei:** *C:\testapp\v1.0\licenses\license.txt*

Verweisen Sie auf die Datei *license.txt* mit dem relativen Pfad *licenses\license.txt*.

## <a name="next-steps"></a>Nächste Schritte

- [Hinzufügen einer Win32-App zu Microsoft Intune](apps-win32-add.md)
