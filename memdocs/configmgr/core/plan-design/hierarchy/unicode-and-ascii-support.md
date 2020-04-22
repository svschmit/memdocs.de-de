---
title: Unicode- und ASCII-Unterstützung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Unterstützung für Unicode- und ASCII-Zeichen in Configuration Manager-Objekten.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bd3dad5f0ef24074ac8c8e6d2edf01d5641b541
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699898"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Unicode- und ASCII-Unterstützung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager erstellt die meisten Objekte mithilfe von Unicode-Zeichen. Allerdings werden von mehreren Objekten nur ASCII-Zeichen unterstützt, oder sie weisen andere Einschränkungen auf.  

## <a name="objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a> Objekte, die ASCII-Zeichen verwenden

Wenn Sie die folgenden Objekte erstellen, unterstützt Configuration Manager nur den ASCII-Zeichensatz:  

- Standortcode  

- Alle Computernamen von Standortsystemservern  

- Folgende Configuration Manager-Konten:  

    > [!NOTE]  
    > Bei diesen Konten werden an Standorten in russischer Sprache sowohl ASCII-Zeichen als auch kyrillische Zeichen (RUS) unterstützt.  

    - Clientpushinstallations-Konto  

    - Verbindungskonto für Verwaltungspunktdatenbank  

    - Netzwerkzugriffskonto  

    - Paketzugriffskonto  

    - Standard-Sendekonto  

    - Standortsystem-Installationskonto  

    - Verbindungskonto des Softwareupdatepunkts  

    - Proxyserverkonto für Softwareupdatepunkt  

    > [!NOTE]  
    > Bei den Konten, die Sie für die rollenbasierte Verwaltung angeben, wird Unicode unterstützt.  
    >
    > Vom Konto des Reporting Services-Punkts wird Unicode mit Ausnahme kyrillischer Zeichen (RUS) unterstützt.  

- Vollständig qualifizierter Domänenname (FQDN) für Standortserver und Standortsysteme  

- Installationspfad für Configuration Manager  

- SQL Server-Instanznamen  

- Pfadnamen der folgenden Standortsystemrollen:  

    - Anmeldungspunkt  

    - Anmeldungsproxypunkt  

    - Reporting Services-Punkt  

    - Zustandsmigrationspunkt  

- Pfadnamen der folgenden Ordner:  

    - Der Ordner, in dem Clientzustandsmigrationsdaten gespeichert werden  

    - Der Ordner mit den Configuration Manager-Berichten  

    - Der Ordner mit der Configuration Manager-Sicherung  

    - Der Ordner, in dem die Installationsquelldateien für die Standorteinrichtung gespeichert werden  

    - Der Ordner, in dem die für Setup erforderlichen Downloads gespeichert werden  

- Pfadnamen der folgenden Objekte:  

    - IIS-Website  

    - Installationspfad der virtuellen Anwendung  

    - Name der virtuellen Anwendung  

- ISO-Dateinamen für Startmedien  


## <a name="additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a> Zusätzliche Einschränkungen

Nachfolgend sind weitere Einschränkungen für unterstützte Zeichensätze und Sprachversionen aufgelistet:  

- In Configuration Manager wird eine Änderung des Gebietsschemas für den Standortservercomputer nicht unterstützt.  

- Von einer Unternehmenszertifizierungsstelle (CA) werden keine Clientcomputernamen mit Doppelbyte-Zeichensätzen (DBCS) unterstützt. Welche Clientcomputernamen verwendet werden können, ist durch die PKI-Einschränkung des IA5-Zeichensatzes eingeschränkt. Configuration Manager unterstützt keine Werte für Zertifizierungsstellennamen oder Antragstellernamen, in denen Doppelbyte-Zeichensätze (DBCS) verwendet werden.  


## <a name="objects-that-arent-localized"></a><a name="BKMK_LangNonLocalize"></a> Objekte, die nicht lokalisiert werden

Die Configuration Manager-Datenbank unterstützt Unicode für die meisten Objekte, die sie speichert. Wenn möglich, werden diese Informationen in der Betriebssystemsprache angezeigt, die dem Gebietsschema eines Computers entspricht. Damit Informationen von der Clientschnittstelle oder der Configuration Manager-Konsole in der Betriebssystemsprache des Computers angezeigt werden, muss das Gebietsschema des Computers mit einer am Standort installierten Client- oder Serversprache übereinstimmen.  

Mehrere Configuration Manager-Objekte unterstützen Unicode nicht. Sie werden in der Datenbank mithilfe von ASCII gespeichert oder verfügen über zusätzliche Spracheinschränkungen. Diese Informationen werden immer im ASCII-Zeichensatz oder in der Sprache, in der Sie das betreffende Objekt erstellt haben, angezeigt.  
