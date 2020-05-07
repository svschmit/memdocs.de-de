---
title: Behandeln von Problemen bei der Richtlinienbereitstellung für den Intune-App-Schutz
description: Hier erfahren Sie, wie Sie Probleme beheben können, die bei der Bereitstellung von Intune-App-Schutzrichtlinien auftreten können.
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.topic: conceptual
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 3b4c02e366f4778e65b4fe4c853ed147fcdb1df3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82072751"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Problembehandlung bei der Richtlinienbereitstellung für den App-Schutz in Intune

## <a name="introduction"></a>Einführung

Dieser Artikel hilft Ihnen, Probleme bei der Anwendung von Richtlinien zum Schutz von Apps in Microsoft Intune zu verstehen und zu beheben. Folgen Sie den Abschnitten, die auf Ihre Situation zutreffen.

## <a name="basic-steps"></a>Grundlegende Schritte

### <a name="collect-initial-data"></a>Sammeln anfänglicher Daten

Bevor Sie mit der Problembehandlung beginnen, sollten Sie einige grundlegende Informationen sammeln, die Ihnen helfen können, das Problem besser zu verstehen und die Zeit für die Lösungsfindung zu verkürzen.

Sammeln Sie die folgenden Informationen:

- Welche Richtlinieneinstellung wird nicht angewendet? Wird überhaupt eine Richtlinie angewendet?
- Wie ist die Benutzererfahrung? Haben Benutzer die gewünschte App installiert und gestartet?
- Wann fing das Problem an? Hat der App-Schutz jemals funktioniert?
- Welche Plattform (Android oder iOS) hat das Problem?
- Wie viele Benutzer sind betroffen? Sind alle oder nur einige Geräte betroffen?
- Wie viele Geräte sind betroffen? Sind alle oder nur einige Geräte betroffen?
- Obwohl die Schutzrichtlinie für Intune-Apps keinen MDM-Dienst (Mobile Device Management) erfordert, verwenden betroffene Benutzer Intune oder einen EMM eines Drittanbieters?
- Sind alle verwalteten Apps oder nur bestimmte Apps betroffen? Sind z. B. Branchenanwendungen mit [Intune App SDK](../developer/app-sdk-get-started.md) betroffen, Store-Apps jedoch nicht?

Anhand der Antworten auf diese Fragen können Sie jetzt mit der Problembehandlung beginnen.

### <a name="verify-prerequisites"></a>Überprüfen der Voraussetzungen

Der nächste Schritt bei der Problembehandlung besteht darin, zu prüfen, ob alle Voraussetzungen erfüllt sind.

Obwohl Sie Intune-App-Schutzrichtlinien unabhängig von jeder MDM-Lösung verwenden können, müssen die folgenden Voraussetzungen erfüllt sein:

