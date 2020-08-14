---
title: BitLocker-Ereignisprotokolle
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie mit BitLocker-Informationen im Windows-Ereignisprotokoll Probleme behandeln.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: troubleshooting
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ef1d5f9a7e8f3c009d1993b82ddef22ce22e235d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128000"
---
# <a name="bitlocker-event-logs"></a>BitLocker-Ereignisprotokolle

*Gilt für: Configuration Manager (Current Branch)*

Der BitLocker-Verwaltungs-Agent und die Webdienste verwenden Windows-Ereignisprotokolle zum Aufzeichnen von Nachrichten. Navigieren Sie in der Ereignisanzeige zu **Anwendungs- und Dienstprotokolle**, **Microsoft**, **Windows**. Der Protokollkanal (Knoten) variiert je nach Computer und Komponente:

- **MBAM**: BitLocker-Verwaltungs-Agent auf einem Clientcomputer
- **MBAM-Web**:
  - Wiederherstellungsdienst auf dem Verwaltungspunkt
  - Self-Service-Portal
  - Administration and Monitoring-Website

Weitere Informationen zu bestimmten Meldungen in diesen Protokollen finden Sie in den folgenden Artikeln:

- [Clientereignisprotokolle](client-event-logs.md)
- [Serverereignisprotokolle](server-event-logs.md)

In jedem Knoten werden standardmäßig zwei Protokollkanäle angezeigt: **Admin** und **Betriebsbereit** Ausführlichere Informationen zur Problembehandlung erhalten Sie auch durch Anzeigen von [Analyse- und Debugprotokollen](#bkmk_debug).

## <a name="log-properties"></a>Protokolleigenschaften

Wählen Sie in der Windows-Ereignisanzeige ein bestimmtes Protokoll aus. Beispiel: **Admin**. Wechseln Sie zum Menü **Aktion**, und wählen Sie **Eigenschaften** aus. Konfigurieren Sie die folgenden Einstellungen:

- **Maximale Protokollgröße (KB)** : Standardmäßig ist diese Einstellung `1028` (1 MB) für alle Protokolle.
- **Wenn die maximale Ereignisprotokollgröße erreicht ist**: Standardmäßig sind die Protokolle **Admin** und **Betriebsbereit** auf **Ereignisse nach Bedarf überschreiben (älteste Ereignisse zuerst)** festgelegt.

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a> Anzeigen von Analyse- und Debugprotokollen

Sie können detailliertere Protokolle zu Zwecken der Problembehandlung aktivieren. Wechseln Sie in der Ereignisanzeige zum Menü **Ansicht**, und wählen Sie **Analyse- und Debugprotokolle anzeigen** aus. Wenn Sie nun zum Protokollkanal navigieren, sehen Sie zwei weitere Protokolle: **Analyse** und **Debuggen**.

> [!TIP]
> Standardmäßig verfügen diese Protokolle über die folgenden Eigenschaften:
>
> - **Maximale Protokollgröße (KB)** : `1028` (1 MB)
> - **Ereignisse nie überschreiben (Protokoll manuell löschen)**

## <a name="export-logs-to-text"></a>Exportieren von Protokollen als Text

Insbesondere mit den [Analyse- und Debugprotokollen](#bkmk_debug) ist es vielleicht einfacher, die Protokolleinträge in einer einzelnen Textdatei zu überprüfen. Verwenden Sie die folgenden PowerShell-Befehle, um die Ereignisprotokolleinträge in Textdateien zu exportieren:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
