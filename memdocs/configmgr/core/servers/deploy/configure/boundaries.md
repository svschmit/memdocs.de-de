---
title: Definieren von Grenzen
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie Netzwerkadressen in Ihrem Internet festlegen können. Diese können Geräte umfassen, die Sie verwalten möchten
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13312c20edbda290daaa0d51908adeb7ab4a6860
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700060"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Definieren von Netzwerkpfaden als Begrenzungsgruppen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Grenzen von Configuration Manager sind Netzwerkpfade in Ihrem Netzwerk, die Geräte enthalten können, die Sie verwalten möchten. Sie können verschiedene Arten von Grenzen erstellen, z. B. einen Active Directory-Standort oder eine IP-Netzwerkadresse. Wenn der Configuration Manager-Client eine ähnliche Netzwerkadresse identifiziert, ist dieses Gerät Teil der Grenze.

Configuration Manager unterstützt die folgenden Arten von Grenzen:

- IP-Subnetz
- Active Directory-Standort
- IPv6-Präfix
- IP-Adressbereich
- VPN (ab Version 2006)

Sie können manuell individuelle Grenzen erstellen oder die [Active Directory-Gesamtstrukturermittlung](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) verwenden. Diese Ermittlungsmethode sucht und erstellt automatisch Grenzen für IP-Subnetze und Active Directory-Standorte. Wenn die Active Directory-Gesamtstrukturermittlung ein Supernetz für einen Active Directory-Standort identifiziert, konvertiert Configuration Manager das Supernetz in eine Grenze vom Typ „IP-Adressbereich“.

Wenn ein Gerät sich nicht in der von Ihnen erwarteten Grenze befindet, liegt dies möglicherweise daran, dass Sie die Netzwerkadresse des Geräts nicht als Grenze definiert haben. Wenn Sie Zweifel in Bezug auf die Netzwerkadresse eines Geräts haben, führen Sie auf dem Gerät die folgenden Windows-Befehle aus, um die Adresse zu bestätigen:

- IP-Adresse: `ipconfig`
- Active Directory-Standort: `nltest /dsgetsite`
- VPN: `ipconfig /all`

## <a name="boundary-types"></a>Grenztypen

### <a name="ip-subnet"></a>IP-Subnetz

Der Typ „IP-Subnetz“ erfordert eine **Subnetz-ID**. Beispielsweise `169.254.0.0`. Wenn Sie die Werte für **Netzwerk** (Standardgateway) und **Subnetzmaske** angeben, berechnet Configuration Manager die **Subnetz-ID** automatisch. Wenn Sie die Grenze speichern, speichert Configuration Manager nur den Wert der Subnetz-ID.

> [!NOTE]
> Configuration Manager unterstützt die direkte Eingabe eines Supernetzes als Grenze nicht. Verwenden Sie stattdessen den Grenztyp IP-Adressbereich.

### <a name="active-directory-site"></a>Active Directory-Standort

Für den Grenztyp **Active Directory-Standort** geben Sie den Standortnamen an. Sie können den Namen eingeben oder in der lokalen Gesamtstruktur des Standortservers nach einem Namen suchen.

Wenn Sie einen Active Directory-Standort als Grenze angeben, umfasst die Grenze alle IP-Subnetze, die Mitglieder dieses Active Directory-Standorts sind. Wenn die Konfiguration des Active Directory-Standorts in Active Directory geändert wird, werden auch die in dieser Grenze enthaltenen Netzwerkorte geändert.  

Active Directory-Standortgrenzen funktionieren nicht für reine Azure Active Directory-Geräte, die auch als in die Clouddomäne eingebundene Geräte bezeichnet werden. Wenn diese Geräte in der lokalen Umgebung den Standort wechseln und Sie nur Grenzen vom Typ „Active Directory-Standort“ erstellen, befinden sich diese Geräte in keiner Grenze.

> [!TIP]
> Verwenden Sie den folgenden Windows-Befehl, um den aktuellen Active Directory-Standort eines Geräts anzuzeigen: `nltest /dsgetsite`.
>
> Um zu ermitteln, ob ein Client in die Clouddomäne eingebunden ist, führen Sie den folgenden Windows-Befehl aus: `dsregcmd /status`. Weitere Informationen finden Sie unter [dsregcmd-Befehl – Gerätestatus](/azure/active-directory/devices/troubleshoot-device-dsregcmd).

