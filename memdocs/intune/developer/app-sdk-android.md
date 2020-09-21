---
title: Entwicklerhandbuch zum Microsoft Intune App SDK für Android
description: Das Microsoft Intune App SDK für Android ermöglicht die Integration von Intune Mobile App Management (MAM) in Ihre Android-App.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 0100e1b5-5edd-4541-95f1-aec301fb96af
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5b29043956a86934f7b1be18606d0b78f25dc50
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608455"
---
# <a name="microsoft-intune-app-sdk-for-android-developer-guide"></a>Entwicklerhandbuch zum Microsoft Intune App SDK für Android

> [!NOTE]
> Lesen Sie am besten zuerst die [Übersicht über das Intune App SDK](app-sdk.md). Dort finden Sie Informationen zu den aktuellen Features des SDK sowie zu den Vorbereitungen, die Sie auf den verschiedenen unterstützten Plattformen für die Integration treffen müssen.
>
> Informationen zum Herunterladen des SDK finden Sie unter [Herunterladen der SDK-Dateien](../developer/app-sdk-get-started.md#download-the-sdk-files).

Mit dem Microsoft Intune App SDK für Android können Sie die Intune-App-Schutzrichtlinien (auch als **APP**- oder MAM-Richtlinien bezeichnet) in Ihre native Android-App integrieren. Mit Intune verwaltete Anwendungen sind in das Intune App SDK integrierte Anwendungen. Intune-Administratoren können ganz einfach App-Schutzrichtlinien für Ihre mit Intune verwaltete App bereitstellen, wenn diese aktiv von Intune verwaltet wird.


## <a name="whats-in-the-sdk"></a>Inhalt des SDK

Das Intune App SDK besteht aus den folgenden Dateien:

* **Microsoft.Intune.MAM.SDK.aar:** Die SDK-Komponenten, mit Ausnahme der JAR-Dateien der Unterstützungsbibliothek.
* **Microsoft.Intune.MAM.SDK.Suppbzw.t.v4.jar**: Die Klassen, die zum Aktivieren von MAM in Apps erforderlich sind, die die Unterstützungsbibliothek von Android Version 4 nutzen.
* **Microsoft.Intune.MAM.SDK.Suppbzw.t.v7.jar**: Die Klassen, die zum Aktivieren von MAM in Apps erforderlich sind, die die Unterstützungsbibliothek von Android Version 7 nutzen.
* **Microsoft.Intune.MAM.SDK.Support.v17.jar:** Die Klassen, die zum Aktivieren von MAM in Apps erforderlich sind, die die Unterstützungsbibliothek von Android Version 17 nutzen. 
* **Microsoft.Intune.MAM.SDK.Support.Text.jar:** Die Klassen, die zum Aktivieren von MAM in Apps erforderlich sind, die die Klassen der Android-Unterstützungsbibliothek im `android.support.text`-Paket nutzen.
* **Microsoft.Intune.MAM.SDK.DownlevelStubs.aar**: Diese AAR-Datei enthält Stubs für Android-Systemklassen, die nur auf neueren Geräten vorhanden sind, auf die aber Methoden in `MAMActivity` verweisen. Neuere Geräte ignorieren diese Stubklassen. Diese AAR-Datei ist nur dann notwendig, wenn Ihre App einen Reflexionvorgang auf Klassen anwendet, die von `MAMActivity` abgeleitet sind. Die meisten Apps müssen sie nicht einbinden. Die AAR-Datei enthält ProGuard-Regeln, um alle zugehörigen Klassen auszuschließen.
* **com.microsoft.intune.mam.build.jar:** Ein Gradle-Plug-In, das die [Integration des SDK unterstützt](#build-tooling).
* **CHANGELOG.md**: Stellt eine Aufzeichnung der Änderungen bereit, die in den einzelnen SDK-Versionen vorgenommen wurden.
* **THIRDPARTYNOTICES.TXT:**  Ein Urheberrechtshinweis für Drittanbieter- und/oder OSS-Code, der in Ihrer App kompiliert wird.


## <a name="requirements"></a>Anforderungen

### <a name="android-versions"></a>Android-Versionen
Das SDK unterstützt Android API 21 (Android 5.0) bis Android API 29 (Android 10.0) vollständig. Es kann in eine App mit der niedrigen Android minSDKVersion 14 integriert werden. In diesen alten Betriebssystemversionen können die Intune-Unternehmensportal-App jedoch nicht installiert und die MAM-Richtlinien nicht verwendet werden.

### <a name="company-portal-app"></a>Unternehmensportal-App
Das Intune App SDK für Android ist darauf angewiesen, dass die [Unternehmensportal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)-App auf dem Gerät vorhanden ist, damit App-Schutzrichtlinien aktiviert werden können. Das Unternehmensportal ruft App-Schutzrichtlinien vom Intune-Dienst ab. Wenn die App initialisiert wird, lädt sie die entsprechende Richtlinie sowie Code, um diese Richtlinie vom Unternehmensportal zu erzwingen.

> [!NOTE]
> Wenn sich die Unternehmensportal-App nicht auf dem Gerät befindet, verhält sich eine mit Intune verwaltete App genauso wie eine normale App, die keine Intune-App-Schutzrichtlinien unterstützt.

Für einen App-Schutz ohne Registrierung des Geräts muss der Benutzer das Gerät _**nicht**_ mithilfe der Unternehmensportal-App registrieren.

## <a name="sdk-integration"></a>SDK-Integration

### <a name="sample-app"></a>Beispiel-App
Ein Beispiel für eine ordnungsgemäße Integration mit dem Intune App SDK ist auf [GitHub](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Android-App) verfügbar. In diesem Beispiel wird das [Gradle-Build-Plug-In](#gradle-build-plugin) verwendet.

### <a name="referencing-intune-app-libraries"></a>Verweisen auf Intune App-Bibliotheken

Das Intune App SDK ist eine Android-Standardbibliothek ohne externe Abhängigkeiten. **Microsoft.Intune.MAM.SDK.aar** enthält sowohl die Schnittstellen, die für die Aktivierung der App-Schutzrichtlinie erforderlich sind, als auch den für die Zusammenarbeit mit der Unternehmensportal-App von Microsoft Intune erforderlichen Code.

**Microsoft.Intune.MAM.SDK.aar** muss als Android-Bibliotheksverweis angegeben werden. Öffnen Sie dazu Ihr App-Projekt in Android Studio, und wechseln Sie zu **File > New > New module** (Datei > Neu > Neues Modul), und wählen Sie dann **Import .JAR/.AAR Package** (JAR/AAR-Paket importieren) aus. Wählen Sie dann das Android-Archivpaket „Microsoft.Intune.MAM.SDK.aar“ aus, um ein Modul für den Dateityp *AAR* zu erstellen. Führen Sie einen Rechtsklick auf das Modul oder die Module aus, die Ihren App-Code enthalten, und navigieren Sie wie folgt: **Module Settings** > **Dependencies tab** >  **+ icon** > **Module dependency** > Select the MAM SDK AAR module you just created > **OK** (Moduleinstellungen > Registerkarte „Abhängigkeiten“ > +-Symbol > Modulabhängigkeit > Wählen Sie das MAM SDK AAR-Modul aus, das Sie gerade erstellt haben > OK). Damit stellen Sie sicher, dass Ihr Modul mit dem MAM SDK kompiliert wird, wenn Sie Ihr Projekt erstellen.

Zusätzlich enthalten die **Microsoft.Intune.MAM.SDK.Support.XXX.jar**-Bibliotheken Intune-Varianten der entsprechenden `android.support.XXX`-Bibliotheken. Sie sind nicht in Microsoft.Intune.MAM.SDK.aar integriert, falls eine App nicht von den Unterstützungsbibliotheken abhängig sein muss.

#### <a name="proguard"></a>ProGuard

Wenn [ProGuard](http://proguard.sourceforge.net/) (oder ein beliebiger anderer Komprimierungs- oder Obfuskationsmechanismus) als Buildschritt verwendet wird, verfügt das SDK über zusätzliche Konfigurationsregeln, die hinzugefügt werden müssen. Wenn Sie die *AAR*-Datei in Ihren Build einschließen, werden unsere Regeln automatisch in den ProGuard-Schritt integriert, und die erforderlichen Klassendateien werden beibehalten.

Die Azure Active Directory Authentication Librarys (ADAL) weisen möglicherweise eigene ProGuard-Einschränkungen auf. Wenn Ihre App ADAL integriert, müssen Sie hinsichtlich dieser Einschränkungen der ADAL-Dokumentation folgen.

### <a name="policy-enforcement"></a>Richtlinienerzwingung
Das Intune App SDK ist eine Android-Bibliothek, die es Ihrer App ermöglicht, die Erzwingung von Intune-Richtlinien zu unterstützen und daran teilzunehmen. 

Die meisten Richtlinien werden halbautomatisch durchgesetzt, aber bestimmte Richtlinien erfordern [zur Erzwingung eine explizite Teilnahme Ihrer App ](#enable-features-that-require-app-participation).
Unabhängig davon, ob Sie die Quelle integrieren, oder Buildtools für die Integration verwenden, müssen die Richtlinien, die eine explizite Teilnahme erforderlich machen, im Code berücksichtigt werden.

Für Richtlinien, die automatisch durchgesetzt werden, erfordern Apps die Vererbung von mehreren Android-Basisklassen durch Vererbung von MAM-Äquivalenten und ebenso Aufrufe von bestimmten Android-Systemdienstklassen durch Aufrufe von MAM-Äquivalenten zu ersetzen. Die spezifischen Ersetzungen, die erforderlich sind, werden [unten](#class-and-method-replacements) aufgeführt und können manuell in Form einer Quellintegration oder automatisch mithilfe von Buildtools ausgeführt werden.

### <a name="build-tooling"></a>Erstellen von Tools
Das SDK stellt Buildtools zur Verfügung (ein Plug-In für Gradle-Builds und ein Befehlszeilentool für Nicht-Gradle-Builds), die die gleichwertigen MAM-Ersetzungen automatisch durchführen. Diese Tools transformieren die durch die Java-Kompilierung erstellten Klassendateien und ändern nicht den ursprünglichen Quellcode.

Die Tools führen nur [direkte Ersetzungen](#class-and-method-replacements) durch. Sie führen keine komplexeren SDK-Integrationen wie [Speichern-unter-Richtlinie](#enable-features-that-require-app-participation), [Mehrere Identitäten](#multi-identity-optional), [App-WE-Registrierung](#app-protection-policy-without-device-enrollment), [AndroidManifest-Änderungen](#manifest-replacements) oder [ADAL-Konfiguration](#configure-azure-active-directory-authentication-library-adal) durch, sodass diese abgeschlossen sein müssen, bevor Ihre App vollständig für Intune aktiviert ist. Lesen Sie den Rest dieser Dokumentation sorgfältig durch, um herauszufinden, welche Integrationspunkte für Ihre Anwendung relevant sind.

> [!NOTE]
> Es ist in Ordnung, die Tools im Rahmen eines Projekts auszuführen, das bereits eine teilweise oder vollständige Quellintegration des MAM SDK durch manuelle Ersetzungen durchgeführt hat. Ihr Projekt muss das MAM SDK weiterhin als Abhängigkeit auflisten.

### <a name="gradle-build-plugin"></a>Gradle-Build-Plug-In
Wenn Ihre App nicht mit Gradle erstellt wird, wechseln Sie zu [Integration mit dem Befehlszeilentool](#command-line-build-tool). 

Das App SDK-Plug-In wird als Teil des SDK als **GradlePlugin/com.microsoft.intune.mam.build.jar** verteilt. Damit Gradle das Plug-In finden kann, muss es dem Buildscript-Klassenpfad hinzugefügt werden. Das Plug-In hängt von [Javassist](https://jboss-javassist.github.io/javassist/) ab, das ebenfalls hinzugefügt werden muss. Fügen Sie Folgendes zu Ihrem `build.gradle`-Stammverzeichnis hinzu, um diese dem Klassenpfad hinzuzufügen.

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.javassist:javassist:3.22.0-GA"
        classpath files("$PATH_TO_MAM_SDK/GradlePlugin/com.microsoft.intune.mam.build.jar")
    }
}
```

Wenden Sie dann in der Datei `build.gradle` für Ihr APK-Projekt das Plug-In einfach an als

```groovy
apply plugin: 'com.microsoft.intune.mam'
```

Standardmäßig wird das Plug-In **nur** auf `project`-Abhängigkeiten angewendet.
Die Testkompilierung ist nicht betroffen. Die Konfiguration kann für die Liste bereitgestellt werden.
* Auszuschließende Projekte
* [Einzubeziehende externe Abhängigkeiten](#usage-of-includeexternallibraries) 
* Von der Verarbeitung auszuschließende bestimmte Klassen
* Von der Verarbeitung auszuschließende Varianten. Diese können sich entweder auf einen vollständigen Variantennamen oder auf einen einzelnen Typ beziehen. Beispiel:
  * Wenn Ihre App die Buildtypen `debug` und `release` mit den Typen {`savory`, `sweet`} und {`vanilla`, `chocolate`} aufweist, können Sie Folgendes angeben
  * `savory`, um alle Varianten mit dem Typ „savory“ auszuschließen, oder `savoryVanillaRelease`, um nur genau diese Variante auszuschließen.

#### <a name="example-partial-buildgradle"></a>Beispiel für partielles build.gradle

```groovy

apply plugin: 'com.microsoft.intune.mam'

dependencies {
    implementation project(':product:FooLib')
    implementation project(':product:foo-project')
    implementation fileTree(dir: "libs", include: ["bar.jar"])
    implementation fileTree(dir: "libs", include: ["zap.jar"])
    implementation "com.contoso.foo:zap-artifact:1.0.0"
    implementation "com.microsoft.bar:baz:1.0.0"
    implementation "com.microsoft.qux:foo:2.0"

    // Include the MAM SDK
    implementation files("$PATH_TO_MAM_SDK/Microsoft.Intune.MAM.SDK.aar")
}
intunemam {
    excludeProjects = [':product:FooLib']
    includeExternalLibraries = ['bar.jar', "com.contoso.foo:zap-artifact", "com.microsoft.*", "!com.microsoft.qux*"]
    excludeClasses = ['com.contoso.SplashActivity']
    excludeVariants=['savory']
}
```

Dies hätte folgende Auswirkungen:
* `:product:FooLib` wird nicht neu geschrieben, da es in `excludeProjects` enthalten ist
* `:product:foo-project` wird neu geschrieben, mit Ausnahme von `com.contoso.SplashActivity`, das übersprungen wird, da es sich in `excludeClasses` befindet
* `bar.jar` wird neu geschrieben, da es in `includeExternalLibraries` enthalten ist
* `zap.jar` wird **nicht** neu geschrieben, da es sich nicht um ein Projekt handelt und es nicht in `includeExternalLibraries` enthalten ist
* `com.contoso.foo:zap-artifact:1.0.0` wird neu geschrieben, da es in `includeExternalLibraries` enthalten ist
* `com.microsoft.bar:baz:1.0.0` wird neu geschrieben, da es in `includeExternalLibraries` über einen Platzhalter (`com.microsoft.*`) enthalten ist
* `com.microsoft.qux:foo:2.0` wird nicht neu geschrieben, obwohl dieses Element mit demselben Platzhalter übereinstimmt wie das vorherige Element, da es explizit über ein Negationsmuster ausgeschlossen wird.

#### <a name="usage-of-includeexternallibraries"></a>Verwendung von includeExternalLibraries

Da das Plug-In standardmäßig nur mit Projektabhängigkeiten arbeitet (normalerweise von der Funktion `project()` bereitgestellt), müssen alle von `fileTree(...)` angegebenen oder von maven oder anderen Paketquellen (z. B. „`com.contoso.bar:baz:1.2.0`“) bezogenen Abhängigkeiten der `includeExternalLibraries`-Eigenschaft zur Verfügung gestellt werden, wenn eine MAM-Verarbeitung von ihnen basierend auf den unten erläuterten Kriterien erforderlich ist. Platzhalter („*“) werden unterstützt. Ein Element, das mit `!` beginnt, ist eine Negation und kann verwendet werden, um Bibliotheken auszuschließen, die andernfalls von einem Platzhalter eingeschlossen werden würden.

Bei der Angabe externer Abhängigkeiten mit Artefaktnotation wird empfohlen, die Versionskomponente im Wert `includeExternalLibraries` wegzulassen. Wenn Sie die Version einbeziehen, muss es sich um die genaue Version handeln. Dynamische Versionsspezifikationen (z. B. `1.+`) werden nicht unterstützt.

Die allgemeine Regel zur Ermittlung, ob Sie Bibliotheken in `includeExternalLibraries` aufnehmen müssen, basiert auf zwei Fragen:
1. Enthält die Bibliothek Klassen, für die es MAM-Entsprechungen gibt? Beispiele: `Activity`, `Fragment`, `ContentProvider`, `Service` usw.
2. Verwendet Ihre App in diesem Fall diese Klassen?

Wenn Sie auf diese beiden Fragen mit „Ja“ antworten, müssen Sie diese Bibliothek in `includeExternalLibraries` einbeziehen. 

| Szenario | Sollte enthalten? |
|--|--|
| Sie schließen eine PDF-Viewer-Bibliothek in Ihre App ein und verwenden den Viewer `Activity` in Ihrer Anwendung, wenn Benutzer versuchen, PDF-Dateien anzuzeigen. | Ja |
| Sie schließen eine HTTP-Bibliothek in Ihre App ein, um die Webleistung zu verbessern. | Nein |
| Sie schließen eine Bibliothek wie React Native ein, die von `Activity`, `Application` und `Fragment` abgeleitete Klassen enthält, und Sie verwenden diese Klassen in Ihrer App oder leiten sie weiter ab. | Ja |
| Sie schließen eine Bibliothek wie React Native ein, die von `Activity`, `Application` und `Fragment` abgeleitete Klassen enthält, aber Sie verwenden nur statische Hilfen oder Hilfsklassen. | Nein |
| Sie schließen eine Bibliothek ein, die von `TextView` abgeleitete Ansichtsklassen enthält, und Sie verwenden diese Klassen in Ihrer App oder leiten sie weiter ab. | Ja |

#### <a name="reporting"></a>Berichterstellung
Das Build-Plug-In kann einen HTML-Bericht über die Änderungen erstellen, die es durchführt. Wenn Sie die Erstellung dieses Berichts anfordern möchten, geben Sie `report = true` im `intunemam`-Konfigurationsblock an. Wenn der Bericht erstellt wird, wird er in `outputs/logs` in das Buildverzeichnis geschrieben.

```groovy
intunemam {
    report = true
}
```

#### <a name="verification"></a>Überprüfung
Das Build-Plug-In kann zusätzliche Überprüfungen ausführen, um nach möglichen Fehlern bei der Verarbeitung der Klassen zu suchen. Geben Sie `verify = true` im `intunemam`-Konfigurationsblock an, um dies erforderlich zu machen. Dadurch verlängert sich allerdings möglicherweise die Zeit für die Ausführung des Plug-In-Tasks um einige Sekunden.

```groovy
intunemam {
    verify = true
}
```


#### <a name="incremental-builds"></a>Inkrementelle Builds
Geben Sie `incremental = true` im `intunemam`-Konfigurationsblock an, wenn Sie wollen, dass inkrementelle Buildvorgänge unterstützt werden.  Dabei handelt es sich um ein experimentelles Feature, das die Buildleistung erhöhen soll, indem nur die Eingabedateien verarbeitet werden, die sich geändert haben.  Die Standardkonfiguration ist `false`.

```groovy
intunemam {
    incremental = true
}
```


#### <a name="dependencies"></a>-Abhängigkeiten

Das Gradle-Plug-In weist eine Abhängigkeit von [Javassist](https://jboss-javassist.github.io/javassist/) auf, die für die Abhängigkeitsauflösung von Gradle verfügbar sein muss (wie oben beschrieben). Javassist wird ausschließlich zur Buildzeit beim Ausführen des Plug-Ins verwendet. Es wird kein Javassist-Code zu Ihrer App hinzugefügt.

> [!NOTE] 
> Sie müssen Version 3.0 oder höher des Android Gradle-Plug-Ins und Gradle 4.1 oder höher verwenden.

### <a name="command-line-build-tool"></a>Befehlszeilen-Buildtool
Wenn Ihr Build Gradle verwendet, fahren Sie mit dem [nächsten Abschnitt](#class-and-method-replacements) fort.

Das Befehlszeilen-Buildtool befindet sich im Ordner `BuildTool` des SDKs. Es führt dieselbe Funktion wie das oben beschriebene Gradle-Plug-In aus, kann aber in benutzerdefinierte oder Nicht-Gradle-Buildsysteme integriert werden. Da es allgemeiner gehalten und daher komplizierter aufzurufen ist, sollte nach Möglichkeit das Gradle-Plug-In verwendet werden.

#### <a name="using-the-command-line-tool"></a>Verwenden des Befehlszeilentools

Das Befehlszeilentool kann mit den bereitgestellten Hilfsskripts im Verzeichnis `BuildTool\bin` aufgerufen werden.

Das Tool erwartet die folgenden Parameter.

| Parameter | Beschreibung |
| -- | -- |
| `--input` | Eine durch Semikolon getrennte Liste von JAR-Dateien und Verzeichnissen von Klassendateien, die geändert werden sollen. Dies sollte alle JAR-Dateien/Verzeichnisse umfassen, die Sie neu schreiben möchten. |
| `--output` | Eine durch Semikolon getrennte Liste von JAR-Dateien und Verzeichnissen, in denen die geänderten Klassen gespeichert werden. Es sollte zu jedem Eingabeeintrag einen Ausgabeeintrag geben, und diese sollten in der entsprechenden Reihenfolge aufgelistet werden. |
| `--classpath` | Der Klassenpfad des Builds. Dieser kann sowohl JAR-Dateien als auch Klassenverzeichnisse enthalten. |
| `--excludeClasses`| Eine durch Semikolon getrennte Liste mit den Namen der Klassen, die vom erneuten Schreiben ausgeschlossen werden sollen. |

Alle Parameter sind erforderlich, mit Ausnahme von `--excludeClasses`, das optional ist.

> [!NOTE]
> In Unix-ähnlichen Systemen ist das Semikolon ein Befehlstrennzeichen. Damit die Shell Befehle nicht aufteilt, sollten Sie alle Semikolons mit '\' umgehen oder den vollständigen Parameter in Anführungszeichen setzen.

#### <a name="example-command-line-tool-invocation"></a>Beispiel für den Aufruf des Befehlszeilentools

``` batch
> BuildTool\bin\BuildTool.bat --input build\product-foo-project;libs\bar.jar --output mam-build\product-foo-project;mam-build\libs\bar.jar --classpath build\zap.jar;libs\Microsoft.Intune.MAM.SDK\classes.jar;%ANDROID_SDK_ROOT%\platforms\android-27\android.jar --excludeClasses com.contoso.SplashActivity
```

Dies hätte folgende Auswirkungen:

* das Verzeichnis `product-foo-project` wird in `mam-build\product-foo-project` neu geschrieben
* `bar.jar` wird in `mam-build\libs\bar.jar` neu geschrieben
* `zap.jar` wird **nicht** neu geschrieben, da es nur in `--classpath` aufgeführt ist
* Die Klasse `com.contoso.SplashActivity` wird **nicht** neu geschrieben, auch wenn sie sich in `--input` befindet

> [!NOTE] 
> Das Buildtool unterstützt derzeit keine AAR-Dateien. Wenn Ihr Buildsystem bei der Bearbeitung von AAR-Dateien nicht bereits `classes.jar` extrahiert, müssen Sie dies vor dem Aufrufen des Buildtools durchführen.


## <a name="class-and-method-replacements"></a>Klassen- und Methodenersetzungen
> [!NOTE] 
> Apps *sollten* mit den [Buildtools](#build-tooling) des SDK integriert werden, die diese Ersetzungen (bis auf [Manifestersetzungen](#manifest-replacements)) alle automatisch durchführen.

Android-Basisklassen müssen durch ihre jeweiligen MAM-Entsprechungen ersetzt werden, um die Intune-Verwaltung zu ermöglichen. Die SDK-Klassen befinden sich zwischen der Android-Basisklasse und der App-eigenen abgeleiteten Version dieser Klasse. Eine App-Aktivität kann z. B. zu einer Vererbungshierarchie führen, die wie folgt aussieht: `Activity` > `MAMActivity` >
`AppSpecificActivity`. Die MAM-Ebene filtert Aufrufe von Systemoperationen, um Ihrer App übergangslos eine verwaltete Ansicht zu bieten.

Zusätzlich zu den Basisklassen verfügen einige Klassen, die Ihre Anwendung ohne Ableitung verwenden könnte (z. B. `MediaPlayer`), auch über erforderliche MAM-Entsprechungen, und [einige Methodenaufrufe müssen ebenfalls ersetzt werden](#wrapped-system-services). Die ausführlichen Details sind unten aufgeführt.

> [!NOTE] 
> Wenn Integrationsvorgänge für Ihre App mithilfe der SDK-[Buildtools](#build-tooling) ausgeführt werden, werden die folgenden Klassen- und Methodenersetzungen automatisch ausgeführt.

| Android-Basisklasse | Intune App SDK-Äquivalent |
|--|--|
| android.app.Activity | MAMActivity |
| android.app.ActivityGroup | MAMActivityGroup |
| android.app.AliasActivity | MAMAliasActivity |
| android.app.Application | MAMApplication |
| android.app.Dialog | MAMDialog |
| android.app.AlertDialog.Builder | MAMAlertDialogBuilder |
| android.app.DialogFragment | MAMDialogFragment |
| android.app.ExpandableListActivity | MAMExpandableListActivity |
| android.app.Fragment | MAMFragment |
| android.app.IntentService | MAMIntentService |
| android.app.LauncherActivity | MAMLauncherActivity |
| android.app.ListActivity | MAMListActivity |
| android.app.ListFragment | MAMListFragment |
| android.app.NativeActivity | MAMNativeActivity |
| android.app.PendingIntent | MAMPendingIntent (siehe [PendingIntent](#pendingintent)) |
| android.app.Service | MAMService |
| android.app.TabActivity | MAMTabActivity |
| android.app.TaskStackBuilder | MAMTaskStackBuilder |
| android.app.backup.BackupAgent | MAMBackupAgent |
| android.app.backup.BackupAgentHelper | MAMBackupAgentHelper |
| android.app.backup.FileBackupHelper | MAMFileBackupHelper |
| android.app.backup.SharePreferencesBackupHelper | MAMSharedPreferencesBackupHelper |
| android.content.BroadcastReceiver | MAMBroadcastReceiver |
| android.content.ContentProvider | MAMContentProvider |
| android.os.Binder | MAMBinder (Nur erforderlich, wenn der Binder nicht von einer Schnittstelle der Android Interface Definition Language (AIDL) generiert wird.) |
| android.media.MediaPlayer | MAMMediaPlayer |
| android.media.MediaMetadataRetriever | android.media.MediaMetadataRetriever |
| android.provider.DocumentsProvider | MAMDocumentsProvider |
| android.preference.PreferenceActivity | MAMPreferenceActivity |
| android.support.multidex.MultiDexApplication | MAMMultiDexApplication |
| android.widget.TextView | MAMTextView |
| android.widget.AutoCompleteTextView | MAMAutoCompleteTextView |
| android.widget.CheckedTextView | MAMCheckedTextView |
| android.widget.EditText | MAMEditText |
| android.inputmethodservice.ExtractEditText | MAMExtractEditText |
| android.widget.MultiAutoCompleteTextView | MAMMultiAutoCompleteTextView |


> [!NOTE]
> Auch wenn Ihre Anwendung keinen Bedarf an einer eigenen abgeleiteten `Application`-Klasse hat, [siehe `MAMApplication` weiter unten](#mamapplication).

### <a name="microsoftintunemamsdksupportv4jar"></a>Microsoft.Intune.MAM.SDK.Support.v4.jar:

| Android-Klasse | Intune App SDK-Äquivalent |
|--|--|
| android.support.v4.app.DialogFragment | MAMDialogFragment
| android.support.v4.app.FragmentActivity | MAMFragmentActivity
| android.support.v4.app.Fragment | MAMFragment
| Android.Support.v4.app.JobIntentService | MAMJobIntentService
| android.support.v4.app.TaskStackBuilder | MAMTaskStackBuilder
| android.support.v4.content.FileProvider | MAMFileProvider
| android.support.v4.content.WakefulBroadcastReceiver | MAMWakefulBroadcastReceiver

### <a name="microsoftintunemamsdksupportv7jar"></a>Microsoft.Intune.MAM.SDK.Support.v7.jar:

|Android-Klasse | Intune App SDK-Äquivalent |
|--|--|
| android.support.v7.app.AlertDialog.Builder | MAMAlertDialogBuilder |
| Android.Support.V7.app.AppCompatActivity | MAMAppCompatActivity |
| android.support.v7.widget.AppCompatAutoCompleteTextView | MAMAppCompatAutoCompleteTextView |
| android.support.v7.widget.AppCompatCheckedTextView | MAMAppCompatCheckedTextView |
| android.support.v7.widget.AppCompatEditText | MAMAppCompatEditText |
| android.support.v7.widget.AppCompatMultiAutoCompleteTextView | MAMAppCompatMultiAutoCompleteTextView |
| android.support.v7.widget.AppCompatTextView | MAMAppCompatTextView |

### <a name="microsoftintunemamsdksupportv17jar"></a>Microsoft.Intune.MAM.SDK.Support.v17.jar:
|Android-Klasse | Intune App SDK-Äquivalent |
|--|--|
| android.support.v17.leanback.widget.SearchEditText | MAMSearchEditText |

### <a name="microsoftintunemamsdksupporttextjar"></a>Microsoft.Intune.MAM.SDK.Support.Text.jar:
|Android-Klasse | Intune App SDK-Äquivalent |
|--|--|
| android.support.text.emoji.widget.EmojiAppCompatEditText | MAMEmojiAppCompatEditText |
| android.support.text.emoji.widget.EmojiAppCompatTextView | MAMEmojiAppCompatTextView |
| android.support.text.emoji.widget.EmojiEditText | MAMEmojiEditText |
| android.support.text.emoji.widget.EmojiTextView | MAMEmojiTextView |

### <a name="renamed-methods"></a>Umbenannte Methoden

In vielen Fällen wurde eine in der Android-Klasse verfügbare Methode in der äquivalenten MAM-Klasse als abgeschlossen gekennzeichnet. In diesem Fall stellt die äquivalente MAM-Klasse eine Methode mit ähnlichem Namen (normalerweise mit dem Suffix `MAM`) bereit, die stattdessen überschrieben werden sollte. Wenn z. B. von `MAMActivity` abgeleitet wird, anstatt `onCreate()` zu überschreiben und `super.onCreate()` aufzurufen, muss `Activity``onMAMCreate()` überschreiben und `super.onMAMCreate()` aufrufen. Der Java-Compiler sollte die abgeschlossenen Einschränkungen erzwingen, um zu verhindern, dass die ursprüngliche Methode anstelle des MAM-Äquivalents überschrieben wird.

### <a name="mamapplication"></a>MAMApplication
Wenn Ihre App eine Unterklasse von `android.app.Application` erstellt, **müssen** Sie stattdessen eine Unterklasse von `com.microsoft.intune.mam.client.app.MAMApplication` erstellen. Wenn Ihre App keine Unterklasse von `android.app.Application` erstellt, **müssen** Sie `"com.microsoft.intune.mam.client.app.MAMApplication"` als das `"android:name"`-Attribut im `<application>`-Tag Ihrer „AndroidManifest.xml“-Datei festlegen.

### <a name="pendingintent"></a>PendingIntent
Anstelle von `PendingIntent.get*` müssen Sie die `MAMPendingIntent.get*`-Methode verwenden. Anschließend können Sie den sich ergebenden `PendingIntent` wie gewohnt verwenden.

### <a name="wrapped-system-services"></a>Umschlossene Systemdienste
Für einige Systemdienstklassen ist es erforderlich, eine statische Methode für eine MAM-Wrapperklasse aufzurufen, anstatt direkt die gewünschte Methode für die Dienstinstanz aufzurufen. So muss z. B. aus einem Aufruf von `getSystemService(ClipboardManager.class).getPrimaryClip()` ein Aufruf von `MAMClipboardManager.getPrimaryClip(getSystemService(ClipboardManager.class)` werden. Es wird nicht empfohlen, diese Ersetzungen manuell vorzunehmen. Überlassen Sie dies stattdessen dem BuildPlugin.

| Android-Klasse | Intune App SDK-Äquivalent |
|--|--|
| android.content.ClipboardManager | MAMClipboard |
| android.content.ContentProviderClient | MAMContentProviderClientManagement |
| android.content.ContentResolver | MAMContentResolverManagement |
| android.content.pm.PackageManager | MAMPackageManagement |
| android.app.DownloadManager | MAMDownloadManagement |
| android.print.PrintManager | MAMPrintManagement |
| android.support.v4.print.PrintHelper | MAMPrintHelperManagement |
| android.view.View | MAMViewManagement |
| android.view.DragEvent | MAMDragEventManagement |
| android.app.NotificationManager | MAMNotificationManagement |
| android.support.v4.app.NotificationManagerCompat | MAMNotificationCompatManagement |

Bei manchen Klassen sind die meisten ihrer Methoden umschlossen, z. B. `ClipboardManager`, `ContentProviderClient`, `ContentResolver` und `PackageManager`, während bei anderen Klassen nur ein oder zwei Methoden umschlossen sind, z. B. `DownloadManager`, `PrintManager`, `PrintHelper`, `View`, `DragEvent`, `NotificationManager` und `NotificationManagerCompat`. Suchen Sie in den APIs, die von den äquivalenten MAM-Klassen verfügbar gemacht werden, nach der exakten Methode, wenn Sie nicht das Build-Plug-In verwenden.

### <a name="manifest-replacements"></a>Manifestersetzungen
Möglicherweise müssen einige der oben aufgeführten Klassenersetzungen sowohl im Manifest als auch im Java-Code vorgenommen werden. Besonderer Hinweis:
* Manifestverweise auf `android.support.v4.content.FileProvider` müssen durch `com.microsoft.intune.mam.client.support.v4.content.MAMFileProvider` ersetzt werden.

## <a name="androidx-libraries"></a>AndroidX-Bibliotheken
Mit Android P kündigte Google einen neuen (umbenannten) Satz von Unterstützungsbibliotheken namens AndroidX an, und Version 28 ist das letzte größere Release der bestehenden android.support-Bibliotheken.

Im Gegensatz zu den Android-Unterstützungsbibliotheken stellen wir keine MAM-Varianten der AndroidX-Bibliotheken bereit. Stattdessen sollte AndroidX wie jede andere externe Bibliothek behandelt und so konfiguriert werden, dass es vom Build-Plug-In/Tool neu geschrieben wird. Für Gradle-Builds kann dies durch das Einbeziehen von `androidx.*` in das Feld `includeExternalLibraries` der Plug-In-Konfiguration erreicht werden. Aufrufe des Befehlszeilentools müssen alle JAR-Dateien explizit auflisten.

### <a name="pre-androidx-architecture-components"></a>Architekturkomponenten vor AndroidX
Viele Komponenten der Android-Architektur einschließlich Room, ViewModel und WorkManager wurden für AndroidX neu paketiert. Wenn Ihre App Varianten dieser Bibliotheken verwendet, die älter als AndroidX sind, sollten Sie dafür sorgen, dass Rewrite-Vorgänge angewendet werden, indem `android.arch.*` im `includeExternalLibraries`-Feld der Konfiguration des Plug-Ins eingeschlossen wird. Alternativ können Sie die Bibliotheken auf ihre AndroidX-Äquivalente aktualisieren.

### <a name="troubleshooting-androidx-migration"></a>Problembehandlung bei der AndroidX-Migration
Beim Migrieren der SDK-integrierten App zu AndroidX tritt möglicherweise ein Fehler wie der folgende auf:

```log
incompatible types: android.support.v7.app.ActionBar cannot be converted to androidx.appcompat.app.ActionBar
```

Diese Fehler können auftreten, wenn Ihre App auf MAM-Unterstützungsklassen verweist. MAM-Unterstützungsklassen umschließen Android-Unterstützungsklassen, die in AndroidX verschoben wurden. Ersetzen Sie zum Bekämpfen solcher Fehler alle Verweise von MAM-Unterstützungsklassen durch die entsprechenden AndroidX-Verweise. Dies kann erreicht werden, indem zunächst die Abhängigkeiten der MAM-Unterstützungsbibliothek von Ihren Gradle-Builddateien entfernt werden. Die fraglichen Zeilen sehen in etwa wie folgt aus:

```Gradle
implementation "com.microsoft.intune.mam:android-sdk-support-v4:$intune_mam_version"
implementation "com.microsoft.intune.mam:android-sdk-support-v7:$intune_mam_version"
```

Beheben Sie anschließend die resultierenden Kompilierzeitfehler, indem Sie alle Verweise auf MAM-Klassen in den Paketen `com.microsoft.intune.mam.client.support.v7` und `com.microsoft.intune.mam.client.support.v4` durch die entsprechenden AndroidX-Verweise ersetzen. Verweise auf `MAMAppCompatActivity` sollten z. B. in `AppCompatActivity` von AndroidX geändert werden. Wie bereits oben erläutert wurde, überschreibt das MAM-Build-Plug-In/-Tool zur Kompilierzeit automatisch Klassen in den AndroidX-Bibliotheken durch die jeweiligen MAM-Entsprechungen.

## <a name="sdk-permissions"></a>SDK-Berechtigungen

Das Intune App SDK erfordert drei [Android-Systemberechtigungen](https://developer.android.com/guide/topics/security/permissions.html) für Apps, die es integrieren:

* `android.permission.GET_ACCOUNTS` (zur Laufzeit angefordert, wenn erforderlich)

* `android.permission.MANAGE_ACCOUNTS`

* `android.permission.USE_CREDENTIALS`

Die Azure Active Directory Authentication Library ([ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/)) verlangt, dass diese Berechtigungen Brokerauthentifizierung ausführen. Wenn diese Berechtigungen der App nicht gewährt oder vom Benutzer widerrufen werden, werden Authentifizierungsflüsse deaktiviert, die den Broker (die Unternehmensportal-App) erfordern.

## <a name="logging"></a>Logging

Die Protokollierung sollte früh initialisiert werden, um die protokollierten Daten optimal nutzen zu können. `Application.onMAMCreate()` ist in der Regel der beste Ort zum Initialisieren der Protokollierung.

Erstellen Sie einen [Java-Handler](https://docs.oracle.com/javase/7/docs/api/java/util/logging/Handler.html), und fügen Sie ihn zum `MAMLogHandlerWrapper` hinzu, um MAM-Protokolle in Ihrer App zu erhalten. Dadurch wird `publish()` für den Anwendungshandler für jede Protokollnachricht aufgerufen.

```java
/**
 * Global log handler that enables fine grained PII filtering within MAM logs.  
 *
 * To start using this you should build your own log handler and add it via
 * MAMComponents.get(MAMLogHandlerWrapper.class).addHandler(myHandler, false);  
 *
 * You may also remove the handler entirely via
 * MAMComponents.get(MAMLogHandlerWrapper.class).removeHandler(myHandler);
 */
public interface MAMLogHandlerWrapper {
    /**
     * Add a handler, PII can be toggled.
     *
     * @param handler handler to add.
     * @param wantsPII if PII is desired in the logs.    
     */
    void addHandler(final Handler handler, final boolean wantsPII);

    /**
     * Remove a handler.
     *
     * @param handler handler to remove.
     */
    void removeHandler(final Handler handler);
}
```

## <a name="diagnostics-information"></a>Diagnoseinformationen
Apps können die `MAMPolicyManager.showDiagnostics(context)`-Methode aufrufen, die eine Aktivität startet, bei der eine Benutzeroberfläche zum Sammeln von Unternehmensportalprotokollen und zum Anzeigen von MAM-Diagnosen angezeigt wird.
Dies ist ein optionales Feature, das beim Debuggen hilfreich sein kann.

Wenn das Unternehmensportal auf dem Gerät nicht installiert ist, wird ein Dialogfeld angezeigt, über das der Benutzer darüber informiert wird, dass diese Informationen derzeit nicht verfügbar sind. Wenn Apps durch die MAM-Richtlinie verwaltet werden, werden detaillierte MAM-Richtlinieneinstellungen angezeigt.

## <a name="mam-strict-mode"></a>Strikter MAM-Modus
Der strikte MAM-Modus stellt einen Mechanismus zum Erkennen von „Smells“ in der App-Nutzung von MAM-APIs oder von auf MAM eingeschränkten Plattform-APIs bereit. Er ist grob an den strikten Android-Modus angelehnt und führt eine Reihe von Überprüfungen durch, die Fehler auslösen, wenn sie fehlschlagen. Er ist nicht dafür gedacht, in Produktionsbuilds aktiviert zu bleiben, es wird jedoch *dringend empfohlen*, ihn bei der internen Entwicklung Ihrer App, beim Debuggen und/oder bei Dogfood-Builds zu verwenden.

Zum Aktivieren rufen Sie

```java
MAMStrictMode.enable();
```
 früh in der Anwendungsinitialisierung (z. B. `Application.onCreate`) auf. 

Wenn bei einer Überprüfung des strikten MAM-Modus ein Fehler auftritt, versuchen Sie zu bestimmen, ob es sich um ein wirkliches Problem handelt, das in Ihrer App behoben werden kann, oder ob es sich um einen False Positive handelt. Wenn Sie der Meinung sind, dass es sich um ein falsch positives Ergebnis handelt, oder wenn Sie nicht sicher sind, informieren Sie bitte das Intune MAM-Team. So können wir sicherstellen, dass wir mit der False Positive-Bestimmung einverstanden sind. Zudem können wir so versuchen, die Erkennung in zukünftigen Versionen zu verbessern. Deaktivieren Sie die fehlgeschlagene Überprüfung, um False Positives zu unterdrücken (weitere Informationen folgen weiter unten).

### <a name="handling-violations"></a>Umgang mit Verstößen
Wenn bei einer Überprüfung ein Fehler auftritt, wird ein `MAMStrictViolationHandler` ausgeführt. Der Standardhandler löst einen `Error` aus, bei dem ein Absturz der App erwartet wird. Dadurch sollen Fehler so störend wie möglich gemacht werden. Es passt außerdem zu der Absicht, den strikten Modus nicht in Produktionsbuilds zu aktivieren.

Wenn Ihre App anders mit Verstößen umgehen soll, kann sie einen eigenen Handler bereitstellen, indem Folgendes aufgerufen wird:

```java
MAMStrictMode.global().setHandler(handler);
```

Dabei wird `MAMStrictViolationHandler` von `handler` implementiert:

```java
public interface MAMStrictViolationHandler {
    /**
     * Called when a MAM Strict Mode check fails.
     *
     * @param check
     *         the check that failed
     * @param detail
     *         additional detail. Note that this might contain usernames or filepaths.
     * @param error
     *         error containing a stack trace. The default implementation throws this error
     */
    void checkFailed(@NonNull MAMStrictCheck check, @NonNull String detail, @NonNull Error error);
}
```

### <a name="suppressing-checks"></a>Unterdrücken von Überprüfungen
Wenn bei einer Überprüfung in einer Situation ein Fehler auftritt, in der Ihre App sich korrekt verhält, melden Sie dies bitte wie oben erwähnt. Manchmal kann es jedoch erforderlich sein, die Überprüfung zu deaktivieren, die zu einem falsch positiven Ergebnis führt – zumindest während Sie auf ein aktualisiertes SDK warten. Die Überprüfung, bei der ein Fehler aufgetreten ist, wird in dem Fehler angezeigt, der vom Standardhandler ausgelöst wird, oder an einen benutzerdefinierten Handler weitergegeben, falls einer festgelegt wurde.

Eine Unterdrückung kann global erfolgen, jedoch wird eine vorübergehende Deaktivierung pro Thread auf der bestimmten Aufrufwebsite bevorzugt. In den folgenden Beispielen werden verschiedene Möglichkeiten zum Deaktivieren von `MAMStrictCheck.IDENTITY_NO_SUCH_FILE` aufgezeigt (wird ausgelöst, wenn versucht wird, eine Datei zu schützen, die nicht vorhanden ist).


#### <a name="per-thread-temporary-suppression"></a>Temporäre Unterdrückung pro Thread
Dies ist der bevorzugte Unterdrückungsmechanismus.
```java
try (StrictScopedDisable disable = MAMStrictMode.thread().disableScoped(MAMStrictCheck.IDENTITY_NO_SUCH_FILE)) {
    // Perform the operation which raised a violation here
}
// The check is no longer disabled once the block exits
```

#### <a name="per-thread-permanent-suppression"></a>Dauerhafte Unterdrückung pro Thread
```java
MAMStrictMode.thread().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```

#### <a name="global-process-wide-suppression"></a>Globale (prozessweite) Unterdrückung
```java
MAMStrictMode.global().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```



## <a name="enable-features-that-require-app-participation"></a>Aktivieren von Funktionen, die App-Beteiligung erfordern

Es gibt verschiedene App-Schutzrichtlinien, die das SDK nicht selbst implementieren kann. Die App kann ihr Verhalten zum Bereitstellen dieser Features mit mehreren APIs steuern, die Sie in der folgenden `AppPolicy`-Schnittstelle finden. Verwenden Sie `MAMPolicyManager.getPolicy`, um eine `AppPolicy`-Instanz abzurufen.

```java
/**
 * External facing application policies.
 */
public interface AppPolicy {

/**
 * Restrict where an app can save personal data.
 * This function is now deprecated. Use getIsSaveToLocationAllowed(SaveLocation, String) instead
 * @return True if the app is allowed to save to personal data stores; false otherwise.
 */
@Deprecated
boolean getIsSaveToPersonalAllowed();

/**
 * Check if policy prohibits saving to a content provider location.
 *
 * @param location
 *            a content URI to check
 * @return True if location is not a content URI or if policy does not prohibit saving to the content location.
 */
boolean getIsSaveToLocationAllowed(Uri location);

/**
 * Determines if the SaveLocation passed in can be saved to by the username associated with the cloud service.
 *
 * @param service
 *           The SaveLocation the data will be saved to.
 * @param username
 *           The AAD UPN associated with the cloud service being saved to. Use null if a mapping between
 *           the AAD username and the cloud service username does not exist or the username is not known.
 * @return true if the location can be saved to by the identity, false if otherwise.
 */
boolean getIsSaveToLocationAllowed(SaveLocation service, String username);

/**
 * Determines if data from the OpenLocation can be opened for the username associated with the data.
 *
 * @param location
 *      The OpenLocation that the data will be opened from.
 * @param username
 *      The AAD UPN associated with the location the data is being opened from. Use null if a mapping between the
 *      AAD username and the cloud service username does not exist or the username is not known.
 * @return true if the data can be opened from the location for the identity, false if otherwise.
 */
boolean getIsOpenFromLocationAllowed(@NonNull OpenLocation location, @Nullable String username);

/**
 * Checks whether any activities which could handle the given intent are allowed by policy. Returns false only if all
 * activities which could otherwise handle the intent are blocked. If there are no activities which could handle the intent
 * regardless of policy, returns true. If some activities are allowed and others blocked, returns true. Note that it is not
 * necessary to use this method for policy enforcement. If your app attempts to launch an intent for which there are no
 * allowed activities, MAM will display a dialog explaining the situation to the user.
 *
 * @param intent
 *         intent to check
 *
 * @return whether any activities which could handle this intent are allowed.
*/
boolean areIntentActivitiesAllowed(Intent intent);

/**
 * Whether the SDK PIN prompt is enabled for the app.
 *
 * @return True if the PIN is enabled. False otherwise.
 */
boolean getIsPinRequired();

/**
 * Whether the Intune Managed Browser is required to open web links.
 * @return True if the Managed Browser is required, false otherwise
 */
boolean getIsManagedBrowserRequired();

/**
 * Check if policy allows taking screenshots.
 *
 * @return True if screenshots will be blocked, false otherwise
 */
boolean getIsScreenCaptureAllowed();

/**
 * Check if policy allows Contact sync to local contact list.
 *
 * @return True if Contact sync is allowed to save to local contact list; false otherwise.
 */
boolean getIsContactSyncAllowed();

/**
 * Get the notification restriction. If {@link NotificationRestriction#BLOCKED BLOCKED}, the app must not show any notifications
 * for the user associated with this policy. If {@link NotificationRestriction#BLOCK_ORG_DATA BLOCK_ORG_DATA}, the app must show
 * a modified notification that does not contain organization data. If {@link NotificationRestriction#UNRESTRICTED
 * UNRESTRICTED}, all notifications are allowed.
 *
 * @return The notification restriction.
 */
NotificationRestriction getNotificationRestriction();

/**
 * This method is intended for diagnostic/telemetry purposes only. It can be used to discover whether file encryption is in use.
 * File encryption is transparent to the app and the app should not need to make any business logic decisions based on this.
 * @return True if file encryption is in use.
 */
boolean diagnosticIsFileEncryptionInUse();

/**
 * Return the policy in string format to the app.
 *  
 * @return The string representing the policy.
 */
String toString();

}
```

> [!NOTE]
> `MAMPolicyManager.getPolicy` gibt stets eine App-Richtlinie ungleich NULL zurück. Dies gilt selbst dann, wenn das Gerät oder die App keiner Intune-Verwaltungsrichtlinie unterliegt.

### <a name="example-determine-if-pin-is-required-for-the-app"></a>Beispiel: Ermittlung, ob eine PIN für die App erforderlich ist

Verfügt die App über eine eigene PIN-Benutzererfahrung, können Sie diese deaktivieren, wenn der IT-Administrator das SDK so konfiguriert hat, das eine App-PIN angefordert wird. Um festzustellen, ob der IT-Administrator die App-PIN-Richtlinie für diese App bereitgestellt hat, rufen Sie die folgende Methode für den aktuellen Endbenutzer auf:

```java

MAMPolicyManager.getPolicy(currentActivity).getIsPinRequired();
```

### <a name="example-determine-the-primary-intune-user"></a>Beispiel: Ermitteln des primären Intune-Benutzers

Zusätzlich zu den in AppPolicy bereitgestellten APIs wird der Benutzerprinzipalname (User Principal Name, **UPN**) auch von der `getPrimaryUser()`-API in der `MAMUserInfo`-Schnittstelle verfügbar gemacht. Rufen Sie Folgendes auf, um den UPN abzurufen:

```java
MAMComponents.get(MAMUserInfo.class).getPrimaryUser();
```

Die vollständige Definition der MAMUserInfo-Schnittstelle folgt unten:

```java
/**
 * External facing user information.
 *
 */
public interface MAMUserInfo {
       /**
        * Get the primary user name.
        *
        * @return the primary user name or null if neither the device nor app is enrolled.
        */
       String getPrimaryUser();
}
```

### <a name="example-data-transfer-between-apps-and-device-or-cloud-storage-locations"></a>Beispiel: Datenübertragung zwischen Apps und Geräte- oder Cloudspeicherorten

Viele Apps implementieren Features, die es dem Endbenutzer ermöglichen, Daten an einem lokalen Dateispeicherort oder in Cloudspeicherdiensten zu speichern oder Daten daraus zu öffnen.
Mit dem Intune App SDK können IT-Administratoren dafür sorgen, dass keine Daten eingehen oder preisgegeben werden, indem sie Richtlinieneinschränkungen entsprechend den Anforderungen ihrer Organisation anwenden.

**Damit die Funktion aktiviert werden kann, ist App-Beteiligung erforderlich.**
Wenn Ihre App das direkte Speichern aus der App an einem persönlichen Speicherort oder einem Cloudspeicherort *oder* das direkte Öffnen von Daten in der App ermöglicht, müssen Sie das entsprechende Feature implementieren, damit IT-Administratoren steuern können, ob das Speichern an einem Speicherort oder das Öffnen aus einem Speicherort erlaubt ist oder nicht.

#### <a name="saving-to-device-or-cloud-storage"></a>Speichern auf dem Gerät oder in einem Cloudspeicher

Die folgende API informiert die App darüber, ob das Speichern in einem persönlichen Speicher gemäß der aktuellen Intune-Administratorrichtlinie zulässig ist.

Rufen Sie Folgendes auf, um zu ermitteln, ob die Richtlinie erzwungen wird:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(
SaveLocation service, String username);
```

Der Parameter `service` muss einen der folgenden `SaveLocation`-Werte aufweisen:

* `SaveLocation.ONEDRIVE_FOR_BUSINESS`
* `SaveLocation.SHAREPOINT`
* `SaveLocation.LOCAL`
* `SaveLocation.ACCOUNT_DOCUMENT`
* `SaveLocation.OTHER`

Informationen zum Bestimmen, ob `ACCOUNT_DOCUMENT` oder `OTHER` an `getIsSaveToLocationAllowed` weitergegeben werden sollen, finden Sie unter [Unbekannte oder nicht aufgelistete Speicherorte](#unknown-or-unlisted-locations).

Weitere Informationen zum `username`-Parameter finden Sie unter [Benutzername für die Datenübertragung](#username-for-data-transfer).

Die vorherige Methode zur Ermittlung, ob die Richtlinie eines Benutzers das Speichern von Daten an verschiedenen Speicherorten gestattet, war `getIsSaveToPersonalAllowed()` innerhalb derselben **AppPolicy**-Klasse.
Diese Funktion ist jetzt **veraltet** und sollte nicht verwendet werden. Der folgende Aufruf entspricht `getIsSaveToPersonalAllowed()`:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(SaveLocation.LOCAL, null);
```

#### <a name="opening-data-from-a-local-or-cloud-storage-location"></a>Öffnen von Daten aus einem lokalen Speicherort oder aus einem Cloudspeicherort

Die folgende API informiert die App darüber, ob das Öffnen aus einem persönlichen Speicher gemäß der aktuellen Intune-Administratorrichtlinie zulässig ist.

Rufen Sie Folgendes auf, um zu ermitteln, ob die Richtlinie erzwungen wird:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsOpenFromLocationAllowed(
OpenLocation location, String username);
```

Der Parameter `location` muss einen der folgenden `OpenLocation`-Werte aufweisen:

* `OpenLocation.ONEDRIVE_FOR_BUSINESS`
* `OpenLocation.SHAREPOINT`
* `OpenLocation.CAMERA`
* `OpenLocation.LOCAL`
* `OpenLocation.ACCOUNT_DOCUMENT`
* `OpenLocation.OTHER`

Der `OpenLocation.CAMERA`-Speicherort sollte übermittelt werden, wenn die App Daten von der Kamera öffnet.
Der `OpenLocation.LOCAL`-Speicherort sollte übermittelt werden, wenn die App Daten aus dem externen Speicher des lokalen Geräts öffnet.
Der `OpenLocation.ACCOUNT_DOCUMENT`-Speicherort sollte übermittelt werden, wenn die App Daten öffnet, die zu einem AAD-Konto gehören, das bei der App angemeldet ist.

Informationen zum Bestimmen, ob `ACCOUNT_DOCUMENT` oder `OTHER` an `getIsOpenFromLocationAllowed` weitergegeben werden sollen, finden Sie unter [Unbekannte oder nicht aufgelistete Speicherorte](#unknown-or-unlisted-locations).

Weitere Informationen zum `username`-Parameter finden Sie unter [Benutzername für die Datenübertragung](#username-for-data-transfer).

#### <a name="unknown-or-unlisted-locations"></a>Unbekannte oder nicht aufgelistete Speicherorte

Wenn der gewünschte Speicherort nicht in den `SaveLocation`- oder `OpenLocation`-Enumerationen aufgeführt ist oder unbekannt ist, bestehen für den `service`/`location`-Parameter zwei Optionen, `ACCOUNT_DOCUMENT` und `OTHER`.
`ACCOUNT_DOCUMENT` sollte verwendet werden, wenn die Daten zu einem AAD-Konto gehören, das bei der App angemeldet ist, jedoch nicht den Wert `ONEDRIVE_FOR_BUSINESS` oder `SHAREPOINT` aufweist. `OTHER` sollte hingegen verwendet werden, wenn dies nicht der Fall ist.

Es ist wichtig, klar zwischen einem verwalteten Konto und einem Konto zu unterscheiden, das denselben UPN wie das verwaltete Konto verwendet.
Beispielsweise ist ein verwaltetes Konto mit dem UPN „user@contoso.com“, mit dem sich ein Benutzer in OneDrive angemeldet hat, nicht identisch mit einem Konto mit dem UPN „user@contoso.com“, mit dem sich ein Benutzer bei Dropbox angemeldet hat.
Wenn durch die Anmeldung beim verwalteten Konto auf einen unbekannten oder nicht aufgeführten Dienst zugegriffen wird (z. B. wenn „user@contoso.com“ für die Anmeldung bei OneDrive verwendet wurde), sollte das durch den Speicherort `ACCOUNT_DOCUMENT` dargestellt werden.
Wenn sich der unbekannte oder nicht aufgeführte Dienst über ein anderes Konto anmeldet (z. B. wenn „user@contoso.com“ für die Anmeldung bei Dropbox verwendet wurde), erfolgt der Zugriff nicht mit einem verwalteten Konto. Das sollte durch den Speicherort `OTHER` dargestellt werden.

#### <a name="username-for-data-transfer"></a>Benutzername für die Datenübertragung

Beim Überprüfen der Speicherrichtlinie sollte der Parameter `username` der UPN/Benutzername/die E-Mail sein, der bzw. die dem Clouddienst zugeordnet ist, in dem gespeichert wird (*nicht* zwingendermaßen identisch mit dem Benutzer, der das Dokument besitzt, das gespeichert wird).
Bei `SaveLocation.LOCAL` handelt es sich um keinen Clouddienst und sollte deshalb immer mit einem `null`-Benutzernamenparameter verwendet werden.

Beim Überprüfen der geöffneten Richtlinie sollte der Parameter `username` der UPN/Benutzername/die E-Mail-Adresse des Clouddiensts sein, aus dem geöffnet wird.
Bei `OpenLocation.LOCAL` und `OpenLocation.CAMERA` handelt es sich um keine Clouddienst-Speicherorte, weshalb sie immer mit einem `null`-Benutzernamenparameter verwendet werden sollten.

Die folgenden Speicherorte erwarten immer einen Benutzernamen, der eine Zuordnung zwischen dem AAD-UPN und dem Benutzernamen des Clouddiensts enthält: `ONEDRIVE_FOR_BUSINESS`, `SHAREPOINT` und `ACCOUNT_DOCUMENT`.

Verwenden Sie `null`, wenn dem AAD-UPN kein Clouddienst-Benutzername zugeordnet werden kann oder der Benutzername nicht bekannt ist.

#### <a name="sharing-blocked-dialog"></a>Dialogfeld zur Blockierung einer Freigabe

Das SDK verfügt über ein Dialogfeld, das den Benutzer darüber benachrichtigt, dass eine Datenübertragungsaktion durch die MAM-Richtlinie blockiert wurde.

Das Dialogfeld sollte dem Benutzer angezeigt werden, wenn die `isSaveToAllowedForLocation`- oder `isOpenFromAllowedForLocation`-API-Aufrufe dazu führen, dass die Aktion zum Speichern/Öffnen blockiert wird.
Im Dialogfeld wird eine generische Meldung angezeigt. Wenn es geschlossen wird, wird wieder die `Activity` angezeigt, von der das Dialogfeld aufgerufen wurde.

Rufen Sie Folgendes auf, um das Dialogfeld anzuzeigen:

``` java
MAMUIHelper.showSharingBlockedDialog(currentActivity)
```

### <a name="allow-for-file-sharing"></a>Zulassen von Dateifreigaben

Wenn das Speichern an öffentlichen Speicherorten nicht zulässig ist, sollte Ihre App den Benutzern weiterhin gestatten, Dateien anzuzeigen, indem sie in den [privaten App-Speicher](https://developer.android.com/training/data-storage) herunterladen und dann über die Systemauswahl geöffnet werden.

### <a name="example-determine-if-notifications-with-organization-data-need-to-be-restricted"></a>Beispiel: Bestimmen, ob Benachrichtigungen mit Unternehmensdaten eingeschränkt werden müssen

Wenn Ihre App Benachrichtigungen anzeigt, müssen Sie die Benachrichtigungseinschränkungsrichtlinie für den Benutzer überprüfen, der der Benachrichtigung zugeordnet ist, bevor die Benachrichtigung angezeigt wird. Rufen Sie Folgendes auf, um zu ermitteln, ob die Richtlinie erzwungen wird.

```java
NotificationRestriction notificationRestriction =
    MAMPolicyManager.getPolicyForIdentity(notificationIdentity).getNotificationRestriction();
```

Wenn für die Einschränkung `BLOCKED` gilt, darf die App keine Benachrichtigungen für den Benutzer anzeigen, der dieser Richtlinie zugeordnet ist. Wenn für die Einschränkung `BLOCK_ORG_DATA` gilt, muss die App eine angepasste Benachrichtigung anzeigen, die keine Unternehmensdaten enthält. Wenn für die Einschränkung `UNRESTRICTED` gilt, sind alle Benachrichtigungen zulässig.

Wenn `getNotificationRestriction` nicht aufgerufen wird, tut das MAM-SDK sein Bestmögliches, um Benachrichtigungen für Apps mit einer Identität automatisch einzuschränken. Wenn die automatische Blockierung aktiviert und `BLOCK_ORG_DATA` festgelegt ist, wird die Benachrichtigung gar nicht erst angezeigt. Wenn Sie eine präzisere Kontrolle haben möchten, überprüfen Sie die Werte von `getNotificationRestriction`, und passen Sie App-Benachrichtigungen entsprechend an.

## <a name="register-for-notifications-from-the-sdk"></a>Registrieren für Benachrichtigungen vom SDK

### <a name="overview"></a>Übersicht
Das Intune App SDK erlaubt Ihrer App die Steuerung des Verhaltens bestimmter Richtlinien, z. B. zur selektiven Zurücksetzung, wenn sie vom IT-Administrator bereitgestellt werden. Wenn ein IT-Administrator eine solche Richtlinie bereitstellt, sendet der Intune-Dienst eine Benachrichtigung an das SDK.

Ihre App muss sich für Benachrichtigungen vom SDK registrieren, indem ein `MAMNotificationReceiver` erstellt und mit `MAMNotificationReceiverRegistry` registriert wird. Zu diesem Zweck werden der Empfänger und der Typ der Benachrichtigung in `App.onCreate` angegeben, wie das folgende Beispiel veranschaulicht:

```java
@Override
public void onCreate() {
  super.onCreate();
  MAMComponents.get(MAMNotificationReceiverRegistry.class)
    .registerReceiver(
      new ToastNotificationReceiver(),
      MAMNotificationType.WIPE_USER_DATA);
}
```

### <a name="mamnotificationreceiver"></a>MAMNotificationReceiver

Die `MAMNotificationReceiver`-Schnittstelle empfängt lediglich Benachrichtigungen vom Intune-Dienst. Einige Benachrichtigungen werden direkt vom SDK verarbeitet, andere erfordern die Beteiligung der App. Eine App **muss** „true“ oder „false“ von einer Benachrichtigung zurückgeben. Sie muss immer "true" zurückgeben, es sei denn, eine von ihr aufgrund der Benachrichtigung ausgeführte Aktion schlägt fehl.

* Dieser Fehler kann beim Intune-Dienst gemeldet werden. Ein Beispiel für ein zu berichtendes Szenario ist, wenn die Anwendung Benutzerdaten nicht zurücksetzt, nachdem der IT-Administrator eine Zurücksetzung initiiert hat.

>[!NOTE]
> Ein Blockieren in `MAMNotificationReceiver.onReceive` ist sicher, weil der zugehörige Rückruf nicht im Benutzeroberflächenthread ausgeführt wird.

Die `MAMNotificationReceiver`-Schnittstelle (gemäß der Definition im SDK) ist nachfolgend enthalten:

```java
/**
 * The SDK is signaling that a MAM event has occurred.
 *
 */
public interface MAMNotificationReceiver {

    /**
     * A notification was received.
     *
     * @param notification
     *            The notification that was received.
     * @return The receiver should return true if it handled the
     *   notification without error (or if it decided to ignore the
     *   notification). If the receiver tried to take some action in
     *   response to the notification but failed to complete that
     *   action it should return false.
     */
    boolean onReceive(MAMNotification notification);
}
```

### <a name="types-of-notifications"></a>Arten von Benachrichtigungen

Folgende Benachrichtigungen werden an die App gesendet; für manche ist ggf. App-Beteiligung erforderlich:

* **WIPE_USER_DATA:** Diese Benachrichtigung wird in einer `MAMUserNotification`-Klasse gesendet. Beim Empfang dieser Benachrichtigung *muss* die App alle Daten im Zusammenhang mit der verwalteten Identität (aus `MAMUserNotification.getUserIdentity()`) löschen. Die Benachrichtigung kann aus verschiedenen Gründen angezeigt werden, z. B. wenn Ihre App `unregisterAccountForMAM` aufruft, wenn ein IT-Administrator eine Gerätezurücksetzung initiiert, oder wenn vom Administrator angeforderte Richtlinien für den bedingten Zugriff nicht erfüllt werden. Wenn Ihre App nicht für diese Benachrichtigung registriert ist, wird das Standardverhalten für Zurücksetzungen ausgeführt. Beim Standardverhalten werden alle Dateien einer App mit einer Identität gelöscht oder alle Dateien, die mit der verwalteten Identität gekennzeichnet sind, bei einer App mit mehreren Identitäten. Diese Benachrichtigung wird niemals an den UI-Thread gesendet.

* **WIPE_USER_AUXILIARY_DATA:** Apps können sich für diese Benachrichtigung registrieren, wenn das Intune App SDK die standardmäßige selektive Zurücksetzung ausführen soll, aber bei der Zurücksetzung weitere Daten entfernt werden sollen. Diese Benachrichtigung ist nicht für Einzelidentitäts-Apps verfügbar und wird nur an Apps mit mehreren Identitäten gesendet. Diese Benachrichtigung wird niemals an den UI-Thread gesendet.

* **REFRESH_POLICY:** Diese Benachrichtigung wird in einer `MAMUserNotification`-Klasse gesendet. Bei Empfang dieser Benachrichtigung müssen jegliche von Ihrer App zwischengespeicherten Intune-Richtlinienentscheidungen für ungültig erklärt und aktualisiert werden. Wenn Ihre App keine Richtlinienannahmen speichert, muss sie nicht für diese Benachrichtigung registriert werden. Es kann nicht garantiert werden, an welche Threads diese Benachrichtigung gesendet wird.

* **REFRESH_APP_CONFIG:** Diese Benachrichtigung wird in einer `MAMUserNotification`-Klasse gesendet. Bei Empfang dieser Benachrichtigung müssen alle zwischengespeicherten Anwendungskonfigurationsdaten für ungültig erklärt und aktualisiert werden. Es kann nicht garantiert werden, an welche Threads diese Benachrichtigung gesendet wird.

* **MANAGEMENT_REMOVED:** Diese Benachrichtigung wird in einer `MAMUserNotification`-Klasse gesendet und informiert die App darüber, dass sie bald zu einer nicht verwalteten App wird. Nachdem sie nicht mehr verwaltet wird, kann die App keine verschlüsselten Dateien und keine mit MAMDataProtectionManager verschlüsselten Daten mehr lesen sowie nicht mehr mit der verschlüsselten Zwischenablage interagieren bzw. anderweitig am Ökosystem der verwalteten Apps teilnehmen. Weitere Informationen finden Sie unten. Diese Benachrichtigung wird niemals an den UI-Thread gesendet.

* **MAM_ENROLLMENT_RESULT**: Diese Benachrichtigung wird in einer `MAMEnrollmentNotification`-Klasse gesendet, um die App darüber zu informieren, dass ein Registrierungsversuch für eine App-Schutzrichtlinie ohne Geräteregistrierung abgeschlossen wurde und um den Status dieses Versuchs bereitzustellen. Es kann nicht garantiert werden, an welche Threads diese Benachrichtigung gesendet wird.

* **COMPLIANCE_STATUS**: Diese Benachrichtigung wird in einer `MAMComplianceNotification`-Klasse gesendet, um die App über das Ergebnis eines Compliancewiederherstellungsversuchs zu informieren. Es kann nicht garantiert werden, an welche Threads diese Benachrichtigung gesendet wird.

> [!NOTE]
> Eine App sollte niemals gleichzeitig für `WIPE_USER_DATA`- und für `WIPE_USER_AUXILIARY_DATA`-Benachrichtigungen registriert werden.

### <a name="management_removed"></a>MANAGEMENT_REMOVED

Die `MANAGEMENT_REMOVED`-Benachrichtigung gibt an, dass ein zuvor von Richtlinien verwalteter Benutzer nicht länger von der Intune-MAM-Richtlinie verwaltet wird. Dazu müssen Benutzerdaten nicht gelöscht oder der Benutzer nicht abgemeldet werden. Wenn ein Löschen erforderlich wäre, würde eine `WIPE_USER_DATA`-Benachrichtigung versendet werden. Viele Apps müssen diese Benachrichtigung möglicherweise überhaupt nicht verarbeiten, Apps, die `MAMDataProtectionManager` verwenden, sollten jedoch [diese Benachrichtigung besonders beachten](#data-protection).

Wenn MAM den `MANAGEMENT_REMOVED`-Empfänger der App aufruft, gilt das Folgende:
* MAM hat bereits zuvor die zur App gehörenden verschlüsselten Dateien außer den geschützten Datenpuffern entschlüsselt. Dateien an öffentlichen Speicherorten auf der SD-Karte, die nicht direkt zur App gehören, z. B. die Ordner „Dokumente“ oder „Downloads“, werden nicht entschlüsselt.
* Neue Dateien oder geschützte Datenpuffer, die von der Empfängermethode erstellt wurden, oder sämtlicher anderer Code, der nach dem Start des Empfängers ausgeführt wird, werden nicht entschlüsselt.
* Die App hat weiterhin Zugriff auf Verschlüsselungsschlüssel, Vorgänge wie die Entschlüsselung von Datenpuffern sind also erfolgreich.

Sobald der Empfänger Ihrer App zurückgegeben wird, besteht kein Zugriff mehr auf Verschlüsselungsschlüssel.

## <a name="configure-azure-active-directory-authentication-library-adal"></a>Konfigurieren der Authentifizierungsbibliothek von Azure Active Directory (Active Directory Authentication Library, ADAL)

> [!NOTE]
> Seit 30. Juni 2020 werden keine neuen Features mehr zur Active Directory-Authentifizierungsbibliothek hinzugefügt. Technischer Support und Sicherheitsupdates werden weiterhin bereitgestellt, Featureupdates jedoch nicht mehr. Für Anwendungen muss ein Upgrade auf die Microsoft-Authentifizierungsbibliothek (Microsoft Authentication Library, MSAL) und Microsoft Graph durchgeführt werden. Weitere Informationen finden Sie im [Leitfaden für die Migration von ADAL zu MSAL für Android](https://docs.microsoft.com/azure/active-directory/develop/migrate-android-adal-msal).


Lesen Sie zunächst die ADAL-Integrationsrichtlinien im [ADAL-Repository auf GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android).

Das SDK ist für seine Szenarien, die die [Authentifizierung](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) und den bedingten Start betreffen, auf [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) angewiesen. Dazu müssen Apps mit [Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-whatis/) konfiguriert sein. Die Konfigurationswerte werden dem SDK über AndroidManifest-Metadaten übermittelt.

Zum Konfigurieren der App und zum Aktivieren der geeigneten Authentifizierung fügen Sie dem App-Knoten in der Datei „AndroidManifest.xml“ Folgendes hinzu. Einige dieser Konfigurationen sind nur erforderlich, wenn Ihre App für die Authentifizierung im Allgemeinen ADAL verwendet. In diesem Fall benötigen Sie die speziellen Werte, die die App verwendet, um sich selbst bei AAD zu registrieren. Damit wird sichergestellt, dass der Endbenutzer nicht zweimal zur Authentifizierung aufgefordert wird, weil AAD zwei separate Registrierungswerte erkennt: einen von der App und einen vom SDK.

```xml
<meta-data
    android:name="com.microsoft.intune.mam.aad.Authority"
    android:value="https://AAD authority/" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.ClientID"
    android:value="your-client-ID-GUID" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.NonBrokerRedirectURI"
    android:value="your-redirect-URI" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.SkipBroker"
    android:value="[true | false]" />
```

### <a name="adal-metadata"></a>ADAL-Metadaten

* **Authority** beschreibt die verwendete AAD-Autorität. Wenn dieser Wert nicht vorhanden ist, wird die öffentliche AAD-Umgebung verwendet.
    > [!NOTE]
    > Legen Sie dieses Feld nicht fest, wenn Ihre App Sovereign Cloud-fähig ist.

* **ClientID** ist die AAD-Client-ID (auch bekannt als Anwendungs-ID), die verwendet werden soll. Sie sollten die Client-ID Ihrer eigenen App verwenden, wenn sie für Azure AD registriert ist oder [Standardregistrierung](#default-enrollment-optional) verwenden, wenn die App ADAL nicht integriert.

* **NonBrokerRedirectURI** ist der Umleitungs-URI von AAD, der in brokerfreien Fällen verwendet wird. Erfolgt keine Angabe, wird der Standardwert `urn:ietf:wg:oauth:2.0:oob` verwendet. Dieser Standardwert ist für die meisten Apps geeignet.

  * Der URI „NonBrokerRedirectURI“ wird nur verwendet, wenn für SkipBroker „true“ gilt.

* **SkipBroker** wird verwendet, um das Standard-ADAL-SOO-Beteiligungsverhalten zu überschreiben. SkipBroker sollte nur für Apps angegeben werden, die eine Client-ID angeben **und** Brokerauthentifizierung/geräteweites SSO nicht unterstützen. In diesem Fall sollte SkipBroker auf „true“ festgelegt werden. Für die meisten Apps sollte der SkipBroker-Parameter nicht festgelegt werden.

  * Eine Client-ID **muss** im Manifest angegeben werden, um einen SkipBroker-Wert anzugeben.

  * Wenn eine Client-ID angegeben wird, ist der Standardwert „false“.

  * Wenn für SkipBroker „true“ gilt, wird NonBrokerRedirectURI verwendet. Apps, die ADAL nicht integrieren und deshalb auch keine Client-ID haben, sind ebenfalls standardmäßig auf „true“ festgelegt.

### <a name="common-adal-configurations"></a>Häufig verwendete ADAL-Konfigurationen

Nachfolgend sind gebräuchliche Methoden zum Konfigurieren einer App mit ADAL aufgeführt. Suchen Sie die Konfiguration Ihrer App und stellen Sie sicher, dass die ADAL-Metadatenparameter (siehe oben) auf die erforderlichen Werte festgelegt sind. In allen Fällen kann die Autorität bei Bedarf für nicht standardmäßige Umgebungen angegeben werden. Wenn nicht anders angegeben, wird die AAD-Autorität für die öffentliche Produktion verwendet.

#### <a name="1-app-does-not-integrate-adal"></a>1. App kann ADAL nicht integrieren
ADAL-Metadaten **dürfen nicht** im Manifest vorhanden sein.

#### <a name="2-app-integrates-adal"></a>2. App kann ADAL integrieren

|Erforderlicher ADAL-Parameter| Wert |
|--|--|
| ClientID | Client-ID der App (von Azure AD generiert, wenn die App registriert ist) |

Wenn erforderlich kann die Autorität angegeben werden.

Sie müssen Ihre App bei Azure AD registrieren und ihr Zugriff auf den App-Schutzrichtliniendienst gewähren:
* Unter [Schnellstart: Registrieren einer Anwendung bei Microsoft Identity Platform](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications) finden Sie Informationen zum Registrieren einer Anwendung bei Azure AD.
* Stellen Sie sicher, dass die Schritte befolgt werden, um Ihrer Android-App Berechtigungen für den Dienst der App-Schutzrichtlinie (App Protection Policy, APP) zu erteilen. Verwenden Sie die Anweisungen im [Leitfaden zu den ersten Schritten mit dem Intune SDK](../developer/app-sdk-get-started.md#next-steps-after-integration) unter „Erteilen von Berechtigungen für den Zugriff auf den Intune-App-Schutzdienst durch Ihre App (optional)“. 

Darüber hinaus finden Sie unten die Anforderungen für den [bedingten Zugriff](#conditional-access).


#### <a name="3-app-integrates-adal-but-does-not-support-brokered-authenticationdevice-wide-sso"></a>3. App kann ADAL integrieren, unterstützt aber keine Brokerauthentifizierung/geräteübergreifende einmalige Anmeldung

|Erforderlicher ADAL-Parameter| Wert |
|--|--|
| ClientID | Client-ID der App (von Azure AD generiert, wenn die App registriert ist) |
| SkipBroker | **True** |

Bei Bedarf können die Autorität und NonBrokerRedirectURI angegeben werden.


### <a name="conditional-access"></a>Bedingter Zugriff
Der bedingte Zugriff (Conditional Access, CA) ist ein [Feature](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer) von Azure Active Directory, das dazu verwendet werden kann, den Zugriff auf AAD-Ressourcen zu steuern. [Intune-Administratoren können Regeln für den bedingten Zugriff definieren](../protect/conditional-access.md), die den Zugriff auf Ressourcen nur über Geräte oder Apps ermöglichen, die von Intune verwaltet werden. Die nachfolgenden Schritte sind erforderlich, um sicherzustellen, dass Ihre App bei Bedarf auf die Ressourcen zugreifen kann. Wenn Ihre App keine AAD-Zugriffstoken erhält oder nur auf Ressourcen zugreift, die nicht durch den bedingten Zugriff geschützt werden können, können Sie diese Schritte überspringen.

1. Befolgen Sie die [ADAL-Integrationsrichtlinien](https://github.com/AzureAD/azure-activedirectory-library-for-android#how-to-use-this-library). 
   Beachten Sie insbesondere Schritt 11 für die Verwendung von Brokern.
2. [Registrieren Sie Ihre Anwendung mit Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration). 
   Den Umleitungs-URI finden Sie oben in den ADAL-Integrationsrichtlinien.
3. Legen Sie die Manifestmetadatenparameter über die oben aufgeführten [häufig verwendeten ADAL-Konfigurationen](#common-adal-configurations) (Punkt 2) fest.
4. Überprüfen Sie, ob alles ordnungsgemäß konfiguriert ist, indem Sie den [gerätebasierten bedingten Zugriff](../protect/conditional-access-intune-common-ways-use.md) im [Azure-Portal](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExchangeConnectorMenu/aad/connectorType/2) aktivieren und bestätigen:
    - Dass die Anmeldung bei Ihrer App Aufforderungen zur Installation und Registrierung des Intune-Unternehmensportals aufruft.
    - Dass die Anmeldung bei Ihrer App nach der Registrierung erfolgreich ausgeführt wird.
5. Sobald Ihre App die Integration des Intune APP SDK geliefert hat, kontaktieren Sie msintuneappsdk@microsoft.com, um Ihre App der Liste der genehmigten Apps für den [App-basierten bedingten Zugriff](https://docs.microsoft.com/intune/conditional-access-intune-common-ways-use#app-based-conditional-access) hinzuzufügen.
6. Sobald Ihre App der Liste hinzugefügt wurde, überprüfen Sie dies, indem Sie den [App-basierten bedingten Zugriff konfigurieren](../protect/app-based-conditional-access-intune-create.md) und sicherstellen, dass die Anmeldung bei Ihrer App erfolgreich abgeschlossen wird.

## <a name="app-protection-policy-without-device-enrollment"></a>App-Schutzrichtlinie ohne Geräteregistrierung

### <a name="overview"></a>Übersicht
Die Intune-App-Schutzrichtlinie ohne Geräteregistrierung (auch als APP-WE oder MAM-WE bezeichnet) ermöglicht, dass Apps von Intune verwaltet werden können, ohne dass das Gerät bei Intune MDM registriert sein muss. APP-WE funktioniert mit oder ohne Geräteregistrierung. Es ist weiterhin erforderlich, dass das Unternehmensportal auf dem Gerät installiert ist, aber der Benutzer muss sich nicht beim Unternehmensportal anmelden und das Gerät registrieren.

> [!NOTE]
> Alle Apps müssen die App-Schutzrichtlinie ohne Geräteregistrierung unterstützen.

### <a name="workflow"></a>Workflow

Wenn eine App ein neues Benutzerkonto erstellt, sollte sie das Konto für die Verwaltung mit dem Intune App SDK registrieren. Das SDK erledigt die Details der Registrierung der App beim APP-WE-Dienst. Bei Bedarf wiederholt es jegliche Registrierungen in entsprechenden Zeitabständen, falls Fehler auftreten.

Die App kann das Intune App-SDK auch nach dem Status eines registrierten Benutzers abfragen, um zu ermitteln, ob der Zugriff des Benutzers auf Unternehmensdaten blockiert werden sollte. Es können mehrere Konten für die Verwaltung registriert werden, aber derzeit darf nur ein Konto zurzeit aktiv beim APP-WE-Dienst registriert sein. Dies bedeutet, dass jeweils nur ein Konto in der App die App-Schutzrichtlinie erhalten kann.

Die App muss einen Rückruf bereitstellen, um das geeignete Zugriffstoken aus der Azure Active Directory Authentication Library (ADAL) im Namen des SDKs zu erlangen. Es wird angenommen, dass die App für die Benutzerauthentifizierung und zum Abrufen eines eigenen Zugriffstokens bereits ADAL verwendet.

Wenn ein Konto vollständig von der App entfernt wird, muss sie die Registrierung für das Konto aufheben, um anzuzeigen, dass die Richtlinie für diesen Benutzer nicht länger von der App angewendet werden soll. Wenn der Benutzer im MAM-Dienst registriert wurde, wird die Registrierung des Benutzers aufgehoben und die App zurückgesetzt.


### <a name="overview-of-app-requirements"></a>Übersicht über die App-Anforderungen

Ihre App muss zum Implementieren der APP-WE-Integration das Benutzerkonto mit dem MAM SDK registrieren:

1. Die App _muss_ eine Instanz der `MAMServiceAuthenticationCallback`-Schnittstelle implementieren und registrieren. Die Rückrufinstanz sollte so früh wie möglich im Lebenszyklus der App registriert werden (in der Regel in der `onMAMCreate()`-Methode der Anwendungsklasse).

2. Wenn ein Benutzerkonto erstellt wurde und sich der Benutzer erfolgreich mit ADAL anmeldet, dann _muss_ die App `registerAccountForMAM()` aufrufen.

3. Wenn ein Benutzerkonto entfernt wurde, sollte die App `unregisterAccountForMAM()` aufrufen, um das Konto aus der Intune-Verwaltung zu entfernen.

    > [!NOTE]
    > Wenn sich ein Benutzer vorübergehend von der App abmeldet, muss die App `unregisterAccountForMAM()` nicht aufrufen. Der Aufruf initiiert möglicherweise eine Zurücksetzung, um Unternehmensdaten für den Benutzer vollständig zu entfernen.


### <a name="mamenrollmentmanager"></a>MAMEnrollmentManager

Alle erforderlichen APIs für die Authentifizierung und Registrierung befinden sich in der `MAMEnrollmentManager`-Schnittstelle. Ein Verweis auf `MAMEnrollmentManager` kann wie folgt abgerufen werden:

```java
MAMEnrollmentManager mgr = MAMComponents.get(MAMEnrollmentManager.class);

// make use of mgr
```

Die zurückgegebenen `MAMEnrollmentManager`-Instanz ist garantiert nicht NULL. Die API-Methoden werden in zwei Kategorien unterteilt: **Authentifizierung** und **Kontoregistrierung**.

```java
package com.microsoft.intune.mam.policy;

public interface MAMEnrollmentManager {
    public enum Result {
        AUTHORIZATION_NEEDED,
        NOT_LICENSED,
        ENROLLMENT_SUCCEEDED,
        ENROLLMENT_FAILED,
        WRONG_USER,
        MDM_ENROLLED,
        UNENROLLMENT_SUCCEEDED,
        UNENROLLMENT_FAILED,
        PENDING,
        COMPANY_PORTAL_REQUIRED;
    }

    //Authentication methods
    interface MAMServiceAuthenticationCallback {
        String acquireToken(String upn, String aadId, String resourceId);
    }
    void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
    void updateToken(String upn, String aadId, String resourceId, String token);

    //Registration methods
    void registerAccountForMAM(String upn, String aadId, String tenantId);
    void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
    void unregisterAccountForMAM(String upn);
    Result getRegisteredAccountStatus(String upn);
}
```

### <a name="account-authentication"></a>Kontoauthentifizierung

In diesem Abschnitt werden die Methoden der Authentifizierungs-API in `MAMEnrollmentManager` und deren Verwendung beschrieben.

```java
interface MAMServiceAuthenticationCallback {
    String acquireToken(String upn, String aadId, String resourceId);
}
void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
void updateToken(String upn, String aadId, String resourceId, String token);
```

1. Die App muss die `MAMServiceAuthenticationCallback`-Schnittstelle implementieren, damit das SDK ein ADAL-Token für den angegebenen Benutzer und die Ressourcen-ID anfordern kann. Die Rückrufinstanz muss für `MAMEnrollmentManager` bereitgestellt werden, indem die zugehörige `registerAuthenticationCallback()`-Methode aufgerufen wird. Möglicherweise ist bereits zu einem frühen Zeitpunkt im Lebenszyklus der App ein Token für Registrierungsversuche oder Eincheckvorgänge zur Aktualisierung der App-Schutzrichtlinie erforderlich, daher ist der ideale Platz zum Registrieren des Rückrufs die `onMAMCreate()`-Methode der `MAMApplication`-Unterklasse der App.

2. Die `acquireToken()`-Methode sollte das Zugriffstoken für die angeforderte Ressource-ID für den angegebenen Benutzer abrufen. Wenn sie das angeforderte Token nicht abrufen kann, muss NULL zurückgeben werden.

    > [!NOTE]
    > Stellen Sie sicher, dass Ihre App die an `acquireToken()` übergebenen `resourceId`- und `aadId`-Parameter verwendet, damit das richtige Token abgerufen wird.

    ```java
    class MAMAuthCallback implements MAMServiceAuthenticationCallback {
        public String acquireToken(String upn, String aadId, String resourceId) {
            return mAuthContext.acquireTokenSilentSync(resourceId, ClientID, aadId).getAccessToken();
        }
    }
    ```

3. Für den Fall, dass die App kein Token bereitstellen kann, wenn das SDK `acquireToken()` aufruft (wenn bei der automatischen Authentifizierung z. B. ein Fehler auftritt und der Zeitpunkt ungeeignet ist, um eine Benutzeroberfläche anzuzeigen), kann die App zu einem späteren Zeitpunkt ein Token bereitstellen, indem die `updateToken()`-Methode aufgerufen wird. Derselbe UPN sowie dieselbe AAD-ID und Ressourcen-ID, die durch den vorherigen Aufruf von `acquireToken()` angefordert wurden, müssen zusammen mit dem abschließend erhaltenen Token an `updateToken()` übergeben werden. Die App sollte diese Methode so früh wie möglich aufrufen, nachdem vom bereitgestellten Rückruf NULL zurückgegeben wurde.

    > [!NOTE]
    > Das SDK ruft `acquireToken()` in regelmäßigen Abständen auf, um das Token abzurufen, daher ist das Aufrufen von `updateToken()` nicht zwingend erforderlich. Es wird jedoch dringend empfohlen, da es beim zeitnahen Abschließen der Registrierungen und Eincheckvorgänge für die App-Schutzrichtlinie helfen kann.


### <a name="account-registration"></a>Kontoregistrierung

In diesem Abschnitt werden die Methoden der Kontoregistrierungs-API in `MAMEnrollmentManager` und deren Verwendung beschrieben.

```java
void registerAccountForMAM(String upn, String aadId, String tenantId);
void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
void unregisterAccountForMAM(String upn);
Result getRegisteredAccountStatus(String upn);
```

1. Die App sollte `registerAccountForMAM()` aufrufen, um ein Konto für die Verwaltung zu registrieren. Ein Benutzerkonto wird über ihren UPN und ihre AAD-Benutzer-ID identifiziert. Zudem ist die Mandanten-ID erforderlich, um die Registrierungsdaten dem AAD-Mandanten des Benutzers zuzuordnen. Die Autorität des Benutzers kann ebenfalls angegeben werden, um die Registrierung bei bestimmten Sovereign Clouds zu ermöglichen. Ausführliche Informationen dazu finden Sie unter [Registrieren einer Sovereign Cloud](#sovereign-cloud-registration).  Das SDK versucht möglicherweise, die App für den angegebenen Benutzer im MAM-Dienst zu registrieren. Wenn bei der Registrierung ein Fehler auftritt, wiederholt das SDK die Registrierung in regelmäßigen Abständen, bis die Registrierung des Kontos aufgehoben wurde. Der Wiederholungszeitraum beträgt in der Regel 12 bis 24 Stunden. Das SDK stellt den Status der Registrierungsversuche asynchron über Benachrichtigungen bereit.

2. Da die AAD-Authentifizierung erforderlich ist, ist der beste Zeitpunkt zum Registrieren des Benutzerkontos im Anschluss an die Anmeldung des Benutzers in der App und der erfolgreichen Authentifizierung mithilfe der ADAL. Die AAD-ID und die Mandanten-ID des Benutzers werden vom Aufruf der ADAL-Authentifizierung als Teil des [`AuthenticationResult`](https://github.com/AzureAD/azure-activedirectory-library-for-android)-Objekts zurückgegeben.
    * Die Mandanten-ID stammt aus der `AuthenticationResult.getTenantID()`-Methode.
    * Informationen zum Benutzer befinden sich in einem untergeordneten Objekt des Typs `UserInfo`, das aus `AuthenticationResult.getUserInfo()` stammt, und die AAD-Benutzer-ID wird durch den Aufruf von `UserInfo.getUserId()` aus diesem Objekt abgerufen.

3. Die App sollte `unregisterAccountForMAM()` aufrufen, um die Registrierung eines Kontos für die Intune-Verwaltung aufzuheben. Wenn das Konto erfolgreich registriert wurde und verwaltet wird, hebt das SDK die Registrierung des Kontos auf und setzt seine Daten zurück. Regelmäßige Registrierungsversuche für das Konto werden beendet. Das SDK stellt den Status der Anforderung zur Aufhebung der Registrierung asynchron über eine Benachrichtigung bereit.

### <a name="sovereign-cloud-registration"></a>Registrieren einer Sovereign Cloud

Anwendungen, die [Sovereign Cloud-fähig](https://www.microsoft.com/trustcenter/cloudservices/nationalcloud) sind, **müssen** `authority` für `registerAccountForMAM()` angeben.  Dies erreichen Sie, indem Sie `instance_aware=true` für acquireToken und extraQueryParameters von [ADAL 1.14.0 und höher](https://github.com/AzureAD/azure-activedirectory-library-for-android/releases/tag/v1.14.0) angeben und anschließend `getAuthority()` für AuthenticationCallback und AuthenticationResult aufrufen.

```java
mAuthContext.acquireToken(this, RESOURCE_ID, CLIENT_ID, REDIRECT_URI, PromptBehavior.FORCE_PROMPT, "instance_aware=true",
        new AuthenticationCallback<AuthenticationResult>() {
            @Override
            public void onError(final Exception exc) {
                // authentication failed
            }

            @Override
            public void onSuccess(final AuthenticationResult result) {
                mAuthority = result.getAuthority();
                // handle other parts of the result
            }
        });
```

> [!NOTE]
> Legen Sie das `com.microsoft.intune.mam.aad.Authority`-Metadatenelement in der Datei AndroidManifest.xml nicht fest.

> [!NOTE]
> Stellen Sie sicher, dass die Autorität ordnungsgemäß in Ihrer `MAMServiceAuthenticationCallback::acquireToken()`-Methode festgelegt ist.

#### <a name="currently-supported-sovereign-clouds"></a>Derzeit unterstützte Sovereign Clouds

1. Azure-Cloud für US-Behörden
2. Microsoft Azure, betrieben von 21Vianet (Azure China)


### <a name="important-implementation-notes"></a>Wichtige Hinweise zur Implementierung

#### <a name="authentication"></a>Authentifizierung

* Wenn die App `registerAccountForMAM()` aufruft, erhält Sie möglicherweise kurze Zeit später über ihre `MAMServiceAuthenticationCallback`-Schnittstelle einen Rückruf zu einem anderen Thread. Idealerweise hat die App vor der Registrierung des Kontos ihr eigenes Token von der ADAL abgerufen, um die Beschaffung des angeforderten Tokens zu beschleunigen. Wenn die App über den Rückruf ein gültiges Token zurückgibt, wird die Registrierung fortgesetzt, und die App erhält das endgültige Ergebnis über eine Benachrichtigung.

* Wenn die App kein gültiges AAD-Token zurückgibt, wird `AUTHORIZATION_NEEDED` als endgültiges Ergebnis des Registrierungsversuchs zurückgegeben. Wenn die App dieses Ergebnis über eine Benachrichtigung erhält, sollte der Registrierungsprozess unbedingt durch die Beschaffung des Tokens für den Benutzer und der Ressource, die zuletzt von `acquireToken()` angefordert wurde und den Aufruf der `updateToken()`-Methode beschleunigt werden, um den Registrierungsprozess noch mal zu initiieren.

* Die registrierte `MAMServiceAuthenticationCallback`-Schnittstelle der App wird ebenfalls aufgerufen, um ein Token für regelmäßige Eincheckvorgänge zum Aktualisieren der App-Schutzrichtlinie abzurufen. Wenn die App ein Token nicht auf Anforderung bereitstellen kann, erhält sie keine Benachrichtigung. Sie sollte jedoch zum nächsten geeigneten Zeitpunkt versuchen, ein Token abzurufen und `updateToken()` aufzurufen, um den Eincheckvorgang zu beschleunigen. Ohne Bereitstellung eines Tokens wird der Rückruf beim nächsten Eincheckversuch weiterhin aufgerufen.

* Die Unterstützung von Sovereign Clouds erfordert die Angabe der Autorität.

#### <a name="registration"></a>Registrierung

* Der Einfachheit halber sind die Registrierungsmethoden idempotent. `registerAccountForMAM()` registriert ein Konto und die App z. B. nur, wenn das Konto noch nicht registriert ist, und `unregisterAccountForMAM()` hebt die Registrierung eines Kontos nur auf, wenn es derzeit registriert ist. Nachfolgende Aufrufe sind Leerbefehle, daher ist es nicht schädlich, diese Methoden mehrmals aufzurufen. Darüber hinaus wird die Übereinstimmung zwischen Aufrufen dieser Methoden und Benachrichtigungen über Ergebnisse nicht garantiert. Wenn z. B. `registerAccountForMAM()` für eine Identität aufgerufen wird, die bereits registriert ist, wird die Benachrichtigung für diese Identität möglicherweise nicht erneut gesendet. Es ist möglich, dass Benachrichtigungen gesendet werden, die mit keinem Aufruf dieser Methoden übereinstimmen, da das SDK möglicherweise regelmäßig Registrierungsversuche im Hintergrund durchführt und das Aufheben der Registrierung möglicherweise durch Zurücksetzungsanforderungen ausgelöst wird, die vom Intune-Dienst empfangen wurden.

* Die Registrierungsmethoden können für eine beliebige Anzahl von unterschiedlichen Identitäten aufgerufen werden, aber derzeit kann nur ein Benutzerkonto erfolgreich registriert sein. Wenn mehrere Benutzerkonten, die für Intune lizenziert und Ziel der App-Schutzrichtlinie sind, zum gleichen oder nahezu dem gleichen Zeitpunkt registriert werden, gibt es keine Garantie dahingehend, welches dieser Benutzerkonten das Rennen macht.

* Abschließend können Sie `MAMEnrollmentManager` abfragen, um zu prüfen, ob ein bestimmtes Konto registriert ist, und um seinen aktuellen Status mithilfe der `getRegisteredAccountStatus()`-Methode abzurufen. Wenn das bereitgestellte Konto nicht registriert ist, gibt diese Methode **NULL** zurück. Wenn das Konto registriert ist, gibt diese Methode den Status des Kontos als eines der Elemente der `MAMEnrollmentManager.Result`-Enumeration zurück.

### <a name="result-and-status-codes"></a>Ergebnis und Statuscodes

Wenn ein Konto erstmalig registriert wird, verfügt es über den Status `PENDING`, wodurch angegeben wird, dass der erste Registrierungsversuch für den MAM-Dienst unvollständig ist. Nachdem der Registrierungsversuch abgeschlossen ist, wird eine Benachrichtigung mit einem der Ergebniscodes aus der folgenden Tabelle gesendet. Darüber hinaus gibt die `getRegisteredAccountStatus()`-Methode den Kontostatus zurück, damit die App immer bestimmen kann, ob der Zugriff für diesen Benutzer auf Unternehmensdaten blockiert ist. Wenn bei der Registrierung ein Fehler auftritt, kann der Kontostatus mit der Zeit wechseln, da das SDK die Registrierung im Hintergrund erneut versucht.

|Ergebniscode | Erläuterung |
| -- | -- |
| `AUTHORIZATION_NEEDED` | Dieses Ergebnis gibt an, dass von der registrierten `MAMServiceAuthenticationCallback`-Instanz der App kein Token bereitgestellt wurde, oder das bereitgestellte Token war ungültig.  Die App sollte ein gültiges Token abrufen und `updateToken()` aufrufen, sofern möglich. |
| `NOT_LICENSED` | Der Benutzer ist für Intune nicht lizenziert oder bei dem Versuch, den Kontakt zum Intune MAM-Dienst herzustellen, ist ein Fehler aufgetreten.  Die App sollte in einem nicht verwalteten (normalen) Zustand fortfahren, und der Benutzer sollte nicht blockiert werden.  Registrierungen werden für den Fall in regelmäßigen Abständen wiederholt, dass der Benutzer zukünftig über eine Lizenz verfügt. |
| `ENROLLMENT_SUCCEEDED` | Der Registrierungsversuch wurde erfolgreich durchgeführt, oder der Benutzer ist bereits registriert.  Im Falle einer erfolgreichen Registrierung wird vor dieser Benachrichtigung eine Benachrichtigung zur Richtlinienaktualisierung gesendet.  Der Zugriff auf Unternehmensdaten sollte zugelassen werden. |
| `ENROLLMENT_FAILED` | Fehler beim Registrierungsversuch.  Weitere Details finden Sie in den Geräteprotokollen.  Die App sollte in diesem Zustand nicht den Zugriff auf Unternehmensdaten gestatten, da zuvor ermittelt wurde, dass der Benutzer für Intune lizenziert ist.|
| `WRONG_USER` | Nur ein Benutzer pro Gerät kann eine App mit dem MAM-Dienst registrieren. Dieses Ergebnis weist darauf hin, dass für den Benutzer, für den dieses Ergebnis zurückgegeben wurde (der zweite Benutzer), die MAM-Richtlinie gilt, aber dass bereits ein anderer Benutzer registriert wurde. Da die MAM-Richtlinie nicht für den zweiten Benutzer erzwungen werden kann, darf Ihre App so lange keinen Zugriff auf die Daten dieses Benutzers gewähren (z. B. indem der Benutzer aus Ihrer App entfernt wird), bis die Registrierung für diesen Benutzer zu einem späteren Zeitpunkt erfolgreich war. Gleichzeitig mit der Rückgabe des `WRONG_USER`-Ergebnisses zeigt die mobile Anwendungsverwaltung eine Aufforderung mit der Option an, das vorhandene Konto zu entfernen. Wenn der menschliche Benutzer dies bestätigt, ist es tatsächlich möglich, dass der zweite Benutzer kurze Zeit später registriert wird. Solange der zweite Benutzer registriert ist, versucht die mobile Anwendungsverwaltung die Registrierung in regelmäßigen Abständen erneut. |
| `UNENROLLMENT_SUCCEEDED` | Die Aufhebung der Registrierung war erfolgreich.|
| `UNENROLLMENT_FAILED` | Fehler bei der Anforderung zur Aufhebung der Registrierung.  Weitere Details finden Sie in den Geräteprotokollen. Allgemein gesagt tritt dies nur auf, wenn die App keinen gültigen (d. h. NULL oder leer) Benutzerprinzipalname übergibt. Es gibt für diese Situation keine direkte und zuverlässige Lösung, die die App anwenden könnte. Wenn dieser Wert zurückgegeben wird, wenn die Registrierung eines gültigen Benutzerprinzipalnamens aufgehoben wird, melden Sie dies dem MAM-Team von Intune bitte als Fehler.|
| `PENDING` | Der anfängliche Registrierungsversuch für den Benutzer wird ausgeführt.  Die App kann den Zugriff auf Unternehmensdaten blockieren, bis das Registrierungsergebnis bekannt ist, aber sie ist dazu nicht verpflichtet. |
| `COMPANY_PORTAL_REQUIRED` | Der Benutzer ist für Intune lizenziert, aber die App kann nicht registriert werden, bis die Unternehmensportal-App auf dem Gerät installiert ist. Das Intune App SDK versucht, den Zugriff auf die App für den angegebenen Benutzer zu blockieren und ihn zur Installation der Unternehmensportal-App zu bewegen (siehe nachfolgende Details). |


### <a name="company-portal-requirement-prompt-override-optional"></a>Aufforderung zur Unternehmensportalanforderung außer Kraft setzen (optional)

Wenn das Ergebnis `COMPANY_PORTAL_REQUIRED` zurückgegeben wird, blockiert das SDK die Verwendung von Aktivitäten, die die Identität verwenden, für die die Registrierung angefordert wurde. Stattdessen führt das SDK dazu, dass diese Aktivitäten eine Aufforderung zum Herunterladen des Unternehmensportals anzeigen. Wenn Sie dieses Verhalten in Ihrer App verhindern möchten, können die Aktivitäten `MAMActivity.onMAMCompanyPortalRequired` implementieren.

Diese Methode wird aufgerufen, bevor das SDK seine standardmäßig blockierende Benutzeroberfläche anzeigt. Wenn die App die Aktivitätsidentität ändert oder die Registrierung des Benutzers aufhebt, der die Registrierung versucht hat, wird die Aktivität nicht vom SDK blockiert. In dieser Situation ist es Aufgabe der App, den Verlust von Unternehmensdaten zu vermeiden. Apps mit mehreren Identitäten (weiter unten erläutert) können die Aktivitätsidentität ändern.

Wenn Sie `MAMActivity` nicht explizit erben (da die Buildtools diese Änderung vornehmen), aber trotzdem diese Benachrichtigung verarbeiten müssen, können Sie stattdessen `MAMActivityBlockingListener` implementieren.

### <a name="notifications"></a>Benachrichtigungen

Wenn die App für Benachrichtigungen des Typs **MAM_ENROLLMENT_RESULT** registriert ist, wird eine `MAMEnrollmentNotification`-Benachrichtigung gesendet, um die App zu informieren, dass die Registrierungsanforderung abgeschlossen wurde. `MAMEnrollmentNotification` wird über die `MAMNotificationReceiver`-Schnittstelle empfangen, wie im Abschnitt [Registrieren für Benachrichtigungen vom SDK](#register-for-notifications-from-the-sdk) beschrieben.

```java
public interface MAMEnrollmentNotification extends MAMUserNotification {
    MAMEnrollmentManager.Result getEnrollmentResult();
}
```

Die `getEnrollmentResult()`-Methode gibt das Ergebnis der Registrierungsanforderung zurück.  Da `MAMUserNotification` von `MAMEnrollmentNotification` erweitert wird, ist die Identität des Benutzers ebenfalls verfügbar, für den die Registrierung versucht wurde. Die App muss die `MAMNotificationReceiver`-Schnittstelle implementieren, um diese Benachrichtigungen zu erhalten. Dieser Vorgang wird ausführlich im Abschnitt [Registrieren für Benachrichtigungen vom SDK](#register-for-notifications-from-the-sdk) beschrieben.

Der Kontostatus für den registrierten Benutzer kann sich ändern, wenn eine Registrierungsbenachrichtigung empfangen wird, aber in einigen Fällen wird der Status nicht geändert. (Wenn z. B. eine `AUTHORIZATION_NEEDED`-Benachrichtigung nach einem informativeren Ergebnis wie `WRONG_USER` empfangen wird, bleibt das informativere Ergebnis als Kontostatus erhalten.)  Sobald das Konto erfolgreich registriert wurde, bleibt der Status solange `ENROLLMENT_SUCCEEDED`, bis die Registrierung des Kontos aufgehoben oder das Konto selbst gelöscht wird.


## <a name="app-ca-with-policy-assurance"></a>App-Steuerung für bedingten Zugriff mit Richtlinienerzwingung

### <a name="overview"></a>Übersicht
Über die App-Steuerung für bedingten Zugriff mit Richtlinienerzwingung ist der Zugriff auf Ressourcen an die Anwendung von Intune-App-Schutzrichtlinien gebunden.  AAD erzwingt dies, indem erzwungen wird, dass die App registriert und von der App-Steuerung für bedingten Zugriff verwaltet wird, bevor einem Token Zugriff auf eine durch die App-Steuerung für bedingten Zugriff mit Richtlinienerzwingung geschützte Ressource gewährt wird.  Die App muss den ADAL-Broker für den Tokenabruf verwenden. Die Einrichtung ist identisch mit der, die oben für den [bedingten Zugriff](#conditional-access) beschrieben wurde.

### <a name="adal-changes"></a>ADAL-Änderungen
Die ADAL-Bibliothek verfügt über einen neuen Fehlercode, der die App darüber informiert, dass die Tatsache, dass ein Token nicht abgerufen werden kann, durch eine fehlende Konformität mit der Verwaltung der App-Steuerung für bedingten Zugriff verursacht wurde.  Wenn die App diesen Fehlercode erhält, muss sie das SDK aufrufen, um zu versuchen, die Konformität wiederherzustellen, indem die App registriert und die Richtlinie angewendet wird. Eine Ausnahme wird von der `onError()`-Methode der ADAL-`AuthenticationCallback`-Schnittstelle empfangen und führt zum Fehlercode `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED`.  In diesem Fahl kann die Ausnahme in eine `IntuneAppProtectionPolicyRequiredException`-Ausnahme umgewandelt werden, aus der zusätzliche Parameter extrahiert werden können, um sie für die Wiederherstellung der Konformität zu verwenden (siehe Beispielcode unten). Sobald die Wiederherstellung der Konformität erfolgreich war, kann die App noch mal versuchen, das Token über ADAL abzurufen.

> [!NOTE]
> Für diesen neuen Fehlercode und weitere Unterstützung für die App-Steuerung für bedingten Zugriff mit Richtlinienerzwingung ist mindestens die Version 1.15.0 der ADAL-Bibliothek erforderlich.

### <a name="mamcompliancemanager"></a>MAMComplianceManager

Die `MAMComplianceManager`-Schnittstelle wird verwendet, wenn der richtlinienbedingte Fehler von ADAL empfangen wird.  Darin ist die `remediateCompliance()`-Methode enthalten, die aufgerufen werden sollte, um zu versuchen, die App in einen konformen Status zu versetzen. Ein Verweis auf `MAMComplianceManager` kann wie folgt abgerufen werden:

```java
MAMComplianceManager mgr = MAMComponents.get(MAMComplianceManager.class);

// make use of mgr
```

Die zurückgegebenen `MAMComplianceManager`-Instanz ist garantiert nicht NULL.

```java
package com.microsoft.intune.mam.policy;

public interface MAMComplianceManager {
    void remediateCompliance(String upn, String aadId, String tenantId, String authority, boolean showUX);
}
```

Die `remediateCompliance()`-Methode wird aufgerufen, um zu versuchen, die App verwalten zu lassen, um die Bedingungen für AAD erfüllen zu können, um dem angeforderten Token Zugriff zu gewähren.  Die ersten vier Parameter können aus der Ausnahme extrahiert werden, die von der ADAL-`AuthenticationCallback.onError()`-Methode empfangen wurde (siehe Codebeispiel unten).  Der letzte Parameter ist ein boolescher Wert, der steuert, ob während dem Versuch, die Konformität wiederherzustellen, eine Benutzeroberfläche angezeigt wird.  Dies ist eine einfache Schnittstelle zum Blockieren des Fortschritts, die als Standardschnittstelle für Apps zur Verfügung gestellt wird, die keine angepasste Benutzeroberfläche während dieses Vorgangs anzeigen müssen.  Es wird nur blockiert, während die Konformität wiederhergestellt wird. Das Endergebnis wird nicht angezeigt.  Die App sollte einen Benachrichtigungsempfänger registrieren, um den Erfolg oder einen Fehlschlag des Versuchs, die Konformität wiederherzustellen, verarbeiten zu können (siehe unten).

Die `remediateCompliance()`-Methode kann eine MAM-Registrierung als Teil der Herstellung von Konformität durchführen.  Die App kann eine Registrierungsbenachrichtigung erhalten, wenn sie einen Benachrichtigungsempfänger für Registrierungsbenachrichtigungen registriert hat.  Die registrierte `MAMServiceAuthenticationCallback`-Schnittstelle der App lässt ihre `acquireToken()`-Methode aufrufen, um ein Token für die MAM-Registrierung zu erhalten. Die `acquireToken()`-Methode wird aufgerufen, bevor die App ihr eigenes Token abgerufen hat. Alle Buchhaltungs- oder Kontoerstellungsaufgaben, die die App nach einem erfolgreichen Tokenabruf ausführt, wurden also möglicherweise noch nicht ausgeführt.  In diesem Fall muss der Rückruf in der Lage sein, ein Token abzurufen.  Wenn kein Token von `acquireToken()` zurückgegeben werden kann, schlägt der Versuch, die Konformität wiederherzustellen, fehl.  Wenn Sie `updateToken()` später mit einem gültigen Token für die angeforderte Ressource aufrufen, wird der Versuch, die Konformität wiederherzustellen, sofort mit diesem Token noch mal ausgeführt.

> [!NOTE]
> Ein automatischer Tokenabruf ist in `acquireToken()` weiterhin möglich, da der Benutzer bereits zum Installieren des Brokers und Registrieren des Geräts geleitet wurde, bevor der `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED`-Fehler empfangen wurde.  Dies führt dazu, dass der Broker über ein gültiges Aktualisierungstoken im Cache verfügt, wodurch ein erfolgreiches automatisches Abrufen des angeforderten Tokens ermöglicht wird.

Hier sehen Sie ein Beispiel, wie der richtlinienbedingte Fehler in der `AuthenticationCallback.onError()`-Methode empfangen wird, und wie `MAMComplianceManager` aufgerufen wird, um den Fehler zu verarbeiten.

```java
public void onError(@Nullable Exception exc) {
    if (exc instanceof AuthenticationException && 
        ((AuthenticationException) exc).getCode() == ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED) {

        final IntuneAppProtectionPolicyRequiredException policyRequiredException = 
            (IntuneAppProtectionPolicyRequiredException) ex;

        final String upn = policyRequiredException.getAccountUpn();
        final String aadId = policyRequiredException.getAccountUserId();
        final String tenantId = policyRequiredException.getTenantId();
        final String authority = policyRequiredException.getAuthorityURL();

        MAMComplianceManager complianceManager = MAMComponents.get(MAMComplianceManager.class);
        complianceManager.remediateCompliance(upn, aadId, tenantId, authority, showUX);
    }
}
```

### <a name="status-notifications"></a>Statusbenachrichtigungen

Wenn die App sich für Benachrichtigungen des Typs **COMPLIANCE_STATUS** registriert, wird eine `MAMComplianceNotification`-Benachrichtigung gesendet, um die App über den endgültigen Status des Versuchs, die Konformität wiederherzustellen, zu informieren. `MAMComplianceNotification` wird über die `MAMNotificationReceiver`-Schnittstelle empfangen, wie im Abschnitt [Registrieren für Benachrichtigungen vom SDK](#register-for-notifications-from-the-sdk) beschrieben.

```java
public interface MAMComplianceNotification extends MAMUserNotification {
    MAMCAComplianceStatus getComplianceStatus();
    String getComplianceErrorTitle();
    String getComplianceErrorMessage();
}
```

Die `getComplianceStatus()`-Methode gibt das Ergebnis des Versuchs, die Konformität wiederherzustellen, als Wert aus der `MAMCAComplianceStatus`-Enumeration zurück.

|Statuscode | Erläuterung |
| -- | -- |
| UNBEKANNT | Der Status ist unbekannt. Diese könnte auf eine unerwartete Fehlerursache hindeuten. Weitere Informationen können den Unternehmensportalprotokollen entnommen werden. |
| KONFORM | Die Wiederherstellung der Konformität war erfolgreich, und die App ist nun mit der Richtlinie konform. Der Abruf des ADAL-Tokens sollte noch mal versucht werden. |
| NOT_COMPLIANT | Der Versuch, die Konformität wiederherzustellen, ist fehlgeschlagen.  Die App ist nicht konform, und der Abruf des ADAL-Tokens sollte nicht noch mal versucht werden, bis die Fehlerbedingung korrigiert wurde.  Zusammen mit MAMComplianceNotification werden zusätzliche Fehlerinformationen gesendet. |
| SERVICE_FAILURE | Beim Versuch, Konformitätsdaten aus dem Intune-Dienst abzurufen, ist ein Fehler aufgetreten. Weitere Informationen können den Unternehmensportalprotokollen entnommen werden. |
| NETWORK_FAILURE | Fehler beim Herstellen einer Verbindung zum Intune-Dienst. Die App sollte noch mal versuchen, das Token abzurufen, wenn die Netzwerkverbindung wiederhergestellt wurde. |
| CLIENT_ERROR | Der Versuch, die Konformität wiederherzustellen, ist aus clientbezogenen Gründen fehlgeschlagen.  Ein Beispiel: Kein Token verfügbar oder falscher Benutzer. Zusammen mit MAMComplianceNotification werden zusätzliche Fehlerinformationen gesendet. |
| PENDING (AUSSTEHEND) | Der Versuch, die Konformität wiederherzustellen, ist fehlgeschlagen, da die Statusantwort noch nicht vom Dienst empfangen wurde, als das Zeitlimit ablief. Die App sollte später noch einmal versuchen, das Token abzurufen. |
| COMPANY_PORTAL_REQUIRED | Das Unternehmensportal muss auf dem Gerät installiert sein, damit die Konformitätswiederherstellung erfolgreich sein kann.  Wenn das Unternehmensportal bereits auf dem Gerät installiert ist, muss die App neu gestartet werden.  In diesem Fall wird ein Dialogfeld angezeigt, das den Benutzer auffordert, die App neu zu starten. |

Wenn der Konformitätsstatus `MAMCAComplianceStatus.COMPLIANT` ist, sollte die App ihren ursprünglichen Tokenabruf neu initiieren (für ihre eigene Ressource). Wenn der Versuch, die Konformität wiederherzustellen, fehlgeschlagen ist, geben die `getComplianceErrorTitle()`- und `getComplianceErrorMessage()`-Methoden lokalisierte Zeichenfolgen zurück, die die App dem Endbenutzer gegebenenfalls anzeigen kann.  In den meisten Fällen können die Fehler von der App nicht behoben werden,. Allgemein ist es also am besten, dass die Kontoerstellung oder Anmeldung fehlschlägt und der Benutzer die Möglichkeit erhält, es später noch mal zu versuchen.  Wenn ein Fehlschlag dauerhaft auftritt, helfen die MAM-Protokolle möglicherweise dabei, die Gründe dafür herauszufinden.  Der Endbenutzer kann die Protokolle übermitteln. Weitere Informationen finden Sie unter [Hochladen von Protokollen und Versenden per E-Mail](../user-help/send-logs-to-your-it-admin-by-email-android.md).

Da `MAMUserNotification` von `MAMComplianceNotification` erweitert wird, ist die Identität des Benutzers ebenfalls verfügbar, für den die Wiederherstellung versucht wurde.

Hier finden Sie ein Beispiel, einen Empfänger mithilfe einer anonymen Klasse zu registrieren, um die MAMNotificationReceiver-Schnittstelle zu implementieren:

```java
final MAMNotificationReceiverRegistry notificationRegistry = MAMComponents.get(MAMNotificationReceiverRegistry.class);
// create a receiver
final MAMNotificationReceiver receiver = new MAMNotificationReceiver() {
    public boolean onReceive(MAMNotification notification) {
        if (notification.getType() == MAMNotificationType.COMPLIANCE_STATUS) {
            MAMComplianceNotification complianceNotification = (MAMComplianceNotification) notification;
            
            // take appropriate action based on complianceNotification.getComplianceStatus()
            
            // unregister this receiver if no longer needed
            notificationRegistry.unregisterReceiver(this, MAMNotificationType.COMPLIANCE_STATUS);
        }
        return true;
    }
};
// register the receiver
notificationRegistry.registerReceiver(receiver, MAMNotificationType.COMPLIANCE_STATUS);
```

> [!NOTE]
> Der Benachrichtigungsempfänger muss registriert werden, bevor `remediateCompliance()` aufgerufen wird, um eine Racebedingung zu vermeiden, die dazu führen könnte, dass die Benachrichtigung ausgelassen wird.

### <a name="implementation-notes"></a>Hinweise zur Implementierung

> [!NOTE]
> **Wichtige Änderung!**  <br>
> Die `MAMServiceAuthenticationCallback.acquireToken()`-Methode der App sollte für das neue `forceRefresh`-Flag *FALSE* an `acquireTokenSilentSync()` übergeben.
> Bisher sollte *TRUE* übergeben werden, um ein Problem mit Aktualisierungstoken vom Broker zu beheben. Es wurde aber ein Problem mit ADAL entdeckt, das den Abruf von Tokens in einigen Szenarios verhindern könnte, wenn für dieses Flag *TRUE* gilt.
```java
AuthenticationResult result = acquireTokenSilentSync(resourceId, clientId, userId, /* forceRefresh */ false);
```

> [!NOTE]
> Wenn während des Versuchs, die Konformität wiederherzustellen, eine benutzerdefinierte blockierte Benutzeroberfläche angezeigt werden soll, sollten Sie für den showUX-Parameter den Wert *false* an `remediateCompliance()` übergeben. Sie müssen zuerst sicherstellen, dass die Benutzeroberfläche angezeigt wird und Sie Ihren Listener für Benachrichtigungen registrieren, bevor `remediateCompliance()` aufgerufen wird.  Dies verhindert eine Racebedingung, bei der die Benachrichtigung ausgelassen werden könnte, wenn `remediateCompliance()` sehr schnell fehlschlägt.  Ein Beispiel: Die `onCreate()`- oder `onMAMCreate()`-Methode einer Subklasse einer Aktivität ist der ideale Ort, um den Benachrichtigungslistener zu registrieren und dann `remediateCompliance()` aufzurufen.  Die Parameter für `remediateCompliance()` können an Ihre Benutzeroberfläche als Zusätze für eine Absicht übergeben werden.  Wenn die Benachrichtigung zum Konformitätsstatus empfangen wird, können Sie das Ergebnis anzeigen oder einfach die Aktivität beenden.

> [!NOTE]
> `remediateCompliance()` registriert das Konto und versucht die Registrierung.  Sobald das Token abgerufen wurde, ist das Aufrufen von `registerAccountForMAM()` nicht mehr nötig, es schadet aber keinesfalls, es dennoch zu tun. Andererseits muss die App, wenn sie das Token nicht abrufen kann und das Benutzerkonto entfernen möchte, `unregisterAccountForMAM()` aufrufen, um das Konto zu entfernen und Registrierungsversuche im Hintergrund zu vermeiden.

## <a name="protecting-backup-data"></a>Schutz von Sicherungsdaten

Seit Android Marshmallow (API 23) bietet Android einer App zwei Möglichkeiten zum Sichern ihrer Daten. Jede Option ist für Ihre App verfügbar und erfordert andere Schritte, um sicherzustellen, dass Intune-Datenschutz ordnungsgemäß implementiert wird. In der folgenden Tabelle können Sie sich einen Überblick über die entsprechenden Aktionen verschaffen, die für ein korrektes Verhalten beim Datenschutz erforderlich sind.  Mehr über die Sicherungsmethoden erfahren Sie im [Android-API-Handbuch](https://developer.android.com/guide/topics/data/backup.html).

### <a name="auto-backup-for-apps"></a>Automatische Sicherung für Apps

Android hat begonnen, [automatische vollständige Sicherungen](https://developer.android.com/guide/topics/data/autobackup.html) auf Google Drive für Apps auf Android Marshmallow-Geräten unabhängig von der Ziel-API der App anzubieten. Wenn Sie in „AndroidManifest.xml“ explizit für `android:allowBackup`**false** festlegen, steht Ihre App niemals für Sicherungen von Android in der Warteschlange, und „Unternehmensdaten“ bleiben innerhalb der App. In diesem Fall ist keine weitere Aktion erforderlich.

Allerdings ist das `android:allowBackup`-Attribut standardmäßig auf „true“ festgelegt – auch wenn `android:allowBackup` nicht in der Manifestdatei angegeben ist. Dies bedeutet, dass alle App-Daten automatisch im Google Drive-Konto des Benutzers gesichert werden – ein Standardverhalten, das ein **Datenverlustrisiko** darstellt. Daher erfordert das SDK die unten beschriebenen Änderungen, um sicherzustellen, dass Datenschutz angewendet wird.  Es ist wichtig, die folgenden Richtlinien zu befolgen, um Kundendaten angemessen zu schützen, wenn Ihre App auf Android Marshmallow-Geräten ausgeführt werden soll.  

Mit Intune können Sie alle [Funktionen für automatische Sicherung](https://developer.android.com/guide/topics/data/autobackup.html) verwenden, die bei Android verfügbar sind, einschließlich der Möglichkeit, benutzerdefinierte Regeln in XML zu definieren, jedoch müssen Sie die folgenden Schritte befolgen, um Ihre Daten zu sichern:

1. Wenn Ihre App **keinen** benutzerdefinierten BackupAgent verwendet, verwenden Sie die Standardeinstellung MAMBackupAgent, um automatische vollständige Sicherungen zu ermöglichen, die mit Intune-Richtlinien kompatibel sind. Fügen Sie Folgendes in das App-Manifest ein:

    ```xml
    android:fullBackupOnly="true"
    android:backupAgent="com.microsoft.intune.mam.client.app.backup.MAMDefaultBackupAgent"
    ```
    
2. **[Optional]** Wenn Sie einen optionalen benutzerdefinierten BackupAgent implementiert haben, müssen Sie sicherstellen, dass Sie MAMBackupAgent oder MAMBackupAgentHelper verwenden. Weitere Informationen finden Sie in den folgenden Abschnitten. Wechseln Sie ggf. zu **MAMDefaultFullBackupAgent** von Intune (in Schritt 1 beschrieben), der eine einfache Sicherung für Android M und höher bietet.

3. Wenn Sie festlegen, welche Art von vollständiger Sicherung Ihre App erhalten soll (ungefiltert, gefiltert oder keine), müssen Sie das Attribut `android:fullBackupContent` auf „true“, „false“ oder eine XML-Ressource in Ihrer App festlegen.

4. Dann _**müssen**_ Sie das, was Sie in `android:fullBackupContent` eingefügt haben, in ein Metadatentag namens `com.microsoft.intune.mam.FullBackupContent` in das Manifest kopieren.

    **Beispiel 1:** Wenn Ihre App vollständige Sicherungen ohne Ausschlüsse erstellen soll, legen Sie sowohl das `android:fullBackupContent`-Attribut als auch das `com.microsoft.intune.mam.FullBackupContent`-Metadatentag auf **TRUE** fest:

    ```xml
    android:fullBackupContent="true"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="true" />  
    ```

    **Beispiel 2:** Wenn Ihre App ihren benutzerdefinierten BackupAgent verwenden und vollständige mit Intune-Richtlinien konforme automatische Sicherungen deaktivieren soll, müssen Sie das Attribut und das Metadatentag auf **FALSE** festlegen:

    ```xml
    android:fullBackupContent="false"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="false" />  
    ```

    **Beispiel 3:** Wenn Ihre App vollständige Sicherungen gemäß Ihren in einer XML-Datei definierten benutzerdefinierten Regeln erstellen soll, legen Sie das Attribut und das Metadatentag auf dieselbe XML-Ressource fest:

    ```xml
    android:fullBackupContent="@xml/my_scheme"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:resource="@xml/my_scheme" />  
    ```


### <a name="keyvalue-backup"></a>Schlüssel/Wert-Sicherung

Die Option [Schlüssel/Wert-Sicherung](https://developer.android.com/guide/topics/data/keyvaluebackup.html) ist für alle APIs ab Version 8 verfügbar, und sie lädt App-Daten zum [Android Backup Service](https://developer.android.com/google/backup/index.html) hoch. Die Datenmenge pro Benutzer Ihrer App ist auf 5MB beschränkt. Wenn Sie die Schlüssel/Wert-Sicherung verwenden, müssen Sie **BackupAgentHelper** oder **BackupAgent** verwenden.

### <a name="backupagenthelper"></a>BackupAgentHelper

„BackupAgentHelper“ ist einfacher zu implementieren als „BackupAgent“, was systemeigene Android-Funktionalität und Intune MAM-Integration anbelangt. „BackupAgentHelper“ ermöglicht dem Entwickler, ganze Dateien und gemeinsam genutzte Einstellungen bei **FileBackupHelper** bzw. **SharedPreferencesBackupHelper** zu registrieren, die bei Erstellung dann „BackupAgentHelper“ hinzugefügt werden. Führen Sie die nachstehenden Schritte aus, um „BackupAgentHelper“ mit Intune MAM zu verwenden:

1. Befolgen Sie die Android-Anleitung zum [Erweitern von BackupAgentHelper](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgentHelper), um die Sicherung mehrerer Identitäten mit „BackupAgentHelper“ zu nutzen.

2. Lassen Sie die MAM-Entsprechung von „BackupAgentHelper“, „FileBackupHelper“ und „SharedPreferencesBackupHelper“ von Ihrer Klasse erweitern.

|Android-Klasse | MAM-Entsprechung |
|--|--|
|BackupAgentHelper |MAMBackupAgentHelper |
|FileBackupHelper | MAMFileBackupHelper
|SharedPreferencesBackupHelper| MAMSharedPreferencesBackupHelper|

Das Befolgen dieser Richtlinien führt zu einer erfolgreichen Sicherung und Wiederherstellung mehrerer Identitäten.

### <a name="backupagent"></a>BackupAgent

„BackupAgent“ ermöglicht Ihnen die explizitere Angabe der zu sichernden Daten. Da der Entwickler maßgeblich für die Implementierung verantwortlich ist, sind weitere Schritte erforderlich, um den ordnungsgemäßen Datenschutz von Intune sicherzustellen. Da die Arbeit größtenteils von Ihnen als Entwickler zu leisten ist, ist die Intune-Integration etwas komplizierter.

**MAM-Integration**:

1. Lesen Sie die Android-Anleitung für die [Schlüssel/Wert-Sicherung](https://developer.android.com/guide/topics/data/keyvaluebackup.html) und insbesondere zum [Erweitern von BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent) sorgfältig durch, um sicherzustellen, dass Ihre BackupAgent-Implementierung den Android-Richtlinien folgt.

2. Lassen Sie `MAMBackupAgent` von Ihrer Klasse erweitern.

**Sicherung mehrerer Identitäten**:

1. Bevor Sie mit der Datensicherung beginnen, prüfen Sie, ob die **Sicherung der zu sichernden Dateien oder Datenpuffer in Szenarien mit mehreren Identitäten tatsächlich vom IT-Administrator genehmigt ist**. Ihnen wurde die `isBackupAllowed`-Funktion in `MAMFileProtectionManager` und `MAMDataProtectionManager` bereitgestellt, um dies zu ermitteln. Wenn die Sicherung der Datei oder des Datenpuffers nicht zulässig ist, sollten Sie sie nicht in Ihre Sicherung einbeziehen.

2. Wenn während der Sicherung die Identitäten der in Schritt 1 überprüften Dateien gesichert werden sollen, müssen Sie `backupMAMFileIdentity(BackupDataOutput data, File … files)` mit den Dateien aufrufen, aus denen Sie Daten extrahieren möchten. So werden automatisch neue Sicherungsentitäten für Sie erstellt und in `BackupDataOutput` geschrieben. Diese Entitäten werden bei der Wiederherstellung automatisch genutzt.

**Wiederherstellung mehrerer Identitäten**:

Die Anleitung zur Datensicherung gibt einen allgemeinen Algorithmus für die Wiederherstellung der Daten Ihrer Anwendung an und stellt im Abschnitt [Erweitern von BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent) ein Codebeispiel bereit. Sie müssen der in diesem Codebeispiel bereitgestellten allgemeinen Struktur hinsichtlich der folgenden Punkte besonders aufmerksam folgen, damit die Wiederherstellung mehrerer Identitäten erfolgreich ausgeführt wird:

1. Sie müssen eine `while(data.readNextHeader())`*-Schleife verwenden, um die Sicherungsentitäten zu durchlaufen.

2. Sie müssen `data.skipEntityData()`* aufrufen, wenn `data.getKey()`* nicht mit dem Schlüssel übereinstimmt, den Sie in `onBackup` erstellt haben. Wenn Sie diesen Schritt nicht ausführen, können Ihre Wiederherstellungen möglicherweise nicht erfolgreich durchgeführt werden.

3. Vermeiden Sie eine Rückgabe während der Verarbeitung von Sicherungsentitäten im `while(data.readNextHeader())`*-Konstrukt, da die automatisch geschriebenen Entitäten sonst verloren gehen.

* Dabei gibt `data` den Namen der lokalen Variablen für **MAMBackupDataInput** an, die bei der Wiederherstellung an Ihre App übergeben wird.

## <a name="multi-identity-optional"></a>Mehrere Identitäten (optional)

### <a name="overview"></a>Übersicht
Standardmäßig wendet das Intune App SDK Richtlinien auf die gesamte App an. Mehrere Identitäten sind ein optionales Feature von Intune zum Schutz von Apps, das aktiviert werden kann, um die identitätsbezogene Anwendung von Richtlinien zu ermöglichen. Dies erfordert eine deutlich stärkere Beteiligung der App als andere Features zum Schutz von Apps.

> [!NOTE]
> Fehlende korrekte App-Teilnahme kann zu Datenverlusten und anderen Sicherheitsproblemen führen.

Sobald der Benutzer das Gerät oder die App registriert, registriert das SDK die dabei verwendete Identität und betrachtet sie als die primäre, von Intune verwaltete Identität. Andere Benutzer der App werden als nicht verwaltet mit uneingeschränkten Richtlinieneinstellungen behandelt.

> [!NOTE]
> Aktuell wird nur eine von Intune verwaltete Identität pro Gerät unterstützt.

Eine Identität ist als Zeichenfolge definiert. Bei Identitäten werden Groß- und Kleinschreibung nicht unterschieden, und Anforderungen einer Identität beim SDK werden möglicherweise nicht mit der gleichen Groß-/Kleinschreibung zurückgegeben, die ursprünglich beim Festlegen der Identität verwendet wurde.

Die App *muss* das SDK informieren, wenn sie die Änderung der aktiven Identität beabsichtigt. In einigen Fällen benachrichtigt das SDK seinerseits die App, wenn eine Änderung der Identität erforderlich ist. In den meisten Fällen kann MAM jedoch nicht wissen, welche Daten auf der Benutzeroberfläche angezeigt oder in einem Thread zu einem bestimmten Zeitpunkt verwendet werden. So verwendet der Dienst die App, um die korrekte Identität festzulegen, um Datenverlust zu vermeiden. In den folgenden Abschnitten wird auf einige bestimmte Szenarios hingewiesen, die App-Aktionen erfordern.

### <a name="enabling-multi-identity"></a>Aktivieren mehrerer Identitäten

Standardmäßig werden alle Apps als Einzelidentitäts-Apps betrachtet. Sie können eine App entsprechen deklarieren, dass sie mit mehreren Identitäten kompatibel ist, indem Sie die folgenden Metadaten in die Datei „AndroidManifest.xml“ einfügen.

```xml
  <meta-data
    android:name="com.microsoft.intune.mam.MAMMultiIdentity"
    android:value="true" />
```

### <a name="setting-the-identity"></a>Festlegen der Identität

Entwickler können die Identität der App-Benutzer auf den folgenden Ebenen mit absteigender Priorität festlegen:

  1. Threadebene
  2. `Context`-Ebene (allgemein `Activity`)
  3. Prozessebene

Eine auf Threadebene festgelegte Identität hat Vorrang vor einer auf `Context`-Ebene festgelegten Identität, die wiederum Vorrang vor einer auf Prozessebene festgelegten Identität besitzt. Eine in einem `Context` festgelegte Identität wird nur bei Bedarf in dazugehörigen Szenarios verwendet. Datei-E/A-Vorgängen ist z. B. kein `Context` zugeordnet. Apps legen in den meisten Fällen die `Context`-Identität für eine Aktivität (`Activity`) fest. Eine App *darf keine* Daten für eine verwaltete Identität anzeigen, es sei denn, die Identität der `Activity` ist auf die gleiche Identität festgelegt. In der Regel ist die Identität auf Prozessebene nur nützlich, wenn die App nur mit einem einzelnen Benutzer auf allen Threads arbeitet. Viele Apps müssen davon nicht Gebrauch machen.

Wenn Ihre App den `Application`-Kontext verwendet, um Systemdienste abzurufen, stellen Sie sicher, dass die Thread- oder Prozessidentität festgelegt wurde, oder dass Sie die Benutzeroberflächenidentität im `Application`-Kontext Ihrer App festgelegt haben.

Wenn Ihre App einen `Service`-Kontext zum Starten von Absichten verwendet, verwenden Sie Inhaltsresolver, oder setzen Sie andere Systemdienste ein, und legen Sie unbedingt die Identität für den `Service`-Kontext fest.

Damit besondere Fälle beim Aktualisieren der Benutzeroberflächenidentität mit `setUIPolicyIdentity` oder `switchMAMIdentity` verarbeitet werden können, können beide Methoden als `IdentitySwitchOption`-Werte übergeben werden.

* `IGNORE_INTENT`: Wird verwendet, wenn der Wechsel einer Identität angefordert wird, der die Absicht ignorieren sollte, die der aktuellen Aktivität zugeordnet ist.
  Beispiel:

  1. Ihre App empfängt eine Absicht von einer verwalteten Identität, die ein verwaltetes Dokument enthält, und Ihre App zeigt das Dokument an.
  2. Der Benutzer wechselt zu seiner persönlichen Identität, Ihre App fordert also ein Benutzeroberflächenidentitätswechsel an. In der persönlichen Identität zeigt Ihre App das Dokument nicht mehr an, Sie können also `IGNORE_INTENT` verwenden, wenn Sie einen Identitätswechsel anfordern.

  Wenn nicht festgelegt, nimmt das SDK an, dass die zuletzt verwendete Absicht immer noch in der App verwendet wird. Dies führt dazu, dass die Empfangsrichtlinie für die neue Identität die Absicht als eingehende Daten behandelt und die entsprechende Identität verwendet.

>[!NOTE]
> Da `CLIPBOARD_SERVICE` für Benutzeroberflächenvorgänge verwendet wird, verwendet das SDK die Benutzeroberflächenidentität der Vordergrundaktivität für `ClipboardManager`-Vorgänge.

Die folgenden Methoden in `MAMPolicyManager` können verwendet werden, um die Identität festzulegen und die zuvor festgelegten Identitätswerte abzurufen.

```java
public static void setUIPolicyIdentity(final Context context, final String identity, final MAMSetUIIdentityCallback mamSetUIIdentityCallback,
final EnumSet<IdentitySwitchOption> options);

public static String getUIPolicyIdentity(final Context context);

public static MAMIdentitySwitchResult setProcessIdentity(final String identity);

public static String getProcessIdentity();

public static MAMIdentitySwitchResult setCurrentThreadIdentity(final String identity);

public static String getCurrentThreadIdentity();

/**
 * Get the current app policy. This does NOT take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use the overload below.
 */
public static AppPolicy getPolicy();

/**
 * Get the current app policy. This DOES take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use this function.
 */
public static AppPolicy getPolicy(final Context context);


public static AppPolicy getPolicyForIdentity(final String identity);

public static boolean getIsIdentityManaged(final String identity);
```

>[!NOTE]
> Sie können die Identität der App durch Festlegung auf NULL löschen.
>
> Die leere Zeichenfolge kann als Identität verwendet werden, die niemals App-Schutzrichtlinien aufweist.

#### <a name="results"></a>Ergebnisse
Alle Methoden zum Festlegen der Identität geben über `MAMIdentitySwitchResult` Ergebniswerte zurück. Vier Werte können zurückgegeben werden:

| Rückgabewert | Szenario |
|--            |--        |
| `SUCCEEDED`    | Die Identitätsänderung war erfolgreich. |
| `NOT_ALLOWED`  | Die Änderung der Identität ist nicht zulässig. Dies tritt auch bei dem Versuch auf, die Benutzeroberflächenidentität (`Context`) festzulegen, wenn für den aktuellen Thread eine andere Identität festgelegt ist. |
| `CANCELLED`    | Der Benutzer hat die Identitätsänderung abgebrochen, in der Regel mithilfe der Schaltfläche „Zurück“ einer PIN- oder Authentifizierungseingabeaufforderung. |
| `FAILED`       | Bei der Identitätsänderung ist aus unbekannten Gründen ein Fehler aufgetreten.|

Die App muss sicherstellen, dass ein Identitätswechsel erfolgreich ist, bevor Unternehmensdaten angezeigt oder verwendet werden. Aktuell sind Prozess- und Threadidentitätswechsel immer für eine App erfolgreich, für die mehrere Identitäten aktiviert sind. Wir behalten und jedoch vor, Fehlerbedingungen hinzuzufügen. Der Identitätswechsel für die Benutzeroberfläche kann möglicherweise für ungültige Argumente nicht erfolgreich sein, falls sie mit der Threadidentität in Konflikt stehen oder der Benutzer die bedingten Startanforderungen aufheben würde (z.B. indem er auf die schwarze Schaltfläche auf dem PIN-Bildschirm klicken drückt). Das Standardverhalten für einen Identitätswechsel für die Benutzeroberfläche für eine Aktivität ist, die Aktivität abzuschließen (siehe `onSwitchMAMIdentityComplete` unten).

Bei Festlegung einer `Context`-Identität über `setUIPolicyIdentity` wird das Ergebnis asynchron gemeldet. Wenn der `Context` eine `Activity` ist, wird dem SDK erst nach einem bedingten Start, der den Benutzer vielleicht zur Eingabe einer PIN oder seiner Unternehmensanmeldeinformationen auffordert, bekannt, ob die Änderung der Identität erfolgreich war. Die App implementiert möglicherweise `MAMSetUIIdentityCallback`, um dieses Ergebnis zu erzielen, oder übergibt einen NULL-Wert für das Rückrufobjekt. Beachten Sie, dass wenn `setUIPolicyIdentity` aufgerufen wird, während das Ergebnis eines früheren Aufrufs von `setUIPolicyIdentity` *im selben Kontext* noch nicht zurückgegeben wurde, der neue Aufruf den alten ersetzt, und der ursprüngliche Aufruf erhält nie ein Ergebnis.

```java
  public interface MAMSetUIIdentityCallback {
    void notifyIdentityResult(MAMIdentitySwitchResult identitySwitchResult);
  }
```

Sie können die Identität einer Activity auch direkt über eine Methode in `MAMActivity` festlegen, anstatt `MAMPolicyManager.setUIPolicyIdentity` aufzurufen. Verwenden Sie zu diesem Zweck die folgende Methode:

```java
     public final void switchMAMIdentity(final String newIdentity, final EnumSet<IdentitySwitchOption> options);
```

Apps können auch eine Methode in `MAMActivity` außer Kraft setzen, wenn die App über das Ergebnis von Versuchen, die Identität dieser Activity zu ändern, benachrichtigt werden soll.

``` java
    public void onSwitchMAMIdentityComplete(final MAMIdentitySwitchResult result);
```

Wenn Sie `onSwitchMAMIdentityComplete` nicht überschreiben (oder die `super`-Methode aufrufen), führt ein fehlgeschlagener Identitätswechsel für eine Aktivität dazu, dass die Aktivität abgeschlossen wird. Wenn Sie die Methode jedoch überschreiben, müssen Sie darauf achten, dass keine Unternehmensdaten angezeigt werden, nachdem ein Identitätswechsel fehlgeschlagen ist.

>[!NOTE]
> Wechseln der Identität kann das Neuerstellen der Activity erfordern. In diesem Fall wird der `onSwitchMAMIdentityComplete`-Rückruf an die neue Instanz der Activity übermittelt.


### <a name="implicit-identity-changes"></a>Implizite Identitätsänderungen

Neben der Möglichkeit der App, die Identität festzulegen, kann die Identität eines Threads oder Kontexts sich basierend auf dem Dateneingang von einer anderen mit Intune verwalteten App ändern, die eine App-Schutzrichtlinie aufweist.

#### <a name="examples"></a>Beispiele
1. Wenn eine Activity durch einen `Intent` gestartet wird, der von einer anderen MAM-App gesendet wird, wird die Identität der Activity basierend auf der effektiven Identität in der anderen App zu dem Zeitpunkt, zu dem der `Intent` gesendet wurde, festgelegt.

2. Für Dienste wird die Identität des Threads ähnlich für die Dauer eines `onStart`- oder `onBind`-Aufrufs festgelegt. Aufrufe von `Binder`, die von `onBind` zurückgegeben werden, legen ebenfalls vorübergehend die Threadidentität fest.

3. An einen `ContentProvider` gerichtete Aufrufe legen auf ähnliche Weise die Threadidentität für ihre Dauer fest.


  Darüber hinaus könnte Benutzerinteraktion mit einer Activity eine implizite Identitätsänderung hervorrufen.

  **Beispiel:** Wenn ein Benutzer während `Resume` eine Autorisierungsanforderung abbricht, führt dies zu einem impliziten Wechsel zu einer leeren Identität.

  Die App wird auf diese Änderungen aufmerksam gemacht und kann sie verbieten, wenn dies erforderlich ist. `MAMService` und `MAMContentProvider` machen die folgende Methode verfügbar, die Unterklassen überschreiben können:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchResultCallback callback);
  ```

  In der `MAMActivity`-Klasse ist ein zusätzlicher Parameter in der Methode vorhanden:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchReason reason,
          final AppIdentitySwitchResultCallback callback);
  ```

  * `AppIdentitySwitchReason` erfasst die Quelle der impliziten Änderung und akzeptiert die Werte `CREATE`, `RESUME_CANCELLED` und `NEW_INTENT`.  Der Grund `RESUME_CANCELLED` wird verwendet, wenn das Fortsetzen der Activity bewirkt, dass PIN, Authentifizierung oder eine andere Konformitätsbenutzeroberfläche angezeigt wird, und der Benutzer versucht, die Benutzeroberfläche abzubrechen, in der Regel mithilfe der Schaltfläche „Zurück“.


    * `AppIdentitySwitchResultCallback` ist wie folgt:

      ```java
      public interface AppIdentitySwitchResultCallback {
          /**
            * @param result
            *            whether the identity switch can proceed.
            */
          void reportIdentitySwitchResult(AppIdentitySwitchResult result);
        }
        ```

      Dabei ist ```AppIdentitySwitchResult``` entweder `SUCCESS` oder `FAILURE`.

Die Methode `onMAMIdentitySwitchRequired` wird für alle impliziten Identitätsänderungen aufgerufen – mit Ausnahme derer, die über einen von `MAMService.onMAMBind` zurückgegebenen Binder erfolgen. Die Standardimplementierungen von `onMAMIdentitySwitchRequired` rufen sofort Folgendes auf:

* `reportIdentitySwitchResult(FAILURE)`, wenn der Grund `RESUME_CANCELLED` ist.

* `reportIdentitySwitchResult(SUCCESS)` in allen anderen Fällen.

  Es ist nicht anzunehmen, dass die meisten Apps einen Wechsel der Identität auf andere Weise blockieren oder verzögern müssen, aber wenn dies für eine App erforderlich ist, müssen die folgenden Punkte berücksichtigt werden:

  * Wenn ein Identitätswechsel blockiert wird, ist das Ergebnis identisch mit dem Verbot des Dateneingangs durch die `Receive`-Freigabeeinstellungen.

  * Wenn ein Dienst im Hauptthread ausgeführt wird, **muss** `reportIdentitySwitchResult` synchron aufgerufen werden. Andernfalls reagiert der UI-Thread nicht mehr.

  * Für die **`Activity`** -Erstellung wird `onMAMIdentitySwitchRequired` vor `onMAMCreate` aufgerufen. Wenn die App die Benutzeroberfläche anzeigen muss, um zu bestimmen, ob das Wechseln der Identität zugelassen wird, muss die Benutzeroberfläche mit einer *anderen* Activity angezeigt werden.

  * Wenn in einer **`Activity`** ein Wechsel zu der leeren Identität mit einem Grund angefordert wird, der `RESUME_CANCELLED` entspricht, muss die App die fortgesetzte Activity ändern, um Daten mit diesem Identitätswechsel konsistent anzuzeigen.  Wenn dies nicht möglich ist, sollte die App den Wechsel verweigern, und der Benutzer wird erneut zur Einhaltung der Richtlinie für die Fortsetzung der Identität aufgefordert (z.B. durch Anzeige des PIN-Eingabe-Bildschirms der App).

    > [!NOTE]
    > Eine App mit mehreren Identitäten empfängt eingehende Daten immer von verwalteten und nicht verwalteten Apps. Es liegt in der Verantwortung der App, Daten von verwalteten Identitäten in einer verwalteten Weise zu behandeln.

  Wenn eine angeforderte Identität verwaltet wird (verwenden Sie `MAMPolicyManager.getIsIdentityManaged` zur Überprüfung), aber die App das Konto nicht verwenden kann (weil z.B. Konten, wie etwa E-Mail-Konten, zunächst in der App eingerichtet werden müssen), sollte das Wechseln der Identität verweigert werden.

#### <a name="build-plugin--tool-considerations"></a>Überlegungen zum Build-Plug-In/Tool
Wenn Sie nicht explizit von `MAMActivity`, `MAMService` oder `MAMContentProvider` erben (da Sie den Buildtools gestatten, diese Änderung vorzunehmen), aber trotzdem Identitätswechsel verarbeiten müssen, können Sie stattdessen `MAMActivityIdentityRequirementListener` (für eine `Activity`) oder `MAMIdentityRequirementListener` (für einen `Service` oder `ContentProviders`) implementieren.
Auf das Standardverhalten für `MAMActivity.onMAMIdentitySwitchRequired` kann durch Aufruf der statischen Methode `MAMActivity.defaultOnMAMIdentitySwitchRequired(activity, identity,
reason, callback)` zugegriffen werden.

Ebenso, wenn Sie `MAMActivity.onSwitchMAMIdentityComplete` überschreiben müssen, können Sie `MAMActivityIdentitySwitchListener` implementieren, ohne explizit von `MAMActivity` zu erben.

### <a name="preserving-identity-in-async-operations"></a>Beibehalten der Identität in asynchronen Vorgängen
Es ist üblich für Vorgänge im UI-Thread, dass Hintergrundaufgaben an einen anderen Thread verteilt werden. Eine App mit mehreren Identitäten muss sicherstellen, dass diese Hintergrundaufgaben mit der entsprechenden Identität arbeiten, die oft der Identität der Aktivität entspricht, die sie verteilt hat. Das MAM SDK bietet `MAMAsyncTask` und `MAMIdentityExecutors` als praktische Hilfe bei der Wahrung der Identität.
Diese müssen verwendet werden, wenn der asynchrone Vorgang Unternehmensdaten in eine Datei schreiben oder mit anderen Apps kommunizieren könnte.

#### <a name="mamasynctask"></a>MAMAsyncTask

Um `MAMAsyncTask` zu verwenden, arbeiten Sie einfach mit einer Vererbung davon anstatt mit `AsyncTask`, und ersetzen Sie die Überschreibungen von `doInBackground` und `onPreExecute` durch `doInBackgroundMAM` bzw. `onPreExecuteMAM`. Der `MAMAsyncTask`-Konstruktor verwendet einen Aktivitätskontext. Beispiel:

```java
AsyncTask<Object, Object, Object> task = new MAMAsyncTask<Object, Object, Object>(thisActivity) {

    @Override
    protected Object doInBackgroundMAM(final Object[] params) {
        // Do operations.
    }

    @Override
    protected void onPreExecuteMAM() {
        // Do setup.
    };
}
```

### <a name="mamidentityexecutors"></a>MAMIdentityExecutors
`MAMIdentityExecutors` erlaubt Ihnen das Umschließen einer vorhandenen `Executor`- oder `ExecutorService`-Instanz als identitätserhaltenden `Executor`/`ExecutorService` mit den Methoden `wrapExecutor` und `wrapExecutorService`. Beispiel:

```java
Executor wrappedExecutor = MAMIdentityExecutors.wrapExecutor(originalExecutor, activity);
ExecutorService wrappedService = MAMIdentityExecutors.wrapExecutorService(originalExecutorService, activity);
```

### <a name="file-protection"></a>Dateischutz
Jeder Datei wird zum Zeitpunkt der Erstellung basierend auf der Thread- und Prozessidentität eine Identität zugewiesen. Diese Identität wird sowohl für die Dateiverschlüsselung als auch die selektive Zurücksetzung verwendet. Nur Dateien, deren Identität verwaltet wird und eine Richtlinie aufweist, die Verschlüsselung erfordert, werden verschlüsselt. Die standardmäßige selektive Funktionszurücksetzung des SDK setzt nur Dateien zurück, denen die verwaltete Identität zugeordnet ist, für die eine Zurücksetzung angefordert wurde. Die App kann die Identität einer Datei mit de `MAMFileProtectionManager`-Klasse abfragen oder ändern.

```java
public final class MAMFileProtectionManager {

   /**
    * Protect a file or directory. This will synchronously trigger whatever protection is required for the file, and will tag the
    * file for future protection changes. If an identity is set on a directory, it is set recursively on all files and
    * subdirectories. New files or directories will inherit their parent directory's identity. If MAM is operating in offline mode,
    * this method will silently do nothing.
    *
    * @param identity
    *        Identity to set.
    * @param file
    *        File to protect.
    *
    * @throws IOException
    *         If the file cannot be protected.
    */
   public static void protect(final File file, final String identity) throws IOException;

   /**
     * Protect a file obtained from a content provider. This is intended to be used for
     * sdcard (whether internal or removable) files accessed through the Storage Access Framework.
     * It may also be used with descriptors referring to private files owned by this app.
     * It is not intended to be used for files owned by other apps and such usage will fail. If
     * creating a new file via a content provider exposed by another MAM-integrated app, the new
     * file identity will automatically be set correctly if the ContentResolver in use was
     * obtained via a Context with an identity or if the thread identity is set.
     *
     * This will synchronously trigger whatever protection is required for the file, and will tag
     * the file for future protection changes. If an identity is set on a directory, it is set
     * recursively on all files and subdirectories. If MAM is operating in offline mode, this
     * method will silently do nothing.
     *
     * @param identity
     *            Identity to set.
     * @param file
     *            File to protect.
     *
     * @throws IOException
     *             If the file cannot be protected.
     */
    public static void protect(final ParcelFileDescriptor file, final String identity) throws IOException;

   /**
    * Get the protection info on a file. This method should only be used if the file is located in the calling application's
    * private storage or the device's shared storage. If opening a file with a content resolver, use the overload which
    * takes a ParcelFileDescriptor instead.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final File file) throws IOException;

   /**
    * Get the protection info on a file descriptor such as one opened through a content resolver.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final ParcelFileDescriptor file) throws IOException;

}

public interface MAMFileProtectionInfo {
    String getIdentity();
}
 ```

#### <a name="app-responsibility"></a>App-Verantwortung
MAM kann nicht automatisch eine Beziehung zwischen Dateien, die gelesen werden und Daten, die in einer `Activity` dargestellt werden, ableiten. Apps *müssen* die Benutzeroberflächenidentität ordnungsgemäß festlegen, bevor Sie Unternehmensdaten anzeigen. Dies beinhaltet Daten, die aus Dateien lesen. Wenn eine Datei von außerhalb der App stammt (entweder von einem `ContentProvider` oder aus einem öffentlich schreibbaren Speicherort), *muss* die App versuchen, die Dateiidentität zu bestimmen (mithilfe der richtigen `MAMFileProtectionManager.getProtectionInfo`-Überladung für die Datenquelle), bevor sie Informationen anzeigen kann, die aus der Datei gelesen werden. Wenn `getProtectionInfo` eine Identität darstellt, die nicht NULL und nicht leer ist, *muss* die Benutzeroberflächenidentität festgelegt werden, damit sie mit dieser Identität übereinstimmt (mithilfe von `MAMActivity.switchMAMIdentity` oder `MAMPolicyManager.setUIPolicyIdentity`). Wenn der Identitätswechsel fehlschlägt, dürfen Daten aus der Datei *nicht angezeigt werden*.

Eine Beispielausführung sollte in etwa folgendermaßen aussehen:
  * Der Benutzer wählt ein Dokument aus, das in der App geöffnet werden soll.
  * Während des Öffnungsvorgangs bestätigt die App die für die Darstellung des Inhalts zu verwendende Identität noch vor dem Lesen von Daten vom Datenträger:

    ```java
    MAMFileProtectionInfo info = MAMFileProtectionManager.getProtectionInfo(docPath)
    if (info != null)
        MAMPolicyManager.setUIPolicyIdentity(activity, info.getIdentity(), callback, EnumSet.noneOf<IdentitySwitchOption.class>)
    ```

  * Die App wartet, bis ein Ergebnis an den Rückruf gemeldet wird.
  * Wenn das gemeldete Ergebnis einen Fehler darstellt, zeigt die App das Dokument nicht an.
  * Die App öffnet und rendert die Datei.
  
Wenn eine App den `DownloadManager` von Android zum Herunterladen von Dateien verwendet, versucht das MAM SDK, diese Dateien mithilfe der Prozessidentität automatisch zu schützen. Wenn die heruntergeladenen Dateien Unternehmensdaten enthalten, liegt es in der Verantwortung der App, `protect` aufzurufen, wenn die Dateien nach dem Download verschoben oder neu erstellt werden.

#### <a name="single-identity-to-multi-identity-transition"></a>Übergang von einer einzelnen zu mehreren Identitäten
Wenn eine App, die zuvor mit einer Intune-Integration mit einer einzelnen Identität veröffentlicht wurde, später mehrere Identitäten integriert, durchlaufen zuvor installierte Apps einen Übergang, der dem Benutzer jedoch nicht angezeigt wird. Es gibt keine entsprechende Benutzeroberfläche. Es ist nicht *erforderlich*, dass die App etwas Explizites unternimmt, um diesen Übergang zu verarbeiten. Alle Dateien, die vor dem Übergang erstellt wurden, werden weiterhin als verwaltet betrachtet. Sie bleiben also verschlüsselt, wenn die Verschlüsselungsrichtlinie aktiviert ist. Wenn es gewünscht ist, können Sie das Upgrade suchen und `MAMFileProtectionManager.protect` verwenden, um bestimmte Dateien oder Verzeichnisse mit der leeren Identität zu taggen. Dadurch wird deren Verschlüsselung entfernt, wenn sie verschlüsselt waren.

#### <a name="offline-scenarios"></a>Offlineszenarios
Die Markierung der Dateiidentität reagiert empfindlich auf den Offlinemodus. Die folgenden Punkte müssen berücksichtigt werden:

* Wenn das Unternehmensportal nicht installiert ist, kann Dateien keine Identität zugeordnet werden.

* Wenn das Unternehmensportal installiert ist, aber die App nicht über die Intune MAM-Richtlinie verfügt, kann Dateien nicht zuverlässig eine Identität zugeordnet werden.

* Wenn die Zuordnung der Dateiidentität verfügbar ist, werden alle zuvor erstellte Dateien als persönlich/nicht verwaltet (zur Identität der leeren Zeichenfolge gehörend) behandelt, wenn die App nicht zuvor als verwaltete App mit einzelner Identität installiert wurde. In diesem Fall werden sie als zu dem registrierten Benutzer gehörend behandelt.

### <a name="directory-protection"></a>Verzeichnisschutz

Verzeichnisse können mithilfe derselben `protect`-Methode geschützt werden, mit der auch Dateien geschützt werden. Der Verzeichnisschutz wird rekursiv auf alle Dateien und Unterverzeichnisse angewendet, die im Verzeichnis enthalten sind, sowie auf neue Dateien, die in diesem Verzeichnis erstellt werden. Da der Verzeichnisschutz rekursiv angewendet wird, kann der `protect`-Aufruf bei großen Verzeichnissen einige Zeit dauern. Aus diesem Grund möchten Apps, die Schutz auf ein Verzeichnis anwenden, das eine große Anzahl von Dateien enthält, `protect` möglicherweise asynchron in einem Hintergrundthread ausführen.

### <a name="data-protection"></a>Schutz von Daten

Es ist nicht möglich, eine Datei als zu mehreren Identitäten gehörend zu kennzeichnen. Apps, die zu einem anderen Benutzer gehörende Daten in der gleichen Datei speichern müssen, können dies manuell mit den Features von `MAMDataProtectionManager` durchführen. So kann die App Daten verschlüsseln und sie an einen bestimmten Benutzer binden. Die verschlüsselten Daten eignen sich für die Speicherung in einer Datei auf dem Datenträger. Sie können die Daten abfragen, die der Identität zugeordnet sind, und die Daten können später entschlüsselt werden.

Apps, die `MAMDataProtectionManager` verwenden, sollten einen Empfänger für die `MANAGEMENT_REMOVED`-Benachrichtigung implementieren. Nach Abschluss dieser Benachrichtigung können Puffer, die über diese Klasse geschützt wurden, nicht mehr gelesen werden, wenn beim Schutz der Puffer die Dateiverschlüsselung aktiviert wurde. Eine App kann diese Situation durch Aufrufen von `MAMDataProtectionManager.unprotect` für alle Puffer während dieser Benachrichtigung beheben. Es ist ebenfalls sicher, den Schutz während dieser Benachrichtigung aufzurufen, wenn Identitätsinformationen bewahrt werden sollen. Während der Benachrichtigung ist die Deaktivierung der Verschlüsselung gewährleistet.


```java

public final class MAMDataProtectionManager {
    /**
     * Protect a stream. This will return a stream containing the protected
     * input.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect, read sequentially. This function
     *            will change the position of the stream but may not have
     *            read the entire stream by the time it returns. The
     *            returned stream will wrap this one. Calls to read on the
     *            returned stream may cause further reads on the original
     *            input stream. Callers should not expect to read directly
     *            from the input stream after passing it to this method.
     *            Calling close on the returned stream will close this one.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static InputStream protect(final InputStream input, final String identity);

    /**
     * Protect a byte array. This will return protected bytes.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static byte[] protect(final byte[] input, final String identity) throws IOException;

    /**
     * Unprotect a stream. This will return a stream containing the
     * unprotected input.
     *
     * @param input
     *            Input data to protect, read sequentially.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static InputStream unprotect(final InputStream input) throws IOException;

    /**
     * Unprotect a byte array. This will return unprotected bytes.
     *
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static byte[] unprotect(final byte[] input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input stream to get information on. Either this input
     *            stream must have been returned by a previous call to
     *            protect OR input.markSupported() must return true.
     *            Otherwise it will be impossible to get protection info
     *            without advancing the stream position. The stream must be
     *            positioned at the beginning of the protected data.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final InputStream input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input bytes to get information on. These must be bytes
     *            returned by a previous call to protect() or a copy of
     *            such bytes.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final byte[] input) throws IOException;
}
```


### <a name="content-providers"></a>Inhaltsanbieter

Wenn die App andere Unternehmensdaten als `ParcelFileDescriptor` über einen `ContentProvider` bereitstellt, muss die App die Methode `isProvideContentAllowed(String)` in `MAMContentProvider` aufrufen und den Benutzerprinzipalnamen (UPN) der Besitzeridentität für den Inhalt übergeben. Wenn diese Funktion „false“ zurückgibt, darf der Inhalt *nicht* an den Aufrufer zurückgegeben werden. Durch einen Inhaltsanbieter zurückgegebene Dateideskriptoren werden automatisch auf Grundlage der Dateiidentität behandelt.

Wenn `MAMContentProvider` nicht explizit geerbt wird und Sie stattdessen den Buildtools gestatten, diese Änderung vorzunehmen, können Sie eine statische Version derselben Methode aufrufen: `MAMContentProvider.isProvideContentAllowed(provider,
contentIdentity)`.

### <a name="selective-wipe"></a>selektives Zurücksetzen

Wenn eine App mit mehreren Identitäten für die `WIPE_USER_DATA`-Benachrichtigung registriert wird, liegt es in der Verantwortung der App, alle Daten des Benutzers zu löschen, der zurückgesetzt wird. Dazu gehören alle Dateien, denen der Benutzer als Identität zugeordnet wurde. Wenn die App Benutzerdaten aus einer Datei entfernt, aber andere Daten in der Datei belassen soll, *muss* die Identität der Datei (über `MAMFileProtectionManager.protect` auf einen persönlichen Benutzer oder die leere Identität) geändert werden. Wenn Verschlüsselungsrichtlinien verwendet werden, werden übrige Dateien des zurückgesetzten Benutzers nicht entschlüsselt und nach dem Zurücksetzen kann nicht mehr auf sie zugegriffen werden.

Eine App, die für `WIPE_USER_DATA` registriert wird, verfügt über keine Vorteile des Standardverhaltens des SDK für die selektive Zurücksetzung. Für Apps, die mehrere Identitäten haben können, kann dieser Verlust erheblicher sein, da die selektive Zurücksetzung nach MAM-Standard nur Dateien zurücksetzt, deren Identität das Ziel einer Zurücksetzung ist. Wenn eine App, die mehrere Identitäten haben kann, eine selektive Zurücksetzung nach MAM-Standard _**und**_ die Ausführung eigener Aktionen bei der Zurücksetzung wünscht, sollte sie für `WIPE_USER_AUXILIARY_DATA`-Benachrichtigungen registriert werden. Diese Benachrichtigung wird sofort vom SDK gesendet, bevor es die selektive Zurücksetzung nach MAM-Standard durchführt. Eine App darf niemals gleichzeitig für `WIPE_USER_DATA` und für `WIPE_USER_AUXILIARY_DATA` registriert sein.

Das standardmäßige selektive Zurücksetzen schließt die App ordnungsgemäß, schließt Aktivitäten ab und beendet den App-Prozess. Wenn Ihre App das standardmäßige selektive Zurücksetzen überschreibt, sollten Sie die App manuell schließen, um zu verhindern, dass der Benutzer nach einem Zurücksetzen auf In-Memory-Daten zugreifen kann.


## <a name="enabling-mam-targeted-configuration-for-your-android-applications-optional"></a>Aktivieren der MAM-Zielkonfiguration für Ihre Android-Anwendungen (optional)
Anwendungsspezifische Schlüssel-Wert-Paare können in der Intune-Konsole für [MAM-WE](../apps/app-configuration-policies-managed-app.md) und [Android Enterprise](../apps/app-configuration-policies-use-android.md) konfiguriert werden.
Diese Schlüssel-Wert-Paare werden von Intune gar nicht übersetzt, sondern an die App übergeben. Anwendungen, die eine solche Konfiguration erhalten wollen, verwenden dazu die `MAMAppConfigManager`- und `MAMAppConfig`-Klasse. Wenn mehrere Richtlinie für dieselbe App vorgesehen sind, gibt es womöglich mehrere konfliktverursachende Werte für denselben Schlüssel.

> [!NOTE] 
> Die Konfigurationseinrichtung für die Übermittlung über die MAM-WE kann in `offline` nicht übermittelt werden (wenn das Unternehmensportal nicht installiert ist).  Nur AppRestrictions von Android Enterprise werden über eine `MAMUserNotification`-Benachrichtigung in diesem Fall für eine leere Identität zugestellt.

### <a name="get-the-app-config-for-a-user"></a>Abrufen der App-Konfiguration für einen Benutzer
Die App-Konfiguration kann folgendermaßen abgerufen werden:
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
```

Wenn es keinen für die mobile Anwendungsverwaltung registrierten Benutzer gibt, Ihre App aber dennoch weiterhin die Android Enterprise-Konfiguration abrufen möchte (die nicht auf einen bestimmten Benutzer abzielt), können Sie einen NULL-Wert oder eine leere Zeichenfolge übergeben.

### <a name="conflicts"></a>Konflikte
Ein Wert, der in der MAM-App-Konfiguration festgelegt ist, überschreibt einen Wert mit demselben Wert in der Android Enterprise-Konfiguration. 

Wenn ein Administrator miteinander in Konflikt stehende Werte für denselben Schlüssel konfiguriert (z. B. indem verschiedene App-Konfigurationen mit demselben Schlüssel für mehrere Gruppen, die denselben Benutzer enthalten, als Zielversion verwendet werden), gibt es für Intune keine Möglichkeit, diesen Konflikt automatisch aufzulösen, und alle Werte werden für Ihre App verfügbar gemacht. 

Ihre App kann alle Werte für einen gegebenen Schlüssel von einem `MAMAppConfig`-Objekt anfordern:
```java
List<Boolean> getAllBooleansForKey(String key)
List<Long> getAllIntegersForKey(final String key)
List<Double> getAllDoublesForKey(final String key)
List<String> getAllStringsForKey(final String key)
```

oder anfordern, dass ein Wert ausgewählt wird:
```java
Boolean getBooleanForKey(String key, BooleanQueryType queryType)
Long getIntegerForKey(String key, NumberQueryType queryType)
Double getDoubleForKey(String key, NumberQueryType queryType)
String getStringForKey(String key, StringQueryType queryType)

enum BooleanQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns true if any of the values are true.
     */
    Or,
    /**
     * In case of conflict, returns false if any of the values are false.
     */
    And
}

enum NumberQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the minimum Integer.
     */
    Min,
    /**
     * In case of conflict, returns the maximum Integer.
     */
    Max
}

enum StringQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the first result ordered alphabetically.
     */
    Min,

    /**
     * In case of conflict, returns the last result ordered alphabetically.
     */
    Max
}
```

Ihre App kann auch die Rohdaten als Liste mit Schlüssel-Wert-Paaren anfordern.

```java
List<Map<String, String>> getFullData()
```


### <a name="full-example"></a>Vollständiges Beispiel
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
String fooValue = null;
if (appConfig.hasConflict("foo")) {
    List<String> values = appConfig.getAllStringsForKey("foo");
    fooValue = chooseBestValue(values);
} else {
    valueToUse = appConfig.getStringForKey("foo", MAMAppConfig.StringQueryType.Any);
}
Long barValue = appConfig.getIntegerForKey("bar", MAMAppConfig.NumberQueryType.Min);
```

### <a name="notification"></a>Benachrichtigung
Die App-Konfiguration fügt einen neuen Benachrichtigungstyp hinzu:
* **REFRESH_APP_CONFIG:** Diese Benachrichtigung wird in einer `MAMUserNotification`-Klasse gesendet und informiert die App, dass neue App-Konfigurationsdaten verfügbar sind.

### <a name="further-reading"></a>Weitere Informationen
Weitere Informationen zum Erstellen einer MAM-Zielkonfigurationsrichtlinie für Apps in Android finden Sie im Abschnitt zu MAM-Zielkonfiguration für Apps unter [How to use Microsoft Intune app configuration policies for Android (Verwenden von Microsoft Intune-App-Konfigurationsrichtlinien für Android for Work)](../apps/app-configuration-policies-managed-app.md).

Die App-Konfiguration kann auch mithilfe der Graph-API konfiguriert werden. Weitere Informationen finden Sie unter [Ressourcentyp „targetedManagedAppConfiguration“](https://docs.microsoft.com/graph/api/resources/intune-mam-targetedmanagedappconfiguration).

## <a name="custom-themes-optional"></a>Benutzerdefinierte Designs (optional)
Ein benutzerdefiniertes Design kann für das MAM-SDK bereitgestellt werden und dann auf alle MAM-Bildschirme und -Dialogfelder angewendet werden. Wenn kein Design bereitgestellt wird, wird ein MAM-Standarddesign verwendet.

### <a name="how-to-provide-a-theme"></a>Bereitstellen eines Designs
Zum Bereitstellen eines Designs müssen Sie in der `Application.onCreate`-Methode die folgende Codezeile hinzufügen:

```java
MAMThemeManager.setAppTheme(R.style.AppTheme);
```

Im obigen Beispiel müssen Sie `R.style.AppTheme` mit dem Stildesign ersetzen, das das SDK anwenden soll.

## <a name="style-customization-deprecated"></a>Stilanpassung (veraltet)

Diese Funktion ist jetzt veraltet und benutzerdefinierte Designs (siehe oben) sind die bevorzugte Möglichkeit, Ansichten anzupassen.

Vom MAM SDK generierte Ansichten können visuell angepasst werden, um der App noch genauer zu entsprechen. Sie können primäre, sekundäre und Hintergrundfarben sowie die Größe des App-Logos anpassen. Diese Anpassung von Formatvorlagen und Stil ist optional und es werden Standardwerte verwendet, wenn kein benutzerdefinierter Stil konfiguriert ist.


### <a name="how-to-customize"></a>Vorgehensweise beim Anpassen
Damit Formatvorlagen- und Stiländerungen auf Intune MAM-Ansichten angewendet werden, müssen Sie zuerst eine XML-Datei für die Außerkraftsetzung von Formatvorlagen und Stil erstellen. Diese Datei sollte im Verzeichnis „/res/xml“ Ihrer App gespeichert werden, und Sie können ihr einen beliebigen Namen zuweisen. Das folgende Beispiel veranschaulicht das Format, das diese Datei einhalten muss.

```xml
<?xml version="1.0" encoding="utf-8"?>
<styleOverrides>
    <item
        name="foreground_color"
        resource="@color/red"/>
    <item
        name="accent_color"
        resource="@color/blue"/>
    <item
        name="background_color"
        resource="@color/green"/>
    <item
        name="logo_image"
        resource="@drawable/app_logo"/>
</styleOverrides>
```

Sie müssen bereits in Ihrer App vorhandene Ressourcen wiederverwenden. Sie müssen z. B. die Farbe „Grün“ in der Datei „colors.xml“ definieren und hier darauf verweisen. Sie können nicht den hexadezimalen Farbcode „#0000ff“ verwenden. Die maximale Größe für das App-Logo beträgt 110 dip (dp). Sie können ein kleineres Logobild verwenden, aber die maximale Größe sorgt für optimale Ansichtsergebnisse. Wenn Sie den Grenzwert von 110 dip überschreiten, wird das Bild herunterskaliert und möglicherweise unscharf angezeigt.

Nachfolgend finden Sie die vollständige Liste der zulässigen Stilattribute, die von ihnen gesteuerten Elemente der Benutzeroberfläche, ihre XML-Elementattributnamen und den Typ der Ressource, der für die einzelnen Attribute erwartet wird.

|Stilattribut | Betroffene Elemente der Benutzeroberfläche | Attributelementname | Erwarteter Ressourcentyp |
| -- | -- | -- | -- |
| Hintergrundfarbe | Hintergrundfarbe für PIN-Bildschirm <Br>Füllfarbe für PIN-Feld | background_color | Farbe |
| Vordergrundfarbe | Vordergrundtextfarbe <br> Rahmen des PIN-Felds im Standardzustand <br> Zeichen (einschließlich verborgener Zeichen) im PIN-Feld, wenn Benutzer eine PIN eingibt| foreground_color | Farbe|
| Akzentfarbe | PIN-Feldrahmen (markiert) <br> Links |accent_color | Farbe |
| App-Logo | Großes Symbol, das auf dem PIN-Bildschirm der Intune-App angezeigt wird | logo_image | Zeichenbar |

## <a name="default-enrollment-optional"></a>Standardregistrierung (Optional)

Im Folgenden wird erläutert, wie Sie eine Benutzeraufforderung beim Start der App für die automatische APP-WE-Dienstregistrierung erforderlich machen (in diesem Abschnitt **Standardregistrierung** genannt), und wie Sie App-Schutzrichtlinien von Intune erforderlich machen, damit nur über Intune geschützte Benutzer Ihre in die SDK integrierte Android LOB-App verwenden dürfen. Außerdem wird dargestellt, wie SSO für Ihre in das SDK integrierte Android LOB-App aktiviert wird. Dies wird für Store-Apps, die von Personen verwendet werden können, die kein Intune verwenden, **nicht** unterstützt.

> [!NOTE] 
> Die Vorteile einer **Standardregistrierung** umfassen u.a. eine vereinfachte Methode zum Abrufen von Richtlinien über den APP-WE-Dienst für eine App auf dem Gerät.

> [!NOTE] 
> **Standardregistrierung** ist Sovereign Cloud-fähig.

Befolgen Sie die folgenden Schritte,um die Standardregistrierung zu aktivieren:

1. Wenn Ihre App ADAL integriert oder Sie SSO aktivieren müssen, [konfigurieren Sie ADAL](#configure-azure-active-directory-authentication-library-adal) entsprechend der [zweiten hier aufgeführten häufig verwendeten ADAL-Konfiguration](#common-adal-configurations). Andernfalls können Sie diesen Schritt überspringen.
   
2. Aktivieren Sie die Standardregistrierung, indem Sie den folgenden Wert unter dem `<application>`-Tag zum Manifest hinzufügen:

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.DefaultMAMServiceEnrollment" android:value="true" />
   ```

   > [!NOTE] 
   > Dabei muss es sich um die einzige MAM-WE-Integration in der App handeln. Wenn es zu weiteren Versuchen kommt, MAMEnrollmentManager-APIs aufzurufen, treten Konflikte auf.

3. Aktivieren Sie die erforderliche MAM-Richtlinie, indem Sie den folgenden Wert unter dem `<application>`-Tag zum Manifest hinzufügen:

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.MAMPolicyRequired" android:value="true" />
   ```

   > [!NOTE] 
   > Dann ist der Benutzer gezwungen, das Unternehmensportal auf dem Gerät herunterzuladen und den Vorgang der Standardregistrierung vor der Nutzung abzuschließen.


## <a name="limitations"></a>Einschränkungen

### <a name="policy-enforcement-limitations"></a>Einschränkungen der Richtlinienerzwingung

* **Verwenden von Inhaltsresolvern:** Durch die Intune-Richtlinie zum Übertragen oder Empfangen kann die Verwendung eines Inhaltsresolvers für den Zugriff auf den Inhaltsanbieter in einer anderen App ganz oder teilweise blockiert werden. Dadurch geben `ContentResolver`-Methoden NULL oder einen Fehlerwert zurück (z. B. gibt `openOutputStream` bei Blockierung `FileNotFoundException` zurück). Die App kann feststellen, ob ein Fehler beim Schreiben von Daten durch einen Inhaltsresolver durch die Richtlinie verursacht wurde (oder würde), indem folgender Aufruf ausgeführt wird:

    ```java
    MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(contentURI);
    ```

    oder wenn es keine zugehörige Aktivität gibt:

    ```java
    MAMPolicyManager.getPolicy().getIsSaveToLocationAllowed(contentURI);
    ```

    Im zweiten Fall müssen Apps mit mehreren Identitäten unbedingt die Threadidentität ordnungsgemäß festlegen (oder eine explizite Identität an den `getPolicy`-Aufruf übergeben).

### <a name="exported-services"></a>Exportierte Dienste
Die im Intune App SDK enthaltene Datei „AndroidManifest.xml“ enthält **MAMNotificationReceiverService**. Dies muss ein exportierter Dienst sein, damit das Unternehmensportal Benachrichtigungen an eine verwaltete App senden kann. Der Dienst prüft den Aufrufer, um sicherzustellen, dass nur das Unternehmensportal Benachrichtigungen senden kann.

### <a name="reflection-limitations"></a>Einschränkungen bei der Reflexion
Einige der MAM-Basisklassen (z. B. `MAMActivity`, `MAMDocumentsProvider`) enthalten Methoden (basierend auf den ursprünglichen Android-Basisklassen), die Parameter- oder Rückgabetypen verwenden, die nur oberhalb bestimmter API-Ebenen vorhanden sind. Aus diesem Grund ist es möglicherweise nicht immer möglich, alle Methoden von App-Komponenten mit Hilfe von Reflexion aufzuzählen. Diese Einschränkung ist nicht auf MAM beschränkt. Sie gilt auch, wenn die App selbst diese Methoden aus den Android-Basisklassen implementiert.

### <a name="robolectric"></a>Robolectric
Das Testen des Verhaltens von MAM SDK unter Robolectric wird nicht unterstützt. Es sind Probleme bei der Ausführung des MAM SDK unter Robolectric bekannt, die aufgrund von Verhaltensweisen auftreten, die echte Geräte oder Emulatoren nicht genau imitieren.

Wenn Sie Ihre Anwendung unter Robolectric testen müssen, wird empfohlen, die Anwendungsklassenlogik in eine Hilfsmethode zu verschieben und Ihre Anwendung für Komponententests mit einer Anwendungsklasse zu erstellen, die nicht von MAMApplication erbt.

## <a name="expectations-of-the-sdk-consumer"></a>Erwartungen des SDK-Consumers

Das Intune SDK verwaltet des von der Android-API bereitgestellten Vertrag; jedoch ist es möglich, dass aufgrund der Richtlinienerzwingung häufiger Fehlerbedingungen ausgelöst werden. Durch diese bewährten Methoden für Android wird die Wahrscheinlichkeit, dass Fehler auftreten, gemindert:

* Es besteht die höhere Wahrscheinlichkeit, dass Android SDK-Funktionen, die möglicherweise NULL zurückgeben, jetzt NULL sind.  Um Probleme zu minimieren, stellen Sie sicher, dass NULL-Überprüfungen an den richtigen Stellen stattfinden.

* Funktionen, die überprüft werden können, müssen über die zugehörigen MAM-Ersatz-APIs überprüft werden.

* Alle abgeleiteten Funktionen müssen an ihre übergeordneten Klassenversionen einen durchgehenden Aufruf ausführen.

* Vermeiden Sie eine nicht eindeutige Verwendung von APIs. So führt beispielsweise die Verwendung von `Activity.startActivityForResult` ohne Überprüfung von „requestCode“ zu unerwartetem Verhalten.

### <a name="services"></a>Dienste
Die Richtlinienerzwingung kann sich auf Dienstinteraktionen auswirken.
Bei Methoden wie `Context.bindService`, die eine Verbindung mit einem gebundenen Dienst aufbauen, kann aufgrund der zugrunde liegenden Richtlinienerzwingung in `Service.onBind` ein Fehler auftreten, was zu `ServiceConnection.onNullBinding` oder `ServiceConnection.onServiceDisconnected` führen kann.
Bei der Interaktion mit einem gebundenen Dienst kann aufgrund der Richtlinienerzwingung in `Binder.onTransact` eine `SecurityException` ausgelöst werden.

## <a name="telemetry"></a>Telemetrie

Das Intune App SDK für Android kontrolliert nicht die Datensammlung über Ihre App. Standardmäßig protokolliert die Unternehmensportal-Anwendung systemgenerierte Daten. Diese Daten werden an Microsoft Intune gesendet. Gemäß der Microsoft-Richtlinie sammeln wir keine personenbezogenen Daten.

> [!NOTE]
> Wenn Benutzer sich dazu entschließen, diese Daten nicht zu senden, müssen sie die Telemetrie unter „Einstellungen“ in der Unternehmensportal-App deaktivieren. Weitere Informationen finden Sie unter [Deaktivieren der Erfassung von Nutzungsdaten durch Microsoft](../user-help/turn-off-microsoft-usage-data-collection-android.md). 

## <a name="recommended-android-best-practices"></a>Empfohlene und bewährte Methoden für Android

* Alle Bibliotheksprojekte sollten dasselbe `android:package` gemeinsam verwenden, wenn dies möglich ist. Dabei kommt es während der Laufzeit nicht sporadisch zu Fehlern, da es sich um ein reines Problem zur Buildzeit handelt. Neuere Versionen des Intune App SDKs werden einen Teil der Redundanz beseitigen.

* Verwenden Sie die neuesten Android SDK-Buildtools.

* Entfernen Sie alle nicht benötigten und nicht verwendeten Bibliotheken (z.B. „android.support.v4“)

## <a name="testing"></a>Test
Weitere Informationen finden Sie unter [Leitfaden für Android-Tests mit dem Microsoft Intune App SDK](app-sdk-android-testing-guide.md).
