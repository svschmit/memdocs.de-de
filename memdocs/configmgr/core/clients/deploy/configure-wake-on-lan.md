---
title: Konfigurieren von Wake-On-LAN
titleSuffix: Configuration Manager
description: Wählen Sie Wake-On-LAN-Einstellungen in Configuration Manager aus.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 512d942d79d11178f010c4f0adb41a25ee432743
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694118"
---
# <a name="how-to-configure-wake-on-lan-in-configuration-manager"></a>Konfigurieren von Wake-On-LAN in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Legen Sie Wake-On-LAN-Einstellungen für Configuration Manager fest, wenn Sie Computer aus dem Energiesparmodus reaktivieren möchten.

## <a name="wake-on-lan-starting-in-version-1810"></a><a name="bkmk_wol-1810"></a> Wake-On-LAN ab Version 1810
<!--3607710-->
Ab Configuration Manager 1810 gibt es eine neue Möglichkeit, Computer aus dem Energiesparmodus zu reaktivieren. Mithilfe der Configuration Manager-Konsole können Sie Clients reaktivieren, auch wenn sich der Client nicht im selben Subnetz wie der Standortserver befindet. Wenn Sie Wartungen durchführen oder Geräte abfragen müssen, sind Sie nicht durch Remoteclients eingeschränkt, die sich im Ruhezustand befinden. Der Standortserver verwendet den Clientbenachrichtigungskanal, um andere Clients zu identifizieren, die im gleichen Remotesubnetz aktiv sind. Diese Clients werden dann verwendet, um eine Wake-On-LAN-Anforderung (Magic Packet) zu senden. Durch die Verwendung des Clientbenachrichtigungskanals wird MAC-Flapping vermieden, das dazu führen könnte, dass der Port vom Router heruntergefahren wird. Die neue Version von Wake-On-LAN kann gleichzeitig mit der [älteren Version](#bkmk_wol-previous) aktiviert werden.

### <a name="limitations"></a>Einschränkungen

- Es muss mindestens ein Client im Zielsubnetz aktiv sein.
- Die folgenden Netzwerktechnologien werden von diesem Feature nicht unterstützt:
   - IPv6
   - 802.1x-Netzwerkauthentifizierung
    >[!NOTE]
    > Die 802.1x-Netzwerkauthentifizierung kann je nach Hardware und deren Konfiguration mit zusätzlicher Konfiguration funktionieren.
- Computer werden nur reaktiviert, wenn Sie sie durch die Clientbenachrichtigung **Reaktivieren** benachrichtigen.
    - Für die Reaktivierung an einem Stichtag wird die ältere Version von Wake-On-LAN verwendet.
    -  Wenn die ältere Version nicht aktiviert ist, erfolgt keine Reaktivierung von Clients für Bereitstellungen, die mit den Einstellungen **Wake-On-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren** oder **Aktivierungspakete senden** erstellt wurden.  

> [!IMPORTANT]
> Es wird empfohlen, die Wake-On-LAN-Funktion nur auf einer begrenzten Anzahl von Geräten gleichzeitig (100) zu verwenden.
>
> Wenn Sie die Wake-On-LAN-Funktion zum Reaktivieren von Computern über die Configuration Manager-Verwaltungskonsole verwenden, werden die Reaktivierungsanforderungen in eine interne Warteschlange gestellt, die gemeinsam mit anderen Funktionen für Echtzeitaktionen genutzt wird. Beispiele für diese anderen Funktionen sind die Ausführung von Skripts, cmpivot und andere Clientbenachrichtigungen über schnelle Kanäle. Je nach Leistung Ihrer Standortsysteme können die Reaktivierungsaktionen einen längeren Zeitraum in Anspruch nehmen und die jeweils andere Echtzeitaktion verzögern. Es wird empfohlen, nicht mehr als 100 Computer gleichzeitig zu reaktivieren. Wenn es in diesem Bereich zu einem Rückstand kommt, der zu Verzögerungen führen kann, können Sie im Verzeichnis „...\inboxes\objmgr.box“ prüfen, ob eine große Anzahl von Dateien mit der Erweiterung „.opa“ vorhanden ist.


### <a name="security-role-permissions"></a>Berechtigungen für Sicherheitsrollen

- **Benachrichtigen der Ressource** unter der Kategorie „Sammlung“

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>Konfigurieren der Clients für die Verwendung von Wake-On-LAN ab Version 1810

Bislang mussten Sie den Client in den Eigenschaften des Netzwerkadapters manuell für Wake-On-LAN aktivieren. Configuration Manager 1810 enthält eine neue Clienteinstellung namens **Netzwerkreaktivierung zulassen**. Konfigurieren und implementieren Sie diese Einstellung, anstatt die Eigenschaften des Netzwerkadapters zu ändern.

1. Rufen Sie unter **Verwaltung** die **Clienteinstellungen** auf.
1. Wählen Sie die Clienteinstellungen aus, die Sie bearbeiten möchten, oder erstellen Sie neue benutzerdefinierte Clienteinstellungen für die Bereitstellung. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](configure-client-settings.md).
1. Wählen Sie unter den **Energieverwaltungseinstellungen** des Clients für die Einstellung **Netzwerkreaktivierung zulassen** die Option **Aktivieren** aus. Weitere Informationen zu dieser Einstellung finden Sie unter [Informationen zu Clienteinstellungen](about-client-settings.md#power-management).

4. Ab Configuration Manager 1902 berücksichtigt die neue Version von Wake-On-LAN den benutzerdefinierten UDP-Port, den Sie für die [Clienteinstellung](about-client-settings.md#power-management) **Wake-On-LAN-Portnummer (UDP)** angeben. Diese Einstellung wird sowohl von der neuen als auch von der älteren Version von Wake-On-LAN verwendet.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>Reaktivieren eines Clients mit der Clientbenachrichtigung ab 1810
 
Sie können einen einzelnen Client oder alle inaktiven Clients in einer Sammlung reaktivieren. Für Geräte in der Sammlung, die bereits aktiv sind, wird keine Aktion ausgeführt. Nur an Clients im Energiesparmodus wird eine Wake-On-LAN-Anforderung gesendet. Weitere Informationen zum Benachrichtigen eines Clients, um ihn zu reaktivieren, finden Sie unter [Clientbenachrichtigung](../manage/client-notification.md).

- **Reaktivieren eines einzelnen Clients:** Klicken Sie mit der rechten Maustaste auf den Client, gehen Sie zu **Clientbenachrichtigung**, und wählen Sie dann **Reaktivieren**.

   ![Clientbenachrichtigung „Reaktivieren“ in der Konsole](media/wol-wake-up-client-notification.png)

- **Reaktivieren aller Clients im Energiesparmodus in einer Sammlung:** Klicken Sie mit der rechten Maustaste auf die Gerätesammlung, gehen Sie zu **Clientbenachrichtigung**, und wählen Sie dann **Reaktivieren**.
   - Diese Aktion kann nicht für integrierte Sammlungen ausgeführt werden.
   - Wenn Sie eine Mischung aus inaktiven und aktiven Clients in einer Sammlung haben, wird eine Wake-On-LAN-Anforderung nur an die Clients im Energiesparmodus gesendet.
   - Ab Configuration Manager 2002 ist diese Aktion in einer Konsole verfügbar, die mit einem Standort der zentralen Verwaltung, einem eigenständigen Standort oder einem untergeordneten primären Standort verbunden ist.
   - Bis Version 1910 ist diese Aktion nur aktiv, wenn die Configuration Manager-Konsole mit einem eigenständigen oder untergeordneten primären Standort verbunden ist. Bei einer Verbindung mit einem Standort der zentralen Verwaltung ist diese Aktion nicht verfügbar.

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>Was ist zu erwarten, wenn nur die neue Version von Wake-On-LAN aktiviert ist?

Wenn Sie nur die neue Version von Wake-On-LAN aktiviert haben, ist nur die Clientbenachrichtigung **Reaktivieren** verfügbar. Clients erhalten keine Benachrichtigung, wenn ein Stichtag für Bereitstellungen wie Tasksequenzen, Softwareverteilung oder die Installation von Softwareupdates gilt. Wenn ein Computer nach dem Energiesparmodus wieder online ist, wird er in der Konsole angezeigt, sobald er beim Verwaltungspunkt eincheckt.

Ab Configuration Manager-Version 1902 können Sie den Wake-On-LAN-Port angeben. Diese Einstellung wird sowohl von der neuen als auch von der älteren Version von Wake-On-LAN verwendet.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>Was ist zu erwarten, wenn beide Versionen von Wake-On-LAN aktiviert sind?

Wenn Sie beide Versionen von Wake-On-LAN aktiviert haben, können Sie die Clientbenachrichtigung **Reaktivieren** verwenden und zum Stichtag reaktivieren. Die Clientbenachrichtigung funktioniert etwas anders als herkömmliches Wake-On-LAN. Eine kurze Erklärung der Funktionsweise der Clientbenachrichtigung finden Sie im Abschnitt [Wake-On-LAN ab Version 1810](#bkmk_wol-1810). Die neue Clienteinstellung **Netzwerkreaktivierung zulassen** ändert die NIC-Eigenschaften, um Wake-On-LAN zu ermöglichen. Sie müssen sie nicht mehr manuell ändern, wenn Ihrer Umgebung neue Computer hinzugefügt werden. Alle weiteren Funktionen von Wake-On-LAN wurden nicht geändert.

Ab Version 1902 berücksichtigt die Clientbenachrichtigung **Reaktivieren** Ihre vorhandene Einstellung für **Wake-On-LAN-Portnummer (UDP)** .


## <a name="wake-on-lan-for-version-1806-and-earlier"></a><a name="bkmk_wol-previous"></a> Wake-On-LAN für Versionen bis 1806

Geben Sie Einstellungen für Wake-On-LAN für Configuration Manager an, wenn Sie Computer aus dem Standbymodus reaktivieren möchten, um die erforderliche Software (Softwareupdates, Anwendungen, Tasksequenzen, Programme usw.) zu installieren.

Sie können Wake-On-LAN erweitern, indem Sie die Clienteinstellungen für den Aktivierungsproxy nutzen. Zum Nutzen des Aktivierungsproxys müssen Sie jedoch zuerst Wake-On-LAN für den Standort aktivieren und **Nur Aktivierungspakete verwenden** sowie die Option **Unicast** für die Wake-On-LAN-Übertragungsmethode angeben. Bei dieser Aktivierungslösung werden auch Ad-hoc-Verbindungen unterstützt, z. B. eine Remotedesktopverbindung.

Verwenden Sie das erste Verfahren, um einen primären Standort für Wake-On-LAN zu konfigurieren. Verwenden Sie das zweite Verfahren, um die Clienteinstellungen für den Aktivierungsproxy zu konfigurieren. Mithilfe des zweiten Verfahrens werden die Clientstandardeinstellungen für die Aktivierungsproxy-Einstellungen konfiguriert, die für alle Computer der Hierarchie gelten. Wenn diese Einstellungen nur auf ausgewählte Computer angewendet werden sollen, erstellen Sie eine benutzerdefinierte Geräteeinstellung und weisen diese einer Sammlung mit den Computern zu, die Sie für den Aktivierungsproxy konfigurieren möchten. Weitere Informationen zum Erstellen von benutzerdefinierten Geräteeinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen](../../../core/clients/deploy/configure-client-settings.md).

Ein Computer, der die Clienteinstellungen des Aktivierungsproxys erhält, wird seine Netzwerkverbindung wahrscheinlich für 1-3 Sekunden unterbrechen. Der Grund hierfür ist, dass der Client die Netzwerkschnittstellenkarte zurücksetzen muss, um den Treiber des Aktivierungsproxys zuzulassen.

> [!WARNING]
> Werten Sie den Aktivierungsproxy zur Vermeidung unerwarteter Störungen der Netzwerkdienste zuerst in einer isolierten und repräsentativen Netzwerkinfrastruktur aus. Verwenden Sie anschließend die benutzerdefinierten Clienteinstellungen, um den Test auf eine ausgewählte Gruppe von Computern in mehreren Subnetzen auszudehnen. Weitere Informationen zum Aktivierungsproxy finden Sie unter [Planen des Aufweckens von Clients](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Konfigurieren von Wake-On-LAN für einen Standort für Versionen bis einschließlich 1806

 Um Wake-On-LAN nutzen zu können, müssen Sie es für jeden Standort in einer Hierarchie aktivieren.

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung > Standortkonfiguration > Standorte**.
2. Klicken Sie zum Konfigurieren auf den primären Standort, und klicken Sie dann auf **Eigenschaften**.
3. Klicken Sie auf die Registerkarte **Wake-On-LAN**, und konfigurieren Sie die Optionen für diesen Standort. Stellen Sie zum Unterstützen des Aktivierungsproxys sicher, dass Sie die Optionen **Nur Aktivierungspakete verwenden** und **Unicast** aktivieren. Weitere Informationen finden Sie unter [Planen der Clientaktivierung](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Klicken Sie auf **OK**, und wiederholen Sie diesen Vorgang für alle primären Standorte in der Hierarchie.

![Aktivieren von Wake-On-LAN in den Standorteigenschaften](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>So konfigurieren Sie die Clienteinstellungen für den Aktivierungsproxy

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung > Clienteinstellungen**.
2. Klicken Sie auf **Clientstandardeinstellungen**, und klicken Sie auf **Eigenschaften**.
3. Wählen Sie **Energieverwaltung** aus, und wählen Sie dann für **Aktivierungsproxy zulassen**, **Ja** aus.
4. Überprüfen und konfigurieren Sie ggf. weitere Einstellungen für den Aktivierungsproxy. Weitere Informationen zu diesen Einstellungen finden Sie unter [Energieverwaltung](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Klicken Sie auf **OK**, um das Dialogfeld zu schließen, und klicken Sie dann erneut auf **OK**, um das Dialogfeld Clientstandardeinstellungen zu schließen.

Sie können die folgenden Wake-On-LAN-Berichte zum Überwachen der Installation und Konfiguration des Aktivierungsproxys verwenden:

- Zusammenfassung des Aktivierungsproxy-Bereitstellungszustands
- Details zum Aktivierungsproxy-Bereitstellungszustand

> [!TIP]
> Mit einer Verbindung zu einem Computer im Standbymodus können Sie testen, ob der Aktivierungsproxy funktioniert. Stellen Sie beispielsweise eine Verbindung mit einem freigegebenen Ordner auf diesem Computer her, oder versuchen Sie, per Remotedesktop eine Verbindung zu dem Computer herzustellen. Stellen Sie bei Verwendung von DirectAccess sicher, dass die IPv6-Präfixe funktionieren, indem Sie die gleichen Tests für einen Computer im Standbymodus durchführen, der sich momentan im Internet befindet.
