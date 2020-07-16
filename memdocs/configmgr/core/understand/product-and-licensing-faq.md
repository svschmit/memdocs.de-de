---
title: Häufig gestellte Fragen zum Produkt und zur Lizenzierung
titleSuffix: Configuration Manager
description: Finden Sie Antworten auf häufige Produkt- und Lizenzfragen zu Configuration Manager.
ms.date: 07/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ce9024fa610c6af19eb40ccf0da662a3e99234f
ms.sourcegitcommit: 01c1ca337e82c5e8e92153079ed89f79e20bde9e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86157823"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Häufig gestellte Fragen für die Configuration Manager-Verzweigungen und -Lizenzierungen

*Gilt für: Configuration Manager (Current Branch) und System Center Configuration Manager (Long-Term Servicing Branch)*

Diese FAQ beziehen sich auf häufige Lizenzierungsfragen über Versionen von Configuration Manager Current Branch und Long-Term Servicing Branch (LTSB), die durch Microsoft-Volumenlizenzierungsprogramme erhältlich sind. Dieser Artikel dient zu Informationszwecken. Die Dokumentation, die die Configuration Manager-Lizenzierung umfasst, wird weder abgelöst noch ersetzt. Weitere Informationen finden Sie unter [Produktbedingungen](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). Die Produktbedingungen beschreiben die Nutzungsbedingungen für alle Microsoft-Produkte im Rahmen der Volumenlizenzierung.

### <a name="whats-current-branch"></a><a name="bkmk_cb"></a> Was ist Current Branch?

Current Branch ist das produktionsbereites Build von Configuration Manager, der ein aktives Servicemodell bereitstellt. Dieses Dienstmodell entspricht der Erfahrung mit Windows 10. Dieser Ansatz unterstützt Kunden, die sich in einem „Cloudintervall“ bewegen und Innovationen schneller umsetzen möchten. Mit dem Current Branch-Dienstmodell werden Sie weiterhin neue Features und Funktionalitäten erhalten. Nur Kunden, die über eine aktive Software Assurance für Configuration Manager-Lizenzen oder über entsprechende Abonnementrechte verfügen, können die Current Branch-Option von Configuration Manager installieren und verwenden.

### <a name="whats-the-long-term-servicing-branch-ltsb"></a><a name="bkmk_ltsb"></a> Was ist Long Term Servicing Branch (LTSB)?  