### <a name="ipv6-prefix"></a>IPv6-Präfix

Für den Grenztyp **IPv6-Präfix** geben Sie ein **Präfix** an. Beispielsweise `2001:1111:2222:3333`.

### <a name="ip-address-range"></a>IP-Adressbereich

Beim Grenztyp **IP-Adressbereich** geben Sie die **IP-Startadresse** und die **IP-Endadresse** für den Bereich an. Der Bereich kann einen Teil eines IP-Subnetzes oder mehrere IP-Subnetze umfassen. Verwenden Sie den Grenztyp „IP-Adressbereich“, um ein Supernetz zu unterstützen.

Sie können diesen Typ auch zum Definieren einer Grenze für eine einzelne IP-Adresse verwenden. In diesem Fall legen Sie die IP-Startadresse und die IP-Endadresse auf denselben Wert fest. Diese Konfiguration kann für einmalige Geräte oder Testumgebungen nützlich sein.

### <a name="vpn"></a>VPN

<!--7020519-->

Ab Version 2006 können Sie einen Grenztyp für VPNs erstellen, um die Verwaltung von Remoteclients zu vereinfachen. Wenn ein Client eine Standortanforderung sendet, enthält diese zusätzliche Informationen zur Netzwerkkonfiguration des Clients. Basierend auf diesen Informationen bestimmt der Server, ob sich der Client in einem VPN befindet. Verbinden Sie das Gerät mit dem VPN, damit Configuration Manager den Client in der Grenze zuordnen kann.

Sie können VPN-Grenzen auf unterschiedliche Weise konfigurieren:

- **VPN automatisch ermitteln**: Configuration Manager erkennt jede VPN-Lösung, die das Point-to-Point-Tunneling-Protokoll (PPTP) verwendet. Wenn Ihr VPN nicht erkannt wird, verwenden Sie eine der anderen Optionen. Der Begrenzungswert in der Konsolenliste ist `Auto:On`.

- **Verbindungsname:** Geben Sie den Namen der VPN-Verbindung auf dem Gerät an. Dies ist unter Windows der Name des Netzwerkadapters für die VPN-Verbindung. Configuration Manager gleicht die ersten 250 Zeichen der Zeichenfolge ab, unterstützt jedoch keine Platzhalterzeichen oder Teilzeichenfolgen. Der Begrenzungswert in der Konsolenliste ist `Name:<name>`, wobei `<name>` der von Ihnen angegebene Verbindungsname ist.

  Angenommen, Sie führen den Befehl `ipconfig` auf dem Gerät aus, und einer der Abschnitte beginnt mit: `PPP adapter ContosoVPN:`. Verwenden Sie die Zeichenfolge `ContosoVPN` als **Verbindungsnamen**. Er wird in der Liste als `Name:CONTOSOVPN` angezeigt.

- **Verbindungsbeschreibung**: Geben Sie die Beschreibung der VPN-Verbindung an. Configuration Manager gleicht die ersten 243 Zeichen der Zeichenfolge ab, unterstützt jedoch keine Platzhalterzeichen oder Teilzeichenfolgen. Der Begrenzungswert in der Konsolenliste ist `Description:<description>`, wobei `<description>` die von Ihnen angegebene Verbindungsbeschreibung ist.

  Angenommen, Sie führen den Befehl `ipconfig /all` auf dem Gerät aus, und einer der Abschnitte enthält die folgende Zeile: `Description . . . . . . . . . . . : ContosoMainVPN`. Verwenden Sie die Zeichenfolge `ContosoMainVPN` als **Verbindungsbeschreibung**. Sie wird in der Liste als `Description:CONTOSOMAINVPN` angezeigt.

> [!IMPORTANT]
> Wenn Sie dieses Feature nach der Aktualisierung des Standorts voll nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Wenn Sie den Standort und die Konsole aktualisieren, wird die neue Funktionalität in der Configuration Manager-Konsole angezeigt. Das gesamte Szenario funktioniert erst, wenn auch die Clientversion aktuell ist.
>
> Wenn Sie diese VPN-Begrenzung während einer Betriebssystembereitstellung verwenden möchten, müssen Sie auch das Startimage aktualisieren, sodass es die neuesten Clientbinärdateien enthält.

