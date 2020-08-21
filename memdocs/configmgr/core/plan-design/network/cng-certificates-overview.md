---
title: 'CNG-Zertifikate: Übersicht'
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zur Unterstützung von CNG-Zertifikaten (Cryptography Next Generation) für Configuration Manager-Clients und -Server.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 191325d05ccc23a4f07d8b39f7927c2b2e543f41
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692654"
---
# <a name="cng-certificates-overview"></a>CNG-Zertifikate: Übersicht
<!-- 1356191 --> 

Configuration Manager bietet eingeschränkte Unterstützung für CNG-Zertifikate (Cryptography: Next Generation). Configuration Manager-Clients können das PKI-Clientauthentifizierungszertifikat mit dem privaten Schlüssel im CNG-Schlüsselspeicheranbieter (KSP) verwenden. Dank der KSP-Unterstützung unterstützen Configuration Manager-Clients hardwarebasierte private Schlüssel, wie z. B. TPM KSP für PKI-Clientauthentifizierungszertifikate.

## <a name="supported-scenarios"></a>Unterstützte Szenarien
Sie können Zertifikatvorlagen des Typs [Cryptography API: Next Generation (CNG)](/windows/win32/seccng/cng-features) für die folgenden Szenarien verwenden:

- Clientregistrierung und Kommunikation mit einem HTTPS-Verwaltungspunkt   
- Softwareverteilung und Anwendungsbereitstellung mit einem HTTPS-Verteilungspunkt   
- Betriebssystembereitstellung  
- Client Messaging SDK (mit dem aktuellen Update) und ISV-Proxy   
- Cloud Management Gateway-Konfiguration  

Verwenden Sie ab Version 1802 CNG-Zertifikate für die folgenden HTTPS-fähigen Serverrollen: <!-- 1357314 -->   
- Verwaltungspunkt
- Verteilungspunkt
- Softwareupdatepunkt
- Zustandsmigrationspunkt     

Verwenden Sie ab Version 1806 CNG-Zertifikate für die folgenden HTTPS-fähigen Serverrollen:

- Zertifikatregistrierungspunkt einschließlich des NDES-Servers mit dem Configuration Manager-Richtlinienmodul. <!--1357314-->

> [!NOTE]
> CNG ist mit Crypto API (CAPI) abwärtskompatibel. CAPI-Zertifikate werden weiterhin unterstützt, auch wenn die CNG-Unterstützung auf dem Client aktiviert ist.

## <a name="unsupported-scenarios"></a>Nicht unterstützte Szenarien

Die folgenden Szenarios werden derzeit nicht unterstützt:

- Die folgenden Serverrollen sind nicht betriebsbereit, wenn sie im HTTPS-Modus installiert werden und ein CNG-Zertifikat an die Website auf IIS (Internetinformationsdienste) gebunden ist: 
    - Anwendungskatalog-Webdienst
    - Anwendungskatalog-Website
    - Anmeldungspunkt  
    - Anmeldungsproxypunkt  

- Softwarecenter zeigt keine Anwendungen und Pakete als verfügbar an, die für Benutzer- oder Benutzergruppensammlungen bereitgestellt werden.

- Mithilfe von CNG-Zertifikaten kann kein Cloudverteilungspunkt erstellt werden.

- Wenn das NDES-Richtlinienmodul ein CNG-Zertifikat für die Clientauthentifizierung nutzt, schlägt die Kommunikation mit dem Zertifikatregistrierungspunkt fehl. 
    - Dies wird ab Configuration Manager Version 1806 unterstützt.

- Wenn Sie beim Erstellen von Tasksequenzmedien ein CNG-Zertifikat angeben, schlägt der Assistent beim Erstellen startbarer Medien fehl.
    - Dies wird ab Configuration Manager Version 1806 unterstützt.

## <a name="to-use-cng-certificates"></a>So verwenden Sie CNG-Zertifikate

Um CNG-Zertifikate zu verwenden, muss die Zertifizierungsstelle (Certification Authority, CA) CNG-Zertifikatvorlagen für Zielcomputer bereitstellen. Vorlagendetails variieren je nach Szenario. Allerdings sind die folgenden Eigenschaften erforderlich:

- Registerkarte **Kompatibilität**

    - Die **Zertifizierungsstelle** muss Windows Server 2008 oder höher sein. Empfohlen wird Windows Server 2012.

    - Der **Zertifikatempfänger** muss Windows Vista/Server 2008 oder höher sein. Empfohlen wird Windows 8/Windows Server 2012.

- Registerkarte **Kryptografie**

    - Die **Anbieterkategorie** muss der **Schlüsselspeicheranbieter** sein. (erforderlich)
    - **Die Anforderung muss einen der folgenden Anbieter verwenden:** muss der **Softwareschlüsselspeicher-Anbieter von Microsoft** sein. 

> [!NOTE]
> Die Anforderungen an Ihre Umgebung oder Organisation können unterschiedlich sein. Wenden Sie sich an Ihren PKI-Experten. Beachten Sie unbedingt, dass eine Zertifikatsvorlage einen Schlüsselspeicheranbieter verwenden muss, um CNG nutzen zu können.

Für optimale Ergebnisse wird empfohlen, einen Antragstellernamen aus Active Directory-Informationen zu erstellen. Verwenden Sie den DNS-Namen für das **Format des Antragstellernamens**, und verwenden Sie den DNS-Namen im alternativen Antragstellernamen. Andernfalls müssen Sie diese Informationen bereitstellen, wenn das Gerät beim Zertifikatprofil registriert wird.