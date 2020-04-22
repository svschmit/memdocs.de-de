---
title: Planen der Clientbereitstellung auf Linux- und UNIX-Computern
titleSuffix: Configuration Manager
description: Planen Sie die Clientbereitstellung auf Linux- und UNIX-Computern in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693728"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Planen der Clientbereitstellung auf Linux- und UNIX-Computern in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

> [!Important]  
> Ab Version 1902 unterstützt Configuration Manager keine Linux- oder UNIX-Clients mehr. 
> 
> Ziehen Sie deshalb Microsoft Azure Management zum Verwalten von Linux-Servern in Betracht. Azure-Lösungen verfügen über umfangreiche Linux-Unterstützung, die i.d.R. über die Funktionen von Configuration Manager hinausgeht (einschließlich der End-to-End-Patchverwaltung für Linux).

Sie können den Configuration Manager-Client auf Computern installieren, auf denen Linux oder UNIX ausgeführt wird. Dieser Client wurde für Server entwickelt, die als Arbeitsgruppencomputer fungieren. Eine Interaktion mit angemeldeten Benutzern wird vom Client nicht unterstützt. Nach der Installation der Clientsoftware und nachdem die Kommunikation zwischen Client und Configuration Manager-Standort hergestellt wurde, können Sie den Client mithilfe der Configuration Manager-Konsole und Berichten verwalten.  

