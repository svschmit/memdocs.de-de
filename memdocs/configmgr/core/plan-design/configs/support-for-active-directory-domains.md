---
title: Unterstützung für Active Directory-Domänen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Anforderungen für ein Configuration Manager-Standortsystem in einer Active Directory Domäne.
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688578"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>Unterstützung für Active Directory-Domänen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Alle Configuration Manager-Standortsysteme müssen Mitglieder einer unterstützten Active Directory-Domäne sein. Configuration Manager-Clientcomputer können Mitglieder der Domäne oder der Arbeitsgruppe sein.  

## <a name="requirements-and-limitations"></a>Anforderungen und Einschränkungen

- Domänennmitgliedschaft gilt auch für Standortsysteme, die internetbasierte Clientverwaltung in einem Umkreisnetzwerk unterstützen. (Diese Netzwerke werden auch als DMZ (Demilitarized Zone, demilitarisierte Zone) oder überwachtes Subnetz bezeichnet.)  

- Änderungen an den folgenden Konfigurationen eines Computers, der eine Standortsystemrolle hostet, werden nicht unterstützt:  

  - Domänenmitgliedschaft (einschließlich Entfernen eines Standortsystems aus der Domäne und anschließendes erneutes Beitreten zu derselben Domäne).

  - Domänenname  

  - Computername  

  Deinstallieren Sie die Standortsystemrolle, bevor Sie diese Änderungen vornehmen. Deinstallieren Sie den Standort zunächst, um diese Änderungen an einem Standortserver vorzunehmen. Sie können auch die Erstellung eines [Standortservers im passiven Modus](../../servers/deploy/configure/site-server-high-availability.md) in Erwägung ziehen, um die Verwaltung dieser Änderung auf einem Standortserver zu unterstützen.

- Configuration Manager unterstützt die Domänen- und Gesamtstrukturfunktionsebene von Windows Server 2008 R2 oder höher.<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Zusammenhanglose Namespaces

Sie können Configuration Manager-Standortsysteme und -Clients in einer Domäne mit einem *zusammenhanglosen Namespace* installieren.  

In einem zusammenhanglosen Namespace stimmt das primäre DNS-Suffix eines Computers nicht mit dem Active Directory DNS-Domänennamen dieses Computers überein. Ein zusammenhangloser Namespace liegt auch vor, wenn der NetBIOS-Domänenname eines Domänencontrollers nicht mit dem Active Directory DNS-Domänennamen übereinstimmt.  

### <a name="disjoint-scenarios"></a>Szenarien für zusammenhanglose Namespaces

In der folgenden Abschnitten werden die für zusammenhanglose Namespaces unterstützten Szenarien aufgeführt.  

#### <a name="scenario-1"></a>Szenario 1

Das primäre DNS-Suffix des Domänencontrollers unterscheidet sich vom Active Directory DNS-Domänennamen. Computer, die Mitglieder der Domäne sind, können zusammenhanglos oder nicht zusammenhanglos sein.

Der Domänencontroller ist in diesem Szenario zusammenhanglos. Computer, die Mitglieder der Domäne sind (z.B. Standortserver und -computer) können ein primäres DNS-Suffix aufweisen, das mit einem der folgenden Elemente übereinstimmt:

- Mit dem primären DNS-Suffix des Domänencontrollers.
- Mit dem Active Directory-Domänennamen.

#### <a name="scenario-2"></a>Szenario 2

Ein Mitgliedscomputer in einer Active Directory DNS-Domäne ist zusammenhanglos, obwohl der Domänencontroller nicht zusammenhanglos ist.

In diesem Szenario unterscheidet sich das primäre DNS-Suffix eines Standortsystems vom Active Directory DNS-Domänennamen. Das primäre DNS-Suffix des Domänencontrollers stimmt mit dem Active Directory DNS-Domänennamen überein. Mitgliedscomputer, die Configuration Manager-Clients sind, können ein primäres DNS-Suffix aufweisen, das mit einem der folgenden Elemente übereinstimmt:

- Mit dem primäre DNS-Suffix des zusammenhanglosen Standortsystemservers.
- Mit dem Active Directory-Domänennamen.

### <a name="configure-disjoint-namespace"></a>Konfigurieren des zusammenhanglosen Namespaces

Damit ein Computer auf zusammenhanglose Domänencontroller zugreifen kann, ändern Sie das Active Directory-Attribut **msDS-AllowedDNSSuffixes** für den Domänenobjektcontainer. Fügen Sie dem Attribut beide DNS-Suffixe hinzu.  

Um sicherzustellen, dass die *Suchliste für DNS-Suffixe* alle DNS-Namespaces in der Organisation enthält, konfigurieren Sie die Suchliste für jeden Computer in der zusammenhanglosen Domäne. Binden Sie die folgenden Suffixe in die Liste der Namespaces ein:

- Das primäre DNS-Suffix des Domänencontrollers.
- Den DNS-Domänennamen.
- Alle zusätzlichen Namespaces für andere Server, mit denen Configuration Manager möglicherweise kommuniziert.

Sie können Gruppenrichtlinien verwenden, um die **Suchliste für DNS-Suffixe** zu konfigurieren.  

> [!IMPORTANT]  
> Wenn Sie in Configuration Manager auf einen Computer verweisen, geben Sie das primäre DNS-Suffix des Computers an. Das Suffix muss mit dem FQDN, der als Attribut **dnsHostName** in der Active Directory-Domäne registriert ist, und mit dem Dienstprinzipalnamen (SPN) des Systems übereinstimmen.  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> Einteilige Domänen

Configuration Manager unterstützt Standortsysteme und Clients in einer einteiligen Domäne, wenn die folgenden Kriterien erfüllt sind:  

- Konfigurieren Sie die einteilige Domäne in Active Directory Domain Services mit einem zusammenhanglosen DNS-Namespace, der über eine gültige Domäne der obersten Ebene verfügt.  

  **Beispiel:** Die einteilige Domäne „Contoso“ ist so konfiguriert, dass sie im DNS von „contoso.com“ einen zusammenhanglosen Namespace aufweist. Wenn Sie das DNS-Suffix in Configuration Manager für einen Computer in der Domäne „Contoso“ festlegen, geben Sie „Contoso.com“ und nicht „Contoso“ an.  

- DCOM-Verbindungen (Distributed Component Object Model) zwischen Standortservern im Systemkontext müssen aufgrund von Kerberos-Authentifizierung erfolgreich sein.  
