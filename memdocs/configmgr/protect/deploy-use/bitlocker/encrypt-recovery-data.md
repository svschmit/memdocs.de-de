---
title: Verschlüsseln von Wiederherstellungsdaten
titleSuffix: Configuration Manager
description: Verschlüsseln Sie BitLocker-Wiederherstellungsschlüssel, Wiederherstellungspakete und TPM-Kennworthashes über das Netzwerk und in der Configuration Manager-Datenbank.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e887d594e80c0f92340081d9b922bfc334d1b3a5
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129187"
---
# <a name="encrypt-recovery-data"></a>Verschlüsseln von Wiederherstellungsdaten

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

Wenn Sie eine BitLocker-Verwaltungsrichtlinie erstellen, stellt Configuration Manager den Wiederherstellungsdienst auf einem Verwaltungspunkt bereit. Wenn Sie auf der Seite **Client Management** (Clientverwaltung) der BitLocker-Verwaltungsrichtlinie **die BitLocker-Verwaltungsdienste konfigurieren**, sichert der Client wichtige Wiederherstellungsinformationen in der Standortdatenbank. Dazu zählen BitLocker-Wiederherstellungsschlüssel, -Wiederherstellungspakete und TPM-Kennworthashs. Wenn Benutzer ihr geschütztes Gerät nicht mehr nutzen können, haben Sie mit diesen Informationen die Möglichkeit, Ihnen wieder Zugriff darauf zu gewähren.

Weil diese Informationen sehr empfindlich sind, müssen Sie sie in den folgenden Situationen schützen:

- Configuration Manager benötigt eine HTTPS-Verbindung zwischen dem Client und dem Wiederherstellungsdienst, um die Daten während der Übertragung über das Netzwerk zu verschlüsseln. Es stehen zwei Optionen zur Verfügung:

  - HTTPS wird für die IIS-Website auf dem Verwaltungspunkt, auf dem der Wiederherstellungsdienst gehostet wird, aktiviert, und nicht für die gesamte Rolle „Verwaltungspunkt“. Diese Option gilt nur für Version 2002 von Configuration Manager.<!-- 5925660 -->

  - Konfigurieren des Verwaltungspunkts für HTTPS. Die Einstellung **Clientverbindungen** muss in den Eigenschaften des Verwaltungspunkts **HTTPS** lauten. Diese Option gilt nur für die Versionen 1910 und 2002 von Configuration Manager.

    > [!NOTE]
    > Das erweiterte HTTP-Protokoll wird derzeit nicht unterstützt.

- Sie sollten diese Daten auch verschlüsseln, wenn sie in der Standortdatenbank gespeichert werden. Wenn Sie ein SQL-Zertifikat erstellen, verschlüsselt Configuration Manager Ihre Daten in SQL.

    Wenn Sie kein Verschlüsselungszertifikat für die BitLocker-Verwaltung erstellen möchten, können Sie angeben, dass die Wiederherstellungsdaten als Nur-Text gespeichert werden sollen. Aktivieren Sie dazu beim Erstellen der BitLocker-Verwaltungsrichtlinie die Option **Allow recovery information to be stored in plain text** (Zulassen, dass Wiederherstellungsinformationen als Nur-Text gespeichert werden).

    > [!NOTE]
    > Zusätzliche Sicherheit bietet eine Verschlüsselung der gesamten Standortdatenbank. Bisher sind keine negativen Auswirkungen der Datenbankverschlüsselung auf die Funktionen von Configuration Manager bekannt.
    >
    > Setzen Sie die Verschlüsselung mit Bedacht ein, insbesondere in großen Umgebungen. Abhängig von den von Ihnen verschlüsselten Tabellen und der SQL-Version kann es zu Leistungseinbußen von bis zu 25 % kommen. Aktualisieren Sie Ihre Sicherungs- und Wiederherstellungspläne, damit Sie die verschlüsselten Daten erfolgreich wiederherstellen können.

## <a name="certificate-requirements"></a>Zertifikatanforderungen

### <a name="https-server-authentication-certificate"></a>HTTPS-Serverauthentifizierungszertifikat

<!--5925660-->

