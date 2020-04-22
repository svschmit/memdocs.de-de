---
title: Gemeinsames Verwalten von internetbasierten Geräten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie sie internetbasierte Windows 10-Geräte für die Co-Verwaltung vorbereiten.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 32c148b695a47241c6646a2a7309f0a27f3b3070
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691048"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Vorbereiten von internetbasierten Geräten für die Co-Verwaltung

Dieser Artikel konzentriert sich auf den zweiten Pfad zur Co-Verwaltung für neue internetbasierte Geräte. In diesem Szenario verfügen Sie über neue Windows 10-Geräte, die in Azure AD eingebunden werden und sich automatisch bei Intune registrieren. Sie installieren den Configuration Manager-Client, um einen Co-Verwaltungsstatus zu erreichen.  

## <a name="windows-autopilot"></a>Windows Autopilot

Für neue Windows 10-Geräte können Sie den Autopilot-Dienst verwenden, um die Windows-Willkommensseite (OOBE) zu konfigurieren. Dieser Prozess umfasst die Einbindung des Geräts in Azure AD und die Registrierung des Geräts in Intune.  

Weitere Informationen finden Sie unter [Übersicht über Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).

Um Ihre Geräte so zu konfigurieren, dass sie automatisch in Intune registriert werden, wenn sie in Azure AD eingebunden werden, lesen Sie  [Registrieren von Windows-Geräten für Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

### <a name="gather-information-from-configuration-manager"></a>Erfassen von Informationen aus Configuration Manager

Sie können mit Configuration Manager die von Intune geforderten Geräteinformationen erfassen und melden. Zu diesen Informationen gehört die Seriennummer des Geräts, der Windows-Produktbezeichner und eine Hardwarebezeichner. Diese Angaben werden verwendet, um das Gerät in Intune zur Unterstützung von Windows Autopilot zu registrieren.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, erweitern Sie die Knoten **Berichterstellung** und **Berichte**, und wählen Sie dann den Knoten **Hardware – allgemein** aus.  

2. Führen Sie den Bericht **Windows Autopilot-Geräteinformationen** aus, und zeigen Sie die Ergebnisse an.  

3. Klicken Sie in der Berichtsanzeige auf das Symbol **Exportieren**, und wählen Sie die Option **CSV (Komma-getrennt)** aus.  

4. Laden Sie nach dem Speichern der Datei die Daten in Intune hoch.  

Weitere Informationen finden Sie unter [Hinzufügen von Geräten in Intune](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices).

### <a name="autopilot-for-existing-devices"></a>Autopilot für vorhandene Geräte
<!--1358333-->

[Windows Autopilot für vorhandene Geräte](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) ist in Windows 10, Version 1809 oder höher, verfügbar. Mit dieser Funktion können Sie ein Reimaging für ein Windows 7-Gerät für den [benutzergesteuerten Windows Autopilot-Modus](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) mit einer einzigen, nativen Configuration Manager-Tasksequenz durchführen und das Gerät bereitstellen.

Weitere Informationen finden Sie unter [Windows Autopilot für vorhandene Geräte: Tasksequenz](../osd/deploy-use/windows-autopilot-for-existing-devices.md).

## <a name="install-the-configuration-manager-client"></a>Installieren des Configuration Manager-Clients

Für internetbasierte Geräte im zweiten Pfad müssen Sie eine App in Intune erstellen. Stellen Sie diese App für Windows 10-Geräte bereit, die noch keine Configuration Manager-Clients sind.

> [!NOTE]
> Bevor Sie diese App Geräten in Intune zuweisen, müssen Sie sicherstellen, dass die Geräte dem CMG-Server-Authentifizierungszertifikat vertrauen. Weitere Informationen finden Sie im Abschnitt [Vertrauenswürdige CMG-Stammzertifikate für Clients](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot). Wenn ein Gerät dem CMG-Serverauthentifizierungszertifikat nicht vertraut, wird der Fehler WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA in der Datei „ccmsetup.log“ auf dem Client angezeigt.

### <a name="get-the-command-line-from-configuration-manager"></a>Abrufen der Befehlszeile aus Configuration Manager

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Co-Verwaltung** aus.  

2. Wählen Sie das Co-Verwaltungsobjekt und anschließend auf dem Menüband **Eigenschaften** aus.  

3. Kopieren Sie die Befehlszeile auf der Registerkarte **Aktivierung**. Fügen Sie sie in Editor ein, um sie für den nächsten Prozess zu speichern.  

Die folgende Befehlszeile ist ein Beispiel: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215-->
Bestimmen Sie, welche Befehlszeileneigenschaften für Ihre Umgebung erforderlich sind:  

- Die folgenden Befehlszeileneigenschaften sind in allen Szenarios erforderlich:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- Die folgenden Eigenschaften sind erforderlich, wenn Sie anstelle von PKI-basierten Clientauthentifizierungszertifikaten Azure AD für die Clientauthentifizierung verwenden:  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- Die folgende Eigenschaft ist erforderlich, wenn der Client zurück in das Intranet wechselt:  
  - SMSMP  

- Wenn Sie Ihr eigenes PKI-Zertifikat verwenden und Ihre CRL im Internet nicht veröffentlicht wird, ist der folgende Parameter erforderlich:  
  - /noCRLCheck  

    Weitere Informationen finden Sie unter [Planen von CRLs](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- Ab Version 2002 können Sie mithilfe der folgenden Eigenschaft Bootstrap für eine Tasksequenz direkt nach der Clientregistrierung ausführen:
  - PROVISIONTS

    Weitere Informationen finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation in Configuration Manager – PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

Auf der Website werden zusätzliche Azure AD-Informationen für Cloud Management Gateway (CMG) veröffentlicht. Ein in Azure AD eingebundener Client ruft diese Informationen beim ccmsetup-Prozess von Cloud Management Gateway ab und verwendet dabei den gleichen Mandanten, mit dem er verknüpft ist. Dieses Verhalten vereinfacht das Registrieren von Geräten zur gemeinsamen Verwaltung in einer Umgebung mit mehreren Azure AD-Mandanten. Die einzigen beiden erforderlichen ccmsetup-Eigenschaften sind **CCMHOSTNAME** und **SMSSiteCode**.<!--3607731-->

> [!NOTE]
> Wenn Sie den Configuration Manager-Client bereits von Intune aus bereitstellen, aktualisieren Sie die Intune-App mit einer neuen Befehlszeile und einer neuen MSI-Komponente. <!-- SCCMDocs-pr issue 3084 -->

Das folgende Beispiel enthält alle diese Eigenschaften:

`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001`

Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](../core/clients/deploy/about-client-installation-properties.md).

### <a name="create-the-app-in-intune"></a>Erstellen der App in Intune

1. Navigieren Sie zum [Azure-Portal](https://portal.azure.com), und öffnen Sie dann die Seite „Intune“.  

2. Klicken Sie auf **Client-Apps** > **Apps** > **Hinzufügen**.  

3. Wählen Sie unter **Weitere** die Option **Branchenspezifische App** aus.  

4. Laden Sie die App-Paketdatei **ccmsetup.msi** hoch. Sie finden diese Datei im folgenden Ordner auf dem Configuration Manager-Standortserver: `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > Wenn Sie den Standort aktualisieren, stellen Sie auch sicher, dass Sie diese App in Intune aktualisieren.  

5. Nachdem die App aktualisiert wurde, konfigurieren Sie die App-Informationen über die Befehlszeile, die Sie aus Configuration Manager kopiert haben.  

> [!IMPORTANT]
> Wenn Sie diese Befehlszeile anpassen, stellen Sie sicher, dass sie nicht mehr als 1.024 Zeichen lang ist. Wenn die Befehlszeile länger als 1.024 Zeichen ist, schlägt die Clientinstallation fehl.