> [!NOTE]
>  Der Configuration Manager-Client für Linux- und UNIX-Computer unterstützt die folgenden Verwaltungsfunktionen:  
> 
> - Clientpushinstallation  
>   -   Betriebssystembereitstellung  
>   -   Anwendungsbereitstellung; stattdessen Bereitstellen von Software mithilfe von Paketen und Programmen.  
>   -   Softwareinventur  
>   -   Softwareupdates  
>   -   Kompatibilitätseinstellungen  
>   -   Remotesteuerung  
>   -   Energieverwaltung  
>   -   Clientprüfung des Clientstatus und Wiederherstellung  
>   -   Internetbasierte Clientverwaltung  

 Weitere Informationen zu den unterstützten Linux- und UNIX-Distributionen sowie zur Hardware, die zum Unterstützen des Clients für Linux und UNIX erforderlich ist, finden Sie unter [Empfohlene Hardware für Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Verwenden Sie die Informationen in diesem Artikel, die Ihnen beim Planen der Bereitstellung des Configuration Manager-Clients für Linux und UNIX helfen.  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a> Erforderliche Komponenten für die Clientbereitstellung für Linux- und UNIX-Server  
 Verwenden Sie die folgende Informationen bestimmen, ob die erforderlichen Komponenten, die direkt auf erfolgreich sein müssen, den Client für Linux und UNIX installieren.  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a> Externe Abhängigkeiten von Configuration Manager  
 In der folgenden Tabelle werden die erforderlichen UNIX- und Linux-Betriebssysteme und Paketabhängigkeiten beschrieben.  

 **Red Hat Enterprise Linux Server Release 5.1 (Tikanga)**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|glibc|C-Standardbibliotheken|2.5-12|  
|Openssl|OpenSSL-Bibliotheken; SNC-Protokoll (Secure Network Communications)|0.9.8b-8.3.el5|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server Release 6**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|glibc|C-Standardbibliotheken|2.12-1.7|  
|Openssl|OpenSSL-Bibliotheken; SNC-Protokoll (Secure Network Communications)|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

 **Red Hat Enterprise Linux Server Release 7**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|glibc|C-Standardbibliotheken|2.17|  
|Openssl|OpenSSL-Bibliotheken; SNC-Protokoll (Secure Network Communications)|1.0.1|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

 **Solaris 10 SPARC**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|Erforderliches Betriebssystem-Patches|PAM-Speicherleck|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math- und Microtasking-Bibliotheken (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math- und Microtasking-Bibliotheken (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Core-Solaris-Bibliotheken (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Core-Solaris-Bibliotheken (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|SUNopenssl-Bibliotheken (Usr)<br /><br /> Sun stellt die OpenSSL-Bibliotheken für Solaris 10 SPARC bereit. Diese werden zusammen mit dem Betriebssystem ausgeliefert.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Pluggable Authentication Modules<br /><br /> SUNWcsr, Core Solaris, (Root) (Sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|Erforderliches Betriebssystem-Patches|PAM-Speicherleck|117464-04|  
|SUNWlibC|Sun Workshop Compiler gebündelt LibC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Math- und Microtasking-Bibliotheken (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (Freigabebibliotheken) (i386)|11.10.0, REV=2005.01.21.16.34|  
|SUNWcslr|Core Solaris-Bibliotheken (Root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|SUNWopenssl-Bibliotheken; OpenSSL-Bibliotheken (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Pluggable Authentication Modules<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0, REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math- und Microtasking-Bibliotheken (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core-Solaris-Bibliotheken (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Freigabebibliotheken)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-Bibliotheken|OpenSSL-Bibliotheken (Usr)|11.11.0, REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math- und Microtasking-Bibliotheken (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core-Solaris-Bibliotheken (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Freigabebibliotheken)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-Bibliotheken|OpenSSL-Bibliotheken (Usr)|11.11.0, REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|glibc-2,4-31,30|C-Standardfreigabebibliothek|2.4-31.30|  
|Openssl|OpenSSL-Bibliotheken; SNC-Protokoll (Secure Network Communications)|0.9.8a-18.15|  
|PAM|Pluggable Authentication Modules|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|C-Standardfreigabebibliothek|2.9-13.2|  
|PAM|Pluggable Authentication Modules|pam-1.0.2-20.1|  

 **Universal Linux (Debian package) Debian, Ubuntu Server**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|libc6|C-Standardfreigabebibliothek|2.3.6|  
|Openssl|OpenSSL-Bibliotheken; SNC-Protokoll (Secure Network Communications)|0.9.8 oder 1.0|  
|PAM|Pluggable Authentication Modules|0.79-3|  

 **Universal Linux (RPM package) CentOS, Oracle Linux**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|glibc|C-Standardfreigabebibliothek|2.5-12|  
|OpenSSL|OpenSSL-Bibliotheken; SNC-Protokoll (Secure Network Communications)|0.9.8 oder 1.0|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|BS-Version|Betriebssystemversion|AIX 6.1: alle Technology Level und Service Packs|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|OpenSSL-Bibliotheken; SNC-Protokoll (Secure Network Communications)|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|BS-Version|Betriebssystemversion|AIX 7.1: alle Technology Level und Service Packs|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|OpenSSL-Bibliotheken; SNC-Protokoll (Secure Network Communications)||  


 **HP-UX 11i v3 IA64**  

|Erforderliches Paket|Beschreibung|Mindestversion|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Spezielle IA-Entwicklungsbibliotheken|B.11.31|  
|SysMgmtMin|Minimale Softwarebereitstellungstools|B.11.31.0709|  
|SysMgmtMin.openssl|OpenSSL-Bibliotheken; SNC-Protokoll (Secure Network Communications)|A.00.09.08d.002|  
|PAM|Pluggable Authentication Modules|Unter HP-UX sind PAM ein Teil der Kernbetriebssystemkomponenten. Es bestehen keine weiteren Abhängigkeiten.|  

 **Abhängigkeiten in Configuration Manager:** In der folgenden Tabelle werden Standortsystemrollen aufgeführt, die Linux- und UNIX-Clients zu unterstützen. Weitere Informationen zu diesen Standortsystemrollen finden Sie unter [Ermitteln der Standortsystemrollen für Configuration Manager-Clients](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Configuration Manager-Standortsystem|Weitere Informationen|  
|---------------------------------------|----------------------|  
|Verwaltungspunkt|Obwohl kein Verwaltungspunkt notwendig ist, um einen Configuration Manager-Client für Linux und UNIX zu installieren, muss ein Verwaltungspunkt vorhanden sein, um Informationen zwischen Clientcomputern und Configuration Manager-Servern zu übertragen. Ohne Verwaltungspunkt können Sie Clientcomputer nicht verwalten.|  
|Verteilungspunkt|Der Verteilungspunkt ist nicht erforderlich, um einen Configuration Manager-Client für Linux und UNIX zu installieren. Die Standortsystemrolle ist jedoch erforderlich, wenn Sie Software für Linux- und UNIX-Servern bereitstellen.<br /><br /> Weil der Configuration Manager-Client für Linux und UNIX Kommunikation mit dem SMB nicht unterstützt, müssen die Verteilungspunkte, die Sie mit dem Client verwenden, HTTP- oder HTTPS-Kommunikation unterstützen.|  
|Fallbackstatuspunkt|Der Fallbackstatuspunkt ist nicht erforderlich, um einen Configuration Manager-Client für Linux und UNIX zu installieren. Jedoch ermöglicht der Fallbackstatuspunkt Computern am Configuration Manager-Standort, Zustandsmeldungen zu senden, wenn sie nicht mit einem Verwaltungspunkt kommunizieren können. Clients kann auch deren Installationsstatus an den Fallbackstatuspunkt senden.|  

 **Firewallanforderungen:** Stellen Sie sicher, dass Firewalls Kommunikation über die Ports, die Sie als Clientanforderungsports angeben, nicht blockieren. Der Client für Linux und UNIX kommuniziert direkt mit Verwaltungspunkten, Verteilungspunkten und Fallbackstatuspunkten.  

 Weitere Informationen zur Clientkommunikation und zu Anforderungsports finden Sie unter  [Konfigurieren des Clients für Linux und UNIX für die Suche nach Verwaltungspunkten](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a> Planen der Kommunikation zwischen Gesamtstruktur-Vertrauensstellungen für Linux- und UNIX-Server  
 Linux- und UNIX-Server, die Sie mit Configuration Manager verwalten, stellen Clients in Arbeitsgruppen dar und erfordern ähnliche Konfigurationen wie Windows-basierte Clients, die sich in einer Arbeitsgruppe befinden. Informationen zur Kommunikation von Arbeitsgruppencomputern finden Sie unter [Kommunikation zwischen Active Directory-Gesamtstrukturen](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a> Dienstidentifizierung nach Client für Linux und UNIX  
 Der Task zum Auffinden von einem Standort befindet, der Dienst für Clients bereitstellt wird als Speicherort bezeichnet. Im Gegensatz zu einem Windows-basierten Client verwendet der Client für Linux und UNIX Active Directory nicht zur Dienstidentifizierung. Darüber hinaus unterstützt der Configuration Manager-Client für Linux und UNIX keine Clienteigenschaft, die das Domänensuffix eines Verwaltungspunkts angibt. Der Client erfährt stattdessen zusätzliche standortsystemserver umfassen, die Dienste für Clients von einem bekannten Verwaltungspunkt, die Sie zuweisen bereitstellen, wenn Sie die Clientsoftware installieren.  

 Weitere Informationen finden Sie unter [Dienstidentifizierung und wie Clients den ihnen zugewiesenen Verwaltungspunkt ermitteln](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a> Planen der Sicherheit und Zertifikate für Linux- und UNIX-Server  
 Für die sichere und authentifizierte Kommunikation mit Configuration Manager-Standorten verwendet der Configuration Manager-Client für Linux und UNIX das gleiche Modell für die Kommunikation wie der Configuration Manager-Client für Windows.  

 Wenn Sie den Linux- und UNIX-Client installieren, können Sie dem Client ein PKI-Zertifikat zuweisen, das ihm die HTTPS-Kommunikation mit Configuration Manager-Standorten ermöglicht. Wenn Sie kein PKI-Zertifikat zuweisen, erstellt der Client ein selbstsigniertes Zertifikat und kommuniziert nur über HTTP.  

 Clients, die ein PKI-Zertifikat bereitgestellt werden, bei der Installation verwenden Sie HTTPS für die Kommunikation mit Verwaltungspunkten. Wenn ein Client nicht an einen Verwaltungspunkt zu finden, der HTTPS unterstützt, wird es zurückgreifen, um HTTP mit dem bereitgestellten PKI-Zertifikat verwenden.  

 Wenn ein Linux- oder UNIX-Client ein PKI-Zertifikat verwendet, müssen Sie sie nicht genehmigen. Wenn ein Client ein selbstsigniertes Zertifikat verwendet, überprüfen Sie die Hierarchieeinstellungen für die Clientgenehmigung in der Configuration Manager-Konsole. Die Genehmigung-Methode ist nicht **alle Computer (nicht empfohlen) automatisch genehmigen**, müssen Sie den Client manuell genehmigen.  

 Weitere Informationen zum manuellen Genehmigen des Clients finden Sie unter [Verwalten von Clients mithilfe des Knotens „Geräte“](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 Informationen zum Verwenden von Zertifikaten in Configuration Manager finden Sie unter [PKI-Zertifikatanforderungen](../../../plan-design/network/pki-certificate-requirements.md).  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a> Informationen zu Zertifikaten für die Verwendung durch Linux- und UNIX-Server  
 Der Configuration Manager-Client für Linux und UNIX verwendet genau wie Windows-basierte Clients ein selbstsigniertes Zertifikat oder ein X.509-PKI-Zertifikat. Bezüglich der PKI-Anforderungen an Configuration Manager-Standortsysteme bestehen bei der Verwaltung von Linux- und UNIX-Clients keine Unterschiede.  

 Die Zertifikate für Linux- und UNIX-Clients, die mit Configuration Server-Standortsystemen kommunizieren, müssen das PKCS#12-Format (Public Key Certificate Standard) aufweisen, und das Kennwort muss bekannt sein, damit Sie es für den Client angeben können, wenn Sie das PKI-Zertifikat festlegen.  

 Der Configuration Manager-Client für Linux und UNIX unterstützt ein einzelnes PKI-Zertifikat und nicht mehrere Zertifikate. Deshalb gelten die Zertifikatauswahlkriterien für einen Configuration Manager-Standort nicht.  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a> Konfigurieren von Zertifikaten für Linux- und UNIX-Server  
 Um einen Configuration Manager-Client für Linux- und UNIX-Server für die HTTPS-Kommunikation zu konfigurieren, müssen Sie den Client bei der Installation für die Verwendung eines PKI-Zertifikats konfigurieren. Sie können ein Zertifikat nicht vor Installation der Clientsoftware bereitstellen.  

 Wenn Sie einen Client installieren, der ein PKI-Zertifikat verwendet, verwenden Sie den Befehlszeilenparameter `-UsePKICert` zur Angabe des Speicherorts und Namens einer PKCS #12-Datei, die das PKI-Zertifikat enthält. Darüber hinaus müssen Sie den Befehlszeilenparameter `-certpw` verwenden, um das Kennwort für das Zertifikat anzugeben.  

 Wenn Sie `-UsePKICert` nicht angeben, generiert der Client ein selbstsigniertes Zertifikat und versucht, nur über HTTP mit Standortsystemservern zu kommunizieren.  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a>-Versionen, die SHA-256 nicht unterstützen  
 Die folgenden Linux- und UNIX-Betriebssysteme, die als Clients für Configuration Manager unterstützt werden, wurden mit OpenSSL-Versionen ohne SHA-256-Unterstützung freigegeben:  

-   Solaris Version 10 (SPARC/x86)  


 Zum Verwalten dieser Betriebssysteme mit Configuration Manager müssen Sie den Configuration Manager-Client für Linux und UNIX mit einem Befehlszeilenschalter installieren, der den Client anweist, die SHA-256-Überprüfung zu überspringen. Unter diesen Betriebssystemversionen ausgeführte Configuration Manager-Clients werden in einem weniger sicheren Modus ausgeführt als Clients, die SHA-256 unterstützen. Dieser weniger sicheren Betriebsmodus weist das folgende Verhalten:  

-   Clients überprüfen nicht die der Richtlinie zugeordnete Standortserversignatur, die sie von einem Verwaltungspunkt anfordern.  

-   Clients überprüfen nicht den Hash für Pakete, die sie von einem Verteilungspunkt herunterladen.  

> [!IMPORTANT]  
>  Die Option `ignoreSHA256validation` ermöglicht Ihnen die Ausführung des Clients für Linux- und UNIX-Computer in einem weniger sicheren Modus. Dies ist für die Verwendung auf älteren Plattformen vorgesehen, die keine Unterstützung für SHA-256 eingefügt haben. Eine Außerkraftsetzung für die Sicherheit und wird nicht von Microsoft empfohlen, dies ist für eine sichere und vertrauenswürdige Datacenter-Umgebung unterstützt wird.  

 Bei der Installation des Configuration Manager-Clients für Linux und UNIX überprüft das Installationsskript die Version des Betriebssystems. Wenn die Betriebssystemversion als eine Version identifiziert wird, die ohne OpenSSL mit SHA-256-Unterstützung freigegeben wurde, tritt bei der Installation des Configuration Manager-Clients ein Fehler auf.  

 Um den Configuration Manager-Client auf Linux- und UNIX-Betriebssystemen zu installieren, die ohne eine Version von OpenSSL freigegeben wurden, die SHA-256 unterstützen, müssen Sie den Befehlszeilenschalter `ignoreSHA256validation` für die Installation verwenden. Wenn Sie diese Befehlszeilenoption für ein entsprechendes Linux- oder UNIX-Betriebssystem verwenden, überspringt der Configuration Manager-Client die SHA-256-Überprüfung und verwendet nach der Installation kein SHA-256 zum Signieren der Daten, die er über HTTP an Standortsysteme übermittelt. Informationen zum Konfigurieren von Linux- und UNIX-Clients für die Verwendung von Zertifikaten finden Sie unter [Planen der Sicherheit und Zertifikate für Linux- und UNIX-Server](#BKMK_SecurityforLnU). Weitere Informationen zum Anfordern von SHA-256 finden Sie unter [Konfigurieren von Signierung und Verschlüsselung](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption).  

> [!NOTE]  
>  Die Befehlszeilenoption `ignoreSHA256validation` wird auf Computern ignoriert, auf denen eine Linux- und UNIX-Version ausgeführt wird, die mit OpenSSL-Versionen inklusive SHA-256-Unterstützung freigegeben wurden.  
