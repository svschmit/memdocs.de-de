---
title: Installieren von Rollen für die lokale Verwaltung mobiler Geräte
titleSuffix: Configuration Manager
description: Installieren Sie die erforderlichen Standortsystem Rollen für die lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724704"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Installieren von Standortsystem Rollen für die lokale Verwaltung mobiler Geräte (MDM) in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) erfordert die folgenden Standortsystem Rollen am Configuration Manager Standort:

- Anmeldungspunkt

- Anmeldungsproxypunkt

- Verteilungspunkt

- Geräte Verwaltungspunkt, bei dem es sich um einen Verwaltungspunkt handelt, den Sie für mobile Geräte zulassen

## <a name="requirements-and-limitations"></a>Anforderungen und Einschränkungen

- Lokale MDM erfordert, dass Sie Standortsystem Rollen für die HTTPS-Kommunikation aktivieren. Weitere Informationen finden Sie unter [Einrichten von Zertifikaten für vertrauenswürdige Verbindungen in der](set-up-certificates-on-premises-mdm.md)lokalen Verwaltung mobiler Geräte (MDM).

- Der Current Branch von Configuration Manager unterstützt nur *Intranetverbindungen* von Geräten zu Verteilungs Punkten und Geräte Verwaltungs Punkten für lokale MDM. Wenn Sie jedoch auch macOS-Computer verwalten, erfordern diese Clients *Internet* Verbindungen mit diesen Rollen. Wenn Sie den Verteilungs Punkt und den Geräte Verwaltungspunkt konfigurieren, verwenden Sie die Option, um **Intranet-und Internetverbindungen zuzulassen**.

- Für Verteilungs Punkte, die Sie für Intranetverbindungen konfigurieren, müssen Sie die Standort Grenzen für diese konfigurieren. Configuration Manager unterstützt nur IPv4-Bereichsgrenzen für lokale MDM. Weitere Informationen finden Sie unter [Definieren von Standortgrenzen und Begrenzungsgruppen](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

- Wenn Sie [Daten Bank Replikate](../../core/servers/deploy/configure/database-replicas-for-management-points.md) mit dem Geräte Verwaltungspunkt verwenden, können neue registrierte Geräte anfänglich keine Verbindung herstellen. Dieser Verbindungsfehler tritt auf, weil das Daten Bank Replikat nicht über die Informationen zum neu registrierten Gerät verfügt, die für eine erfolgreiche Verbindung erforderlich sind. Replikate werden alle fünf Minuten synchronisiert. Geräte können nach der Registrierung, bei der es sich in der Regel um zwei Verbindungsversuche handelt, keine Verbindung herstellen. Dann werden Geräte erfolgreich verbunden.

## <a name="add-roles"></a>Hinzufügen von Rollen

Wenn Sie eine lokale MDM zu einem Standort hinzufügen, auf dem die meisten Geräte mit dem Configuration Manager-Client verwaltet werden, sind möglicherweise bereits einige dieser Rollen auf dem-Standort installiert. Der Verteilungs Punkt ist z. b. eine gängige Rolle, und der Geräte Verwaltungspunkt ist zum Verwalten von macOS-Geräten erforderlich.

Weitere Informationen zum Hinzufügen von Rollen zu Ihrer Site finden Sie unter [Hinzufügen von Standortsystem Rollen](../../core/servers/deploy/configure/install-site-system-roles.md).

## <a name="configure-roles"></a>Rollen konfigurieren

Konfigurieren Sie neue oder vorhandene Rollen für die Verwaltung mobiler Geräte. Führen Sie die folgenden Schritte aus, um den Verteilungs Punkt und den Geräte Verwaltungspunkt so zu konfigurieren, dass er für die lokale MDM ordnungsgemäß funktioniert:

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Server und Standortsystemrollen** aus.

1. Wählen Sie den Standortsystem Server mit dem Verteilungs Punkt oder Geräte Verwaltungspunkt aus, den Sie konfigurieren möchten. Wählen Sie den Server in der Liste aus, und wählen Sie dann im Detailbereich Standortsystem Rollen die Option **Standortsystem** Rolle aus. Wählen Sie im Menüband auf der Registerkarte **Standort Rolle** die Option **Eigenschaften**aus.

    > [!TIP]
    > An einem großen Standort können Sie die Ansicht so festlegen, dass nur Server mit bestimmten Rollen angezeigt werden. Wenn Sie den Knoten **Server und Standort System Rollen** auswählen, wählen Sie im Menüband auf dem Starttag **Server mit Rolle**aus. Wählen Sie dann die gewünschte Rolle aus der Liste der Rollen aus, die zurzeit am Standort verfügbar sind.

    Vergewissern Sie sich auf der Registerkarte **Allgemein** der **Eigenschaften des Standort Systems**, dass der **Name** ein voll qualifizierter Domänen Name (Fully Qualified Domain Name, FQDN) ist. Schließen Sie die Eigenschaften.

1. Wählen Sie in der Konsolen Liste einen Server mit einer lokalen Verteilungs Punkt Rolle aus. Wählen Sie im Detailbereich Standort System Rollen die Rolle **Verteilungs Punkt** aus. Wählen Sie im Menüband auf der Registerkarte **Standort Rolle** die Option **Eigenschaften**aus. In den **Eigenschaften des Verteilungs Punkts**auf der Registerkarte **Kommunikation** :

    1. Wählen Sie **https**aus, und wählen Sie **nur Intranetverbindungen zulassen**aus.

        > [!IMPORTANT]
        > Wenn Sie auch macOS-Computer mit dem Configuration Manager-Client verwalten, verwenden Sie stattdessen **Intranet-und Internetverbindungen zulassen** .

    1. Aktivieren Sie die Option zum **Herstellen einer Verbindung zwischen mobilen Geräten und diesem Verteilungs Punkt**, und schließen Sie dann die Eigenschaften.

1. Öffnen Sie die Eigenschaften für die Standortsystem Rolle " **Verwaltungspunkt** ".

    1. Wählen Sie auf der Registerkarte **Allgemein** die Option **https**aus, und wählen Sie **nur Intranetverbindungen zulassen**aus.

        > [!IMPORTANT]
        > Wenn Sie auch macOS-Computer mit dem Configuration Manager-Client verwalten, verwenden Sie stattdessen **Intranet-und Internetverbindungen zulassen** .

    1. Aktivieren Sie die Option zum **Zulassen der Verwendung dieses Verwaltungs Punkts durch mobile Geräte und Macintosh-Computer**, und schließen Sie dann die Eigenschaften.

        > [!NOTE]
        > Diese Option wandelt den Verwaltungspunkt effektiv in einen *Geräte* Verwaltungspunkt um.  

## <a name="next-step"></a>Nächster Schritt

Nachdem Sie die Rollen für die Verwaltung mobiler Geräte hinzugefügt und konfiguriert haben, konfigurieren Sie die Server als vertrauenswürdige Endpunkte. Diese Vertrauensstellung ermöglicht es den Rollen, mit verwalteten Geräten zu kommunizieren und diese zu registrieren.

> [!div class="nextstepaction"]
> [Set up certificates for trusted communications](set-up-certificates-on-premises-mdm.md)
