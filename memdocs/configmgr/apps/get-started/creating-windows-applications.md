---
title: Erstellen von Windows-Anwendungen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Windows-Anwendungen in Configuration Manager erstellen und bereitstellen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 6b7ce4fd1ab09607f167696df35f3b5f19469b0d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688988"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Erstellen von Windows-Anwendungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zusätzlich zu den anderen Configuration Manager-Anforderungen und -Vorgängen zum [Erstellen einer Anwendung](../deploy-use/create-applications.md) müssen Sie beim Erstellen und Bereitstellen von Anwendungen für Windows-Geräte auch die nachfolgenden Aspekte berücksichtigen.  

## <a name="general-considerations"></a><a name="bkmk_general"></a> Allgemeine Aspekte  

Configuration Manager unterstützt die Bereitstellung von App-Paketen (.appx) und App Bundles (.appxbundle) für Windows 8.1- und Windows 10-Geräte.

Wenn Sie eine Anwendung in der Configuration Manager-Konsole erstellen, wählen Sie als **Typ** der Anwendungsinstallationsdatei **Windows-App-Paket (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** aus. Weitere Informationen zum Erstellen von Apps im Allgemeinen finden Sie unter [Erstellen von Anwendungen](../deploy-use/create-applications.md). Weitere Informationen zum MSIX-Format finden Sie unter [Unterstützung für MSIX-Format](#bkmk_msix).

> [!Note]  
> Wenn Sie neue Configuration Manager-Features nutzen möchten, müssen Sie zunächst die Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a> Bereitstellen von Windows-App-Paketen für alle Benutzer auf einem Gerät
<!--1358310-->
Stellen Sie eine Anwendung mit einem Windows-App-Paket für alle Benutzer auf dem Gerät bereit. Ein allgemeines Beispiel für dieses Szenario ist das Bereitstellen einer App aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen, z. B. Minecraft: Education Edition, für alle Geräte, die von Kursteilnehmer einer Bildungseinrichtung verwendet werden. Zuvor hat Configuration Manager die Installation solcher Anwendungen nur für einzelne Benutzer unterstützt. Wenn ein Schüler sich an einem neuen Gerät anmeldet, musste er warten, bevor er auf eine App zugreifen konnte. Wenn die App nun für das Gerät für alle Benutzer bereitgestellt wird, können sie schneller produktiv sein.

> [!Important]  
> Beachten Sie bei der Installation, Bereitstellung und Aktualisierung, dass verschiedene Versionen des gleichen Windows-App-Pakets auf einem Gerät zu unerwarteten Ergebnissen führen können. Dieses Verhalten kann auftreten, wenn Sie Configuration Manager zum Bereitstellen der App verwenden, aber dann zulassen, dass Benutzer die App über den Microsoft Store aktualisieren können. Weitere Informationen finden Sie im Abschnitt „Nächste Schritte“ unter [Verwalten von Apps aus dem Microsoft Store für Unternehmen](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Wenn Sie eine offline lizenzierte App bereitstellen, lässt Configuration Manager nicht zu, dass Windows die App automatisch über den Microsoft Store aktualisiert.  

Configuration Manager unterstützt die App-Bereitstellung unter allen unterstützten Versionen von Windows 10.<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

Aktivieren Sie die Option **Diese Anwendung für alle Benutzer auf dem Gerät bereitstellen**, um einen Windows-App-Bereitstellungstyp für dieses Feature zu konfigurieren. Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../deploy-use/create-applications.md).

> [!Note]  
> Wenn Sie eine bereitgestellte Anwendung auf Geräten deinstallieren müssen, an denen sich bereits ein Benutzer angemeldet hat, müssen Sie zwei Deinstallationsbereitstellungen erstellen. Erstellen Sie die erste Deinstallationsbereitstellung für eine Gerätesammlung, die die Geräte enthält. Erstellen Sie die zweite Deinstallationsbereitstellung für eine Benutzersammlung, die die Benutzer enthält, die sich bereits an den Geräten bei der bereitgestellten Anwendung angemeldet haben. Wenn Sie eine bereitgestellte Anwendung auf einem Gerät deinstallieren, deinstalliert Windows sie nicht für die Benutzer.

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a> Unterstützung für MSIX-Format
<!--1357427-->

Configuration Manager unterstützt die Bereitstellung von App-Paketen (.msix) und App Bundles (.msixbundle) für Windows 10. Diese Formate werden von Windows 10, Version 1809 oder höher, unterstützt.

- Eine Übersicht über MSIX finden Sie unter [A closer look at MSIX (MSIX von Nahem betrachtet)](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).  

- Informationen zum Erstellen einer neuen MSIX-App finden Sie unter [MSIX support introduced in Insider Build 17682 (Einführung der MSIX-Unterstützung in Insider Build 17682)](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

### <a name="convert-applications-to-msix"></a>Konvertieren von Anwendungen in MSIX
<!--3607729, fka 1359029-->

Konvertieren Sie Ihre vorhandenen Windows Installer-Anwendungen (MSI) in das MSIX-Format.

#### <a name="prerequisites-for-msix"></a>Voraussetzungen für MSIX

- Ein Referenzgerät mit Windows 10, Version 1809 oder höher  

- Melden Sie sich auf diesem Gerät bei Windows als Benutzer mit lokalen Administratorrechten an  

- Installieren Sie auf diesem Gerät die folgenden Apps:  

  - Configuration Manager-Konsole  

  - [MSIX-Paketerstellungstool](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) aus dem Microsoft Store  

  - Den [Treiber für das MSIX-Paketerstellungstool](/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)<!--SCCMDocs-pr issue #3091-->  

Installieren Sie keine anderen Apps oder Dienste auf diesem Gerät. Dies ist Ihr Referenzsystem.

#### <a name="process-to-convert-applications-to-msix-format"></a>Prozess zum Konvertieren von Anwendungen in das MSIX-Format

1. Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungen** aus.  

2. Wählen Sie eine Anwendung mit dem Windows Installer-Bereitstellungstyp (MSI) aus.  

    > [!Note]  
    > Sie müssen vom Referenzgerät aus auf den Quellinhalt der Anwendung zugreifen können.  
    >
    > Der Name der Anwendung darf keine Sonderzeichen enthalten. Configuration Manager verwendet den App-Namen als Namen der Ausgabedatei.  
    >
    > Installieren Sie diese Anwendung nicht vorher auf dem Referenzgerät.  

3. Wählen Sie im Menüband **In MSIX konvertieren** aus.

Wenn der Assistent abgeschlossen ist, erstellt das MSIX-Paketerstellungstool eine MSIX-Datei an dem Speicherort, den Sie im Assistenten angegeben haben. Bei diesem Vorgang installiert Configuration Manager die Anwendung im Hintergrund auf dem Referenzgerät.

Wenn der Prozess fehlschlägt, verweist die Zusammenfassungsseite auf die Protokolldatei mit weiteren Informationen. Wenn ein Fehler beim Erfassen des Benutzerstatus auftritt, melden Sie sich von Windows ab. Das erneute Anmelden behebt ggf. das Problem.

Um diese MSIX-App zu nutzen, müssen Sie sie zunächst digital signieren, damit Clients ihr vertrauen. Weitere Informationen zu diesem Prozess finden Sie in den folgenden Artikeln:

- [MSIX – MSIX-Paketerstellungstool – Signieren des MSIX-Pakets](https://blogs.msdn.microsoft.com/sgern/2018/09/06/msix-the-msix-packaging-tool-signing-the-msix-package/)
- [Signieren eines App-Pakets mit SignTool](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

Nachdem Sie die App signiert haben, erstellen Sie in Configuration Manager einen neuen Bereitstellungstyp für die Anwendung. Weitere Informationen finden Sie unter [Bereitstellungstypen für die Anwendung erstellen](../deploy-use/create-applications.md#bkmk_create-dt) in diesem Thema.

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a> Tasksequenz-Bereitstellungstyp

<!--3555953-->

> [!Note]  
> In dieser Version von Configuration Manager ist der Tasksequenz-Bereitstellungstyp als Vorabfeature enthalten. Wie Sie es aktivieren, erfahren Sie unter [Pre-release features (Features von Vorabreleases)](../../core/servers/manage/pre-release-features.md).  

Ab Version 2002 können Sie komplexe Anwendungen mithilfe von Tasksequenzen über das Anwendungsmodell installieren. Fügen Sie einer App einen Tasksequenz-Bereitstellungstyp hinzu, um die App entweder zu installieren oder zu deinstallieren. Dieser Bereitstellungstyp ermöglicht Folgendes:

<!-- - Deploy an app task sequence to a user collection -->

- Anzeigen der App-Tasksequenz mit einem Symbol im Softwarecenter. Anhand eines Symbols können Benutzer die App-Tasksequenz leichter finden und bestimmen.

- Definieren zusätzlicher Metadaten für die App-Tasksequenz, einschließlich lokalisierter Informationen.

Als Bereitstellungstyp für eine App können Sie nur eine Tasksequenz hinzufügen, die nicht der Bereitstellung des Betriebssystems dient. Tasksequenzen mit hoher Auswirkung, Betriebssystembereitstellung oder -upgrade werden nicht unterstützt. Eine benutzerorientierte Bereitstellung wird weiterhin im Benutzerkontext des lokalen Kontos „System“ ausgeführt.

Wenn Sie diesen Bereitstellungstyp zu einer App hinzufügen, konfigurieren Sie die zugehörigen Eigenschaften auf der Seite **Tasksequenz**. Weitere Informationen finden Sie unter [Optionen der **Bereitstellungstyp-** Tasksequenz](../deploy-use/create-applications.md#bkmk_dt-ts).

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>Voraussetzungen für einen Tasksequenz-Bereitstellungstyp

Erstellen einer benutzerdefinierten Tasksequenz:

- Wählen Sie nicht auf die Bereitstellung des Betriebssystems bezogene Schritte wie z.B.: **Installieren des Pakets**, **Ausführen der Befehlszeile** oder **Ausführen des PowerShell-Skripts**. Weitere Informationen einschließlich der vollständigen Liste der unterstützten Schritte finden Sie unter [Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md).

- Aktivieren Sie in „Tasksequenzeigenschaften“ auf der Registerkarte **Benutzerbenachrichtigung** nicht die Option für eine Tasksequenz mit hohen Auswirkungen.

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

Wenn Sie die Anwendung erstellen, um einen Tasksequenz-Bereitstellungstyp hinzuzufügen, benötigt das Benutzerkonto die Berechtigung zum Lesen von Tasksequenzen.<!-- 6348976 --> Verwenden Sie eine der folgenden Optionen zum Konfigurieren der Berechtigungen:

- Fügen Sie das Benutzerkonto des App-Administrators der integrierten Rolle **Analyst mit Leseberechtigung** hinzu. Diese Rolle ermöglicht es ihnen, alle Configuration Manager-Objekte anzuzeigen.

- Kopieren Sie die integrierte Rolle **Anwendungsadministrator**, um eine benutzerdefinierte Rolle zu erstellen. Fügen Sie die Berechtigung **Lesen** für das Objekt **Tasksequenzpaket** hinzu.

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>Bekannte Probleme beim Tasksequenz-Bereitstellungstyp

- Sie können keine App-Tasksequenz für eine Benutzersammlung bereitstellen.

- Verwenden Sie den Schritt **Anwendung installieren** in dieser Tasksequenz nicht. Verwenden Sie den Schritt [Paket installieren](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage), um Apps zu installieren.

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a> Unterstützung für UWP-Apps (Universelle Windows-Plattform)  

Windows 10-Geräte erfordern keinen Querladeschlüssel für die Installation branchenspezifischer Apps. Wenn Sie das Querladen unter Windows jedoch aktivieren möchten, muss für den Registrierungsschlüssel `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` der Wert **1** festgelegt werden.  

Wenn Sie diesen Registrierungsschlüssel nicht konfigurieren, legt Configuration Manager diesen Wert automatisch auf **1** fest, wenn Sie zum ersten Mal eine App auf dem Gerät bereitstellen. Wenn Sie diesen Wert auf **0**festgelegt haben, kann Configuration Manager den Wert nicht automatisch ändern, und die Bereitstellung der branchenspezifischen App schlägt fehl.  

Sie können branchenspezifische UWP-Apps digital signieren. Dabei sollten Sie ein Codesignaturzertifikat verwenden, das auf jedem Gerät, auf dem die App bereitgestellt wird, als vertrauenswürdig eingestuft wird. Sie können entweder Zertifikate Ihrer Organisations-PKI nutzen oder ein Zertifikat eines Drittanbieters erwerben, dessen öffentliches Stammzertifikat von Windows bereits als vertrauenswürdig eingestuft wurde.  

Bei der Signierung von App-Paketen für mobile Apps können Sie auf die folgende Tabelle zurückgreifen, um den Typ des zu verwendenden Codesignaturzertifikats zu ermitteln:

| Paket  | Symantec  | Nicht-Symantec  |
|---------|---------|---------|
| Universelle **.appx**-Pakete auf mobilen Windows 10-Geräten | Ja | Ja |
| **.xap**-Pakete | Ja | Nein |
| **.appx**-Pakete für Windows Phone 8.1 zur Installation auf mobilen Windows 10-Geräten | Ja | Nein |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a> Bereitstellen von Windows Installer-Apps auf MDM-registrierten Windows 10-Geräten  

Mit dem Bereitstellungstyp **Windows Installer über MDM (\*.msi)** können Sie Windows Installer-basierte Apps auf MDM-registrierten Geräten unter Windows 10 erstellen und bereitstellen.  

Wenn Sie diesen Bereitstellungstyp verwenden, sollten Sie die folgenden Punkte berücksichtigen:

- Sie sollten nur eine einzelne Datei mit der MSI-Erweiterung hochladen.  

- Configuration Manager verwendet zur App-Erkennung den Produktcode und die Produktversion der Datei.  

- Windows orientiert sich am Standardneustartverhalten der App. Configuration Manager steuert nicht das Neustartverhalten der App.  

- Benutzerspezifische MSI-Pakete werden für einen einzelnen Benutzer installiert.  

- Computerspezifische MSI-Pakete werden für alle Benutzer des Geräts installiert.  

- Configuration Manager unterstützt App-Updates. Die MSI-Produktcodes aller Versionen müssen identisch sein.  