## <a name="create-a-boundary"></a>Erstellen einer Grenze

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Hierarchiekonfiguration**, und klicken Sie auf den Knoten **Grenzen**.

1. Wählen Sie im Menüband auf der Registerkarte **Start** in der Gruppe **Erstellen** die Option **Grenze erstellen** aus.

1. Geben Sie auf der Registerkarte **Allgemein** des Fensters **Grenze erstellen** die folgenden Informationen an:

    - **Beschreibung:** Identifizieren Sie die Grenze anhand eines Anzeigenamens oder Verweises.

        > [!NOTE]
        > Configuration Manager benennt die Grenze automatisch basierend auf Typ und Gültigkeitsbereich. Sie können den Namen nicht ändern.

    - **Typ:** Wählen Sie den Typ der zu erstellenden Grenze aus. Geben Sie dann weitere Informationen an, die für den Typ erforderlich sind. Weitere Informationen finden Sie unter [Grenztypen](#boundary-types).

1. Wechseln Sie zur Registerkarte **Begrenzungsgruppen**. Wenn im Standort bereits Begrenzungsgruppen vorhanden sind, können Sie die neue Grenze sofort zu einer oder mehreren Gruppen hinzufügen.

1. Klicken Sie auf **OK**, um die neue Grenze zu speichern.

## <a name="configure-a-boundary"></a>Konfigurieren einer Grenze

> [!TIP]
> Wenn Sie eine Grenze erstellen, weist Configuration Manager ihr automatisch einen Namen zu, der auf dem Typ und Gültigkeitsbereich der Grenze basiert. Sie können diesen Namen nicht ändern. Geben Sie eine Beschreibung ein, anhand derer Sie die Grenze in der Configuration Manager-Konsole identifizieren können.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Hierarchiekonfiguration**, und klicken Sie auf den Knoten **Grenzen**.

1. Wählen Sie die Grenze aus, die Sie ändern möchten. Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Eigenschaften** auf **Eigenschaften**.

1. Im Fenster **Eigenschaften** für die Grenze auf der Registerkarte **Allgemein** können Sie die folgenden Einstellungen konfigurieren:

    - Bearbeiten Sie die **Beschreibung**.
    - Ändern Sie den **Typ** der Grenze.
    - Ändern Sie den Gültigkeitsbereich einer Grenze durch Bearbeiten der Netzwerkadressen. Sie können beispielsweise für eine Active Directory-Standortgrenze einen neuen Active Directory-Standortnamen angeben.

1. Wechseln Sie zur Registerkarte **Standortsysteme**, um die Standortsysteme anzuzeigen, die dieser Grenze zugeordnet sind. Sie können diese Konfiguration nicht über die Eigenschaften einer Grenze ändern.

    > [!TIP]
    > Damit ein Server als Standortsystem für eine Grenze aufgeführt werden kann, ordnen Sie den Server als Standortsystemserver für mindestens eine Begrenzungsgruppe zu, in der diese Grenze enthalten ist. Diese Konfiguration erfolgt auf der Registerkarte **Referenzen** einer Begrenzungsgruppe. Weitere Informationen finden Sie unter [Konfigurieren der Standortzuweisung und Auswählen von Standortsystemservern](boundary-group-procedures.md#bkmk_references).

1. Um die Begrenzungsgruppenmitgliedschaft für diese Grenze zu ändern, wählen Sie die Registerkarte **Begrenzungsgruppen** aus:

    - Klicken Sie zum Hinzufügen der Grenze zu einer oder mehreren Begrenzungsgruppen auf **Hinzufügen**. Wählen Sie mindestens eine Begrenzungsgruppe aus, und klicken Sie auf **OK**.

    - Wenn Sie diese Grenze aus einer Begrenzungsgruppe entfernen möchten, wählen Sie die Begrenzungsgruppe aus, und klicken Sie auf **Entfernen**.

1. Klicken Sie auf **OK**, um die Eigenschaften der Grenze zu schließen und die Konfiguration zu speichern.

## <a name="next-steps"></a>Nächste Schritte

Jede Grenze kann von jedem Standort in Ihrer Hierarchie verwendet werden. Fügen Sie eine Grenze nach dem Erstellen zu mindestens einer [Begrenzungsgruppe](boundary-groups.md) hinzu.