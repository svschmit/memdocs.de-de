---
title: Genehmigen von Anwendungen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Einstellungen und Verhalten für die Genehmigung von Anwendungen in Configuration Manager.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 659dd91c4b6bbeba6e2e93d3318683a4006aa5ff
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606599"
---
# <a name="approve-applications-in-configuration-manager"></a>Genehmigen von Anwendungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Beim [Bereitstellen von Anwendungen](deploy-applications.md) in Configuration Manager können vor der Installation die Genehmigung anfordern. Benutzer fordern die Anwendung in Software Center an, und Sie überprüfen diese Anforderung dann in der Configuration Manager-Konsole. Sie können die Anforderung genehmigen oder verweigern.

## <a name="approval-settings"></a><a name="bkmk_approval"></a> Genehmigungseinstellungen

Das Verhalten bei der Anwendungsgenehmigung hängt davon ab, ob Sie die empfohlene [optionale App-Genehmigungserfahrung](#bkmk_opt) aktivieren. Eine der folgenden Genehmigungseinstellungen wird auf der Seite **Bereitstellungseinstellungen** der Anwendungsbereitstellung angezeigt:  

### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a><a name="bkmk_opt"></a> Ein Administrator muss eine Anforderung für diese Anwendung auf dem Gerät genehmigen

> [!Note]  
> Configuration Manager aktiviert dieses Feature nicht automatisch. Aktivieren Sie vor der Verwendung das optionale Feature **Anwendungsanforderungen für Benutzer pro Gerät genehmigen**. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
>
> Wenn Sie dieses Feature nicht aktivieren, wird die [vorherige Oberfläche](#bkmk_prior) angezeigt.  

Der Administrator muss Anforderungen für die Anwendung genehmigen, bevor der Benutzer sie auf dem Gerät installieren kann, für das er die Anforderung gestellt hat. Wenn ein Administrator die Anforderung genehmigt, kann der Benutzer die Anwendung nur auf diesem spezifischen Gerät installieren. Der Benutzer muss eine weitere Anforderung senden, um die Anwendung auf einem anderen Gerät installieren zu können. Diese Option ist ausgegraut, wenn der Zweck der Bereitstellung **Erforderlich** lautet, oder wenn die Anwendung für eine Gerätesammlung bereitgestellt wird. <!--1357015-->  

> [!Note]  
> Wenn Sie neue Configuration Manager-Features nutzen möchten, müssen Sie zunächst die Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.<!--SCCMDocs issue 646-->  

Zeigen Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** unter **Anwendungsverwaltung** die **Anwendungsanforderungen** an. (In Version 1902 und früher heißt dieser Knoten **Genehmigungsanforderungen**.) Sie finden jetzt in der Liste die Spalte **Gerät** für jede Anforderung. Wenn Sie eine Aktion zur Anforderung ausführen, enthält das Dialogfeld „Anwendungsanforderung“ auch den Namen des Geräts, von dem aus der Benutzer die Anforderung übermittelt hat.

Wenn eine Anforderung nicht innerhalb von 30 Tagen genehmigt wird, wird sie entfernt. Ausstehende Genehmigungsanforderungen können durch eine Neuinstallation abgebrochen werden.  

Wenn Sie eine Genehmigung für die Bereitstellung in einer Gerätesammlung benötigen, wird die Anwendung nicht im Softwarecenter angezeigt. Wenn Sie eine Genehmigung für die Bereitstellung in einer Benutzersammlung benötigen, wird die Anwendung im Softwarecenter angezeigt. Sie können sie mit der Clienteinstellung **Nicht genehmigte Anwendungen im Softwarecenter ausblenden** weiterhin vor Benutzern ausblenden. Weitere Informationen finden Sie unter [Softwarecenter-Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#software-center).

Nachdem Sie eine Anwendung für die Installation genehmigt haben, können Sie die Anforderung in der Configuration Manager-Konsole **verweigern**. Wenn Benutzer die Anwendung noch nicht installiert haben, werden sie durch diese Aktion daran gehindert, neue Kopien der Anwendung aus dem Software Center zu installieren. Wenn eine Anwendung zuvor genehmigt und installiert wurde und Sie die Anforderung der Anwendung **ablehnen**, deinstalliert der Client die Anwendung vom Gerät des Benutzers.<!--1357891-->

Ab Version 1906: Wenn Sie eine App-Anforderung in der Konsole genehmigen und dann ablehnen, können Sie sie erneut genehmigen. Die App wird auf dem Client erneut installiert, nachdem Sie sie genehmigt haben.  <!-- 4224910 -->

Diesen Genehmigungsprozess können Sie mit dem PowerShell-Cmdlet [Approve-CMApprovalRequest](/powershell/module/configurationmanager/approve-cmapprovalrequest) automatisieren. Ab Version 1902 enthält dieses Cmdlet den Parameter **InstallActionBehavior**. Verwenden Sie diesen Parameter, um festzulegen, ob die Anwendung sofort oder außerhalb der Geschäftszeiten installiert werden soll.<!-- SCCMDocs-pr issue #3418 -->

Ab Version 1906 können Sie erkennen, welche Bereitstellungen eine Genehmigung erfordern. Wählen Sie eine App im Knoten **Anwendungen** aus. Wechseln Sie im Detailbereich zur Registerkarte **Bereitstellungen**. Es wird standardmäßig eine neue Spalte angezeigt: **Genehmigung erforderlich**.

#### <a name="retry-the-install-of-pre-approved-applications"></a><a name="bkmk_retry"></a> Wiederholen der Installation vorab genehmigter Anwendungen

<!--4336307-->
Ab Version 1906 können Sie die Installation einer App wiederholen, die Sie zuvor für einen Benutzer oder ein Gerät genehmigt haben. Die Genehmigungsoption gilt nur für verfügbare Bereitstellungen. Wenn der Benutzer die App deinstalliert oder der erste Installationsvorgang fehlschlägt, wird ihr Zustand von Configuration Manager nicht neu bewertet, sondern es erfolgt eine Neuinstallation. Dieses Feature ermöglicht es einem Supporttechniker, die App-Installation für einen Benutzer, der um Hilfe bittet, schnell zu wiederholen.

1. Öffnen Sie die Configuration Manager-Konsole als Benutzer, der über die Berechtigung **Genehmigen** für das Anwendungsobjekt verfügt. Beispielsweise verfügen die integrierten Rollen **Anwendungsadministrator** und **Anwendungsautor** über diese Berechtigung.

1. Stellen Sie eine App bereit, die eine Genehmigung erfordert, und genehmigen Sie sie.

    > [!Tip]  
    > Alternativ [installieren Sie eine Anwendung für ein Gerät](install-app-for-device.md). Es erstellt eine genehmigte Anforderung für die App auf dem Gerät.  

Wenn die Anwendung nicht erfolgreich installiert werden kann oder der Benutzer die Anwendung deinstalliert, versuchen Sie es mit dem folgenden Verfahren erneut:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungsanforderungen** aus. (In Version 1902 und früher heißt dieser Knoten **Genehmigungsanforderungen**.)

1. Wählen Sie die zuvor genehmigte App aus. Wählen auf dem Menüband in der Gruppe „Genehmigungsanforderung“ **Installation wiederholen** aus.

#### <a name="other-app-approval-resources"></a>Andere Ressourcen zur App-Genehmigung

- [Verbesserungen bei der Genehmigung von Anwendungen in Configuration Manager 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534)
- [Updates für den Genehmigungsprozess von Anwendungen in Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048)

### <a name="require-administrator-approval-if-users-request-this-application"></a><a name="bkmk_prior"></a> Genehmigung durch Administrator erforderlich, wenn Benutzer diese Anwendung anfordern

> [!Note]  
> Diese Erfahrung gilt, wenn Sie die empfohlene [optionale App-Genehmigungserfahrung](#bkmk_opt) nicht aktivieren.

Der Administrator muss Anforderungen für die Anwendung genehmigen, bevor der Benutzer sie installieren kann. Diese Option ist ausgegraut, wenn der Zweck der Bereitstellung **Erforderlich** lautet, oder wenn die Anwendung für eine Gerätesammlung bereitgestellt wird.  

Genehmigungsanforderungen für Anwendungen werden im Arbeitsbereich **Softwarebibliothek** unter **Anwendungsverwaltung** im Knoten **Anwendungsanforderungen** angezeigt. (In Version 1902 und früher heißt dieser Knoten **Genehmigungsanforderungen**.) Wenn eine Anforderung nicht innerhalb von 30 Tagen genehmigt wird, wird sie entfernt. Ausstehende Genehmigungsanforderungen können durch eine Neuinstallation abgebrochen werden.  

Nachdem Sie eine Anwendung für die Installation genehmigt haben, können Sie die Anforderung in der Configuration Manager-Konsole **verweigern**. Diese Aktion bewirkt nicht, dass der Client die Anwendung auf Geräten deinstalliert. Benutzer werden daran gehindert, neue Kopien der Anwendung aus dem Softwarecenter zu installieren.  

## <a name="email-notifications"></a><a name="bkmk_email-approve"></a> E-Mail-Benachrichtigungen

<!--1321550-->

Sie können E-Mail-Benachrichtigungen zum Genehmigen von Anwendungsanforderungen konfigurieren. Wenn ein Benutzer eine Anwendung anfordert, erhalten Sie eine E-Mail. Klicken Sie auf die Links in der E-Mail, um die Anforderung ohne die Configuration Manager-Konsole zu genehmigen oder abzulehnen.

Beim Erstellen einer neuen Bereitstellung für die Anwendung können Sie die E-Mail-Adressen der Benutzer definieren, die die Anforderung genehmigen oder verweigern können. Wenn Sie die Liste der E-Mail-Adressen im Nachhinein bearbeiten müssen, rufen Sie den Arbeitsbereich **Überwachung** auf, erweitern Sie **Warnungen**, und wählen Sie dann den Knoten **Abonnements** aus. Klicken Sie über eines der **Anwendung per E-Mail genehmigen**-Abonnements, das mit Ihrer Anwendungsbereitstellung verknüpft ist, auf **Eigenschaften**.

Wenn mehr als eine Warnung angezeigt wird, können Sie bestimmen, welche Warnung mit welcher Bereitstellung einhergeht. Öffnen Sie die Eigenschaften der Warnung, und zeigen Sie die Liste der **ausgewählten Warnungen** auf der Registerkarte „Allgemein“ an. Die Bereitstellung wird für dieses Abonnement als Warnung aktiviert.

Benutzer können einen Kommentar an die Anforderung im Softwarecenter anfügen. Dieser Kommentar wird in der Anwendungsanforderung in der Configuration Manager-Konsole angezeigt. Ab Version 1902 wird dieser Kommentar auch in der E-Mail angezeigt. Die Aufnahme dieses Kommentars unterstützt die genehmigenden Personen bei der Entscheidungsfindung, ob die Anforderung zu genehmigen oder abzulehnen ist.<!--3594063-->

### <a name="prerequisites"></a>Voraussetzungen

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>Senden von E-Mail-Benachrichtigungen und Ergreifen von Maßnahmen im internen Netzwerk

Durch diese Voraussetzungen erhalten Empfänger eine E-Mail mit einer Benachrichtigung zur Anforderung. Wenn sie sich ebenfalls im internen Netzwerk befinden, können sie die Anforderung über die E-Mail genehmigen oder verweigern.

- Aktivieren Sie das [optionale Feature](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **Anwendungsanforderungen für Benutzer pro Gerät genehmigen**.  

- Konfigurieren Sie [E-Mail-Benachrichtigungen für Warnungen](../../core/servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

    > [!NOTE]
    > Der Administrator, der die Anwendung bereitstellt, braucht die Berechtigung zum Erstellen einer Warnung und eines Abonnements. Wenn er nicht über diese Berechtigungen verfügt, wird am Ende des **Assistenten zum Bereitstellen von Software** ein Fehler angezeigt: „Sie besitzen nicht die erforderlichen Berechtigungen, um diesen Vorgang auszuführen.“<!-- 2810283 -->

- Aktivieren Sie den SMS-Anbieter am primären Standort, um ein Zertifikat zu verwenden.<!--SCCMDocs-pr issue 3135--> Verwenden Sie eine der folgenden Optionen:  

  - (Empfohlen) Aktivieren Sie [Erweitertes HTTP](../../core/plan-design/hierarchy/enhanced-http.md) für den primären Standort.

    > [!Note]  
    > Wenn der primäre Standort ein Zertifikat für den SMS-Anbieter erstellt, wird dieses vom Webbrowser auf dem Client nicht als vertrauenswürdig eingestuft. Anhand Ihrer Sicherheitseinstellungen wird beim Antworten auf eine Anwendungsanforderung möglicherweise eine Sicherheitswarnung angezeigt.  

  - Binden Sie ein PKI-basiertes Zertifikat in IIS manuell an Port 443 auf dem Server, auf dem die SMS-Anbieterrolle am primären Standort gehostet wird.

> [!NOTE]
> Wenn sich mehrere untergeordnete primäre Standorte in einer Hierarchie befinden, konfigurieren Sie diese Voraussetzungen für jeden primären Standort, an dem Sie dieses Feature aktivieren möchten. Die Links in der E-Mail-Benachrichtigung gelten für den Verwaltungsdienst am primären Standort.<!-- 7108472 -->

#### <a name="to-take-action-from-internet"></a>Ergreifen von Maßnahmen über das Internet

Durch diese optionalen, zusätzlichen Voraussetzungen können Empfänger die Anforderung überall genehmigen oder verweigern, sofern sie über Internetzugriff verfügen.

- Aktivieren Sie den Verwaltungsdienst für den SMS-Anbieter über Cloud Management Gateway. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Server und Standortsystemrollen** aus. Wählen Sie den Server mit der Rolle „SMS-Anbieter“ aus. Wählen Sie im Detailbereich die Rolle **SMS-Anbieter** aus, und klicken Sie dann im Menüband der Registerkarte „Standortrolle“ auf **Eigenschaften**. Aktivieren Sie die Option **Datenverkehr vom Configuration Manager-Cloudverwaltungsgateway für den Verwaltungsdienst zulassen**.  

- Für den SMS-Anbieter ist **.NET 4.5.2** oder höher erforderlich.  

- Richten Sie [Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) ein.

- Binden Sie den Standort in die [Azure-Dienste](../../core/servers/deploy/configure/azure-services-wizard.md) für die **Cloudverwaltung** ein.

- Aktivieren Sie [Azure AD-Benutzerermittlung](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

- Konfigurieren Sie die Einstellungen in Azure AD manuell:  

    1. Navigieren Sie zum [Azure-Portal](https://portal.azure.com) als Benutzer mit den Berechtigungen für *Globaler Administrator*. Wechseln Sie zu **Azure Active Directory**, und wählen Sie **App-Registrierungen** aus.  

    1. Wählen Sie die Anwendung aus, die Sie für die **Cloud Management**-Integration für Configuration Manager erstellt haben.  

    1. Wählen Sie im Menü **Verwalten** die Option **Authentifizierung** aus.  

        1. Fügen Sie im Bereich **Umleitungs-URIs** den folgenden Pfad ein: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

        1. Ersetzen Sie `<CMG FQDN>` durch den FQDN (vollqualifizierter Domänenname) Ihres CMG-Diensts (Cloud Management Gateway). Zum Beispiel: GraniteFalls.Contoso.com.  

        1. Klicken Sie dann auf **Speichern**.  

    1. Wählen Sie im Menü **Verwalten** die Option **Manifest** aus.  

        1. Suchen Sie im Bereich „Manifest bearbeiten“ nach der Eigenschaft **oauth2AllowImplicitFlow**.  

        1. Ändern Sie ihren Wert in **TRUE**. Die gesamte Zeile sollte wie die folgende Beispielzeile aussehen: `"oauth2AllowImplicitFlow": true,`  

        1. Wählen Sie **Speichern** aus.  

### <a name="configure-email-approval"></a>Konfigurieren der E-Mail-Genehmigung

1. [Stellen Sie in der Configuration Manager-Konsole eine Anwendung bereit](deploy-applications.md), sofern eine für eine Benutzersammlung verfügbar ist. Aktivieren Sie sie auf der Seite **Bereitstellungseinstellungen** zur Genehmigung. Geben Sie dann E-Mail-Adressen ein, an die Benachrichtigungen gesendet werden sollen. Trennen Sie die E-Mail-Adressen durch Semikolons (`;`).  

     > [!Note]  
     > Alle Benutzer in Ihrer Azure AD-Organisation, die die E-Mail erhalten, können die Anforderung genehmigen. Leiten Sie die E-Mail nur an andere Personen weiter, wenn diese bestimmte Maßnahmen durchführen sollen.  

2. Fordern Sie als Benutzer die Anwendung im Softwarecenter an.  

3. Innerhalb von fünf Minuten erhalten Sie einer E-Mail-Benachrichtigung. Der Inhalt der E-Mail ähnelt dem folgenden Beispiel:  

![Beispiel für eine E-Mail-Benachrichtigung zur Genehmigung von Anwendungen](media/1321550-email.png)

> [!Note]  
> Der Link zum Genehmigen oder Ablehnen steht zur einmaligen Nutzung zur Verfügung. Nehmen Sie beispielsweise an, ein Gruppenalias wird für den Empfang von Benachrichtigungen konfiguriert. Meg genehmigt die Anforderung. Nun kann Bruce die Anforderung nicht ablehnen.  

Überprüfen Sie zur Problembehandlung die Datei **NotiCtrl.log**, die sich auf dem Standortserver befindet.

## <a name="maintenance"></a>Wartung

Configuration Manager speichert die Informationen zu Anforderungen zur Genehmigung von Anwendungen in der Standortdatenbank. Anforderungen, die abgebrochen oder verweigert werden, werden nach 30 Tagen aus dem Anforderungsverlauf des Standorts gelöscht. Sie können dieses Löschverhalten mit dem [Standortwartungstask](../../core/servers/manage/maintenance-tasks.md) **Veraltete Anwendungsanforderungsdaten löschen** konfigurieren. Genehmigte und ausstehende Anwendungsanforderungen werden nie vom Standort gelöscht.