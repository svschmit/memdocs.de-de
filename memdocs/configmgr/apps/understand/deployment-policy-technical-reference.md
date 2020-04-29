---
title: Technische Referenz zur Anwendungsbereitstellungsrichtlinie
titleSuffix: Configuration Manager
description: Technische Referenz zur Problembehandlung bei Anwendungsbereitstellungsrichtlinien für Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688828"
---
# <a name="application-deployment-policy"></a>Anwendungsbereitstellungsrichtlinie

*Gilt für: Configuration Manager (Current Branch)*

## <a name="policy-creation"></a>Richtlinienerstellung

Wenn Sie eine Anwendung bereitstellen, wird eine Instanz der Klasse [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) erstellt, die die Zuweisung einer Anwendung zu einer Sammlung darstellt. Diese Aktivität kann in **SMSProv.log** nachverfolgt werden.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

In der Configuration Manager-Datenbank werden diese Informationen in der Tabelle `CI_CIAssignments` gespeichert, wobei `AssignmentType` 2 eine Anwendungsbereitstellung darstellt. Wenn die Zuweisung erstellt wird, stellt die SMS-Datenbankmonitor-Komponente eine Änderung in der Tabelle fest und benachrichtigt dann den Objekt-Replikationsmanager, die CI-Zuweisungsrichtlinie (CIA) zu verarbeiten. Die Objekt-Replikationsmanager-Komponente erstellt dann die Richtlinie für die Anwendungszuweisung in der Datenbank, die in der Tabelle `Policy` in der Datenbank gespeichert ist, und die Richtlinien-ID basiert auf der eindeutigen Anwendungs-ID. Diese Aktivität kann in **objreplmgr.log** nachverfolgt werden, indem auf die eindeutige Zuweisungs-ID verwiesen wird, die von der SQL-Abfrage erhalten werden kann, auf die im Abschnitt [Vorbereitung](app-deployment-technical-reference.md#before-you-begin) verwiesen wird.

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

Die Richtlinie für die Anwendungszuweisung kann in der Datenbank mithilfe einer SQL-Abfrage ähnlich wie unten angezeigt werden.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>Richtlinienziel

Nachdem die Richtlinie generiert wurde, ordnet die Richtlinienanbieter-Komponente diese Richtlinie den Ressourcen in der Sammlung zu, auf die die Anwendungsbereitstellung ausgerichtet ist. Die auf Richtlinien ausgerichteten Informationen werden in der Tabelle `ResPolicyMap` in der Datenbank gespeichert. Sie können die von der obigen Abfrage zurückgegebene PADBID verwenden, um diese Aktivität in **policypv.log** nachzuverfolgen. Die im Protokoll aufgezeichnete PADBID stimmt jedoch möglicherweise nicht immer mit der von der obigen Abfrage zurückgegebenen PADBID überein, wenn mehrere Richtlinien gleichzeitig verarbeitet werden.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> Die Tabelle `ResPolicyMap` enthält keine Zielinformationen für Anwendungen, die als **Verfügbar** für Benutzersammlungen bereitgestellt werden. Das Softwarecenter fragt beim Verwaltungspunkt eine Liste dieser Anwendungen ab, und die Informationen zu den Richtlinien für diese Anwendungen werden dynamisch generiert, wenn ein Benutzer eine Anwendung beim Softwarecenter anfordert.

## <a name="next-steps"></a>Nächste Schritte

- [Anwendungsbereitstellung für Gerätesammlungen](device-deployment-technical-reference.md)
- [Anwendungsbereitstellung für Benutzersammlungen](user-deployment-technical-reference.md)
