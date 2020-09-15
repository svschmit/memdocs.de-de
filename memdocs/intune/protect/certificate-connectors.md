---
title: C-Zertifikatconnectors für Microsoft Intune – Azure | Microsoft-Dokumentation
description: Erfahren Sie mehr über Zertifikatconnectors für Zertifikate und Zertifikatprofile des Typs Simple Certificate Enrollment Protocol (SCEP) oder Public Key Cryptography Standards (PKCS) mit Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f891e7989ad3f0f8d798dd9a5f0207a19ac5b95
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2020
ms.locfileid: "89428894"
---
# <a name="certificate-connectors-for-microsoft-intune"></a>Zertifikatconnectors für Microsoft Intune

Zum Unterstützen der Verwendung von Zertifikaten für die Authentifizierung und die Signierung und Verschlüsselung von E-Mails mithilfe von S/MIME erfordert Intune einen Zertifikatconnector. Ein Zertifikatconnector ist eine Software, die Sie auf einem lokalen Server installieren können. Der Connector ermöglicht über die Cloud verwalteten Geräten die Bereitstellung von Zertifikaten über eine lokale Infrastruktur, ähnlich wie eine ausstellende Zertifizierungsstelle.

In diesem Artikel werden die verfügbaren Connectors, ihre Lebenszyklen, die Voraussetzungen für ihre Verwendung und das Durchführen von Updates beschrieben.  

## <a name="available-connectors"></a>Verfügbare Connectors

Für Intune stehen zwei Zertifikatconnectors zur Verfügung. Für jeden bestehen eigene Anwendungsfälle und Anforderungen.

### <a name="pfx-certificate-connector-for-microsoft-intune"></a>PFX Certificate Connector für Microsoft Intune

Der **PFX-Zertifikatconnector** unterstützt die Zertifikatbereitstellung für PCKS#12-Zertifikatanforderungen und verarbeitet Anforderungen für PFX-Dateien, die für die S/MIME-E-Mail-Verschlüsselung für einen spezifischen Benutzer in Intune importiert werden.

> [!TIP]
> Vor dem Update vom August für diesen Connector wurden PKCS#12-Zertifikatanforderungen vom *Intune-Zertifikatconnector* verarbeitet. Mit dem Update vom August wurde die Funktionalität für alle PKCS-Zertifikatanforderungen im *PFX-Zertifikatconnector* konsolidiert, der automatische Updates des Connectors auf neue Versionen unterstützt und die Verwendung der Version 4.7.2 von .NET Framework erfordert.
>
> Die Funktionalität des Microsoft Intune-Connectors ist nicht veraltet und kann weiterhin mit PKCS-Zertifikatprofilen verwendet werden. Wenn Sie jedoch nicht SCEP verwenden oder die Verwendung von NDES anderweitig benötigen, können Sie zum PFX-Zertifikatconnector wechseln und NDES von Ihren Servern entfernen. 

**Der PFX-Zertifikatconnector:**