- Dem Benutzer muss eine Intune-Lizenz zugewiesen sein.
- Der Benutzer muss zu einer Sicherheitsgruppe gehören, für die eine App-Schutzrichtlinie gilt. Die gleiche App-Schutzrichtlinie muss auf die verwendete App ausgerichtet sein.
- Bei Android-Geräten ist die Unternehmensportal-App erforderlich, um App-Schutzrichtlinien zu erhalten.
- Wenn Sie [Word-, Excel- oder PowerPoint](https://products.office.com/business/office)-Apps verwenden, müssen die folgenden zusätzlichen Anforderungen erfüllt sein:
    - Mit dem Azure Active Directory-Konto (Azure AD) des Benutzers muss eine Lizenz für [Microsoft 365 Business oder Enterprise](https://products.office.com/business/compare-more-office-365-for-business-plans) verknüpft sein. Das Abonnement muss die Office-Apps auf mobilen Geräten enthalten und kann ein Cloudspeicherkonto mit [OneDrive for Business](https://onedrive.live.com/about/business/) umfassen. Office 365-Lizenzen können im [Microsoft 365 Admin Center](https://admin.microsoft.com) zugewiesen werden. Befolgen Sie dazu diese [Anweisungen](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).
    - Der Benutzer muss über einen verwalteten Speicherort verfügen, der mit der differenzierten Funktion **Speichern unter** konfiguriert ist. Dieser Befehl befindet sich unter der Einstellung **Kopien von Organisationsdaten speichern** für die Anwendungsschutzrichtlinie. Wenn z. B. der verwaltete Speicherort OneDrive ist, muss die [OneDrive](https://onedrive.live.com/about/)-App in der Word-, Excel- oder PowerPoint-App des Benutzer konfiguriert werden.
    - Wenn der verwaltete Speicherort OneDrive ist, muss die App unter die App-Schutzrichtlinie fallen, die für den Benutzer angegeben ist.

  > [!NOTE]
  > Die mobilen Office-Apps unterstützen zurzeit nur SharePoint Online, nicht jedoch SharePoint lokal.

- Wenn Sie Intune-App-Schutzrichtlinien zusammen mit lokalen Ressourcen (Microsoft Skype for Business und Microsoft Exchange Server) verwenden, müssen Sie [HMA (hybride moderne Authentifizierung) für Skype for Business und Exchange aktivieren](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview).

Intune-App-Schutzrichtlinien erfordern, dass die Identität des Benutzers zwischen der App und dem [Intune App SDK](../developer/app-sdk-get-started.md) konsistent ist. Die einzige Möglichkeit, diese Konsistenz zu garantieren, ist eine moderne Authentifizierung. Es gibt Szenarien, in denen Apps in einer lokalen Konfiguration ohne moderne Authentifizierung funktionieren können. Die Ergebnisse sind jedoch weder konsistent noch gewährleistet.

Weitere Informationen darüber, wie Sie HMA für hybride und lokale Konfigurationen von Skype for Business aktivieren können, finden Sie in den folgenden Artikeln:

- **Hybrid**<br>
[Hybride moderne Authentifizierung für SfB und Exchange wird allgemein verfügbar](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **Lokal**<br>
[Moderne Authentifizierung für lokales SfB mit AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>Prüfen des App-Schutzrichtlinienstatus

Gehen Sie wie folgt vor, um den Schutzstatus Ihrer App zu überprüfen:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Klicken Sie auf **Apps** > **Überwachen** > **Status des App-Schutzes** und dann auf die Kachel **Zugewiesene Benutzer**.
3. Klicken Sie auf der Seite **App-Berichterstellung** auf **Benutzer auswählen**, um eine Liste von Benutzern und Gruppen anzuzeigen.
4. Suchen und wählen Sie einen der betroffenen Benutzer aus der Liste aus, und wählen Sie dann **Benutzer auswählen** aus. Im oberen Bereich von „App-Berichterstellung“ können Sie sehen, ob der Benutzer für den App-Schutz und O365 lizenziert ist. Sie können auch den App-Status für alle Geräte des Benutzers anzeigen.
5. Notieren Sie sich wichtige Informationen wie die Zielanwendungen, Gerätetypen, Richtlinien, den Check-In-Status des Geräts und den Zeitpunkt der letzten Synchronisierung.

> [!NOTE]
> App-Schutzrichtlinien werden nur angewendet, wenn Apps im beruflichen Kontext verwendet werden. Dies ist z. B. der Fall, wenn der Benutzer über ein Geschäftskonto auf Apps zugreift.

Weitere Informationen finden Sie unter [Überprüfen der Einrichtung von App-Schutzrichtlinien in Microsoft Intune](../apps/app-protection-policies-validate.md).

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>Überprüfen Sie, ob die Benutzeridentität zwischen der App und dem Intune App SDK konsistent ist.

In den meisten Szenarien melden sich die Benutzer mit ihrem Benutzerprinzipalnamen (UPN) bei ihren Konten an. In einigen Umgebungen (z. B. in lokalen Szenarien) können Benutzer jedoch eine andere Form von Anmeldeinformationen verwenden. In diesen Fällen könnten Sie feststellen, dass der in der App verwendete UPN nicht mit dem UPN-Objekt in Azure AD übereinstimmt. Wenn dieses Problem auftritt, werden die App-Schutzrichtlinien nicht wie erwartet angewendet.

Die von Microsoft empfohlenen bewährten Methoden bestehen darin, den UPN der primären SMTP-Adresse zuzuordnen. Diese Vorgehensweise ermöglicht es Benutzern, sich mit einer einheitlichen Identität bei verwalteten Apps, dem Intune-App-Schutz und anderen Azure AD-Ressourcen anzumelden. Weitere Informationen finden Sie unter [Azure AD UserPrincipalName-Auffüllung](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

Wenn Ihre Umgebung alternative Anmeldemethoden erfordert, finden Sie weitere Informationen unter [Konfigurieren einer alternativen Anmelde-ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id), insbesondere unter [Hybride moderne Authentifizierung mit alternativer ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### <a name="verify-that-the-user-is-targeted"></a>Überprüfen Sie, ob der Benutzer das Ziel ist

Die Intune-App-Schutzrichtlinien müssen auf Benutzer ausgerichtet werden. Wenn Sie die App-Schutzrichtlinie keinem Benutzer oder keiner Benutzergruppe zuweisen, wird die Richtlinie nicht angewendet.

Führen Sie die folgenden Schritte aus, um zu überprüfen, ob die Richtlinie auf den Zielbenutzer angewendet wird:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Überwachen** > **App-Schutzstatus** und dann die Kachel **Benutzerstatus** aus (basierend auf der Betriebssystemplattform des Geräts).
Wählen Sie im sich öffnenden Bereich **App-Berichterstellung** die Option **Benutzer auswählen** aus, um nach einem Benutzer zu suchen.
3. Wählen Sie den Benutzer in der Liste aus. Die Details zu diesem Benutzer werden angezeigt.

Wenn Sie die Richtlinie einer Benutzergruppe zuweisen, stellen Sie sicher, dass der Benutzer der Benutzergruppe angehört. Gehen Sie hierzu folgendermaßen vor:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Gruppen > Alle Gruppen** aus, und suchen Sie dann die Gruppe, die für Ihre App-Schutzrichtlinienzuweisung verwendet wird. Anschließend wählen Sie sie aus.
3. Wählen Sie unter dem Abschnitt **Verwalten** die Option **Mitglieder** aus.
4. Wenn der betroffene Benutzer nicht aufgeführt ist, überprüfen Sie [App- und Ressourcenzugriff mithilfe von Azure Active Directory-Gruppen verwalten](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) und Ihre Gruppenmitgliedschaftsregeln. Stellen Sie sicher, dass der betroffene Benutzer in der Gruppe enthalten ist.
5. Stellen Sie sicher, dass der betroffene Benutzer nicht zu einer Gruppe gehört, die von der Richtlinie ausgeschlossen ist.

> [!IMPORTANT]
> - Die Intune-App-Schutzrichtlinie muss Benutzergruppen und nicht Gerätegruppen zugewiesen werden.
> - Wenn das betroffene Gerät das Apple-Programm zur Geräteregistrierung (DEP) verwendet, stellen Sie sicher, dass **Benutzeraffinität** aktiviert ist. User Affinity ist für alle Apps erforderlich, die Benutzerauthentifizierung unter DEP benötigen.
> - Wenn das betroffene Gerät Android Enterprise verwendet, unterstützen nur Arbeitsprofile die App-Schutzrichtlinien.


### <a name="verify-that-the-managed-app-is-targeted"></a>Überprüfen Sie, ob die verwaltete App das Ziel ist

Wenn Sie Intune-App-Schutzrichtlinien konfigurieren, müssen die Zielanwendungen das [Intune App SDK](../developer/app-sdk-get-started.md) verwenden. Andernfalls funktionieren die App-Schutzrichtlinien möglicherweise nicht ordnungsgemäß.

Stellen Sie sicher, dass die Zielanwendung in [Durch Microsoft Intune geschützte Apps](../apps/apps-supported-intune-apps.md) aufgeführt ist. Stellen Sie bei Branchen- oder benutzerdefinierten Apps sicher, dass die Apps die neueste Version des [Intune App SDK](../developer/app-sdk-get-started.md) verwenden. Beachten Sie dabei Folgendes:

Für iOS ist diese Vorgehensweise wichtig, da jede Version Korrekturen enthält, die sich auf die Anwendung dieser Richtlinien und ihre Funktionsweise auswirken. Weitere Informationen finden Sie unter [Intune App SDK – iOS-Versionen](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases).
Für Android ist diese Vorgehensweise nicht so wichtig. Die Benutzer müssen jedoch die neueste Version der Unternehmensportal-App installiert haben, da die Unternehmensportal-App als Broker-Agent für die Richtlinien fungiert.

> [!NOTE]
> Ab September 2019 wird Intune iOS-Apps mit Intune App SDK 8.1.1 und höher unterstützen. Apps, die mit SDK-Versionen erstellt wurden, die älter als 8.1.1 sind, werden nicht mehr unterstützt. 

## <a name="more-information"></a>Weitere Informationen

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Spezielle Anforderungen für Intune MDM-verwaltete Geräte

Wenn Sie eine App-Schutzrichtlinie erstellen, können Sie sie auf alle App-Typen oder auf die folgenden App-Typen ausrichten:

- Apps auf nicht verwalteten Geräten
- Apps auf durch Intune verwalteten Geräten
- Apps im Android-Arbeitsprofil

> [!NOTE] 
> Um die App-Typen anzugeben, legen Sie **Auf alle App-Typen ausrichten** auf **Nein** fest, und wählen Sie dann aus der Liste **App-Typen** aus.

Für iOS sind die folgenden zusätzlichen [App-Konfigurationseinstellungen](../apps/app-configuration-policies-use-ios.md) erforderlich, um App-Schutzrichtlinieneinstellungen für Apps auf in Intune registrierten Geräten bereitzustellen:

- **IntuneMAMUPN** muss für alle mit MDM (Intune oder Drittanbieter-EMM) verwalteten Anwendungen konfiguriert sein. Weitere Informationen finden Sie unter „Konfigurieren der Benutzer-UPN-Einstellung für Microsoft Intune oder Drittanbieter-EMM“.
- **IntuneMAMDeviceID** muss für alle mit MDM verwalteten Drittanbieter- und Branchenanwendungen konfiguriert sein.
- **IntuneMAMDeviceID** muss als Geräte-ID-Token konfiguriert sein. Beispiel: key=IntuneMAMDeviceID, value={{deviceID}}. Weitere Informationen finden Sie unter [Hinzufügen von App-Konfigurationsrichtlinien für verwaltete iOS-Geräte](../apps/app-configuration-policies-use-ios.md).
- Wenn nur der **IntuneMAMDeviceID**-Wert konfiguriert ist, betrachtet die Intune-App das Gerät als „nicht verwaltet“.

### <a name="scenario-policy-changes-are-not-working"></a>Szenario: Richtlinienänderungen funktionieren nicht
Das [Intune App SDK](../developer/app-sdk-get-started.md) prüft regelmäßig auf Richtlinienänderungen. Dieser Prozess kann sich jedoch aus einem der folgenden Gründe verzögern:

- Die App hat sich nicht beim Dienst angemeldet.
- Die Unternehmensportal-App wurde von dem Gerät entfernt.

Die Intune-App-Schutzrichtlinie stützt sich auf die Benutzeridentität. Daher sind eine gültige Anmeldung, die ein Geschäfts-, Schul- oder Unikonto für die App verwendet, und eine konsistente Verbindung zum Dienst erforderlich. Wenn sich der Benutzer nicht bei der Anwendung angemeldet hat oder die Unternehmensportal-App von dem Gerät entfernt wurde, gelten die Richtlinienaktualisierungen nicht.

Es kann zudem bis zu 8 Stunden dauern, bis Änderungen und Aktualisierungen für App-Schutzrichtlinien angewendet werden. Gegebenenfalls erzwingt das Schließen aller Apps und der Neustart des Geräts in der Regel eine frühere Anwendung der Richtlinienaktualisierung.

Gehen Sie wie folgt vor, um den Schutzstatus der App zu überprüfen:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Klicken Sie auf **Apps** > **Überwachen** > **Status des App-Schutzes** und dann auf die Kachel **Zugewiesene Benutzer**.
3. Klicken Sie auf der Seite „App-Berichterstellung“ auf **Benutzer auswählen**, um eine Liste von Benutzern und Gruppen zu öffnen.
4. Suchen und wählen Sie einen der betroffenen Benutzer aus der Liste aus, und wählen Sie dann **Benutzer auswählen** aus.
5. Überprüfen Sie die derzeit angewandten Richtlinien, einschließlich des Status und der letzten Synchronisierungszeit.
6. Wenn der Status **Nicht eingecheckt** lautet oder wenn die Anzeige anzeigt, dass kürzlich keine Synchronisierung erfolgt ist, prüfen Sie, ob der Benutzer über eine konsistente Netzwerkverbindung verfügt. Stellen Sie für Android-Benutzer sicher, dass sie die neueste Version der Unternehmensportal-App installiert haben.

> [!IMPORTANT]
> Das [Intune App SDK](../developer/app-sdk-get-started.md) prüft alle 30 Minuten auf die selektive Zurücksetzung. Änderungen an bestehenden Richtlinien für Benutzer, die bereits angemeldet sind, werden jedoch möglicherweise bis zu 8 Stunden lang nicht angezeigt. Um diesen Prozess zu beschleunigen, sollten sich die Benutzer von der App abmelden und dann wieder anmelden oder ihre Geräte neu starten.

Die Intune-App-Schutzrichtlinie umfasst die Unterstützung mehrerer Identitäten. Intune kann die App-Schutzrichtlinien nur auf das Geschäfts-, Schul- oder Unikonto anwenden, das bei der App angemeldet ist. Es wird jedoch nur ein Geschäfts-, Schul- oder Unikonto pro Gerät unterstützt.

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>Szenario: Die Richtlinie wird angewendet, aber iOS-Benutzer können dennoch Arbeitsdateien an nicht verwaltete Apps übertragen
Mit dem Feature **Open in Management** (![Schaltfläche „Open-in“](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg)) für iOS-Geräte kann die Übertragung von Dateien zwischen Apps, die über den MDM-Kanal bereitgestellt werden, eingeschränkt werden. Je nach Konfiguration kann der Benutzer Arbeitsdateien von verwalteten Speicherorten wie OneDrive und Exchange auf nicht verwaltete Apps oder Speicherorte übertragen. Das iOS-Feature **Open in Management** funktioniert außerhalb anderer Datenübertragungsmethoden. Daher wird sie von den Einstellungen **Speichern unter** und **Kopieren/Einfügen** nicht beeinflusst.

Sie können Intune-App-Schutzrichtlinien zusammen mit dem iOS-Feature **Open in Management** verwenden, um Unternehmensdaten wie folgt zu schützen:

- **Mitarbeitereigene Geräte, die nicht von einer MDM-Lösung verwaltet werden**: Sie können die Einstellungen der App-Schutzrichtlinie so festlegen, dass die **App nur Daten an per Richtlinien verwaltete Apps übertragen darf**. Bei dieser Konfiguration bietet das **Open-In**-Verhalten in einer per Richtlinie verwalteten App nur andere per Richtlinie verwaltete Apps als Optionen für die Freigabe an. Wenn ein Benutzer z. B. versucht, eine geschützte Datei als Anhang von OneDrive in der nativen E-Mail-App zu senden, ist diese Datei nicht lesbar.

- **Geräte, die mithilfe einer MDM-Lösung verwaltet werden**: Bei Geräten, die in Intune oder MDM-Drittanbieterlösungen registriert sind, wird die gemeinsame Datennutzung durch Apps mit App-Schutzrichtlinien und andere verwaltete, über MDM bereitgestellte iOS-Apps von der Intune-App und dem **Open in Management**-Feature von iOS gesteuert.<br/><br/>
Wenn Sie sicherstellen möchten, dass Apps, die Sie mithilfe einer MDM-Lösung bereitstellen, auch den Intune-App-Schutzrichtlinien zugeordnet werden, konfigurieren Sie die Benutzer-UPN-Einstellung gemäß der Beschreibung in [Konfigurieren der Benutzer-UPN-Einstellung](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).<br/><br/>Um festzulegen, wie Daten an andere Apps übertragen werden sollen, aktivieren Sie die Einstellung **Organisationsdaten an andere Apps senden**, und wählen Sie die gewünschte Freigabestufe aus.<br/><br/>Um festzulegen, wie eine App Daten von anderen Apps empfangen soll, aktivieren Sie die Einstellung **Daten von anderen Apps empfangen**, und wählen Sie die gewünschte Datenempfangsstufe aus.

Weitere Informationen zum Empfangen und Freigeben von App-Daten finden Sie unter [Einstellungen für die Datenverlagerung](../apps/app-protection-policy-settings-ios.md#data-protection).

Weitere Informationen finden Sie unter [Verwalten der Datenübertragung zwischen iOS-Apps in Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md).

## <a name="references"></a>Verweise

Wenn Sie immer noch auf der Suche nach einer Lösung für ein verwandtes Problem oder nach weiteren Informationen zu Intune sind, posten Sie eine Frage in unserem [Microsoft Intune-Forum](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Viele Supporttechniker, MVPs und Mitglieder unseres Entwicklungsteams besuchen die Foren. Es besteht also eine gute Chance, dass Sie jemanden finden, der über die erforderlichen Informationen verfügt.

Informationen zum Öffnen einer Supportanfrage für das Microsoft Intune-Produktsupportteam finden Sie unter [Anfordern von Support für Microsoft Intune](../fundamentals/get-support.md).

Weitere Informationen zur Intune-App-Schutzrichtlinie finden Sie in den folgenden Artikeln:

- [Behandlung bei Verwaltungsproblemen von mobilen Geräten](../apps/troubleshoot-mam.md)
- [Häufig gestellte Fragen zu MAM und App-Schutz](../apps/mam-faq.md)
- [Tipp zur Unterstützung: Problembehandlung bei Intune-App-Schutzrichtlinien mithilfe von Protokolldateien auf lokalen Geräten](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

Alle aktuellen Neuigkeiten, Informationen und technischen Tipps finden Sie in den offiziellen Blogs:

- [Blog des Microsoft Intune-Supportteams](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Blog von Microsoft Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zur Intune-Problembehandlung finden Sie unter [Verwenden des Problembehandlungsportals zur Unterstützung von Benutzern Ihres Unternehmens](../fundamentals/help-desk-operators.md). 
- Erfahren Sie mehr über bekannte Probleme in Microsoft Intune. Weitere Informationen finden Sie unter [Intune Customer Success](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Benötigen Sie zusätzliche Hilfe? Weitere Informationen finden Sie unter [Anfordern von Support für Microsoft Intune](../fundamentals/get-support.md).