LTSB ist eine produktionsbereite Version des Configuration Managers. Er dient den Kunden, die ihre Software Assurance-Rechte oder entsprechende Abonnementrechte auslaufen lassen. Im Vergleich zu Current Branch verfügt LTSB über [eingeschränkte Funktionalität](introduction-to-the-ltsb.md#features-that-arent-available). Kunden, die die Software Assurance oder entsprechende Abonnementrechte verfallen lassen, müssen Current Branch von Configuration Manager deinstallieren. Kunden, die über unbefristete Lizenzrechte für Configuration Manager verfügen, können den Build der LTSB-Version von der Version von Configuration Manager installieren und verwenden, die zum Zeitpunkt des Verfalls aktuell ist.

### <a name="what-do-the-acronyms-sa-and-lsa-mean-in-regard-to-configuration-manager"></a><a name="bkmk_licensing-acronyms"></a> Was bedeuten die Akronyme *SA* und *L&SA* in Bezug auf Configuration Manager?

**Software Assurance** und **Lizenz und Software Assurance** (L&SA) sind jeweils Lizenzoptionen, die Rechte zur Verwendung von Configuration Manager gewähren. SA ist eine Option für einen Kunden, der die SA-Abdeckung aus einer vorherigen Vereinbarung erneuert. L&SA ist eine Option für einen Kunden, der eine neue Lizenz- und SA-Abdeckung erwirbt.

- **Software Assurance (SA):** Kunden müssen über eine aktive SA für Configuration Manager-Lizenzen oder über entsprechende Abonnementrechte verfügen, um die Current Branch-Option von Configuration Manager zu installieren und zu verwenden.

  Während SA für einige Microsoft-Produkte optional ist, ist es die einzige Möglichkeit Rechte für die Verwendung von Current Branch in Configuration Manager *(oder entsprechende Abonnementrechte)* zu erhalten. Weitere Informationen finden Sie in den [Häufig gestellten Fragen zur Software Assurance](https://www.microsoft.com/licensing/licensing-programs/FAQ-Software-Assurance.aspx).

- **Microsoft-Lizenz und Software Assurance (L&SA):** Kunden, die neue Lizenzen für Configuration Manager kaufen, müssen L&SA (Lizenz und SA-Abdeckung) erwerben.

  - Die SA gewährt Rechte zur Verwendung von Current Branch.

  - Wenn Ihre SA abläuft, Sie jedoch noch eine Lizenz für Configuration Manager besitzen, können Sie Current Branch nicht mehr verwenden. Weitere Informationen finden Sie in den FAQ zu [Wenn mein SA abläuft, und ich L&SA hatte, was erhalte ich?](#bkmk_sa-expires)

Weitere Informationen zu Lizenzangeboten finden Sie unter [Optionen des Lizenzerwerbs](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs) und [Lizenzproduktbedingungen](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  

### <a name="what-are-equivalent-subscriptions"></a><a name="bkmk_equiv-sub"></a> Was sind *entsprechende Abonnements*?

Entsprechende Abonnements beziehen sich auf Programme wie [Enterprise Mobility + Security](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) oder [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise). Es kann andere geben, aber diese Programme sind die Häufigsten. In den Produktbedingungen der Microsoft-Volumenlizenzierung werden diese Programme als entsprechende Verwaltungslizenzen bezeichnet.

Configuration Manager ist in den folgenden Plänen enthalten:

- Intune-Benutzerabonnementlizenz (USL)
- EMS E3
- EMS E5
- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F1

<!-- Sources:
https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans
https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing
-->

> [!IMPORTANT]
> Configuration Manager ist nicht im [Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business)-Plan enthalten.

### <a name="what-changes-with-licensing-for-co-management-in-microsoft-endpoint-manager"></a><a name="bkmk_mem"></a> Was ändert sich durch die Lizenzierung für die Coverwaltung im Microsoft Endpoint Manager?

<!-- 7202432 -->

Durch die Coverwaltungslizenz können Configuration Manager-Kunden mit Software Assurance Intune-PC-Verwaltungsrechte verwenden, ohne zusätzliche Intune-Lizenzen erwerben und Benutzern zuweisen zu müssen. Diese Lizenz erleichtert Ihnen die Verwaltung von Windows-Geräten mit dem Microsoft Endpoint Manager.

- Geräte, die bereits von Configuration Manager verwaltet werden und die Sie bei Intune für die Coverwaltung registrieren, verfügen über fast die gleichen Rechte wie ein eigenständig verwalteter Intune-PC. Wenn Sie Windows auf diesem Gerät zurücksetzen, können Sie es nicht mit Windows Autopilot bereitstellen. Für Autopilot benötigen Sie die Vollversion einer Intune-Lizenz.

- Wenn Sie ein Windows 10-Gerät auf andere Weise bei Intune registrieren, ist weiterhin die Vollversion einer Intune-Lizenz erforderlich. Sie können Autopilot beispielsweise zur Bereitstellung eines Geräts verwenden, oder ein Benutzer kann diesen Dienst nutzen, um sich manuell selbst zu registrieren.

- Damit vorhandene von Configuration Manager verwaltete Geräte bei Intune für die Coverwaltung im großen Stil registriert werden können, verwendet die Coverwaltung ein Azure Active Directory-Feature (Azure AD) zur automatischen Registrierung für Windows 10. Für die automatische Registrierung bei der Co-Verwaltung sind Lizenzen für Azure AD Premium (AADP1) und Intune erforderlich. Seit dem 1. Dezember 2019 müssen Sie für dieses Szenario keine einzelnen Intune-Lizenzen mehr zuweisen. Der Microsoft Endpoint Manager enthält nun die Intune-Lizenzen für die Co-Verwaltung. Für dieses Szenario sind jedoch weiterhin separate AADP1-Lizenzen erforderlich. Für andere Registrierungsszenarios müssen Sie weiterhin Intune-Lizenzen zuweisen.

- Wenn Sie Intune für die Verwaltung von iOS-, Android- oder macOS-Geräten verwenden möchten, benötigen Sie ein entsprechendes Intune-Abonnement über eine eigenständige Intune-Lizenz, Enterprise Mobility + Security (EMS) oder Microsoft 365.

- Wenn Sie nicht über einen Abonnementplan verfügen, der mit Intune in Zusammenhang steht, müssen Sie mindestens eine Intune-Lizenz erwerben, damit die Coverwaltung unterstützt wird. Mit dieser Lizenz kann der Administrator den Abonnementplan aktivieren und auf das Admin Center für den Microsoft Endpoint Manager zugreifen.

- Wenn Sie das in Microsoft 365 integrierte Feature [Basic Mobility and Security](https://support.microsoft.com/office/capabilities-of-built-in-mobile-device-management-for-microsoft-365-a1da44e5-7475-4992-be91-9ccec25905b0) verwenden, können Sie nicht die neue Coverwaltungslizenz für einen Benutzer verwenden, der ebenfalls über Geräte verfügt, die von „Basic Mobility and Security“ verwaltet werden. Damit Sie die Coverwaltungslizenz für das von Configuration Manager verwaltete Gerät des Benutzers verwenden können, gehen Sie wie folgt vor:

  - Weisen Sie dem Benutzer die Vollversion einer Intune-Lizenz zu, und verwalten Sie seine Geräte über Intune.
  - Heben Sie die Registrierung der Geräte über „Basic Mobility and Security“ auf.

- Die Lizenzierung, die Sie zuvor für System Center Configuration Manager hatten, gilt weiterhin für Microsoft Endpoint Configuration Manager. Verwenden Sie bei der Installation eines neuen Standorts vorhandene Product Keys.

|Komponente | Coverwaltungslizenz | Vollversion einer Intune-Lizenz |
|---------|---------|---------|
|Windows 10-Registrierung|Ja (nur für vorhandene von Configuration Manager verwaltete Geräte)|Ja|
|iOS, Android, macOS-Registrierung|Nein|Ja|
|Autopilot|Nein|Ja|
|Verwaltung mobiler Anwendungen|Nein|Ja|
|Bedingter Zugriff<br>(zusätzlich AADP1 erforderlich)|Ja|Ja|
|Geräteprofile|Ja|Ja|
|Softwareupdateverwaltung|Ja|Ja|
|Inventarisierung|Ja|Ja|
|App-Verwaltung|Ja|Ja|
|Remoteunterstützung<br>(TeamViewer-Lizenz erforderlich)|Ja|Ja|
|Desktop Analytics<br>(Windows-Abonnementlizenzen erforderlich)|Ja|N/V|
|Mandantenanfügung|Ja|N/V|
|Endpunktanalyse|Ja|Ja|

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Voraussetzungen für die Coverwaltung](../../comanage/overview.md#prerequisites)
- [Anforderungen für Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)
- [Voraussetzungen für Desktop Analytics](../../desktop-analytics/overview.md#prerequisites)
- [Voraussetzungen für Mandantenanfügungsvorgänge](../../tenant-attach/device-sync-actions.md#prerequisites)
- [Voraussetzungen für die Endpunktanalyselizenzierung](../../../analytics/overview.md#licensing-prerequisites)
- [Verwenden des bedingten Zugriffs mit Intune](../../../intune/protect/conditional-access.md#use-conditional-access-with-intune)
- [Voraussetzungen für TeamViewer](../../../intune/remote-actions/teamviewer-support.md#prerequisites)

### <a name="i-have-enterprise-mobility--security-and-it-expired-what-must-i-do-now"></a><a name="bkmk_ems-expires"></a> Ich habe Enterprise Mobility + Security, und es ist abgelaufen. Was muss ich nun tun?  

EMS gewährt Rechte zur Verwendung von Configuration Manager Current Branch und Long-Term Service Branch. Wenn diese Rechte abgelaufen sind, verfügen Sie über keine Rechte mehr für die Verwendung eines Branch und müssen sie deinstallieren.  

### <a name="if-my-sa-expires-and-i-had-lsa-what-do-i-get"></a><a name="bkmk_sa-expires"></a> Wenn mein SA abläuft, und ich L&SA hatte, was erhalte ich?

Wenn Ihre SA nach dem 1. Oktober 2016 abgelaufen ist, können Sie eine unbefristete Lizenz behalten, um LTSB zu verwenden. Dies hängt davon ab, unter welchem Programm Sie L&SA erworben haben. Wenn Sie aktuell Current Branch verwenden, müssen Sie sie deinstallieren und anschließend LTSB installieren. Eine Migration oder Konvertierung von LTSB aus Current Branch wird nicht unterstützt.

Wenn Ihre SA vor dem 1. Oktober 2016 abgelaufen ist, und Sie eine unbefristete Lizenz für Configuration Manager erhalten haben, ist Ihre einzige Option für die weitere Verwendung das Installieren und Verwenden von System Center 2012 R2 Configuration Manager und der verfügbaren Servicepacks. Sie mussten Current Branch deinstallieren, als Ihre SA abgelaufen war, und die frühere Version des Produkts neu installieren. Es gibt keine Unterstützung für die Migration oder Herabstufung von Current Branch von Configuration Manager auf frühere Versionen von Configuration Manager.

Wenn Sie System Center Endpoint Protection verwenden, müssen Sie es deinstallieren, wenn Ihr SA abläuft. System Center Endpoint Protection bietet keine *L (Lizenz)* -Rechte und keine unbefristeten Rechte.<!--506238-->

### <a name="do-i-own-the-current-branch"></a><a name="bkmk_owncb"></a> „Gehört“ mir Current Branch?

Nein. Sie sind lizenziert Current Branch zu verwenden, während Sie eine aktive SA haben. Zum Beispiel haben Sie über die *L&SA*, wenn die *SA* abläuft, nur die *L (Lizenz)* -Rechte, die keine Rechte zur Verwendung von Current Branch enthalten. Wenn Ihre L unbefristete Rechte bereitstellt, können Sie die Configuration Manager-LTSB anstelle von Current Branch verwenden. Wenn Ihre SA vor dem 1. Oktober 2016 abgelaufen ist, können Sie auch System Center 2012 R2 Configuration Manager verwenden.

### <a name="can-i-purchase-configuration-manager-standalone-without-sa"></a><a name="bkmk_standalone"></a> Kann ich Configuration Manager eigenständig ohne SA erwerben?

Nein. Die einzige Möglichkeit Rechte zur Verwendung von Configuration Manager zu bekommen, ist der Erwerb einer Lizenz mit SA oder über ein entsprechendes Abonnement. Es gibt Entwicklerprogramme, wie MSDN, in denen Configuration Manager für Entwicklungs- und Testzwecke, aber nicht für den produktiven Einsatz angeboten wird.

### <a name="does-a-non-production-environment-for-testing-or-development-require-an-explicit-license"></a><a name="bkmk_lab"></a> Erfordert eine Nicht-Produktionsumgebung zum Testen oder Entwickeln eine explizite Lizenz?

<!-- SCCMDocs#1848 -->

- Wenn Sie dieselbe Current Branch-Software wie Ihre Produktionsumgebung verwenden, benötigen Sie eine explizite Lizenz. Wenden Sie sich an Ihr Kontoteam, um zu ermitteln, ob Ihr spezifischer Lizenzvertrag mehrere Instanzen in mehreren Umgebungen abdeckt.

- Einige Entwicklerprogramme wie MSDN bieten Produkte wie Configuration Manager für Entwicklungs- und Testzwecke, aber nicht für den Einsatz in der Produktion.

- Für eine temporäre Umgebung können Sie die [Evaluierungsversion](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) 180 Tage lang verwenden.

- Für eine Laborumgebung können Sie den [Technical Preview-Branch](../get-started/technical-preview.md) verwenden. Technical Preview verfügt über die gleiche Funktionalität wie Current Branch, weist jedoch einige Einschränkungen hinsichtlich der Skalierung und der unterstützten Plattformen auf.

### <a name="do-i-have-rights-to-install-any-update-in-the-configuration-manager-console"></a><a name="bkmk_update-rights"></a> Verfüge ich über Rechte zum Installieren von Updates in der Configuration Manager Konsole?

Wenn Sie eine aktive *SA* haben, dann ja.

Wenn Sie keine aktive SA haben, deinstallieren Sie Current Branch, und installieren Sie dann die LTSB von Configuration Manager. LTSB erhält keine Updates für die inkrementellen Versionen von Configuration Manager, erhält jedoch basierend auf den Support Lifecycle Sicherheitsupdates.

### <a name="i-have-purchased-ems-or-microsoft-365-through-a-cloud-solution-provider-csp-do-i-have-rights-to-use-configuration-manager"></a><a name="bkmk_csp"></a> Ich habe EMS oder Microsoft 365 über einen Cloud Solution Provider (CSP) erworben. Verfüge ich über Rechte, Configuration Manager zu verwenden?

Ja, Sie dürfen Configuration Manager verwenden, um Clients, die durch die EMS-Lizenz abgedeckt sind, zu verwalten. Laden Sie zunächst die [Evaluierungssoftware](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) herunter, und installieren Sie sie. Wenden Sie sich anschließend an den Microsoft-Support, um den Lizenzschlüssel zu erhalten.<!--issue472--> Wenn Sie mit dem Microsoft-Support sprechen, geben Sie zur Referenz die interne Artikel-ID 4033838 an.<!-- SCCMDocs issue 493 -->

### <a name="is-my-subscription-end-date-the-same-as-an-sa-expiration-date"></a><a name="bkmk_expiration-date"></a> Ist mein Abonnement-Enddatum das gleiche wie ein SA-Ablaufdatum?

Wenn *SA* oder Ihr Abonnement aktiv ist, stehen Ihnen Nutzungsrechte für Current Branch von Configuration Manager zur Verfügung. Ein aktives Abonnement ist gleichbedeutend mit einer aktiven *SA*, aber keine unbefristete *„L“ (Lizenz)* . Sobald Ihr Abonnement beendet ist, deinstallieren Sie Current Branch. Zu diesem Zeitpunkt haben Sie keine Rechte mehr für die Verwendung von LTSB.  

### <a name="what-are-the-use-rights-associated-with-the-sql-technology-provided-with-configuration-manager"></a><a name="bkmk_sql"></a> Welche Nutzungsrechte sind mit der SQL-Technologie verbunden, die mit Configuration Manager bereitgestellt wird?

Configuration Manager umfasst SQL Server-Technologie. Die Lizenzbedingungen von Microsoft für dieses Produkt erlauben es Ihnen, die SQL Server-Technologie nur zur Unterstützung von Configuration Manager-Komponenten zu verwenden. SQL Server-Clientzugriffslizenzen sind für diesen Verwendungszweck nicht erforderlich.

Zu den zugelassenen Nutzungsrechten für die SQL-Funktionen mit Configuration Manager gehören:

- Standortdatenbankrolle
- Windows Server Update Services (WSUS) für Softwareupdatepunkt-Rolle
- SQL Server Reporting Services (SSRS) für Berichterstattungspunkt-Rolle
- Data Warehouse-Dienstpunktrolle
- Datenbankreplikate für Verwaltungspunktrollen

Die SQL Server-Lizenz, die im Lieferumfang von Configuration Manager enthalten ist, unterstützt jede von Ihnen installierte SQL Server-Instanz, um eine Datenbank für Configuration Manager zu hosten. Allerdings können nur Datenbanken für Configuration Manager in der vorstehenden Liste auf diesem SQL Server ausgeführt werden, wenn Sie diese Lizenz verwenden. Wenn eine Datenbank den SQL Server mit einem weiteren Microsoft- oder Drittanbieterprodukt gemeinsam nutzt, benötigen Sie eine separate Lizenz für diese SQL Server-Instanz.
 <!-- sms500967 -->

### <a name="does-on-premises-mobile-device-management-mdm-require-an-intune-subscription"></a><a name="bkmk_opmdm"></a> Wird zur lokalen Verwaltung mobiler Geräte (MDM) ein Intune-Abonnement benötigt?

Bis Version 1806 wird zum Starten der lokalen MDM ein Microsoft Intune-Abonnement benötigt. Das Abonnement ist nur erforderlich, um die Lizenzierung der Geräten zu verfolgen und dient nicht zum Verwalten oder Speichern von Geräteverwaltungsinformationen. Die Speicherung der gesamten Verwaltungsdaten erfolgt mithilfe der lokalen Configuration Manager-Infrastruktur in Ihrem Unternehmen.  

Ab Version 1810 ist für neue lokale MDM-Bereitstellungen keine Intune-Verbindung mehr erforderlich.<!--3607730, fka 1359124--> Für Ihre Organisation sind weiterhin Intune-Lizenzen erforderlich, damit dieses Feature genutzt werden kann. Weitere Informationen finden Sie im [Blogbeitrag des Intune-Supports](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).
