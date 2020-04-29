---
title: BitLocker-Self-Service-Portal
titleSuffix: Configuration Manager
description: Verwenden des Self-Service-Benutzerportals in Configuration Manager für die BitLocker-Wiederherstellung
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fda719aed4d70cd9783d158e17d546b698497997
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699688"
---
# <a name="bitlocker-self-service-portal"></a>BitLocker-Self-Service-Portal

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

Wenn BitLocker nach der [Installation des BitLocker-Self-Service-Portals](setup-websites.md) das Gerät eines Benutzers sperrt, kann dieser unabhängig auf seine Computer zugreifen. Das Self-Service-Portal erfordert kein Eingreifen der Helpdesk-Mitarbeiter.

[![Screenshot des standardmäßigen BitLocker-Self-Service-Portals](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> Damit er einen Wiederherstellungsschlüssel vom Self-Service-Portal abrufen kann, muss sich ein Benutzer mindestens einmal erfolgreich am Computer angemeldet haben. Diese Anmeldung muss lokal auf dem Gerät erfolgen, nicht in einer Remotesitzung. Andernfalls müssen Sie sich für die Schlüsselwiederherstellung an den Helpdesk wenden. Ein Helpdeskadministrator kann die [Website für Verwaltung und Überwachung](helpdesk-portal.md) verwenden, um den Wiederherstellungsschlüssel anzufordern.

BitLocker kann das Gerät in den folgenden Situationen sperren:

- Der Benutzer vergisst das BitLocker-Kennwort oder die PIN.

- Es gibt eine Änderung an den Betriebssystemdateien, am BIOS oder dem Trusted Platform Module (TPM) des Geräts.

So fordern Sie den BitLocker-Wiederherstellungsschlüssel beim Self-Service-Portal an

1. Wenn BitLocker ein Gerät sperrt, wird beim Start der BitLocker-Wiederherstellungsbildschirm angezeigt. Notieren Sie sich die 32-stellige BitLocker-Wiederherstellungsschlüssel-ID.

1. Wechseln Sie auf einem anderen Computer im Webbrowser zum Self-Service-Portal, z. B. `https://webserver.contoso.com/SelfService`.

1. Lesen Sie den Hinweis und akzeptieren Sie ihn.

1. Geben Sie in das Feld **Wiederherstellungsschlüssel-ID** die ersten acht Ziffern der BitLocker-Wiederherstellungsschlüssel-ID ein. Wenn sie mit mehreren Schlüsseln übereinstimmt, geben Sie alle 32 Ziffern ein.

1. Wählen Sie eine der folgenden Optionen für den **Grund** für diese Anforderung aus:

    - BIOS/TPM geändert
    - Betriebssystemdateien geändert
    - PIN/Passphrase verloren

1. Wählen Sie **Schlüssel abrufen** aus. Das Self-Service-Portal zeigt den 48-stelligen **BitLocker-Wiederherstellungsschlüssel** an.

1. Geben Sie diesen 48-stelligen Code im BitLocker-Wiederherstellungsbildschirm auf Ihrem Computer ein.

> [!NOTE]
> Das BitLocker-Self-Service-Portal kann nach einer gewissen Zeit der Inaktivität ein Timeout verursachen. So kann z. B. nach fünf Minuten eine Timeoutwarnung mit einem 60-Sekunden-Zähler angezeigt werden.
>
> ![Timeoutwarnung des BitLocker-Self-Service-Portals](media/bitlocker-self-service-portal-timeout-warning.png)
>
> Wenn Sie nicht auf den Countdown reagieren, läuft die Sitzung ab.
>
> ![Seite für abgelaufene BitLocker-Self-Service-Portalsitzung](media/bitlocker-self-service-portal-session-expired.png)
