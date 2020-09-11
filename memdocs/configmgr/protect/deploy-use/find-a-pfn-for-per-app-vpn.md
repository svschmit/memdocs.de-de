---
title: Suchen eines Paketfamiliennamens (PFN) für Pro-App-VPN
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die zwei Methoden, einen Paketfamiliennamen zu suchen, sodass Sie ein Pro-App-VPN konfigurieren können.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 357b13b06bcfaabf6c22f68a3c21e498630cebf2
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608212"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Suchen eines Paketfamiliennamens (PFN) für Pro-App-VPN

*Gilt für: Configuration Manager (Current Branch)*


Es gibt zwei Methoden, einen PFN zu suchen, sodass Sie ein Pro-App-VPN konfigurieren können.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Suchen eines PFN für eine App, die auf einem Windows-10-Computer installiert ist

Wenn die App, mit der Sie arbeiten, bereits auf einem Windows-10-Computer installiert ist, können Sie das PowerShell-Cmdlet [Get-AppxPackage](/powershell/module/appx/get-appxpackage) zum Abrufen des PFN verwenden.

Die Syntax für Get-AppxPackage lautet:

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> Möglicherweise müssen Sie PowerShell als Administrator ausführen, um den PFN abrufen zu können

Verwenden Sie beispielsweise `Get-AppxPackage` zum Abrufen von Informationen zu allen universellen Apps, die auf dem Computer installiert sind.

Verwenden Sie `Get-AppxPackage *<app_name>` zum Abrufen von Informationen über eine App, deren Namen Sie kennen oder teilweise kennen. Beachten Sie die Verwendung des Platzhalterzeichens, das vor allem dann nützlich ist, wenn Sie nicht den vollständigen Namen der App kennen. Verwenden Sie beispielsweise beim Abrufen von Informationen für OneNote `Get-AppxPackage *OneNote`.


Hier sind die abgerufenen Informationen für OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Suchen einer PFN, wenn die App nicht auf einem Computer installiert ist

1. Wechseln Sie zu https://www.microsoft.com/store/apps.
2. Geben Sie den Namen der App in der Suchleiste ein. Suchen Sie in unserem Beispiel nach OneNote.
3. Klicken Sie auf den Link zur App. Beachten Sie, dass die URL, auf die Sie zugreifen, eine Reihe von Buchstaben am Ende hat. In unserem Beispiel sieht die URL folgendermaßen aus: `https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. Fügen Sie in einer anderen Registerkarte die folgende URL ein: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`. Ersetzen Sie dabei `<app id>` durch die App-ID, die Sie von https://www.microsoft.com/store/apps erhalten haben (die Reihe von Buchstaben am Ende der URL aus Schritt 3). In unserem Beispiel, das Beispiel OneNote, fügen Sie ein: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

Die gewünschten Informationen werden in Microsoft Edge angezeigt. Klicken Sie in Internet Explorer auf **Öffnen**, um die Informationen zu sehen. Der PFN-Wert erscheint in der ersten Zeile. Hier ist das Ergebnis in unserem Beispiel:

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```