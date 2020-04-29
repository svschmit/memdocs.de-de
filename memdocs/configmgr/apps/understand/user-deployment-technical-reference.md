---
title: Technische Referenz zur App-Bereitstellung für Benutzer
titleSuffix: Configuration Manager
description: Technische Referenz zur Problembehandlung bei Anwendungsbereitstellungen für Benutzer für Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690268"
---
# <a name="application-deployment-policy-for-users"></a>Anwendungsbereitstellungsrichtlinie für Benutzer

*Gilt für: Configuration Manager (Current Branch)*

Wenn eine Anwendung in einer Benutzersammlung bereitgestellt wird, wird die Richtlinie für die Bereitstellung nur für erforderliche Bereitstellungen erstellt. Für verfügbare Bereitstellungen wird die Richtlinie erstellt, wenn der Benutzer versucht, die Anwendung über das Softwarecenter zu installieren. In diesem Artikel wird der Bereitstellungsprozess sowohl für erforderliche als auch für verfügbare Bereitstellungen erläutert.

> [!TIP]
> Alle zur Überprüfung der Clientprotokolle erforderlichen Informationen erhalten Sie durch Ausführen der SQL-Abfrage, auf die im Abschnitt [Vorbereitung](app-deployment-technical-reference.md#before-you-begin) verwiesen wird.

## <a name="required-deployments"></a>Erforderliche Bereitstellungen

Die Richtlinie für eine erforderliche Anwendungsbereitstellung für eine Benutzersammlung richtet sich an alle Benutzer in der Sammlung, wenn die Bereitstellung erstellt wird. Die clientseitige Verarbeitung für diese Bereitstellungen ähnelt einer erforderlichen Bereitstellung für eine Gerätesammlung. Die Aktivierung der Bereitstellung erfolgt zur definierten verfügbaren Zeit, und die Erzwingung erfolgt zur definierten Stichtagszeit. Weitere Informationen finden Sie unter [Anwendungsbereitstellung für Gerätesammlungen](device-deployment-technical-reference.md).

## <a name="available-deployments"></a>Verfügbare Bereitstellungen

Anwendungen, die in einer Benutzersammlung als verfügbar bereitgestellt werden, verhalten sich anders. Diese Verhaltensänderung ermöglicht es dem Administrator, den Benutzern Anwendungen zur Verfügung zu stellen, ohne Ressourcenkonflikte für die Richtlinien zu verursachen. Wenn ein Benutzer das Softwarecenter startet, wird eine Liste der Anwendungen, die für den Benutzer verfügbar sind, vom Verwaltungspunkt in Echtzeit abgefragt. Diese Anforderung wird an das virtuelle Verzeichnis `CMUserService_WindowsAuth` am Verwaltungspunkt gestellt und kann im virtuellen Verzeichnis **SCClient_[Benutzername].log** auf dem Client eingesehen werden.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

Wenn der Verwaltungspunkt diese Anforderung erhält, fragt er die Liste der für den Benutzer verfügbaren Anwendungen ab, indem er die gespeicherte Prozedur `usp_GetApplicationPropertyValuesFiltered` ausführt. Diese Aktivität kann in **UserService.log** auf dem Verwaltungspunkt nachverfolgt werden.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

Das Softwarecenter empfängt die Liste und zeigt die Anwendungen an, die der Benutzer installieren kann. Wenn der Benutzer auf die Anwendung klickt, werden zusätzliche Informationen über die Anwendung vom Verwaltungspunkt abgefragt, was die Ausführung von gespeicherten Prozeduren wie „usp_GetApplicationInfo“, „usp_GetAppModelApplicationSupersedence“, „usp_GetDeploymentTypeForAnApp“ usw. umfasst.

Die Bereitstellung wird aktiviert, wenn der Benutzer die Anwendung auswählt und auf die Schaltfläche **Installieren** klickt und ein DCM-Agent-Auftrag erstellt wird, um die Anwendung auszuwerten. Wenn die Anwendung geeignet ist, wird ein weiterer DCM-Agent-Auftrag erstellt, um die Anwendung herunterzuladen und zu erzwingen. Diese Aktivität kann in **DCMAgent.log** auf dem Client nachverfolgt werden.

## <a name="next-steps"></a>Nächste Schritte

- [Grundlegendes zu Clientkomponenten für die Anwendungsbereitstellung](client-components-technical-reference.md)
