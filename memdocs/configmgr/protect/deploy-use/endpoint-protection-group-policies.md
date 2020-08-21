---
title: Verwalten von Endpoint Protection mithilfe von Gruppenrichtlinien
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Endpoint Protection mithilfe von Gruppenrichtlinien verwalten.
ms.date: 08/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d028dc6149ae1fee2d61634b96ccf450fc8f4b24
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700598"
---
# <a name="use-group-policy-settings-to-manage-endpoint-protection-in-previous-versions-of-windows"></a>Verwenden Sie Gruppenrichtlinieneinstellungen, um Endpoint Protection in früheren Windows-Versionen zu verwalten.

**Gilt für:**

- [Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2O8jv)
- System Center Endpoint Protection auf folgenden älteren Geräten:
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

Möglicherweise verfügen Sie über eine Reihe von älteren Windows-Geräten, die für Endpoint Protection aktiviert sind, sich aber außerhalb Ihrer Configuration Manager-Hierarchie befinden. Beispielsweise Geräte in einem Umkreisnetzwerk oder Geräte, die durch Fusionen und Übernahmen integriert werden. 

Sie können Endpoint Protection in solchen Geräten mithilfe von Gruppenrichtlinieneinstellungen verwalten, die wie folgt beschrieben werden:

- [Kopieren von Endpoint Protection-Richtliniendefinitionen](#copy-endpoint-protection-policy-definitions)
- Laden Sie Richtliniendefinitionen für Endpoint Protection an einen der folgenden Speicherorte:
    - [Zentraler Speicher auf einem Domänencontroller (empfohlen)](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [Lokales Gerät](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> Informationen zur Verwendung von Gruppenrichtlinieneinstellungen für die Verwaltung von Microsoft Defender Antivirus in Windows 10, Windows Server 2019 und Windows Server 2016 finden Sie unter [Verwenden von Gruppenrichtlinieneinstellungen zum Konfigurieren und Verwalten von Microsoft Defender Antivirus](/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus).

## <a name="copy-endpoint-protection-policy-definitions"></a>Kopieren von Endpoint Protection-Richtliniendefinitionen

Kopieren Sie auf einem Gerät mit einer älteren Windows-Version, das von Endpoint Protection verwaltet wird, die Endpoint Protection-Richtliniendefinitionsdateien.

1. Wechseln Sie zu **C:\Programme\Microsoft Security Client\Admx**. 

2. Komprimieren Sie die folgenden Dateien in eine ZIP-Datei, z. B. **SCEP_admx.zip**:
    - **EndPointProtection.adml**
    - **EndPointProtection.admx**
3. Kopieren Sie die ZIP-Datei in einen temporären Ordner. Beispiel: **C:\temp_SCEP_GPO_admx**.
4. Entpacken Sie die Datei. 

> [!NOTE]
> Die Registrierungsschlüssel zum Konfigurieren der Richtlinieneinstellungen für Endpoint Protection befinden sich in **Hkey_Local_Machine\Software\Policies\Microsoft\Microsoft Antimalware**.

## <a name="load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller"></a>Laden von Endpoint Protection-Gruppenrichtlinieneinstellungen in einen zentralen Speicher auf einem Domänencontroller

Wenn Sie einen [zentralen Speicher für administrative Vorlagen für Gruppenrichtlinien](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra) verwenden, führen Sie die folgenden Schritte aus, um Richtlinieneinstellungen für die Endpoint Protection-Gruppe zu laden und zu konfigurieren. Dies ist die empfohlene Methode.

1. Wechseln Sie zu dem Ordner, in dem Sie die Definitionsdateien der Endpoint Protection-Richtlinie extrahiert haben.
2. Kopieren Sie die ADMX- und ADML-Dateien in den Ordner **PolicyDefinitions** auf dem Domänencontroller:
    1. Kopieren Sie **EndPointProtection.admx** nach **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions**. 
    2. Kopieren Sie **EndPointProtection.adml** nach **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions\\de-DE**.  

    Beispiel:
    
    - Kopieren Sie **EndPointProtection.admx** nach **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions**.
    - Kopieren Sie **EndPointProtection.adml** nach **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions\de-DE**.
    
    Dabei steht **DC** für den Namen Ihres Domänencontrollers und **contoso.com** für Ihre Domäne.

3. Öffnen Sie die [Gruppenrichtlinien-Verwaltungskonsole](/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11), und erstellen Sie ein neues Gruppenrichtlinienobjekt (GPO) in Ihrer Domäne, z. B. **Endpoint Protection**.
4. Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt für Endpoint Protection, und klicken Sie dann auf **Bearbeiten**.
5. Wechseln Sie im Editor für die Verwaltung von Gruppenrichtlinien zu **Computerkonfiguration** > **Richtlinien** > **Verwaltungsvorlagen: Richtliniendefinitionen** > **Windows-Komponenten** > **Endpoint Protection**.

   Die Liste der Endpoint Protection-Gruppenrichtlinien wird angezeigt.

6. Erweitern Sie den Abschnitt, der die Einstellung enthält, die Sie konfigurieren möchten, doppelklicken Sie auf die Einstellung, um sie zu öffnen, und nehmen Sie Konfigurationsänderungen vor.

## <a name="load-endpoint-protection-group-policy-settings-into-your-local-device"></a>Laden von Richtlinieneinstellungen der Endpoint Protection-Gruppe auf Ihr lokales Gerät

Anstatt den zentralen Speicher zum Laden von Endpoint Protection-Richtliniendefinitionen zu verwenden, können Sie diese lokal auf Ihrem Gerät speichern.

1. Wechseln Sie zu dem Ordner, in dem Sie die Definitionsdateien der Endpoint Protection-Richtlinie extrahiert haben.
2. Kopieren Sie die ADMX- und ADML-Dateien in Ihren lokalen Ordner „PolicyDefinitions“.
    1. Kopieren Sie **EndPointProtection.admx** nach **%SystemRoot%/PolicyDefinitions**. 
    2. Kopieren Sie **EndPointProtection.adml** nach **%SystemRoot%/PolicyDefinitions/de-DE**.
    
    Beispiel:

    - Kopieren Sie **EndPointProtection.admx** nach **C:\Windows\PolicyDefinitions**.
    - Kopieren Sie **EndPointProtection.adml** nach **C:\Windows\PolicyDefinitions\de-DE**.
    
3. Öffnen Sie den lokalen Gruppenrichtlinien-Editor.
4. Wechseln Sie zu **Computerkonfiguration** > **Verwaltungsvorlagen** > **Windows-Komponenten** > **Endpoint Protection**.

    Die Liste der Endpoint Protection-Gruppenrichtlinien wird angezeigt.

5. Erweitern Sie den Abschnitt, der die Einstellung enthält, die Sie konfigurieren möchten, doppelklicken Sie auf die Einstellung, um sie zu öffnen, und nehmen Sie Konfigurationsänderungen vor.

## <a name="next-steps"></a>Nächste Schritte
- Eine Übersicht über Endpoint Protection finden Sie unter [Endpoint Protection](endpoint-protection.md).
- Informationen zur manuellen Konfiguration von Endpoint Protection auf einem eigenständigen Client finden Sie unter [Konfigurieren von Endpoint Protection auf einem eigenständigen Client](endpoint-protection-configure-standalone-client.md).