---
title: Fehlermeldungen
titleSuffix: Configuration Manager
description: Informationen zu Fehlermeldungen im Paketkonvertierungs-Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688968"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Technische Referenz zu Fehlermeldungen im Paketkonvertierungs-Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1357861-->

In diesem Artikel werden die im Paketkonvertierungs-Manager angezeigten Fehlermeldungen beschrieben. Ferner werden die möglichen Ursachen des Fehlers und Methoden zur Behebung beschrieben. Der Paketkonvertierungs-Manager protokolliert Fehlermeldungen in **PCMTrace.log**. Weitere Informationen, z.B. zum Steuern des Ausführlichkeitsgrads, finden Sie unter [Protokolldateien](troubleshoot-pcm.md#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>Fehler bei der Erstellung der Anwendung mit der folgenden Ausnahme

Die angegebene Ausnahme trat während der Übermittlung des Anwendungsobjekts an den Configuration Manager-Server auf.

Überprüfen Sie Ihre Berechtigungen in Configuration Manager sowie die Verbindung, und versuchen Sie es erneut. Wenn das Problem dadurch nicht behoben wird, untersuchen Sie die Dateien **PCMtrace.log** (Ausführlichkeitsgrad 4) und **SMSProv.log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Konvertierungsfehler – GILT FÜR EINEN PAKETTRANSFORMATIONSSTATUS

Eine allgemeine Ausnahme ist während der Konvertierung des Pakets aufgetreten. Untersuchen Sie die Protokolldatei **PCMtrace.log** (Ausführlichkeitsstufe 4).

Überprüfen Sie die Zugriffsberechtigungen für die Netzwerkfreigabe (Paketdatenquelle) sowie die Verbindung, und versuchen Sie es erneut. Wenn das Problem dadurch nicht behoben wird, untersuchen Sie die Datei **PCMtrace.log** (Ausführlichkeitsgrad 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>Es wurde weder ein konvertiertes Paket noch die daraus erstellte Anwendung in den Workflowausgaben gefunden
Die Anwendung (konvertiertes Paket/Programm) wurde gelöscht.

Bearbeiten Sie das abhängige Paket/Programm, um sicherzustellen, dass es vorhanden ist.


#### <a name="objects-were-not-created-successfully"></a>Objekte wurden nicht erfolgreich erstellt.
Mehrere Ursachen sind möglich.

Überprüfen Sie Ihre Berechtigungen in Configuration Manager sowie die Verbindung, und versuchen Sie es erneut. Wenn das Problem dadurch nicht behoben wird, untersuchen Sie die Dateien **PCMtrace.log** (Ausführlichkeitsgrad 4) und **SMSProv.log**.


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Schließen Sie den Assistenten, und beheben Sie alle Probleme mit dem ausgewählten Paket. Weitere Informationen finden Sie in „PCMTrace.Log“.
Mehrere Ursachen sind möglich.

Überprüfen Sie Ihre Berechtigungen in Configuration Manager sowie die Verbindung, und versuchen Sie es erneut. Wenn das Problem dadurch nicht behoben wird, untersuchen Sie die Dateien **PCMtrace.log** (Ausführlichkeitsgrad 4) und **SMSProv.log**.


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>Bei einigen Bereitstellungstypen sind keine Erkennungsmethoden vorhanden. Für alle Bereitstellungstypen müssen Erkennungsmethoden vorhanden sein
Dem Programm fehlen Erkennungsmethoden.

Fügen Sie während des Vorgangs **Korrigieren und konvertieren** mindestens eine Erkennungsmethode hinzu.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Fehler beim Vorbereiten des Pakets für die Konvertierung
Mehrere Ursachen sind möglich.

Überprüfen Sie Ihre Berechtigungen in Configuration Manager sowie die Verbindung, und versuchen Sie es erneut. Wenn das Problem dadurch nicht behoben wird, untersuchen Sie die Dateien **PCMtrace.log** (Ausführlichkeitsgrad 4) und **SMSProv.log**.


