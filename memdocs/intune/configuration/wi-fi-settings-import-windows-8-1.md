---
title: 'Importieren von WLAN-Einstellungen für Windows-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Exportieren Sie WLAN-Einstellungen als XML-Datei von einem Windows-Gerät mithilfe von „netsh wlan“. Importieren Sie anschließend diese Datei in Intune, um ein WLAN-Profil für Geräte zu erstellen, auf denen Windows 8.1, Windows 10 oder Windows Holographic for Business ausgeführt wird.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d17614424cdb20d2d88d818fcdd015c229150d66
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556335"
---
# <a name="import-wi-fi-settings-for-windows-devices-in-intune"></a>Importieren von WLAN-Einstellungen für Windows-Geräte in Intune

Für Geräte, die Windows ausführen, können Sie ein WLAN-Konfigurationsprofil aus einer zuvor exportierten Datei importieren. **Für Geräte, auf denen Windows 10 und höher ausgeführt wird, können Sie auch direkt in Intune [ein WLAN-Profil erstellen](wi-fi-settings-windows.md)** .

Diese Funktion gilt für:

- Windows 8.1 und höher
- Windows 10 und höher
- Windows 10 Desktop oder Mobile
- Windows Holographic for Business

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Geräteprofil.](wi-fi-settings-configure.md) Der Profilname **muss** mit dem Namensattribut in der WLAN-Profil-XML-Datei identisch sein. Andernfalls tritt ein Fehler auf.

## <a name="import-the-wi-fi-settings-into-intune"></a>Importieren der WLAN-Einstellungen in Intune

- **Verbindungsname:** Geben Sie einen Namen für die WLAN-Verbindung ein. Dieser Name wird Benutzern beim Suchen nach verfügbaren WLAN-Netzwerken angezeigt.
- **Profil-XML**: Wählen Sie die Schaltfläche „Durchsuchen“ und die XML-Datei mit den WLAN-Profileinstellungen aus, die Sie importieren möchten.
- **Dateiinhalte**: Zeigt den XML-Code des ausgewählten Konfigurationsprofils an.

## <a name="export-wi-fi-settings-from-a-windows-device"></a>Exportieren von WLAN-Einstellungen von einem Windows-Gerät

Verwenden Sie unter Windows `netsh wlan`, um ein vorhandenes WLAN-Profil in eine XML-Datei zu exportieren, die von Intune gelesen werden kann. Der Schlüssel muss in Nur-Text exportiert werden, damit das Profil erfolgreich verwendet werden kann.

Führen Sie auf einem Windows-Computer, auf dem das erforderliche WLAN-Profil bereits installiert ist, die folgenden Schritte aus:

1. Erstellen Sie einen lokalen Ordner für die exportierten WLAN-Profile, z. B. **C:\WiFi**.
2. Öffnen Sie eine Eingabeaufforderung als Administrator.
3. Führen Sie den Befehl `netsh wlan show profiles` aus. Notieren Sie sich den Namen des Profils, das Sie exportieren möchten. In diesem Beispiel lautet der Profilname **WiFiName**.
4. Führen Sie den Befehl `netsh wlan export profile name="ProfileName" folder=c:\Wifi` aus. Dieser Befehl erstellt eine WLAN-Profildatei mit dem Namen **Wi-Fi-WiFiName.xml** im Zielordner.

> [!IMPORTANT]
>
> - Wenn Sie ein WLAN-Profil mit einem vorinstallierten Schlüssel exportieren, **müssen** Sie `key=clear` zum Befehl hinzufügen. Geben Sie z. B. Folgendes ein:
>
>   `netsh wlan export profile name="ProfileName" key=clear folder=c:\Wifi`
>
> - Die Verwendung eines vorinstallierten Schlüssels mit Windows 10 verursacht einen Wartungsfehler in Intune. In diesem Fall wird das WLAN-Profil ordnungsgemäß dem Gerät zugewiesen, und das Profil funktioniert wie erwartet.
> - Vergewissern Sie sich, dass die Datei geschützt ist, wenn Sie ein WLAN-Profil exportieren, das einen vorinstallierten Schlüssel enthält. Der Schlüssel wird in Nur-Text angegeben. Daher sind Sie für die Sicherheit des Schlüssels verantwortlich.

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie dessen Status](device-profile-monitor.md).

Weitere Informationen, auch zu anderen Plattformen, finden Sie in der [Übersicht über WLAN-Einstellungen](wi-fi-settings-configure.md).