- unterstützt mehrere Instanzen dieses Connectors für jeden Intune-Mandanten. Jede Instanz dieses Connectors muss auf einer Windows Server-Instanz installiert werden und über Zugriff auf den privaten Schlüssel verfügen, der zum Verschlüsseln der Kennwörter für die hochgeladenen PFX-Dateien verwendet wurde.
- kann auf demselben Server installiert werden, der eine Instanz des *Microsoft Intune-Connectors* hostet.
- unterstützt [automatische Updates](#automatic-update) auf neue Versionen. Zum automatischen Installieren neuer Version muss der Computer, der den Connector hostet, **autoupdate.msappproxy.net** über Port **443** kontaktieren. Wenn das automatische Update des Connectors fehlschlägt, können Sie das Update manuell durchführen.
- unterstützt die Zertifikatsperrung (erfordert die Ausführung von Version **6.2008.60.607** oder höher).
- weist dieselben Netzwerkanforderungen wie [verwaltete Geräte](../fundamentals/intune-endpoints.md#access-for-managed-devices) auf.

  Weitere Informationen finden Sie unter [Netzwerkendpunkte für Microsoft Intune](../fundamentals/intune-endpoints.md) und [Anforderungen an die Intune-Netzwerkkonfiguration und Bandbreite](../fundamentals/network-bandwidth-use.md).

**Der Windows-Server, auf dem der Connector installiert wird, muss:**

- Windows Server 2012 R2 oder höher ausführen.
- .NET Framework 4.7.2 ausführen.  

**So installieren Sie den PFX-Zertifikatconnector:**

Weitere Informationen zur Installation dieses Connectors finden Sie unter [Herunterladen, Installieren und Konfigurieren des PFX-Zertifikatconnectors](certficates-pfx-configure.md).

### <a name="microsoft-intune-connector"></a>Microsoft Intune-Connector

Der **Microsoft Intune-Connector** wird manchmal *Microsoft Intune Certificate Connector* genannt. Dieser Connector unterstützt die Zertifikatbereitstellung, wenn Sie *SCEP (Simple Certificate Enrollment-Protokoll)* verwenden und über eine Zertifizierungsstelle der Active Directory-Zertifikatdienste verfügen. Diese Art von Zertifizierungsstelle wird auch *Microsoft-Zertifizierungsstelle* genannt.

Wenn Sie SCEP mit einer Microsoft-Zertifizierungsstelle verwenden, müssen Sie auch **NDES (Network Device Enrollment Service)** konfigurieren. Aus diesem Grund wird dieser Connector häufig als *NDES-Zertifikatconnector* bezeichnet.

Wenn Sie eine [Drittanbieter-Zertifizierungsstelle](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration) verwenden, müssen Sie diesen Connector nicht verwenden und NDES ist nicht erforderlich.

**Der Microsoft Intune-Connector:**

- wird auf einem Windows-Server installiert, der auch eine Instanz des *PFX-Zertifikatconnectors* hosten kann.
- unterstützt bis zu 100 Instanzen dieses Connectors pro Mandant, wobei sich jede Instanz auf einem separaten Windows-Server befindet. Wenn Sie mehrere Connectors verwenden:
  - sollten alle Instanzen des *Microsoft Intune-Connectors* in Ihrer Umgebung dieselbe Version aufweisen.
  - unterstützt Ihre Infrastruktur Redundanz und Lastenausgleiche, da jede verfügbare Connectorinstanz Ihre Zertifikatanforderungen verarbeiten kann.
- erfordert ein [manuelles Update](#manual-update) zum Installieren der neuen Version des Connectors. Für ein manuelles Update müssen Sie den aktuellen Connector deinstallieren und dann die neue Version des Connectors installieren. Es sollten keine weiteren Aktionen erforderlich sein.
- unterstützt den *FIPS-Modus (Federal Information Processing Standard)* . FIPS ist nicht erforderlich. Wenn FIPS aktiviert ist, können Sie Zertifikate ausstellen und widerrufen.
- weist dieselben Netzwerkanforderungen wie [verwaltete Geräte](../fundamentals/intune-endpoints.md#access-for-managed-devices) auf.

  Weitere Informationen finden Sie unter [Netzwerkendpunkte für Microsoft Intune](../fundamentals/intune-endpoints.md) und [Anforderungen an die Intune-Netzwerkkonfiguration und Bandbreite](../fundamentals/network-bandwidth-use.md).

**Der Windows-Server, auf dem der Connector installiert wird, muss:**

- Windows Server 2012 R2 oder höher ausführen.
- .NET Framework 4.5 ausführen. Wenn dieser Connector auf demselben Server wie der *PFX-Zertifikatconnector* installiert wird, müssen Sie .NET Framework 4.7.2 verwenden, da dies für den PFX-Connector erforderlich ist.
- ein anderer Server als der sein, der Ihre ausstellende Zertifizierungsstelle hostet.
- über Zugriff auf einen Server verfügen, auf dem NDES ausgeführt wird, wenn er für SCEP mit einer Microsoft-Zertifizierungsstelle verwendet wird. NDES wird auf einem Windows-Server ausgeführt. Dabei kann es sich um denselben Server handeln, auf dem dieser Connector ausgeführt wird.

**Wenn NDES erforderlich ist:**

- [muss die erweiterte Sicherheitskonfiguration von Internet Explorer auf dem Server deaktiviert sein, der NDES hostet](/previous-versions/windows/it-pro/windows-server-2003/cc775800(v=ws.10)). Dies gilt auch für den Server, der den *Microsoft Intune-Connector* hostet.
- erfordert der Connector zusätzliche Konfigurationen für die Kommunikation mit NDES. Vorgehensweisen zum Installieren und Konfigurieren von NDES finden Sie unter den Vorgehensweisen zum Installieren des *Microsoft Intune-Connectors*.

  Weitere Informationen zu NDES finden Sie unter [Leitfaden zum Registrierungsdienst für Netzwerkgeräte](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).

**So installieren Sie den Microsoft Intune-Connector:**

Anweisungen zur Installation dieses Connectors finden Sie unter [Konfigurieren der Infrastruktur zur Unterstützung von SCEP mit Intune](certificates-scep-configure.md).

## <a name="connector-lifecycle"></a>Connector-Lebenszyklus

Es werden regelmäßig aktualisierte Versionen der Zertifikatconnectors veröffentlicht. Ankündigungen für neue Connectorreleases finden Sie im Artikel zu den (Neuigkeiten](../fundamentals/whats-new.md) für Intune und im Abschnitt [Neuerungen für Connectors](#whats-new-for-connectors) am Ende dieses Artikels.

Wenn eine neue Version veröffentlicht wird, wird die Unterstützung für die vorherige Version mit einer begrenzten Übergangsfrist für die fortgesetzte Verwendung eingestellt. Nach Ablauf der Übergangsfrist endet die Unterstützung für die veraltete Version. Dann kann sie jederzeit nicht mehr funktionieren. Die Übergangsfrist beträgt sechs Monate.

Sie sollten so bald wie möglich ein Update auf die neueste Version Ihres Connectors planen. Jeder Connector weist einen anderen Updatepfad auf:

- **PFX-Zertifikatconnector für Microsoft Intune:** unterstützt automatische Updates.
- **Microsoft Intune-Connector:** erfordert ein manuelles Update.

### <a name="automatic-update"></a>Automatisches Update

Wenn es vom Connectortyp und Ihrer Umgebung unterstützt wird, kann Intune ein automatisches Update auf die neueste Version des Connectors durchführen, kurz nachdem diese Connectorversion veröffentlicht wurde.  

Damit automatische Updates durchgeführt werden können, muss der Server, auf dem der Connector gehostet wird, auf den **Azure-Updatedienst** zugreifen:

- Port: **443**
- Endpunkt: **autoupdate.msappproxy.net**

Wenn der Zugriff für automatische Updates durch Firewalls, die Infrastruktur oder Netzwerkkonfigurationen eingeschränkt wird, müssen Sie diese Blockierprobleme beheben oder den Connector manuell auf die neueste Version aktualisieren.

### <a name="manual-update"></a>Manuelles Update

Die Vorgehensweise zum Durchführen eines manuellen Updates für einen Zertifikatconnector ist identisch mit der Neuinstallation eines Connectors.

Sie können ein manuelles Update für einen Zertifikatconnector durchführen, selbst wenn dieser automatische Updates unterstützt. Beispielsweise können Sie ein manuelles Update für den Connector durchführen, wenn ein automatisches Update durch Ihre Netzwerkkonfiguration blockiert wird.  

### <a name="to-reinstall-a-certificate-connector"></a>Neuinstallation eines Zertifikatconnectors

1. Verwenden Sie **Windows-Apps und -Features** zum Deinstallieren des Connectors auf dem Windows-Server, der den Connector hostet.

2. Verwenden Sie anschließend die Vorgehensweise zum Installieren einer neuen Version des Connectors. Stellen Sie sicher, dass Sie beim Installieren einer neueren Version eines Connectors nach neuen oder aktualisierten Voraussetzungen prüfen:
   - SCEP: [Konfigurieren der Infrastruktur für die Unterstützung von SCEP mit Intune](certificates-scep-configure.md)
   - PKCS: [Herunterladen, Installieren und Konfigurieren des PFX-Zertifikatconnectors für Microsoft Intune](certficates-pfx-configure.md)

## <a name="connector-status-and-version"></a>Status und Version des Connectors

Im Microsoft Endpoint Manager Admin Center können Sie einen Zertifikatconnector auswählen, um dessen Statusinformationen einzusehen und dessen Version zu überprüfen:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Navigieren Sie zu **Mandantenverwaltung** > **Connectors und Tokens** > **Zertifikatconnectors**.

3. Wählen Sie den Connector aus, dessen Status Sie anzeigen möchten.

Beim Anzeigen des Connectorstatus:

- werden veraltete Connectors mit einer **Warnung** angezeigt. Die Warnung wird nach der sechs Monate langen Übergangsfrist in einen Fehler geändert.
- wird für Connectors nach Überschreitung der Übergangsfrist ein Fehler angezeigt. Diese Connectors werden nicht mehr unterstützt und können jederzeit ihre Funktionsfähigkeit verlieren.

## <a name="whats-new-for-connectors"></a>Neuerungen für Connectors

Es werden regelmäßig Updates für die beiden Certificate Connectors veröffentlicht. Sobald wir ein Update für einen Connector veröffentlichen, werden Sie hier darüber informiert.

### <a name="pfx-certificate-connector-release-history"></a>Releaseverlauf des PFX-Zertifikatconnectors

Der *PFX-Zertifikatconnector für Microsoft Intune* [unterstützt automatische Updates](#automatic-update).

#### <a name="august-26-2020"></a>26. August 2020

**Version 6.2008.60.607:** Änderungen in diesem Release:

- .NET Framework-Version 4.7.2 ist erforderlich.
- Der PFX-Zertifikatconnector ersetzt nun den *Microsoft Intune-Connector* für die Verwendung von PKCS-Zertifikatprofilen. Der *PFX-Zertifikatconnector* ist nun der einzige Connector, der für die Verwendung von PCKS#12- oder importierten PFX-Zertifikaten erforderlich ist.
- Die Unterstützung der Verwendung von PKCS-Zertifikatprofilen mit allen unterstützten Plattformen außer Windows 8.1 wurde hinzugefügt.
- Die Unterstützung der Zertifikatsperrung für S/MIME in Outlook wurde hinzugefügt.

#### <a name="november-18-2019"></a>18. November 2019

**Version: 6.1911.11.602:** Änderungen in diesem Release:

- Die S/MIME-Unterstützung für PFX wurde hinzugefügt.  

#### <a name="may-17-2019"></a>17. Mai 2019

**Version 6.1905.0.404:** Änderungen in diesem Release:

- Ein Problem wurde behoben, bei dem vorhandene PFX-Zertifikate weiter erneut verarbeitet werden, was bewirkt, dass der Connector die Verarbeitung neuer Anforderungen beendet. 

#### <a name="may-6-2019"></a>6\. Mai 2019

**Version 6.1905.0.402:** Änderungen in diesem Release:

- Das Abrufintervall für den Connector wird von 5 Minuten auf 30 Sekunden verkürzt.

#### <a name="april-2-2019"></a>2\. April 2019

**Version 6.1904.0.401:** Änderungen in diesem Release:

- Dieser Connector unterstützt nun automatische Updates.
- Es wurde ein Problem behoben, bei dem die Möglichkeit bestand, dass sich der Connector nach der Anmeldung mit dem globalen Administratorkonto nicht bei Intune registrieren konnte.

### <a name="microsoft-intune-connector-release-history"></a>Releaseverlauf des Microsoft Intune-Connectors

#### <a name="april-2-2019"></a>2\. April 2019

**Version 6.1904.1.0:** Änderungen in diesem Release:  

- Es wurde ein Problem behoben, bei dem die Möglichkeit bestand, dass sich der Connector nach der Anmeldung mit dem globalen Administratorkonto nicht bei Intune registrieren konnte.
- Umfasst Fehlerbehebungen in Bezug auf die Zuverlässigkeit bei Zertifikatsperrungen
- Umfasst Fehlerbehebungen in Bezug auf die Leistung, um die Verarbeitung von Anforderungen von PKCS-Zertifikaten zu beschleunigen

## <a name="next-steps"></a>Nächste Schritte

Erstellen Sie SCEP-, PKCS- oder über PKCS importierte Zertifikatprofile für jede Plattform, die Sie verwenden möchten. Weitere Informationen zum Fortfahren finden Sie in den folgenden Artikeln:

- [Konfigurieren Ihrer Infrastruktur für die Unterstützung von SCEP-Zertifikaten mit Intune](certificates-scep-configure.md)  
- [Konfigurieren Ihrer Microsoft Intune-Zertifikatsinfrastruktur für PKCS](certficates-pfx-configure.md)  
- [Erstellen eines importierten PKCS-Zertifikatprofils](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