In der Current Branch-Version 1910 von Configuration Manager war zum Integrieren des BitLocker-Wiederherstellungsdiensts ein HTTPS-fähiger Verwaltungspunkt erforderlich. Die HTTPS-Verbindung ist erforderlich, um die Wiederherstellungsschlüssel im Netzwerk zwischen dem Configuration Manager-Client und dem Verwaltungspunkt zu verschlüsseln. Das Konfigurieren des Verwaltungspunkts und sämtlicher Clients für HTTPS stellt für viele Kunden eine Herausforderung dar.

Ab Version 2002 gilt die HTTPS-Anforderung für die IIS-Website, auf der der Wiederherstellungsdienst gehostet wird, und nicht für die gesamte Rolle „Verwaltungspunkt“. Durch diese Änderungen werden die Wiederherstellungsschlüssel trotz weniger strenger Zertifikatanforderungen bei der Übertragung weiterhin verschlüsselt.

Für die Eigenschaft **Clientverbindungen** des Verwaltungspunkts kann nun **HTTP** oder **HTTPS** angegeben werden. Wenn der Verwaltungspunkt für **HTTP** konfiguriert ist, ist für die Unterstützung des BitLocker-Wiederherstellungsdiensts Folgendes erforderlich:

1. Erwerb eines Serverauthentifizierungszertifikats Binden des Zertifikats an die IIS-Website des Verwaltungspunkts, auf der der BitLocker-Wiederherstellungsdienst gehostet wird

2. Konfiguration der Clients, sodass diese dem Serverauthentifizierungszertifikat vertrauen Dieses Vertrauen kann auf zwei Wegen sichergestellt werden:

    - Verwenden Sie ein Zertifikat eines öffentlichen und global vertrauenswürdigen Zertifikatanbieters. Hierbei kann es sich beispielsweise um DigiCert, Thawte oder VeriSign handeln. Windows-Clients schließen vertrauenswürdige Stammzertifizierungsstellen von diesen Anbietern ein. Wenn Sie ein Serverauthentifizierungszertifikat von einem dieser Anbieter verwenden, sollten Ihre Clients dem Zertifikat automatisch vertrauen.

    - Verwenden Sie ein Zertifikat, das von einer Zertifizierungsstelle über die Public Key-Infrastruktur (PKI) Ihrer Organisation ausgestellt wird. Die meisten PKI-Implementierungen integrieren vertrauenswürdige Stammzertifizierungsstellen in Windows-Clients. Ein Beispiel ist die Verwendung von Active Directory-Zertifikatdienste mit einer Gruppenrichtlinie. Wenn Sie das Serverauthentifizierungszertifikat über eine Zertifizierungsstelle ausstellen, der Ihre Clients nicht automatisch vertrauen, fügen Sie den Clients ein vertrauenswürdiges Stammzertifikat der Zertifizierungsstelle hinzu.

> [!TIP]
> Die einzigen Clients, die mit dem Wiederherstellungsdienst kommunizieren müssen, sind die, für die eine BitLocker-Verwaltungsrichtlinie mit einer **Clientverwaltungsregel** gelten soll.

Verwenden Sie für den Client **BitLockerManagementHandler.log**, um bei dieser Verbindung auftretende Probleme zu beheben. Dieses Protokoll zeigt die vom Client für die Verbindung mit dem Wiederherstellungsdienst verwendete URL an. Suchen Sie nach einem Eintrag, der mit `Checking for Recovery Service at` beginnt.

> [!NOTE]
> Wenn Ihr Standort über mehr als einen Verwaltungspunkt verfügt, aktivieren Sie HTTPS an allen Verwaltungspunkten des Standorts, mit denen ein von BitLocker verwalteter Client möglicherweise kommunizieren könnte. Wenn der HTTPS-Verwaltungspunkt nicht verfügbar ist, könnte der Client auf einen HTTP-Verwaltungspunkt ausweichen und dann seinen Wiederherstellungsschlüssel nicht hinterlegen.
>
> Diese Empfehlung gilt für beide Optionen: Aktivieren Sie den Verwaltungspunkt für HTTPS, oder aktivieren Sie die IIS-Website, die den Wiederherstellungsdienst auf dem Verwaltungspunkt hostet.

### <a name="sql-encryption-certificate"></a>SQL-Verschlüsselungszertifikat

