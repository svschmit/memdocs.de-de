---
title: Konfigurieren von Einstellungen des kabelgebundenen Netzwerks für macOS-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Erstellen Sie ein Gerätekonfigurationsprofil für das kabelgebundene Netzwerk für macOS-Geräte, oder fügen Sie eines hinzu. Hier erfahren Sie mehr über die verschiedenen Einstellungen, das Hinzufügen von Zertifikaten sowie das Auswählen eines EAP-Typs und einer Authentifizierungsmethode in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41b11a29cdfd61382e68130479a1ab465bf354c6
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107419"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>Hinzufügen von Einstellungen für kabelgebundene Netzwerke für macOS-Geräte in Microsoft Intune

Sie können ein Profil mit bestimmten Einstellungen für das kabelgebundene Netzwerk erstellen und dann auf Ihren macOS-Geräten bereitstellen. Microsoft Intune bietet viele Features, darunter die Authentifizierung bei Ihrem Netzwerk, das Hinzufügen eines PKCS- oder SCEP-Zertifikats u.v.m.

In diesem Artikel werden die Einstellungen beschrieben, die Sie konfigurieren können.

## <a name="before-you-begin"></a>Vorbereitung

[Hinzufügen und Verwenden eines Konfigurationsprofils für Geräte in kabelgebundenen Netzwerken](wired-networks-configure.md)

> [!NOTE]
> Diese Einstellungen sind für alle Registrierungstypen verfügbar. Weitere Informationen zu den Registrierungstypen finden Sie unter [macOS-Registrierung](../enrollment/macos-enroll.md).

## <a name="wired-network"></a>Kabelgebundenes Netzwerk

- **Netzwerkschnittstelle**: Wählen Sie die Netzwerkschnittstellen auf dem Gerät aus, für die das Profil gilt, und gehen Sie dabei in Reihenfolge der Priorität der Dienste vor. Folgende Optionen sind verfügbar:
  
  - **Erstes aktives Ethernet** (Standardwert)
  - **Zweites aktives Ethernet**
  - **Drittes aktives Ethernet**
  - **Erstes Ethernet**
  - **Zweites Ethernet**
  - **Drittes Ethernet**
  - **Jedes Ethernet**

  Optionen mit „aktiv“ im Namen verwenden Schnittstellen, die aktiv auf dem Gerät ausgeführt werden. Wenn es keine aktiven Schnittstellen gibt, wird die nächste Schnittstelle in Reihenfolge der Priorität der Dienste konfiguriert. Standardmäßig ist die Option **Erstes aktives Ethernet** ausgewählt. Dies ist auch die von macOS konfigurierte Standardeinstellung.

- **EAP-Typ**: Wählen Sie den EAP-Typ (Extensible Authentication-Protokoll) zur Authentifizierung von gesicherten kabelgebundenen Verbindungen aus. Folgende Optionen sind verfügbar:

  - **EAP-FAST:** Geben Sie die **PAC-Einstellungen (Protected Access Credential)** ein. Bei dieser Option werden geschützte Zugriffsanmeldeinformationen verwendet, um einen authentifizierten Tunnel zwischen dem Client und dem Authentifizierungsserver zu erstellen. Folgende Optionen sind verfügbar:
    - **Nicht verwenden (PAC)**
    - **PAC verwenden:** Wenn eine PAC-Datei vorhanden ist, wird diese verwendet.
    - **PAC verwenden und bereitstellen:** Mit dieser Option wird die PAC-Datei erstellt und zu Ihren Geräten hinzugefügt.
    - **PAC anonym verwenden und bereitstellen:** Mit dieser Option wird die PAC-Datei erstellt und ohne Authentifizierung beim Server zu Ihren Geräten hinzugefügt.

  - **EAP-TLS**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** – **Zertifikatservernamen:** Fügen Sie mindestens einen allgemeinen Namen **hinzu**, der in den von der vertrauenswürdigen Zertifizierungsstelle ausgestellten Zertifikaten verwendet wird. Wenn Sie diese Informationen eingeben, können Sie das Fenster für dynamische Vertrauensstellungen umgehen, das auf Benutzergeräten bei der Verbindungsherstellung mit diesem Netzwerk angezeigt wird.
    - **Stammzertifikat zur Servervalidierung:** Wählen Sie ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Dieses Zertifikat wird dem Server bereitgestellt, wenn der Client eine Verbindung mit dem Netzwerk herstellt. Es dient der Authentifizierung der Verbindung.
    - **Clientauthentifizierung** - **Zertifikate:** Wählen Sie das SCEP- oder PKCS-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.
    - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

  - **EAP-TTLS**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** – **Zertifikatservernamen:** Fügen Sie mindestens einen allgemeinen Namen **hinzu**, der in den von der vertrauenswürdigen Zertifizierungsstelle ausgestellten Zertifikaten verwendet wird. Wenn Sie diese Informationen eingeben, können Sie das Fenster für dynamische Vertrauensstellungen umgehen, das auf Benutzergeräten bei der Verbindungsherstellung mit diesem Netzwerk angezeigt wird.
    - **Stammzertifikat zur Servervalidierung:** Wählen Sie ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Dieses Zertifikat wird dem Server bereitgestellt, wenn der Client eine Verbindung mit dem Netzwerk herstellt. Es dient der Authentifizierung der Verbindung.
    - **Clientauthentifizierung:** Wählen Sie eine **Authentifizierungsmethode** aus. Folgende Optionen sind verfügbar:
      - **Benutzername und Kennwort**: Diese Option fordert den Benutzer zur Eingabe des Benutzernamens und Kennworts für die Authentifizierung der Verbindung auf. Geben Sie außerdem Folgendes ein:
        - **Nicht-EAP-Methode (innere Identität)** : Wählen Sie aus, wie die Verbindung authentifiziert werden soll. Achten Sie darauf, dass Sie das gleiche Protokoll auswählen, das auch in Ihrem Netzwerk konfiguriert ist. Folgende Optionen sind verfügbar:
          - **Unverschlüsseltes Kennwort (PAP)**
          - **Challenge Handshake Authentication-Protokoll (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP, Version 2 (MS-CHAP v2)**
      - **Zertifikate:** Wählen Sie das SCEP- oder PKCS-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.
      - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

  - **LEAP**

  - **PEAP**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** – **Zertifikatservernamen:** Fügen Sie mindestens einen allgemeinen Namen **hinzu**, der in den von der vertrauenswürdigen Zertifizierungsstelle ausgestellten Zertifikaten verwendet wird. Wenn Sie diese Informationen eingeben, können Sie das Fenster für dynamische Vertrauensstellungen umgehen, das auf Benutzergeräten bei der Verbindungsherstellung mit diesem Netzwerk angezeigt wird.
    - **Stammzertifikat zur Servervalidierung:** Wählen Sie ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Dieses Zertifikat wird dem Server bereitgestellt, wenn der Client eine Verbindung mit dem Netzwerk herstellt. Es dient der Authentifizierung der Verbindung.
    - **Clientauthentifizierung:** Wählen Sie eine **Authentifizierungsmethode** aus. Folgende Optionen sind verfügbar:
      - **Benutzername und Kennwort**: Diese Option fordert den Benutzer zur Eingabe des Benutzernamens und Kennworts für die Authentifizierung der Verbindung auf.
      - **Zertifikate:** Wählen Sie das SCEP- oder PKCS-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.
      - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber vielleicht keine Aktionen durch. Denken Sie daran, dieses [Profil zuzuweisen](device-profile-assign.md) und seinen [Status zu überwachen](device-profile-monitor.md).
