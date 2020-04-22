---
title: Bereitstellen der BitLocker-Verwaltung
titleSuffix: Configuration Manager
description: In diesem Artikel erfahren Sie, wie Sie den BitLocker-Verwaltungs-Agent für Konfigurations-Manager-Clients und den Wiederherstellungsdienst für Verwaltungspunkte bereitstellen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be5ecd02817d315da4a3bea1f21285eb5a77d77e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709358"
---
# <a name="deploy-bitlocker-management"></a>Bereitstellen der BitLocker-Verwaltung

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

Die BitLocker-Verwaltung in Configuration Manager enthält die folgenden Komponenten:

- **BitLocker-Verwaltungs-Agent:** Dieser Agent wird von Configuration Manager auf einem Gerät aktiviert, wenn Sie [eine Richtlinie erstellen](#create-a-policy) und [diese in einer Sammlung](#deploy-a-policy) bereitstellen.

- **Wiederherstellungsdienst:** Diese Serverkomponente empfängt BitLocker-Wiederherstellungsdaten von Clients. Weitere Informationen finden Sie unter [Wiederherstellungsdienst](#recovery-service).

Führen Sie folgende Schritte vor dem Erstellen und Bereitstellen von BitLocker-Verwaltungsrichtlinien aus:

- Überprüfen der [Voraussetzungen](../../plan-design/bitlocker-management.md#prerequisites)

- Bei Bedarf, [Verschlüsseln der Wiederherstellungsschlüssel](encrypt-recovery-data.md) in der Standortdatenbank

## <a name="create-a-policy"></a>Erstellen einer Richtlinie

Wenn Sie diese Richtlinie erstellen und bereitstellen, aktiviert der Konfigurations-Manager-Client den BitLocker-Verwaltungs-Agent auf dem Gerät.

> [!NOTE]
> Wenn Sie eine BitLocker-Verwaltungsrichtlinie erstellen möchten, benötigen Sie in Configuration Manager die Rolle **Hauptadministrator**.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, erweitern Sie **Endpoint Protection**, und wählen Sie den Knoten **BitLocker-Verwaltung** aus.

1. Klicken Sie im Menüband auf **BitLocker-Verwaltungssteuerungsrichtlinie erstellen**.

1. Geben Sie auf der Seite **Allgemein** einen Namen und optional eine Beschreibung ein. Wählen Sie die Komponenten aus, die auf Clients mit dieser Richtlinie aktiviert werden sollen:  

    - **Operating System Drive** (Betriebssystemlaufwerk): Steuert, ob das Betriebssystemlaufwerk verschlüsselt ist

    - **Festplattenlaufwerk:** Verwaltet die Verschlüsselung für zusätzliche Datenlaufwerke auf einem Gerät

    - **Wechseldatenträger:** Verwaltet die Verschlüsselung für Laufwerke, die Sie von einem Gerät entfernen können, z. B. USB-Schlüssel

    - **Client Management** (Clientverwaltung): Dient zum Verwalten der Sicherung von Informationen zur BitLocker-Laufwerkverschlüsselung des Schlüsselwiederherstellungsdiensts  

1. Konfigurieren Sie auf der Seite **Setup** die folgenden globalen Einstellungen für die BitLocker-Laufwerkverschlüsselung:

    > [!NOTE]
    > Configuration Manager wendet diese Einstellungen an, wenn Sie BitLocker aktivieren. Ist das Laufwerk bereits verschlüsselt oder wird es gerade ausgeführt, wird durch eine Änderung der Richtlinieneinstellungen die Laufwerkverschlüsselung auf dem Gerät nicht geändert.
    >
    > Wenn Sie diese Einstellungen deaktivieren oder nicht konfigurieren, verwendet BitLocker die Standardverschlüsselungsmethode (AES, 128 Bit).

    - Aktivieren Sie für Windows 8.1-Geräte die Option für die **Verschlüsselungsmethode und die Verschlüsselungsstärke für Laufwerke**. Wählen Sie dann die Verschlüsselungsmethode aus.

    - Aktivieren Sie für Windows 10-Geräte die Option für die **Verschlüsselungsmethode und die Verschlüsselungsstärke für Laufwerke (Windows 10)** . Wählen Sie anschließend jeweils die Verschlüsselungsmethode für Betriebssystemlaufwerke, Festplattenlaufwerke und Wechseldatenträger aus:

    Weitere Informationen zu diesen und anderen Einstellungen auf dieser Seite finden Sie unter [Einstellungsreferenz für BitLocker – Setup](../../tech-ref/bitlocker/settings.md#setup).

1. Geben Sie auf der Seite **Operating System Drive** (Betriebssystemlaufwerk) die folgenden Einstellungen an:  

    - **Operating System Drive Encryption Settings** (Verschlüsselungseinstellungen des Betriebssystemlaufwerks): Wenn Sie diese Einstellung aktivieren, muss der Benutzer das Betriebssystemlaufwerk schützen, und BitLocker verschlüsselt das Laufwerk. Wenn Sie sie deaktivieren, kann der Benutzer das Laufwerk nicht schützen.  

    Auf Geräten mit kompatiblem TPM können zwei Typen von Authentifizierungsmethoden beim Systemstart verwendet werden, um verschlüsselte Daten zusätzlich zu schützen. Beim Starten des Computers kann nur das TPM zur Authentifizierung verwendet werden, oder es kann zusätzlich die Eingabe einer persönlichen Identifikationsnummer (PIN) angefordert werden. Konfigurieren Sie die folgenden Einstellungen:

    - **Select protector for operating system drive** (Schutzkomponente für Betriebssystemlaufwerk auswählen): Wählen Sie aus, ob TPM und PIN oder nur TPM verwendet werden soll.

    - **Minimale PIN-Länge für Systemstart konfigurieren**: Wenn Sie eine PIN anfordern, ist dieser Wert die kürzeste Länge, die der Benutzer angeben kann. Der Benutzer gibt diese PIN ein, wenn der Computer hochfährt, um das Laufwerk zu entsperren. Die Standardeinstellung für die minimale PIN-Länge ist `4`.

    Weitere Informationen zu diesen und anderen Einstellungen auf dieser Seite finden Sie unter [Einstellungsreferenz – Betriebssystemlaufwerk](../../tech-ref/bitlocker/settings.md#os-drive).

1. Geben Sie auf der Seite **Fixed Drive** (Festplattenlaufwerk) die folgenden Einstellungen an:

    - **Fixed data drive encryption** (Verschlüsselung für Festplattenlaufwerke): Wenn Sie diese Einstellung aktivieren, fordert BitLocker den Schutz aller Festplattenlaufwerke an. Anschließend werden die Laufwerke von BitLocker verschlüsselt. Wenn Sie diese Richtlinie aktivieren, aktivieren Sie entweder die automatische Entsperrung oder die Einstellungen für eine **Kennwortrichtlinie für Festplattenlaufwerke**.

    - **Configure auto-unlock for fixed data drive** (Automatische Entsperrung für Festplattenlaufwerk konfigurieren): Hiermit wird BitLocker das automatische Entsperren aller verschlüsselter Laufwerke gestattet oder vorgegeben. Für die automatische Entsperrung ist es auch erforderlich, dass BitLocker das Betriebssystemlaufwerk verschlüsselt.

    Weitere Informationen zu diesen und anderen Einstellungen auf dieser Seite finden Sie unter [Einstellungsreferenz – Festplattenlaufwerk](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. Geben Sie auf der Seite **Removable Drive** (Wechseldatenträger) die folgenden Einstellungen an:

    - **Removable data drive encryption** (Verschlüsselung für Wechseldatenträger): Wenn Sie diese Einstellung aktivieren und Benutzern die Anwendung des BitLocker-Schutzes erlauben, speichert der Konfigurations-Manager-Client Wiederherstellungsinformationen zu den Wechseldatenträgern im Wiederherstellungsdienst auf dem Verwaltungspunkt. Dadurch können Benutzer das Laufwerk wiederherstellen, wenn sie das Kennwort der Schutzvorrichtung vergessen oder verloren haben.

    - **Benutzer können BitLocker-Schutz auf Wechseldatenträger anwenden:** Benutzer können den BitLocker-Schutz für einen Wechseldatenträger aktivieren.

    - **Removable data drive password policy** (Kennwortrichtlinie für Wechseldatenträger): Mit diesen Einstellungen legen Sie die Einschränkungen für Kennwörter fest, die zum Entsperren von Wechseldatenträgern mit BitLocker-Schutz verwendet werden.

    Weitere Informationen zu diesen und anderen Einstellungen auf dieser Seite finden Sie unter [Einstellungsreferenz – Wechseldatenträger](../../tech-ref/bitlocker/settings.md#removable-drive).

1. Geben Sie auf der Seite **Clientverwaltung** die folgenden Einstellungen an:

    > [!IMPORTANT]
    > Wenn Sie über keinen Verwaltungspunkt mit einer HTTPS-fähigen Website verfügen, sollten Sie diese Einstellung nicht konfigurieren. Weitere Informationen finden Sie unter [Wiederherstellungsdienst](#recovery-service).

    - **BitLocker-Verwaltungsdienste konfigurieren:** Wenn Sie diese Einstellung aktivieren, sichert Configuration Manager die Schlüsselwiederherstellungsinformationen automatisch und ohne Meldung in der Standortdatenbank. Wird diese Einstellung deaktiviert oder nicht konfiguriert, speichert Configuration Manager die Schlüsselwiederherstellungsinformationen nicht.

        - **Select BitLocker recovery information to store** (Zu speichernde BitLocker-Wiederherstellungsinformationen auswählen): Konfigurieren Sie diese Einstellung so, dass ein Wiederherstellungskennwort und ein Schlüsselpaket oder nur ein Wiederherstellungskennwort verwendet werden.

        - **Speicherung von Wiederherstellungsinformationen im Nur-Text-Format zulassen:** Ohne Verschlüsselungszertifikat für die BitLocker-Verwaltung speichert Configuration Manager die Schlüsselwiederherstellungsinformationen im Nur-Text-Format. Weitere Informationen finden Sie unter [Verschlüsseln von Wiederherstellungsdaten](encrypt-recovery-data.md).

    Weitere Informationen zu diesen und anderen Einstellungen auf dieser Seite finden Sie unter [Einstellungsreferenz – Clientverwaltung](../../tech-ref/bitlocker/settings.md#client-management).

1. Schließen Sie den Assistenten ab.

Wenn Sie die Einstellungen einer vorhandenen Richtlinie ändern möchten, wählen Sie diese in der Liste aus, und klicken Sie auf **Eigenschaften**.

Wenn Sie mehr als eine Richtlinie erstellen, können Sie ihre relative Priorität konfigurieren. Wenn Sie mehrere Richtlinien auf einem Client bereitstellen, werden anhand des Prioritätswerts die Einstellungen bestimmt.

## <a name="deploy-a-policy"></a>Bereitstellen einer Richtlinie

1. Wählen Sie im Knoten **BitLocker-Verwaltung** eine vorhandene Richtlinie aus. Klicken Sie im Menüband auf **Bereitstellen**.

1. Wählen Sie eine Gerätesammlung als Bereitstellungsziel aus.

1. Wenn Sie möchten, dass die Gerätelaufwerke jederzeit potenziell verschlüsselt oder entschlüsselt werden können, aktivieren Sie die Option **Wiederherstellung außerhalb des Wartungsfensters zulassen**. Wenn die Sammlung über Wartungsfenster verfügt, wird diese BitLocker-Richtlinie dennoch korrigiert.

1. Konfigurieren Sie für den Zeitplan die Option **Einfach** oder **Benutzerdefiniert**. Standardmäßig wertet der Client alle 12 Stunden seine Konformität mit dieser Richtlinie aus.

1. Klicken Sie auf **OK**, um die Richtlinie bereitzustellen.

Sie können mehrere Bereitstellungen mit derselben Richtlinie erstellen. Wenn Sie weitere Informationen zu den einzelnen Bereitstellungen aufrufen möchten, wählen Sie die Richtlinie im Knoten **BitLocker-Verwaltung** aus, und wechseln Sie dann im Detailbereich zur Registerkarte **Bereitstellungen**.

## <a name="monitor"></a>Überwachen

Im Detailbereich des Knotens **BitLocker-Verwaltung** können Sie sich grundlegende Konformitätsstatistiken zur Richtlinienbereitstellung ansehen:

- Anzahl konformer Elemente
- Fehleranzahl
- Anzahl bei Nichtkonformität

Wechseln Sie zur Registerkarte **Bereitstellungen**, um den Konformitätsprozentsatz und die empfohlene Aktion aufzurufen. Wählen Sie die Bereitstellung aus, und klicken Sie dann im Menüband auf **Status anzeigen**. Durch diese Aktion wird die Ansicht auf den Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen** umgestellt. Ähnlich wie bei anderen Konfigurationsrichtlinienbereitstellungen wird in dieser Ansicht ein ausführlicherer Konformitätsstatus angezeigt.

Weitere Informationen dazu, warum Clients nicht mit der BitLocker-Verwaltungsrichtlinie konform sind, finden Sie unter [Codes für Nichtkonformität](../../tech-ref/bitlocker/non-compliance-codes.md).

Weitere Informationen zur Problembehandlung finden Sie unter [Problembehandlung für BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

Verwenden Sie zur Überwachung und Problembehandlung folgende Protokolle:

### <a name="client-logs"></a>Clientprotokolle

- MBAM-Ereignisprotokoll: Navigieren Sie in der Windows-Ereignisanzeige zu „Anwendungen und Dienste“ > „Microsoft“ > „Windows“ > „MBAM“  Weitere Informationen finden Sie unter [BitLocker-Ereignisprotokolle](../../tech-ref/bitlocker/about-event-logs.md) und [Clientereignisprotokolle](../../tech-ref/bitlocker/client-event-logs.md).

- **BitlockerMangementHandler.log** im Pfad der Clientprotokolle, standardmäßig `%WINDIR%\CCM\Logs`

### <a name="management-point-logs-recovery-service"></a>Verwaltungspunktprotokolle (Wiederherstellungsdienst)

- Ereignisprotokoll des Wiederherstellungsdiensts: Navigieren Sie in der Windows-Ereignisanzeige zu „Anwendungen und Dienste“ > „Microsoft“ > „Windows“ > „MBAM-Web“ Weitere Informationen finden Sie unter [BitLocker-Ereignisprotokolle](../../tech-ref/bitlocker/about-event-logs.md) und [Serverereignisprotokolle](../../tech-ref/bitlocker/server-event-logs.md).

- Ablaufverfolgungsprotokolle für Recovery Service: `<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Wiederherstellungsdienst

Der BitLocker-Wiederherstellungsdienst ist eine Serverkomponente, die BitLocker-Wiederherstellungsdaten von Konfigurations-Manager-Clients empfängt. Der Wiederherstellungsdienst wird vom Standort bereitgestellt, wenn Sie eine BitLocker-Verwaltungsrichtlinie erstellen. Configuration Manager installiert den Wiederherstellungsdienst automatisch auf jedem Verwaltungspunkt mit einer HTTPS-fähigen Website.

Configuration Manager speichert diese Wiederherstellungsinformationen in der Standortdatenbank. Ohne Verschlüsselungszertifikat für die BitLocker-Verwaltung speichert Configuration Manager die Schlüsselwiederherstellungsinformationen im Nur-Text-Format.

Weitere Informationen finden Sie unter [Verschlüsseln von Wiederherstellungsdaten](encrypt-recovery-data.md).

## <a name="migration-considerations"></a>Migrationsüberlegungen

Wenn Sie zurzeit Microsoft BitLocker Administration and Monitoring (MBAM) verwenden, können Sie die Verwaltung nahtlos zu Configuration Manager migrieren. Beim Bereitstellen von BitLocker-Verwaltungsrichtlinien in Configuration Manager werden von Clients automatisch Wiederherstellungsschlüssel und Pakete in den Configuration Manager-Wiederherstellungsdienst hochgeladen.

> [!IMPORTANT]
> Wenn Sie von einer eigenständigen MBAM-Bereitstellung zur Configuration Manager-BitLocker-Verwaltung migrieren und Funktionen der eigenständigen MBAM-Bereitstellung benötigen, dürfen Sie keine eigenständigen MBAM-Server oder -Komponenten für die Configuration Manager-BitLocker-Verwaltung wiederverwenden. Wenn Sie diese Server wiederverwenden, funktioniert die eigenständige MBAM-Bereitstellung nicht mehr, wenn die Komponenten der Configuration Manager-BitLocker-Verwaltung auf diesen Servern installiert werden. Führen Sie unter keinen Umständen das Skript „MBAMWebSiteInstaller.ps1“ aus, um die BitLocker-Portale auf eigenständigen MBAM-Servern einzurichten. Für das Setup der Configuration Manager-BitLocker-Verwaltung sollten Sie separate Server verwenden.

### <a name="group-policy"></a>Gruppenrichtlinie

- Die Einstellungen für die BitLocker-Verwaltung sind vollständig mit den MBAM-Gruppenrichtlinieneinstellungen kompatibel. Wenn Geräte sowohl Gruppenrichtlinieneinstellungen als auch Configuration Manager-Richtlinien erhalten, sollten Sie diese so konfigurieren, dass sie übereinstimmen.

- Configuration Manager implementiert nicht alle MBAM-Gruppenrichtlinieneinstellungen. Wenn Sie zusätzliche Einstellungen der Gruppenrichtlinie konfigurieren, werden diese vom BitLocker-Verwaltungs-Agent auf Konfigurations-Manager-Clients berücksichtigt.

### <a name="tpm-password-hash"></a>TPM-Kennworthash

- In früheren Versionen des MBAM-Clients wird der TPM-Kennworthash nicht in Configuration Manager hochgeladen. Der Client lädt den TPM-Kennworthash nur einmal hoch.

- Wenn Sie diese Informationen zum Configuration Manager-Wiederherstellungsdienst migrieren müssen, löschen Sie das TPM auf dem Gerät. Nach dem Neustart wird der neue TPM-Kennworthash in den Wiederherstellungsdienst hochgeladen.

### <a name="re-encryption"></a>Erneute Verschlüsselung

Wenn Laufwerke bereits mit der BitLocker-Laufwerkverschlüsselung geschützt sind, werden diese von Configuration Manager nicht noch einmal verschlüsselt. Wenn Sie eine BitLocker-Verwaltungsrichtlinie bereitstellen, die nicht dem aktuellen Schutz des Laufwerks entspricht, wird diese als nicht konform gemeldet. Das Gerät bleibt weiterhin geschützt.

Angenommen, Sie haben ein Gerät mit MBAM ohne PIN-Schutz verschlüsselt, obwohl die Configuration Manager-Richtlinie eine PIN erfordert. Das Laufwerk ist nicht mit der Richtlinie konform, obwohl das Laufwerk verschlüsselt ist.

Als Problemumgehung müssen Sie zuerst BitLocker auf dem Gerät deaktivieren. Anschließend stellen Sie eine neue Richtlinie mit den neuen Einstellungen bereit.

## <a name="next-steps"></a>Nächste Schritte

[Einrichten von BitLocker-Portalen](setup-websites.md)
