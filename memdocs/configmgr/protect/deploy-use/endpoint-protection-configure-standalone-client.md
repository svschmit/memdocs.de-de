---
title: Konfigurieren von Endpoint Protection auf einem eigenständigen Client
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Endpoint Protection auf einem eigenständigen Client konfigurieren.
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f8d116879b0a85f3276d848b01c69d575b8b69fd
ms.sourcegitcommit: 41b2b50d5870dc127a8848a6657d56112f92515a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87758311"
---
# <a name="configure-endpoint-protection-on-a-standalone-client"></a>Konfigurieren von Endpoint Protection auf einem eigenständigen Client

*Gilt für: Configuration Manager (Current Branch)*

Ihr Unternehmen verfügt möglicherweise über eine Reihe von eigenständigen Clients, die Sie nicht mit Microsoft Endpoint Configuration Manager verwalten oder schützen können. Ohne jeglichen Endpunktschutz sind diese eigenständigen Clients anfällig für potenzielle Schadsoftwareangriffe. Sie können solche eigenständigen Clients mit Endpoint Protection, wie in diesem Thema beschrieben, manuell konfigurieren, um sie zu schützen.

So konfigurieren Sie Endpoint Protection manuell auf einem eigenständigen Client

- [Erstellen einer Richtlinie für Antischadsoftware für den eigenständigen Client](#create-an-antimalware-policy-for-the-standalone-client)
- [Übertragen des Endpoint Protection-Clientinstallationspakets auf den eigenständigen Client](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [Installieren von Endpoint Protection auf dem eigenständigen Client](#install-endpoint-protection-on-the-standalone-client)

## <a name="prerequisites"></a>Voraussetzungen

Im Folgenden sind die Voraussetzungen für die Konfiguration von Endpoint Protection auf einem eigenständigen Client aufgeführt:

- Sie benötigen Zugriff auf das Endpoint Protection-Clientinstallationspaket **scepinstall.exe**. Sie finden dieses Paket im Ordner **C:\Programme\Microsoft Configuration Manager\Client**. 
- Stellen Sie sicher, dass das [Antischadsoftware-Plattformupdate für Endpoint Protection-Clients von Januar 2017](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie) installiert ist. 

## <a name="create-an-antimalware-policy-for-the-standalone-client"></a>Erstellen einer Richtlinie für Antischadsoftware für den eigenständigen Client

In diesem Schritt erstellen Sie eine benutzerdefinierte Richtlinie für Antischadsoftware in der Configuration Manager-Konsole, und übertragen sie dann auf den eigenständigen Client.

Beim Erstellen der Richtlinie für Antischadsoftware müssen Sie die Quelle für das Definitionsupdate so konfigurieren, dass die Richtliniendefinitionen auf dem eigenständigen Client auf dem neuesten Stand gehalten werden. Sie können die Quelle für das Definitionsupdate als [Microsoft Update](endpoint-definitions-microsoft-updates.md) und [Microsoft Malware Protection Center](endpoint-definitions-protection-center.md) konfigurieren, wenn Ihr eigenständiger Client mit dem Internet verbunden ist. Alternativ wählen Sie [Netzwerkfreigabe](endpoint-definitions-network.md) als Definitionsverteilungsquelle aus, und aktualisieren Sie sie regelmäßig mit dem neuesten Definitionsupdatepaket. 

So erstellen Sie eine Richtlinie für Antischadsoftware für den eigenständigen Client

1. Klicken Sie in der **Configuration Manager**-Konsole auf **Assets und Konformität**.
2. Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie dann auf **Richtlinien für Antischadsoftware**.
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Richtlinie für Antischadsoftware erstellen**.
4. In der **Allgemeine** Teil der **Richtlinie für Antischadsoftware erstellen** Dialogfeld Geben Sie einen Namen und eine Beschreibung für die Richtlinie.
5. Konfigurieren Sie im Dialogfeld **Richtlinie für Antischadsoftware erstellen** die Einstellungen, die Sie für diese Richtlinie benötigen, und klicken dann auf **OK**. Eine Liste konfigurierbarer Einstellungen finden Sie unter [Liste von Richtlinieneinstellungen für Antischadsoftware](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings).
    > [!NOTE]
    > Wählen Sie für die Einstellung **Definitionsupdates** die Option **Updates von Microsoft Update** und **Updates, die von Microsoft Malware Protection Center verteilt werden** aus, wenn Ihr eigenständiger Client mit dem Internet verbunden ist.  
    > Alternativ können Sie **Updates von UNC-Dateifreigaben** auswählen, um die Richtliniendefinitionen über die Netzwerkfreigabe zu verteilen. Fügen Sie dann mindestens einen UNC-Pfad zum Speicherort der Definitionsupdatedateien auf einer Netzwerkfreigabe hinzu.

6. Exportieren Sie die neu erstellte Richtlinie als XML:
    1. Klicken Sie in der Liste **Richtlinien für Antischadsoftware** mit der rechten Maustaste auf Ihre Richtlinie.
    1. Wählen Sie **Exportieren** aus.
    1. Speichern Sie die Richtlinie als XML-Datei, z. B. **standalone.xml**.
7. Übertragen Sie die neue XML-Datei der Richtlinie für Antischadsoftware auf den eigenständigen Zielclient, auf dem Sie Endpoint Protection konfigurieren möchten.

## <a name="transfer-endpoint-protection-client-installation-package-to-the-standalone-client"></a>Übertragen des Endpoint Protection-Clientinstallationspakets auf den eigenständigen Client

In diesem Schritt kopieren Sie das Installationspaket des Endpoint Protection-Clients (**scepinstall.exe**) vom Configuration Manager-Server und übertragen es auf den eigenständigen Client.

1. Melden Sie sich am Configuration Manager-Server an.
2. Navigieren Sie zum Ordner **Client** des Configuration Manager-Installationsordners (**C:\Programme\Microsoft Configuration Manager\Client**).
3. Kopieren Sie **scepinstall.exe**.
4. Übertragen Sie **scepinstall.exe** auf den eigenständigen Zielclient, auf dem Sie die Endpoint Protection-Clientsoftware installieren möchten.

## <a name="install-endpoint-protection-on-the-standalone-client"></a>Installieren von Endpoint Protection auf dem eigenständigen Client
In diesem Schritt führen Sie das Installationspaket (**scepinstall.exe**) und die Richtlinie für Antischadsoftware (beide zuvor vom Configuration Manager-Server übertragen) von der Eingabeaufforderung auf dem eigenständigen Client aus.

So installieren Sie Endpoint Protection auf dem eigenständigen Client

1. Öffnen Sie auf dem eigenständigen Client eine Eingabeaufforderung als Administrator.
2. Wechseln Sie in das Verzeichnis, in dem Sie die Installationsdatei **scepinstall.exe** gespeichert haben.
3. Geben Sie den folgenden Befehl ein, um **scepinstall.exe** mit der Richtlinie für Antischadsoftware auszuführen:

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    Ersetzen Sie `full path` durch den Pfad, in dem Sie die XML-Datei der Richtlinie für Antischadsoftware gespeichert haben, und `policy file` durch den Dateinamen der Richtlinie für Antischadsoftware.
 
    Das Installationsprogramm wird extrahiert und der Installations-Assistent gestartet.

4. Befolgen Sie die Bildschirmanweisungen, um die Clientinstallation abzuschließen.

    Auf dem letzten Bildschirm des Installations-Assistenten ist die Option, den Computer nach Erhalt der neuesten Updates auf potenzielle Bedrohungen zu überprüfen, standardmäßig ausgewählt. Sie können das Kontrollkästchen deaktivieren, um die Überprüfung zu überspringen.

## <a name="change-antimalware-policy-settings-on-a-standalone-endpoint-protection-client"></a>Ändern von Richtlinieneinstellungen für Antischadsoftware auf einem eigenständigen Endpoint Protection-Client

So ändern oder aktualisieren Sie die Richtlinie für Antischadsoftware auf Ihrem eigenständigen Endpoint Protection Client 

1. [Erstellen einer Richtlinie für Antischadsoftware für den eigenständigen Client](#create-an-antimalware-policy-for-the-standalone-client).
2. Führen Sie den folgenden Befehl auf dem eigenständigen Client aus:

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

Ersetzen Sie `full path` durch den Pfad, in dem Sie die neue XML-Datei der Richtlinie für Antischadsoftware gespeichert haben, und `policy file` durch den Dateinamen der Richtlinie für Antischadsoftware.

## <a name="next-steps"></a>Nächste Schritte

Informationen zur Verwendung von Endpoint Protection zur Verwaltung von Sicherheit und Schadsoftware auf Configuration Manager-Clientcomputern finden Sie unter [Konfigurieren von Endpoint Protection](endpoint-protection-configure.md).