Verwenden Sie dieses SQL-Zertifikat für Configuration Manager, um BitLocker-Wiederherstellungsdaten in der Standortdatenbank zu verschlüsseln. Sie können beim Erstellen und Bereitstellen des Verschlüsselungszertifikats für die BitLocker-Verwaltung einen eigenen Prozess verwenden, vorausgesetzt die folgenden Anforderungen sind erfüllt:

- Der Name des Verschlüsselungszertifikats für die BitLocker-Verwaltung muss `BitLockerManagement_CERT` lauten.

- Verschlüsseln Sie dieses Zertifikat mit einem Datenbankhauptschlüssel.

- Die folgenden SQL-Benutzer benötigen die Berechtigung **Control** (Steuern) für das Zertifikat:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Stellen Sie für jede Standortdatenbank in Ihrer Hierarchie dasselbe Zertifikat bereit.

- Erstellen Sie das Zertifikat mit der neuesten Version von SQL Server in Ihrer Umgebung. Beispiel:
  - Zertifikate, die mit SQL Server 2016 oder höher erstellt wurden, sind mit SQL Server 2014 oder niedriger kompatibel.
  - Zertifikate, die mit SQL Server 2014 oder niedriger erstellt wurden, sind mit SQL Server 2016 oder höher nicht kompatibel.

## <a name="example-scripts"></a>Beispielskripts

Diese SQL-Skripts sind Beispiele für das Erstellen und Bereitstellen eines Verschlüsselungszertifikats für die BitLocker-Verwaltung in der Configuration Manager-Standortdatenbank.

### <a name="create-certificate"></a>Zertifikat erstellen

Dieses Beispielskript führt die folgenden Aktionen aus:

- Erstellt ein Zertifikat
- Legt die Berechtigungen fest.
- Erstellt einen Datenbankhauptschlüssel

Bevor Sie dieses Skript in einer Produktionsumgebung verwenden, ändern Sie die folgenden Werte:

- Name der Standortdatenbank (`CM_ABC`)
- Kennwort zum Erstellen des Hauptschlüssels (`MyMasterKeyPassword`)
- Ablaufdatum des Zertifikats (`20391022`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Sichern des Zertifikats

Mit diesem Beispielskript wird eine Sicherung des Zertifikats gespeichert. Wenn Sie das Zertifikat in einer Datei speichern, können Sie es in anderen Standortdatenbanken in der Hierarchie [wiederherstellen](#restore-certificate).

Bevor Sie dieses Skript in einer Produktionsumgebung verwenden, ändern Sie die folgenden Werte:

- Name der Standortdatenbank (`CM_ABC`)
- Dateipfad und Name (`C:\BitLockerManagement_CERT_KEY`)
- Kennwort für den Exportschlüssel (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Speichern Sie die exportierte Zertifikatsdatei und das dazugehörige Kennwort an einem sicheren Ort.

### <a name="restore-certificate"></a>Zertifikat wiederherstellen

Dieses Beispielskript stellt ein Zertifikat aus einer Datei wieder her. Mit diesem Prozess können Sie ein Zertifikat bereitstellen, das Sie in einer anderen Standortdatenbank erstellt haben.

Bevor Sie dieses Skript in einer Produktionsumgebung verwenden, ändern Sie die folgenden Werte:

- Name der Standortdatenbank (`CM_ABC`)
- Kennwort des Masterschlüssels (`MyMasterKeyPassword`)
- Dateipfad und Name (`C:\BitLockerManagement_CERT_KEY`)
- Kennwort für den Exportschlüssel (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Überprüfen des Zertifikats

Verwenden Sie dieses SQL-Skript, um zu überprüfen, ob SQL das Zertifikat erfolgreich mit den benötigten Berechtigungen erstellt hat.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Wenn das Zertifikat gültig ist, gibt das Skript den Wert `1` zurück.

## <a name="see-also"></a>Weitere Informationen:

Weitere Informationen zu diesen SQL-Befehlen finden Sie in den folgenden Artikeln:

- [Verschlüsselungsschlüssel für SQL Server und Datenbank](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [Erstellen eines Zertifikats](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [Sichern eines Zertifikats](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [Erstellen eines Hauptschlüssels](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [Sichern des Hauptschlüssels](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [Erteilen von Zertifikatberechtigungen](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
