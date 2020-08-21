---
title: Aktualisieren von Windows-Geräten auf eine neuere Version
titleSuffix: Configuration Manager
description: Verwenden Sie Configuration Manager, um Windows 10-Geräte automatisch auf eine andere Windows-Edition zu aktualisieren.
ms.date: 07/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 920f3c9aabcdec1242a6f5e5fc8e6b65c5cc0b53
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694609"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>Ausführen von Upgrades auf eine neue Edition für Windows-Geräte mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die **Upgraderichtlinie** für die Edition ermöglicht Ihnen ein automatisches Upgrade von Windows 10-Geräten auf eine andere Version.

Die folgenden Upgradepfade werden unterstützt:

- Von Windows 10 Pro auf Windows 10 Enterprise
- Von Windows 10 Home auf Windows 10 Education
- Von Windows 10 Mobile auf Windows 10 Mobile Enterprise

Auf den Geräten muss die Configuration Manager-Clientsoftware ausgeführt werden. Über die [lokale MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) verwaltete Geräte werden nicht unterstützt.

## <a name="before-you-start"></a>Vorbereitung

Bevor Sie beginnen, Geräte auf die neueste Version zu aktualisieren, benötigen Sie Folgendes:  

- Für Desktopeditionen von Windows 10: einen gültigen Product Key für die neue Windows-Version auf allen Geräten, die das Ziel dieser Richtlinie sind. Dieser Product Key kann ein Mehrfachaktivierungsschüssel oder ein generischer Volumenlizenzschlüssel sein. Ein generischer Volumenlizenzschlüssel wird auch als Clientsetupschlüssel für den Schlüsselverwaltungsdienst (KMS) bezeichnet. Weitere Informationen finden Sie unter [Planen der Volumenaktivierung](/windows/deployment/volume-activation/plan-for-volume-activation-client). Eine Liste der KMS-Clientsetupschlüssel finden Sie im Windows Server-Aktivierungshandbuch in [Anhang A](/windows-server/get-started/kmsclientkeys). <!--496871-->  

- Für Windows 10 Mobile: eine XML-Lizenzdatei aus dem Microsoft Business Center. Diese Datei enthält die Lizenzierungsinformationen für die neue Windows-Version auf allen Geräten, die Ziel dieser Richtlinie sind. Laden Sie die ISO-Datei für **Windows 10 Mobile Enterprise** einschließlich der Lizenzierungs-XML herunter.<!-- SCCMDocs#2033 -->

- Zum Verwalten dieses Richtlinientyps muss Ihnen die Configuration Manager-Sicherheitsrolle **Hauptadministrator** zugewiesen sein.

## <a name="configure-the-policy"></a>Konfigurieren der Richtlinie  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, erweitern Sie **Konformitätseinstellungen**, und wählen Sie den Knoten **Windows 10-Editionsupgrade** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Editionsupgraderichtlinie erstellen** aus.  

3. Wählen Sie **Richtlinie erstellen**.  

4. Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Editionsaktualisierungsrichtlinien**die folgenden Informationen an:  

    - **Name**: Geben Sie einen Namen für die Editionsupgraderichtlinie ein.  

    - **Beschreibung** (optional): Sie können eine Beschreibung für die Richtlinie eingeben, anhand derer Sie sie in der Configuration Manager-Konsole erkennen können.  

    - **SKU, auf die das Gerät aktualisiert werden soll**: Wählen Sie aus der Dropdownliste die Zieleditionen von Windows 10 Desktop oder Windows 10 Mobile aus.  

    - **Lizenzinformationen**: Sie können eine der folgenden Optionen auswählen:  

        - **Product Key**: Geben Sie einen gültigen Product Key für die Zieledition von Windows 10 Desktop ein.  

            > [!NOTE]  
            > Nach der Erstellung einer Richtlinie mit einem Product Key können Sie den Product Key später nicht mehr bearbeiten. Configuration Manager zeigt den Schlüssel aus Sicherheitsgründen verdeckt an. Geben Sie den gesamten Schlüssel noch mal ein, um den Product Key zu ändern.  

        - **Lizenzdatei**: Wählen Sie **Durchsuchen** aus, um eine gültige Lizenzdatei im XML-Format auszuwählen. Configuration Manager verwendet diese Lizenzdatei, um Windows 10 Mobile-Geräte zu aktualisieren.  

5. Schließen Sie den Assistenten ab.  

## <a name="deploy-the-policy"></a>Bereitstellen der Richtlinie  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, erweitern Sie **Konformitätseinstellungen**, und wählen Sie den Knoten **Windows 10-Editionsupgrade** aus.  

2. Wählen Sie die Windows 10-Richtlinie für Editionsupgrade aus, die Sie bereitstellen möchten. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Bereitstellung** die Option **Bereitstellen** aus.  

3. Wählen Sie die Gerätesammlung aus, für die Sie die Richtlinie bereitstellen möchten.

4. Wählen Sie den Zeitplan aus, nach dem der Client die Richtlinie bewertet.

5. Schließen Sie den Assistenten ab.

## <a name="next-steps"></a>Nächste Schritte

Überwachen Sie diese Bereitstellung über den Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung**. Möglicherweise werden Fehler angezeigt, die auf eine erfolglose Bereitstellung hinweisen, zum Beispiel:

- **Für dieses Gerät nicht anwendbar**
- **Fehler bei der Konvertierung des Datentyps**

Diese Fehler bedeuten nicht, dass die Bereitstellung gescheitert ist. Vergewissern Sie sich am Zielgerät, dass das Upgrade erfolgreich ausgeführt wurde.

Sobald der Client die gewünschte Richtlinie ausgewertet hat, wird das Upgrade innerhalb von zwei Stunden angewendet. [Einige Versionen von Windows](/windows/deployment/upgrade/windows-10-edition-upgrades) müssen zu diesem Zeitpunkt möglicherweise neu gestartet werden. Stellen Sie sicher, dass Sie jeden Benutzer informieren, dem Sie die Richtlinie bereitstellen, oder planen Sie die Ausführung der Richtlinie außerhalb der Arbeitsstunden der Benutzer.

Wenn der folgende Fehler in der Datei **DcmWmiProvider.log** auf dem Client auftritt, überprüfen Sie, ob Sie den richtigen Schlüssel für Ihr Aktivierungsszenario verwenden. Weitere Informationen finden Sie im Abschnitt [Bevor Sie beginnen](#before-you-start). Wenn Sie einen Schlüsselverwaltungsdienst (Key Management Service, KMS) für die Aktivierung nutzen, stellen Sie sicher, dass Sie einen [KMS-Clientsetupschlüssel](/windows-server/get-started/kmsclientkeys) verwenden.  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>Weitere Informationen:

- [Planen der Volumenaktivierung](/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Windows 10-Editionsupgrade](/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Upgraden von Windows 10-Editionen oder Verlassen des S-Modus auf Geräten mit Microsoft Intune](/intune/edition-upgrade-configure-windows-10)