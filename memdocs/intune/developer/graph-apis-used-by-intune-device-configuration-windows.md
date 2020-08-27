---
title: Graph-APIs zum Konfigurieren von Geräten in Microsoft InTune-Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Hier finden Sie eine Liste aller Graph-API Entitäten mit dem entsprechenden Windows CSP-und Offset-URI auf Windows 10-Geräten und neueren Geräten, die beim Konfigurieren von Geräten in Microsoft InTune verwendet werden. Sehen Sie sich die passende API und den CSP für freigegebene PCs, Endpoint Protection, Microsoft Defender Advanced Threat Protection, Identity Protection, Windows 10 Teams, Kiosk und Windows Update für Unternehmen an.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb30db6043a1b2f02db8baa93f324fa38449769c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915652"
---
# <a name="graph-apis-and-matching-windows-10-csps-used-in-intune"></a>In Intune verwendete Graph-APIs und übereinstimmende Windows 10-Kryptografiedienstanbieter

Microsoft InTune verwendet die [Graph-API Entitäten](/graph/api/resources/intune-graph-overview) (öffnet eine andere Dokumentations Website) zum Konfigurieren von Geräten (**InTune**  >  -**Gerätekonfiguration**), auf denen Windows 10 und höher ausgeführt wird. Der Graph-API verwendet Konfigurations Dienstanbieter (CSPs), um Konfigurationseinstellungen auf Geräten zu lesen, festzulegen, zu ändern und/oder zu löschen.

Diese Liste gilt für:

- Windows 10 und höher

In diesem Artikel werden die Graph-Entitäten und ihre entsprechenden Windows 10-CSPs und Offset-URIs aufgelistet.

Diese Informationen sind für eine Vielzahl von Szenarios nützlich. Informationen zum Beispiel finden Sie unter Was wird von InTune verwendet? siehe Einstellungen zum Einschließen von benutzerdefinierten Oma-URI-Konfigurationen usw. 

## <a name="windows-10-csps"></a>Windows 10-CSPs

Weitere Informationen zu Windows 10-Konfigurations Dienstanbietern finden Sie in der [Referenz zum Konfigurations Dienstanbieter](/windows/client-management/mdm/configuration-service-provider-reference) (öffnet eine andere Dokumentations Website).

## <a name="graph-api-properties-to-csp-mapping"></a>Graph-API der Zuordnung von Eigenschaften zu CSP

In der folgenden Liste werden die meisten Graph-API Entitäten angezeigt, die von Microsoft InTune für die Windows 10-Gerätekonfiguration verwendet werden. Außerdem werden der entsprechende Windows 10 CSP und der Offset-URI angezeigt.

Um die Windows 10-Versionen anzuzeigen, die die folgenden APIs betreffen, verwenden Sie die Windows 10- [Konfigurations Dienstanbieter-Referenz](/windows/client-management/mdm/configuration-service-provider-reference) (öffnet eine andere Dokumentations Website).

### <a name="editionupgradeconfigurationlicense"></a>Editionupgradeconfiguration. License 
**CSP**:./Device/Vendor/MSFT/WindowsLicensing  
**Offset-URI**:/UpgradeEditionWithLicense

### <a name="editionupgradeconfigurationlicensetype"></a>Editionupgradeconfiguration. licenmentype 
**CSP**:./Device/Vendor/MSFT/WindowsLicensing  
**Offset-URI**:/LicenseKeyType

### <a name="editionupgradeconfigurationproductkey"></a>Editionupgradeconfiguration. ProductKey 
**CSP**:./Device/Vendor/MSFT/WindowsLicensing  
**Offset-URI**:/UpgradeEditionWithProductKey

### <a name="editionupgradeconfigurationwindowssmode"></a>Editionupgradeconfiguration. windowssmode 
**CSP**:./Device/Vendor/MSFT/WindowsLicensing  
**Offset-URI**:/SMode/SwitchingPolicy

### <a name="sharedpcconfigurationaccountmanagerpolicy"></a>Sharedpcconfiguration. accountmanagerpolicy 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/DeletionPolicy,/DiskLevelCaching,/InactiveThreshold,/DiskLevelDeletion

### <a name="sharedpcconfigurationaccountmanagerpolicy-windows-holographic-for-business-edition-targeted-devices"></a>Sharedpcconfiguration. accountmanagerpolicy (Windows Holographic for Business Edition-Zielgeräte) 
**CSP**:./Vendor/MSFT/AccountManagement  
**Offset-URI**:/DeletionPolicy,/StorageCapacityStartDeletion,/StorageCapacityStopDeletion,/ProfileInactivityThreshold

### <a name="sharedpcconfigurationallowedaccounts"></a>Sharedpcconfiguration. Zuweisung 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/AccountModel

### <a name="sharedpcconfigurationallowlocalstorage"></a>Sharedpcconfiguration. allowlocalstorage 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/RestrictLocalStorage

### <a name="sharedpcconfigurationdisableaccountmanager"></a>Sharedpcconfiguration. disableaccountmanager 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/EnableAccountManager

### <a name="sharedpcconfigurationdisableedupolicies"></a>Sharedpcconfiguration. disableedupolicies 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/SetEduPolicies

### <a name="sharedpcconfigurationdisablepowerpolicies"></a>Sharedpcconfiguration. disablepowerpolicies 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/SetPowerPolicies

### <a name="sharedpcconfigurationdisablesigninonresume"></a>Sharedpcconfiguration. disablesigninonresume 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/SignInOnResume

### <a name="sharedpcconfigurationenabled"></a>Sharedpcconfiguration. aktiviert 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/EnableSharedPCMode

### <a name="sharedpcconfigurationidletimebeforesleepinseconds"></a>Sharedpcconfiguration. idletimebeforesleepinseconds 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/InactiveThreshold

### <a name="sharedpcconfigurationkioskappdisplayname"></a>Sharedpcconfiguration. kioskappdisplayname 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/KioskModeUserTileDisplayText

### <a name="sharedpcconfigurationkioskappusermodelid"></a>Sharedpcconfiguration. kioskappusermodelid 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/KioskModeAUMID

### <a name="sharedpcconfigurationlocalstorage"></a>Sharedpcconfiguration. localStorage 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/RestrictLocalStorage

### <a name="sharedpcconfigurationmaintenancestarttime"></a>Sharedpcconfiguration. maintenvorfahren Zeichen Zeit 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/MaintenanceStartTime

### <a name="sharedpcconfigurationsetaccountmanager"></a>Sharedpcconfiguration. setaccountmanager
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/EnableAccountManager

### <a name="sharedpcconfigurationsetedupolicies"></a>Sharedpcconfiguration. "ctedupolicies" 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/SetEduPolicies

### <a name="sharedpcconfigurationsetpowerpolicies"></a>Sharedpcconfiguration. setpowerpolicies 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/SetPowerPolicies

### <a name="sharedpcconfigurationsigninonresume"></a>Sharedpcconfiguration. signinonresume 
**CSP**:./Vendor/MSFT/SharedPC  
**Offset-URI**:/SignInOnResume

### <a name="windows10endpointconfigurationsmartscreenblockoverrideforfiles"></a>Windows10endpointconfiguration. smartscreenblockoverrideforfiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/SmartScreen/PreventOverrideForFilesInShell

### <a name="windows10endpointprotectionconfigurationapplicationguardallowfilesaveonhost"></a>Windows10EndpointProtectionConfiguration. applicationguardallowfilesaveonhost 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/SaveFilesToHost

### <a name="windows10endpointprotectionconfigurationapplicationguardallowpersistence"></a>Windows10EndpointProtectionConfiguration. applicationguardallowpersistenz 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/AllowPersistence

### <a name="windows10endpointprotectionconfigurationapplicationguardallowprinttolocalprinters"></a>Windows10EndpointProtectionConfiguration. applicationguardallowprinttolocalprinters 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/PrintingSettings

### <a name="windows10endpointprotectionconfigurationapplicationguardallowprinttonetworkprinters"></a>Windows10EndpointProtectionConfiguration. applicationguardallowprinttonetworkprinter 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/PrintingSettings

### <a name="windows10endpointprotectionconfigurationapplicationguardallowprinttopdf"></a>Windows10EndpointProtectionConfiguration. applicationguardallowprinttopdf 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/PrintingSettings

### <a name="windows10endpointprotectionconfigurationapplicationguardallowprinttoxps"></a>Windows10EndpointProtectionConfiguration. applicationguardallowprinttoxps 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/PrintingSettings

### <a name="windows10endpointprotectionconfigurationapplicationguardallowvirtualgpu"></a>Windows10EndpointProtectionConfiguration. applicationguardallowvirtualgpu 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/AllowVirtualGPU

### <a name="windows10endpointprotectionconfigurationapplicationguardblockclipboardsharing"></a>Windows10EndpointProtectionConfiguration. applicationguardblockclipboardsharing 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/ClipboardSettings

### <a name="windows10endpointprotectionconfigurationapplicationguardblockfiletransfer"></a>Windows10EndpointProtectionConfiguration. applicationguardblockfiletransfer 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/ClipboardFileType

### <a name="windows10endpointprotectionconfigurationapplicationguardblocknonenterprisecontent"></a>Windows10EndpointProtectionConfiguration. applicationguardblocknonenterpritscontent 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/BlockNonEnterpriseContent

### <a name="windows10endpointprotectionconfigurationapplicationguardenabled"></a>Windows10EndpointProtectionConfiguration. applicationguardenabled 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Settings/AllowWindowsDefenderApplicationGuard

### <a name="windows10endpointprotectionconfigurationapplicationguardforceauditing"></a>Windows10EndpointProtectionConfiguration. applicationguardforceauditing 
**CSP**:./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset-URI**:/Audit/AuditApplicationGuard

### <a name="windows10endpointprotectionconfigurationbitlockerallowstandarduserencryption"></a>Windows10EndpointProtectionConfiguration. bitlockerallowstandarduserencryption 
**CSP**:./Device/Vendor/MSFT/BitLocker  
**Offset-URI**:/AllowStandardUserEncryption

### <a name="windows10endpointprotectionconfigurationbitlockerdisablewarningforotherdiskencryption"></a>Windows10EndpointProtectionConfiguration. bitlockerdisablewarningforotherdiskencryption 
**CSP**:./Device/Vendor/MSFT/BitLocker  
**Offset-URI**:/AllowWarningForOtherDiskEncryption

### <a name="windows10endpointprotectionconfigurationbitlockerenablestoragecardencryptiononmobile"></a>Windows10EndpointProtectionConfiguration. bitlockerenablestoragecardencryptiononmobile 
**CSP**:./Device/Vendor/MSFT/BitLocker  
**Offset-URI**:/RequireStorageCardEncryption

### <a name="windows10endpointprotectionconfigurationbitlockerencryptdevice"></a>Windows10EndpointProtectionConfiguration. bitlockerverschlüsseltdevice 
**CSP**:./Device/Vendor/MSFT/BitLocker  
**Offset-URI**:/RequireDeviceEncryption

### <a name="windows10endpointprotectionconfigurationbitlockerfixeddrivepolicy"></a>Windows10EndpointProtectionConfiguration. bitlockerfixeddrivepolicy 
**CSP**:./Device/Vendor/MSFT/BitLocker  
**Offset-URI**:/EncryptionMethodByDriveType,/FixedDrivesRequireEncryption,/FixedDrivesRecoveryOptions

### <a name="windows10endpointprotectionconfigurationbitlockerremovabledrivepolicy"></a>Windows10EndpointProtectionConfiguration. bitlockerremovabledrivepolicy 
**CSP**:./Device/Vendor/MSFT/BitLocker  
**Offset-URI**:/EncryptionMethodByDriveType,/RemovableDrivesRequireEncryption

### <a name="windows10endpointprotectionconfigurationbitlockersystemdrivepolicy"></a>Windows10EndpointProtectionConfiguration. bitlockersystemdrivepolicy 
**CSP**:./Device/Vendor/MSFT/BitLocker  
**Offset-URI**:/EncryptionMethodByDriveType,/SystemDrivesRequireStartupAuthentication,/SystemDrivesMinimumPINLength,/SystemDrivesRecoveryMessage,/SystemDrivesRecoveryOptions

### <a name="windows10endpointprotectionconfigurationclientconnectionencryptionlevel"></a>windows10endpointprotectionconfiguration. clientconnectionverschlüsselungsebene 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/RemoteDesktopServices/ClientConnectionEncryptionLevel

### <a name="windows10endpointprotectionconfigurationconfiguresmbv1clientdriver"></a>windows10endpointprotectionconfiguration.configureSMBV1ClientDriver 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSecurityGuide/ConfigureSMBV1ClientDriver

### <a name="windows10endpointprotectionconfigurationconnectivitydownloadingofprintdriversoverhttp"></a>Windows10EndpointProtectionConfiguration. connectivitydownloadingof printdriversoverhttp 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/DisableDownloadingOfPrintDriversOverHTTP

### <a name="windows10endpointprotectionconfigurationconnectivityhardeneduncpaths"></a>Windows10EndpointProtectionConfiguration. connectivityhardeneduncpath 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/HardenedUNCPaths

### <a name="windows10endpointprotectionconfigurationconnectivityinternetdownloadforwebpublishingandonlineorderingwizards"></a>Windows10EndpointProtectionConfiguration. connectivityinternetdownloadforwebpublishingandonlineorderingassistenten 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/DisableInternetDownloadForWebPublishingAndOnlineOrderingWizards

### <a name="windows10endpointprotectionconfigurationconnectivityprintingoverhttp"></a>Windows10EndpointProtectionConfiguration. connectivityprintingoverhttp 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/DiablePrintingOverHTTP

### <a name="windows10endpointprotectionconfigurationcredentialsuienumerateadministrators"></a>Windows10EndpointProtectionConfiguration. kredentialsuienumerateadministrators 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/CredentialsUI/EnumerateAdministrators

### <a name="windows10endpointprotectionconfigurationdefenderadditionalguardedfolders"></a>Windows10EndpointProtectionConfiguration. defenderadditionalguarbedfolder 
**CSP**:./Device/Vendor/MSFT/Policy **Offset-URI**:/config/Defender/ControlledFolderAccessProtectedFolders

### <a name="windows10endpointprotectionconfigurationdefenderadvancedransomewareprotectiontype"></a>Windows10EndpointProtectionConfiguration. defenderadvancedransomewareschutztype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderattacksurfacereductionexcludedpaths"></a>Windows10EndpointProtectionConfiguration. defenderangreisurfakereductionexcluzerdpath 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionOnlyExclusions

### <a name="windows10endpointprotectionconfigurationdefenderemailcontentexecution"></a>Windows10EndpointProtectionConfiguration. defenderemailcontentexecution 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowEmailScanning

### <a name="windows10endpointprotectionconfigurationdefenderemailcontentexecutiontype"></a>Windows10EndpointProtectionConfiguration. defenderemailcontentexecutiontype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules (CSP/Konfiguration erfordert Diagramm Eigenschaften: windows10endpointprotection/Configuration. defenderofficeappsotherprocessinjectiontype, windows10endpointprotection/Configuration. defenderofficeappsexecutablecontentkreationorlaunchtype, windows10endpointprotection/Configuration. defenderofficeappslaunchchildprocesstype, windows10endpointprotection/Configuration. defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration. defenderscriptobfuscatedmacrocodetype, windows10endpointprotection/Configuration. defenderscriptdownloader adedpayloadexecutiontype, windows10endpointprotection/Configuration. defenderemailcontentexecutiontype, windows10endpointprotection/Configuration. defenderpreventkredentialstealingtype, windows10endpointprotection/Configuration. defenderuntreuhänder dusbprocesstype

### <a name="windows10endpointprotectionconfigurationdefenderexploitprotectionxml"></a>Windows10EndpointProtectionConfiguration. defenderexploitschutzxml 
**CSP**:./Device/Vendor/MSFT/Policy **Offset-URI**:/config/ExploitGuard/ExploitProtectionSettings

### <a name="windows10endpointprotectionconfigurationdefenderexploitprotectionxmlfilename"></a>Windows10EndpointProtectionConfiguration. defenderexploitschutzxmlfilename 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/ExploitGuard/ExploitProtectionSettings

### <a name="windows10endpointprotectionconfigurationdefenderguardedfoldersallowedapppaths"></a>Windows10EndpointProtectionConfiguration. defenderguarddfoldersallowedapppath 
**CSP**:./Device/Vendor/MSFT/Policy **Offset-URI**:/config/Defender/ControlledFolderAccessAllowedApplications

### <a name="windows10endpointprotectionconfigurationdefenderguardmyfolderstype"></a>Windows10EndpointProtectionConfiguration. defenderguardmyfolderstype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/EnableControlledFolderAccess

### <a name="windows10endpointprotectionconfigurationdefendernetworkprotectiontype"></a>Windows10EndpointProtectionConfiguration. defendernetworkschutztype 
**CSP**:./Device/Vendor/MSFT/Policy **Offset-URI**:/config/Defender/EnableNetworkProtection

### <a name="windows10endpointprotectionconfigurationdefenderofficeappsexecutablecontentcreationorlaunch"></a>Windows10EndpointProtectionConfiguration. defenderofficeappsexecutablecontentkreationorlaunch 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderofficeappsexecutablecontentcreationorlaunchtype"></a>Windows10EndpointProtectionConfiguration. defenderofficeappsexecutablecontentkreationorlaunchtype
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules (CSP/Konfiguration erfordert Diagramm Eigenschaften: windows10endpointprotection/Configuration. defenderofficeappsotherprocessinjectiontype, windows10endpointprotection/Configuration. defenderofficeappsexecutablecontentkreationorlaunchtype, windows10endpointprotection/Configuration. defenderofficeappslaunchchildprocesstype, windows10endpointprotection/Configuration. defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration. defenderscriptobfuscatedmacrocodetype, windows10endpointprotection/Configuration. defenderscriptdownloader adedpayloadexecutiontype, windows10endpointprotection/Configuration. defenderemailcontentexecutiontype, windows10endpointprotection/Configuration. defenderpreventkredentialstealingtype, windows10endpointprotection/Configuration. defenderuntreuhänder dusbprocesstype

### <a name="windows10endpointprotectionconfigurationdefenderofficeappslaunchchildprocess"></a>Windows10EndpointProtectionConfiguration. defenderofficeappslaunchchildprocess 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderofficeappslaunchchildprocesstype"></a>Windows10EndpointProtectionConfiguration. defenderofficeappslaunchchildprocesstype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules (CSP/Konfiguration erfordert Diagramm Eigenschaften: windows10endpointprotection/Configuration. defenderofficeappsotherprocessinjectiontype, windows10endpointprotection/Configuration. defenderofficeappsexecutablecontentkreationorlaunchtype, windows10endpointprotection/Configuration. defenderofficeappslaunchchildprocesstype, windows10endpointprotection/Configuration. defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration. defenderscriptobfuscatedmacrocodetype, windows10endpointprotection/Configuration. defenderscriptdownloader adedpayloadexecutiontype, windows10endpointprotection/Configuration. defenderemailcontentexecutiontype, windows10endpointprotection/Configuration. defenderpreventkredentialstealingtype, windows10endpointprotection/Configuration. defenderuntreuhänder dusbprocesstype

### <a name="windows10endpointprotectionconfigurationdefenderofficeappsotherprocessinjection"></a>Windows10EndpointProtectionConfiguration. defenderofficeappsotherprocessinjection 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderofficeappsotherprocessinjectiontype"></a>Windows10EndpointProtectionConfiguration. defenderofficeappsotherprocessinjectiontype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules (CSP/Konfiguration erfordert Diagramm Eigenschaften: windows10endpointprotection/Configuration. defenderofficeappsotherprocessinjectiontype, windows10endpointprotection/Configuration. defenderofficeappsexecutablecontentkreationorlaunchtype, windows10endpointprotection/Configuration. defenderofficeappslaunchchildprocesstype, windows10endpointprotection/Configuration. defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration. defenderscriptobfuscatedmacrocodetype, windows10endpointprotection/Configuration. defenderscriptdownloader adedpayloadexecutiontype, windows10endpointprotection/Configuration. defenderemailcontentexecutiontype, windows10endpointprotection/Configuration. defenderpreventkredentialstealingtype, windows10endpointprotection/Configuration. defenderuntreuhänder dusbprocesstype 

### <a name="windows10endpointprotectionconfigurationdefenderofficemacrocodeallowwin32imports"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeMacroCodeAllowWin32Imports 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderofficemacrocodeallowwin32importstype"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeMacroCodeAllowWin32ImportsType 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules (CSP/Konfiguration erfordert Diagramm Eigenschaften: windows10endpointprotection/Configuration. defenderofficeappsotherprocessinjectiontype, windows10endpointprotection/Configuration. defenderofficeappsexecutablecontentkreationorlaunchtype, windows10endpointprotection/Configuration. defenderofficeappslaunchchildprocesstype, windows10endpointprotection/Configuration. defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration. defenderscriptobfuscatedmacrocodetype, windows10endpointprotection/Configuration. defenderscriptdownloader adedpayloadexecutiontype, windows10endpointprotection/Configuration. defenderemailcontentexecutiontype, windows10endpointprotection/Configuration. defenderpreventkredentialstealingtype, windows10endpointprotection/Configuration. defenderuntreuhänder dusbprocesstype

### <a name="windows10endpointprotectionconfigurationdefenderpreventcredentialstealingtype"></a>Windows10EndpointProtectionConfiguration. defenderpreventkredentialstealingtype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules (CSP/Konfiguration erfordert Diagramm Eigenschaften: windows10endpointprotection/Configuration. defenderofficeappsotherprocessinjectiontype, windows10endpointprotection/Configuration. defenderofficeappsexecutablecontentkreationorlaunchtype, windows10endpointprotection/Configuration. defenderofficeappslaunchchildprocesstype, windows10endpointprotection/Configuration. defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration. defenderscriptobfuscatedmacrocodetype, windows10endpointprotection/Configuration. defenderscriptdownloader adedpayloadexecutiontype, windows10endpointprotection/Configuration. defenderemailcontentexecutiontype, windows10endpointprotection/Configuration. defenderpreventkredentialstealingtype, windows10endpointprotection/Configuration. defenderuntreuhänder dusbprocesstype

### <a name="windows10endpointprotectionconfigurationdefenderprocesscreation"></a>Windows10EndpointProtectionConfiguration. defenderprocesscreations 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderprocesscreationtype"></a>Windows10EndpointProtectionConfiguration. defenderprocesscreationtype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderprotectagainstpotentiallyunwantedapplications"></a>Windows10EndpointProtectionConfiguration. defenderprotectagainstpotenallyunwantedapplications 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSecurityGuide/TurnOnWindowsDefenderProtectionAgainstPotentiallyUnwantedApplications

### <a name="windows10endpointprotectionconfigurationdefenderscriptdownloadedpayloadexecution"></a>Windows10EndpointProtectionConfiguration. defenderscriptdownloader adedpayloadexecution 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderscriptdownloadedpayloadexecutiontype"></a>Windows10EndpointProtectionConfiguration. defenderscriptdownloader adedpayloadexecutiontype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules (CSP/Konfiguration erfordert Diagramm Eigenschaften: windows10endpointprotection/Configuration. defenderofficeappsotherprocessinjectiontype, windows10endpointprotection/Configuration. defenderofficeappsexecutablecontentkreationorlaunchtype, windows10endpointprotection/Configuration. defenderofficeappslaunchchildprocesstype, windows10endpointprotection/Configuration. defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration. defenderscriptobfuscatedmacrocodetype, windows10endpointprotection/Configuration. defenderscriptdownloader adedpayloadexecutiontype, windows10endpointprotection/Configuration. defenderemailcontentexecutiontype, windows10endpointprotection/Configuration. defenderpreventkredentialstealingtype, windows10endpointprotection/Configuration. defenderuntreuhänder dusbprocesstype

### <a name="windows10endpointprotectionconfigurationdefenderscriptobfuscatedmacrocode"></a>Windows10EndpointProtectionConfiguration. defenderscriptobfuscatedmakrocode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderscriptobfuscatedmacrocodetype"></a>Windows10EndpointProtectionConfiguration. defenderscriptobfuscatedmacrocodetype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules (CSP/Konfiguration erfordert Diagramm Eigenschaften: windows10endpointprotection/Configuration. defenderofficeappsotherprocessinjectiontype, windows10endpointprotection/Configuration. defenderofficeappsexecutablecontentkreationorlaunchtype, windows10endpointprotection/Configuration. defenderofficeappslaunchchildprocesstype, windows10endpointprotection/Configuration. defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration. defenderscriptobfuscatedmacrocodetype, windows10endpointprotection/Configuration. defenderscriptdownloader adedpayloadexecutiontype, windows10endpointprotection/Configuration. defenderemailcontentexecutiontype, windows10endpointprotection/Configuration. defenderpreventkredentialstealingtype, windows10endpointprotection/Configuration. defenderuntreuhänder dusbprocesstype

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterblockexploitprotectionoverride"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterblockexploitschutzoverride 
**CSP**:./Device/Vendor/MSFT/Policy **Offset-URI**:/config/WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisableaccountui"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterdisableaccountui 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/DisableAccountProtectionUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisableappbrowserui"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterdisableappbrowserui 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/DisableAppBrowserUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablefamilyui"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterdisablefamilyui 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/DisableFamilyUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablehealthui"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterdisablehealthui 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/DisableHealthUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablenetworkui"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterdisablenetworkui 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/DisableNetworkUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablesecurebootui"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterdisablesecurebootui 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/HideSecureBoot

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisabletroubleshootingui"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterdisabletroubleshootingui 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/HideTPMTroubleshooting

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablevirusui"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterdisablevirusui 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/DisableVirusUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterhelpemail"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterhelpeer Mail 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/Email

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterhelpphone"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterhelpphone 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/Phone

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterhelpurl"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterhelpurl 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/URL

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenteritcontactdisplay"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenteritcontactdisplay 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/WindowsDefenderSecurityCenter/EnableCustomizedToasts,/WindowsDefenderSecurityCenter/EnableInAppCustomization

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenternotificationsfromapp"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenternotificationsfromapp 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/HideWindowsSecurityNotificationAreaControl

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterorganizationdisplayname"></a>Windows10EndpointProtectionConfiguration. defendersecuritycenterorganizationdisplayname 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsDefenderSecurityCenter/CompanyName

### <a name="windows10endpointprotectionconfigurationdefenderuntrustedexecutable"></a>Windows10EndpointProtectionConfiguration. defenderuntreudexecutable 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderuntrustedexecutabletype"></a>Windows10EndpointProtectionConfiguration. defenderuntreudexecutabletype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderuntrustedusbprocess"></a>Windows10EndpointProtectionConfiguration. defenderuntreudusbprocess 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderuntrustedusbprocesstype"></a>Windows10EndpointProtectionConfiguration. defenderuntreudusbprocesstype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AttackSurfaceReductionRules (CSP/Konfiguration erfordert Diagramm Eigenschaften: windows10endpointprotection/Configuration. defenderofficeappsotherprocessinjectiontype, windows10endpointprotection/Configuration. defenderofficeappsexecutablecontentkreationorlaunchtype, windows10endpointprotection/Configuration. defenderofficeappslaunchchildprocesstype, windows10endpointprotection/Configuration. defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration. defenderscriptobfuscatedmacrocodetype, windows10endpointprotection/Configuration. defenderscriptdownloader adedpayloadexecutiontype, windows10endpointprotection/Configuration. defenderemailcontentexecutiontype, windows10endpointprotection/Configuration. defenderpreventkredentialstealingtype, windows10endpointprotection/Configuration. defenderuntreuhänder dusbprocesstype

### <a name="windows10endpointprotectionconfigurationdeviceguardenablesecurebootwithdma"></a>Windows10EndpointProtectionConfiguration. deviceguardenablesecurebootwithdma 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceGuard/RequirePlatformSecurityFeatures

### <a name="windows10endpointprotectionconfigurationdeviceguardenablevirtualizationbasedsecurity"></a>Windows10EndpointProtectionConfiguration. deviceguardenablevirtualizationbasedsecurity 
**CSP**:./Device/Vendor/MSFT/Policy **Offset-URI**:/config/DeviceGuard/EnableVirtualizationBasedSecurity

### <a name="windows10endpointprotectionconfigurationdeviceguardlaunchsystemguard"></a>Windows10EndpointProtectionConfiguration. deviceguardlaunchsystemguard 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceGuard/ConfigureSystemGuardLaunch

### <a name="windows10endpointprotectionconfigurationdeviceguardlocalsystemauthoritycredentialguardsettings"></a>Windows10EndpointProtectionConfiguration. deviceguardlocalsystemautoritykredentialguardsettings 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceGuard/LsaCfgFlags

### <a name="windows10endpointprotectionconfigurationdmaguarddeviceenumerationpolicy"></a>Windows10EndpointProtectionConfiguration. dmaguarddeviceenumerationpolicy 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DmaGuard/DeviceEnumerationPolicy

### <a name="windows10endpointprotectionconfigurationeventlogserviceapplicationlogmaximumfilesizeinkb"></a>Windows10EndpointProtectionConfiguration. eventlogserviceapplicationlogmaximumfilesizin KB 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/EventLogService/SpecifyMaximumFileSizeApplicationLog

### <a name="windows10endpointprotectionconfigurationeventlogservicesecuritylogmaximumfilesizeinkb"></a>Windows10EndpointProtectionConfiguration. eventlogservicesecuritylogmaximumfilesizeinkb 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/EventLogService/SpecifyMaximumFileSizeSecurityLog

### <a name="windows10endpointprotectionconfigurationeventlogservicesystemlogmaximumfilesizeinkb"></a>Windows10EndpointProtectionConfiguration. eventlogservicesystemlogmaximumfilesizeinkb 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/EventLogService/SpecifyMaximumFileSizeSystemLog

### <a name="windows10endpointprotectionconfigurationexplorerdataexecutionprevention"></a>Windows10EndpointProtectionConfiguration. explorerdataexecutionprevention 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/FileExplorer/TurnOffDataExecutionPreventionForExplorer

### <a name="windows10endpointprotectionconfigurationexplorerheapterminationoncorruption"></a>Windows10EndpointProtectionConfiguration. explorerheapterminationoncorruption 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/FileExplorer/TurnOffHeapTerminationOnCorruption

### <a name="windows10endpointprotectionconfigurationfirewallblockstatefulftp"></a>Windows10EndpointProtectionConfiguration. firewallblockstatuefulftp 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/DisableStatefulFtp

### <a name="windows10endpointprotectionconfigurationfirewallcertificaterevocationlistcheckmethod"></a>Windows10EndpointProtectionConfiguration. firewallcertificaterevocationlistcheckmethod 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/CRLcheck

### <a name="windows10endpointprotectionconfigurationfirewallidletimeoutforsecurityassociationinseconds"></a>Windows10EndpointProtectionConfiguration. firewallidletimeoutforsecurityassociationinseconds 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/SaIdleTime

### <a name="windows10endpointprotectionconfigurationfirewallipsecexemptionsallowdhcp"></a>Windows10EndpointProtectionConfiguration. firewallipsecexemptionsallowdhcp 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/IPsecExempt

### <a name="windows10endpointprotectionconfigurationfirewallipsecexemptionsallowicmp"></a>Windows10EndpointProtectionConfiguration. firewallipsecexemptionsallowicmp 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/IPsecExempt

### <a name="windows10endpointprotectionconfigurationfirewallipsecexemptionsallowneighbordiscovery"></a>Windows10EndpointProtectionConfiguration. firewallipsecexemptionsallownachbardiscovery 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/IPsecExempt

### <a name="windows10endpointprotectionconfigurationfirewallipsecexemptionsallowrouterdiscovery"></a>Windows10EndpointProtectionConfiguration. firewallipsecexemptionsallowrouterdiscovery 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/IPsecExempt

### <a name="windows10endpointprotectionconfigurationfirewallmergekeyingmodulesettings"></a>Windows10EndpointProtectionConfiguration. firewallmergekeyingmodulesettings 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/OpportunisticallyMatchAuthSetPerKM

### <a name="windows10endpointprotectionconfigurationfirewallpacketqueueingmethod"></a>Windows10EndpointProtectionConfiguration. firewallpacketqueueingmethod 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/EnablePacketQueue

### <a name="windows10endpointprotectionconfigurationfirewallpresharedkeyencodingmethod"></a>Windows10EndpointProtectionConfiguration. firewallpresharedkeyencodingmethod 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/Global/PresharedKeyEncoding

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomain"></a>Windows10EndpointProtectionConfiguration. firewallprofiledomain 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/EnableFirewall,/DisableStealthMode,/Shielded,/DisableUnicastResponsesToMulticastBroadcast,/DisableInboundNotifications,/AuthAppsAllowUserPrefMerge,/GlobalPortsAllowUserPrefMerge,/AllowLocalPolicyMerge,/DefaultOutboundAction,/DefaultInboundAction,/DisableStealthModeIpsecSecuredPacketExemption,/AllowLocalIpsecPolicyMerge

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomaininboundconnectionsblocked"></a>windows10endpointprotectionconfiguration. firewallprofiledomain. inboundconnectionsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/DomainProfile/DefaultInboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomaininboundnotificationsblocked"></a>windows10endpointprotectionconfiguration. firewallprofiledomain. inboundnotificationsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/DomainProfile/DisableInboundNotifications

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomaininboundnotificationsblocked"></a>windows10endpointprotectionconfiguration. firewallprofiledomain. inboundnotificationsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/DomainProfile/EnableFirewall

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomainoutboundconnectionsblocked"></a>windows10endpointprotectionconfiguration. firewallprofiledomain. outboundconnectionsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/DomainProfile/DefaultOutboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivate"></a>Windows10EndpointProtectionConfiguration. firewallprofileprivate 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/EnableFirewall,/DisableStealthMode,/Shielded,/DisableUnicastResponsesToMulticastBroadcast,/DisableInboundNotifications,/AuthAppsAllowUserPrefMerge,/GlobalPortsAllowUserPrefMerge,/AllowLocalPolicyMerge,/DefaultOutboundAction,/DefaultInboundAction,/DisableStealthModeIpsecSecuredPacketExemption,/AllowLocalIpsecPolicyMerge

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivatefirewallenabled"></a>windows10endpointprotectionconfiguration. firewallprofileprivate. firewallaktivierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PrivateProfile/EnableFirewall

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivateinboundconnectionsblocked"></a>windows10endpointprotectionconfiguration. firewallprofileprivate. inboundconnectionsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PrivateProfile/DefaultInboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivateinboundnotificationsblocked"></a>windows10endpointprotectionconfiguration. firewallprofileprivate. inboundnotificationsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PrivateProfile/DisableInboundNotifications

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivateoutboundconnectionsblocked"></a>windows10endpointprotectionconfiguration. firewallprofileprivate. outboundconnectionsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PrivateProfile/DefaultOutboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublic"></a>Windows10EndpointProtectionConfiguration. firewallprofilepublic 
**CSP**:./Vendor/MSFT/Firewall  
**Offset-URI**:/EnableFirewall,/DisableStealthMode,/Shielded,/DisableUnicastResponsesToMulticastBroadcast,/DisableInboundNotifications,/AuthAppsAllowUserPrefMerge,/GlobalPortsAllowUserPrefMerge,/AllowLocalPolicyMerge,/DefaultOutboundAction,/DefaultInboundAction,/DisableStealthModeIpsecSecuredPacketExemption,/AllowLocalIpsecPolicyMerge

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicconnectionsecurityrulesfromgrouppolicymerged"></a>windows10endpointprotectionconfiguration. firewallprofilepublic. connectionsecurityrulesfromgrouppolicygemergt 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PublicProfile/AllowLocalIpsecPolicyMerge

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicfirewallenabled"></a>windows10endpointprotectionconfiguration. firewallprofilepublic. firewallaktivierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PublicProfile/EnableFirewall

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicinboundconnectionsblocked"></a>windows10endpointprotectionconfiguration. firewallprofilepublic. inboundconnectionsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PublicProfile/DefaultInboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicinboundnotificationsblocked"></a>windows10endpointprotectionconfiguration. firewallprofilepublic. inboundnotificationsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PublicProfile/DisableInboundNotifications

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicoutboundconnectionsblocked"></a>windows10endpointprotectionconfiguration. firewallprofilepublic. outboundconnectionsblockierte 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PublicProfile/DefaultOutboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicpolicyrulesfromgrouppolicymerged"></a>windows10endpointprotectionconfiguration. firewallprofilepublic. policyrulesfromgrouppolicygemergt 
**CSP**:./Device/Vendor/MSFT/Firewall  
**Offset-URI**:/MdmStore/PublicProfile/AllowLocalPolicyMerge

### <a name="windows10endpointprotectionconfigurationlanmanagerauthenticationlevel"></a>Windows10EndpointProtectionConfiguration. lanmanagerauthenticationlevel 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkSecurity \_ lanmanagerauthenticationlevel

### <a name="windows10endpointprotectionconfigurationlanmanagerworkstationdisableinsecureguestlogons"></a>Windows10EndpointProtectionConfiguration. lanmanagerworkstationdisableinsecureguestlogons 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LanmanWorkstation/EnableInsecureGuestLogons

### <a name="windows10endpointprotectionconfigurationlanmanagerworkstationenableinsecureguestlogons"></a>Windows10EndpointProtectionConfiguration. lanmanagerworkstationenableinsecureguestlogons 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LanmanWorkstation/EnableInsecureGuestLogons

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsadministratoraccountname"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAdministratorAccountName 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Accounts \_ RenameAdministratorAccount

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsadministratorelevationpromptbehavior"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAdministratorElevationPromptBehavior
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ verhaltheioferelevationpromptforadministrators

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowanonymousenumerationofsamaccountsandshares"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsallowanonymousenproerationofsamaccountsandshares 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkAccess \_ donotallowanonymousentoerationofsamaccountsandshares

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowpku2uauthenticationrequests"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowPKU2UAuthenticationRequests 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkSecurity \_ AllowPKU2UAuthenticationRequests

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowremotecallstosecurityaccountsmanager"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsallowremotecallstosecurityaccountimanager 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkAccess \_ restrictclientsallowedtomakeremotecallstosam

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowremotecallstosecurityaccountsmanagerhelperbool"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsallowremotecallstosecurityaccountimanagerhelperbool 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkAccess \_ restrictclientsallowedtomakeremotecallstosam

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowsystemtobeshutdownwithouthavingtologon"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsallowsystemrebeshutdownwithouthavingtologon 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Shutdown \_ allowsystemtobeshutdownwithouthavingtologon

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowuiaccessapplicationelevation"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsallowuiaccessapplicationelevation 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ zusetzeraccessapplicationstopromptforelevation

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowuiaccessapplicationsforsecurelocations"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsallowuiaccessapplicationsforsecuumsetzungen 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ onlyelevateuiaccessapplicationsthatareinstalledinsecu-Umsetzungen

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowundockwithouthavingtologon"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsallowundockwithouthavingtologon 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Devices zugedodockwithouthavingtologon \_

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsblockmicrosoftaccounts"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsblockmicrosoftaccounts 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Accounts \_ blockmicrosoftaccounts

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsblockremotelogonwithblankpassword"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsblockremotelogonwithblankpassword 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Accounts \_ limitlocalaccountuseofblankpasswordstoconsolelogononly

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsblockremoteopticaldriveaccess"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsblockremoteopticaldriveaccess 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Devices \_ restrictcdromaccesstolocallyloggedonuseronly

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsblockusersinstallingprinterdrivers"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsblockusersinstallingprinterdrivers 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Devices \_ preventusersfrominstallingprinterdrivers\connectingtosharedprinter

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsclearvirtualmemorypagefile"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsclearvirtualmemorypagefile 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Shutdown \_ clearvirtualmemorypagefile

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsclientdigitallysigncommunicationsalways"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsclientdigitallysigncommunicationsalways 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/MicrosoftNetworkClient \_ digitallysigncommunicationsalways

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsclientsendunencryptedpasswordtothirdpartysmbservers"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsclientsendunverschlüsseltedpasswordumthirdpartysmbservers 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/MicrosoftNetworkClient \_ sendunverschlüsseltedpasswordtothirdpartysmbservers

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdetectapplicationinstallationsandpromptforelevation"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsdetectapplicationinstallationsandpromptforelevation 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ detectapplicationinstallationsandpromptforelevation

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableadministratoraccount"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableAdministratorAccount 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Accounts \_ EnableAdministratorAccountStatus

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableclientdigitallysigncommunicationsifserveragrees"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsdisableclientdigitallysigncommunicationsif Server-Stimmen 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/MicrosoftNetworkClient \_ digitallysigncommunicationsif Server-Zustimmung

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableguestaccount"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsdisableguestaccount 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Accounts \_ enableguestaccountstatus

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableserverdigitallysigncommunicationsalways"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsdisableserverdigitallysigncommunicationsalways 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/MicrosoftNetworkServer \_ digitallysigncommunicationsalways

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableserverdigitallysigncommunicationsifclientagrees"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsdisableserverdigitallysigncommunicationsif clientzustimmt 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/MicrosoftNetworkServer \_ digitallysigncommunicationsif clientstimmen

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdonotallowanonymousenumerationofsamaccounts"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsdonotallowanonymousentoerationofsamaccounts 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkAccess \_ donotallowanonymousentoerationofsamaccounts

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdonotrequirectrlaltdel"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsdonotrequirectrlaltdel 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ donotrequirectrlaltdel

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdonotstorelanmanagerhashvalueonnextpasswordchange"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsdonotstorelanmanagerhashvalueonnextpasswordchange 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkSecurity \_ donotstorelanmanagerhashvalueonnextpasswordchange

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsenableadministratoraccount"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsEnableAdministratorAccount 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Accounts \_ EnableAdministratorAccountStatus

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsenableguestaccount"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsenableguestaccount 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Accounts \_ enableguestaccountstatus

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsformatandejectofremovablemediaalloweduser"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsformatandejecdefremovablemediazuweisung weduser 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Devices-Zuweisung von "" \_

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsguestaccountname"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsguestaccountname 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/Accounts \_ renameguestaccount

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionshidelastsignedinuser"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionshidelta astsignetdinuser 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ donotdisplaylastsignetdin

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionshideusernameatsignin"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionshideusernameatsignin 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ donotdisplayusernameatsignin

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsinformationdisplayedonlockscreen"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsinformationdisplayedonlockscreen 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ displayuserinformationwhenthesessionislock

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsinformationshownonlockscreen"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsinformationshownonlockscreen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ displayuserinformationwhenthesessionislock

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionslogonmessagetext"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionslogonmessagetext 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ messagetextforusersattemptingtologon

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionslogonmessagetitle"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionslogonmessagetitle 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ messagetitleforusersattemptingtologon

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsmachineinactivitylimit"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsmachineinactivitylimit 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ machineinactivitylimit

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsmachineinactivitylimitinminutes"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsmachineinactivitylimitinminutes 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ machineinactivitylimit

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsminimumsessionsecurityforntlmsspbasedclients"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsminimumsessionsecurityforntlmsspbasedclients 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkSecurity \_ minimumsessionsecurityforntlmsspbasedclients

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsminimumsessionsecurityforntlmsspbasedservers"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsminimumsessionsecurityforntlmsspbasedservers 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkSecurity \_ minimumsessionsecurityforntlmsspbasedservers

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsonlyelevatesignedexecutables"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsonlyelevatesignetdexecutables 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ onlyelevateexecutablefilesthataresignedandvalidieren

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsrestrictanonymousaccesstonamedpipesandshares"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsrestrictanonymousaccesstonamedpipesandshares 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/NetworkAccess \_ restrictanonymousaccesstonamedpipesandshares

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionssmartcardremovalbehavior"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionssmartcardremuvalbehavior 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/InteractiveLogon \_ smartcardrejovalbehavior

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsstandarduserelevationpromptbehavior"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsstandarduserelevationpromptbehavior 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ verhaltheioferelevationpromptforstandardusers

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsswitchtosecuredesktopwhenpromptingforelevation"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsswitchtosecuredesktop\promptingforelevation 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ switchtothesecuredesktop\promptingforelevation

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsuseadminapprovalmode"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsumenadminapprovalmode 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ useadminapprovalmode

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsuseadminapprovalmodeforadministrators"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsumenadminapprovalmodeforadministrators 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ RunAllAdministratorsInAdminApprovalMode

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsvirtualizefileandregistrywritefailurestoperuserlocations"></a>Windows10EndpointProtectionConfiguration. localsecurityoptionsvirtualizefileandregistryschreitefailurestoperuserlocations 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/LocalPoliciesSecurityOptions/userAccountControl \_ virtualizefileandregistryschreitefailurestoperuserlocations

### <a name="windows10endpointprotectionconfigurationnetworkicmpredirectsoverrideospfgeneratedroutes"></a>Windows10EndpointProtectionConfiguration. networkicmpredirectsoverridecoospf generatedroutes 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSLegacy/AllowICMPRedirectsToOverrideOSPFGeneratedRoutes

### <a name="windows10endpointprotectionconfigurationnetworkignorenetbiosnamereleaserequestsexceptfromwinsservers"></a>Windows10EndpointProtectionConfiguration. networkignorsetbiosnamereleaserequestsexceptfromwinsservers 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSLegacy/AllowTheComputerToIgnoreNetBIOSNameReleaseRequestsExceptFromWINSServers

### <a name="windows10endpointprotectionconfigurationnetworkipsourceroutingprotectionlevel"></a>Windows10EndpointProtectionConfiguration. networkipsourceroutingschutzlevel 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSLegacy/IPSourceRoutingProtectionLevel

### <a name="windows10endpointprotectionconfigurationnetworkipv6sourceroutingprotectionlevel"></a>Windows10EndpointProtectionConfiguration.NetworkIpV6SourceRoutingProtectionLevel 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSLegacy/IPv6SourceRoutingProtectionLevel

### <a name="windows10endpointprotectionconfigurationpasswordpinlogon"></a>Windows10EndpointProtectionConfiguration. passwordpinlogon 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/CredentialProviders/AllowPINLogon

### <a name="windows10endpointprotectionconfigurationpowershellshellscriptblocklogging"></a>Windows10EndpointProtectionConfiguration. powershellshellscriptblocklogging 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsPowerShell/TurnOnPowerShellScriptBlockLogging

### <a name="windows10endpointprotectionconfigurationremoteassistancesolicitedsetting"></a>Windows10EndpointProtectionConfiguration. remoteassistancesolicitedsetting 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/HardenedUNCPaths

### <a name="windows10endpointprotectionconfigurationremotedesktopservicesclientconnectionencryptionlevel"></a>Windows10EndpointProtectionConfiguration. remotedesktopservicesclientconnectionverschlüsselungsstufe 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/RemoteDesktopServices/ClientConnectionEncryptionLevel

### <a name="windows10endpointprotectionconfigurationremotedesktopservicesdriveredirection"></a>Windows10EndpointProtectionConfiguration. remotedesktopservicesdriveredirection 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/RemoteDesktopServices/DoNotAllowDriveRedirection

### <a name="windows10endpointprotectionconfigurationremotedesktopservicespasswordsaving"></a>Windows10EndpointProtectionConfiguration. remotedesktopservicespasswordsave 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/RemoteDesktopServices/DoNotAllowPasswordSaving

### <a name="windows10endpointprotectionconfigurationremotedesktopservicespromptforpassworduponconnection"></a>Windows10EndpointProtectionConfiguration. remotedesktopservicespromptforpassworduponconnection 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/RemoteDesktopServices/PromptForPasswordUponConnection

### <a name="windows10endpointprotectionconfigurationremotedesktopservicessecurerpccommunication"></a>Windows10EndpointProtectionConfiguration. remotedesktopservicessecurerpccommunication 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/RemoteDesktopServices/RequireSecureRPCCommunication

### <a name="windows10endpointprotectionconfigurationremotehostdelegationofnonexportablecredentials"></a>Windows10EndpointProtectionConfiguration. remotehostdelegationofnonexportableanmelde Informationen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/CredentialsDelegation/RemoteHostAllowsDelegationOfNonExportableCredentials

### <a name="windows10endpointprotectionconfigurationremotemanagementclientbasicauthentication"></a>Windows10EndpointProtectionConfiguration. remotemanagementclientbasicauthentication 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Remotemanagement/AllowBasicAuthentication- \_ Client

### <a name="windows10endpointprotectionconfigurationremotemanagementclientdigestauthentication"></a>Windows10EndpointProtectionConfiguration. remotemanagementclientdigestauthentication 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Remotemanagement/DisallowDigestAuthentication

### <a name="windows10endpointprotectionconfigurationremotemanagementclientunencryptedtraffic"></a>Windows10EndpointProtectionConfiguration. remotemanagementclientunverschlüsseltedtraffic 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Remotemanagement/AllowUnencryptedTraffic- \_ Client

### <a name="windows10endpointprotectionconfigurationremotemanagementservicebasicauthentication"></a>Windows10EndpointProtectionConfiguration. remotemanagementservicebasicauthentication 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Remotemanagement/AllowBasicAuthentication- \_ Dienst

### <a name="windows10endpointprotectionconfigurationremotemanagementservicestoringrunascredentials"></a>Windows10EndpointProtectionConfiguration. remotemanagementservicestoringrunasanmeldeinformationen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Remotemanagement/DisallowStoringOfRunAsCredentials

### <a name="windows10endpointprotectionconfigurationremotemanagementserviceunencryptedtraffic"></a>Windows10EndpointProtectionConfiguration. remotemanagementserviceunverschlüsseltedtraffic 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Remotemanagement/AllowUnencryptedTraffic- \_ Dienst

### <a name="windows10endpointprotectionconfigurationrpcunauthenticatedclientoptions"></a>Windows10EndpointProtectionConfiguration. rpcunauthentieredclientoptions 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/RemoteProcedureCall/RestrictUnauthenticatedRPCClients

### <a name="windows10endpointprotectionconfigurationsecurityguideapplyuacrestrictionstolocalaccountsonnetworklogon"></a>Windows10EndpointProtectionConfiguration. securityguideapplyuacrestrictionstolocalaccountsonnetworklogon 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSecurityGuide/ApplyUACRestrictionsToLocalAccountsOnNetworkLogon

### <a name="windows10endpointprotectionconfigurationsecurityguidesmbv1clientdriverstartconfiguration"></a>Windows10EndpointProtectionConfiguration.SecurityGuideSmbV1ClientDriverStartConfiguration 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSecurityGuide/ConfigureSMBV1ClientDriver

### <a name="windows10endpointprotectionconfigurationsecurityguidesmbv1server"></a>Windows10EndpointProtectionConfiguration.SecurityGuideSmbV1Server 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSecurityGuide/ConfigureSMBV1Server

### <a name="windows10endpointprotectionconfigurationsecurityguidestructuredexceptionhandlingoverwriteprotection"></a>Windows10EndpointProtectionConfiguration. securityguidestructuredexceptionhandlingoverschreiteprotection 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSecurityGuide/EnableStructuredExceptionHandlingOverwriteProtection

### <a name="windows10endpointprotectionconfigurationsecurityguidewdigestauthentication"></a>Windows10EndpointProtectionConfiguration. securityguidewdigestauthentication 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/MSSecurityGuide/WDigestAuthentication

### <a name="windows10endpointprotectionconfigurationsmartscreenblockoverrideforfiles"></a>Windows10EndpointProtectionConfiguration. smartscreenblockoverrideforfiles 
**CSP**:./Device/Vendor/MSFT/Policy **Offset-URI**:/config/DeviceGuard/RequirePlatformSecurityFeatures

### <a name="windows10endpointprotectionconfigurationsmartscreenenableinshell"></a>Windows10EndpointProtectionConfiguration. smartscreenenableinshell 
**CSP**:./Device/Vendor/MSFT/Policy **Offset-URI**:/config/SmartScreen/EnableSmartScreenInShell

### <a name="windows10endpointprotectionconfigurationsolicitedremoteassistance"></a>windows10endpointprotectionconfiguration. solicitedremoteassistance 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/RemoteAssistance/SolicitedRemoteAssistance

### <a name="windows10endpointprotectionconfigurationuserrightsaccesscredentialmanagerastrustedcaller"></a>Windows10EndpointProtectionConfiguration. userright Access scredentialmanagerastrustedcaller 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/AccessCredentialManagerAsTrustedCaller

### <a name="windows10endpointprotectionconfigurationuserrightsaccessfromnetwork"></a>windows10EndpointProtectionConfiguration. userrighungsaccessfromnetwork 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/AccessFromNetwork

### <a name="windows10endpointprotectionconfigurationuserrightsactaspartoftheoperatingsystem"></a>Windows10EndpointProtectionConfiguration. userrightactasparametatderoperatingsystem 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/ActAsPartOfTheOperatingSystem

### <a name="windows10endpointprotectionconfigurationuserrightsallowaccessfromnetwork"></a>Windows10EndpointProtectionConfiguration. userrightsallowaccessfromnetwork 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/AccessFromNetwork

### <a name="windows10endpointprotectionconfigurationuserrightsbackupdata"></a>Windows10EndpointProtectionConfiguration. userrigh\backupdata 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/BackupFilesAndDirectories

### <a name="windows10endpointprotectionconfigurationuserrightsblockaccessfromnetwork"></a>Windows10EndpointProtectionConfiguration. userright Block Access fromnetwork 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/DenyAccessFromNetwork

### <a name="windows10endpointprotectionconfigurationuserrightschangesystemtime"></a>Windows10EndpointProtectionConfiguration. userrightschangesystemtime 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/ChangeSystemTime

### <a name="windows10endpointprotectionconfigurationuserrightscreateglobalobjects"></a>Windows10EndpointProtectionConfiguration. userrightscreateglobalobjects 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/CreateGlobalObjects

### <a name="windows10endpointprotectionconfigurationuserrightscreatepagefile"></a>Windows10EndpointProtectionConfiguration. userrightscreatepagefile 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/CreatePageFile

### <a name="windows10endpointprotectionconfigurationuserrightscreatepermanentsharedobjects"></a>Windows10EndpointProtectionConfiguration. userrightscreatepermanentsharedobjects 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/CreatePermanentSharedObjects

### <a name="windows10endpointprotectionconfigurationuserrightscreatesymboliclinks"></a>Windows10EndpointProtectionConfiguration. userrightscreatesymboliclinks 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/CreateSymbolicLinks

### <a name="windows10endpointprotectionconfigurationuserrightscreatetoken"></a>Windows10EndpointProtectionConfiguration. userrightscreatetoken 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/CreateToken

### <a name="windows10endpointprotectionconfigurationuserrightsdebugprograms"></a>Windows10EndpointProtectionConfiguration. userrightibugprograms 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/DebugPrograms

### <a name="windows10endpointprotectionconfigurationuserrightsdelegation"></a>Windows10EndpointProtectionConfiguration. userrighationdelegation 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/EnableDelegation

### <a name="windows10endpointprotectionconfigurationuserrightsdenyaccessfromnetwork"></a>windows10EndpointProtectionConfiguration. userrightendenyaccessfromnetwork 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/DenyAccessFromNetwork

### <a name="windows10endpointprotectionconfigurationuserrightsgeneratesecurityaudits"></a>Windows10EndpointProtectionConfiguration. userrightengeneratesecurityüberwachungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/GenerateSecurityAudits

### <a name="windows10endpointprotectionconfigurationuserrightsimpersonateclient"></a>Windows10EndpointProtectionConfiguration. userrightsimpersonateclient 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/ImpersonateClient

### <a name="windows10endpointprotectionconfigurationuserrightsincreaseschedulingpriority"></a>Windows10EndpointProtectionConfiguration. userrightsinkreaseschedulingpriority 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/IncreaseSchedulingPriority

### <a name="windows10endpointprotectionconfigurationuserrightsloadunloaddrivers"></a>Windows10EndpointProtectionConfiguration. userrighgsloadunloaddrivers 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/LoadUnloadDeviceDrivers

### <a name="windows10endpointprotectionconfigurationuserrightslocallogon"></a>Windows10EndpointProtectionConfiguration. userrighsorloczuweisung 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/AllowLocalLogOn

### <a name="windows10endpointprotectionconfigurationuserrightslockmemory"></a>Windows10EndpointProtectionConfiguration. userrighunlockmemory 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/LockMemory

### <a name="windows10endpointprotectionconfigurationuserrightsmanageauditingandsecuritylogs"></a>Windows10EndpointProtectionConfiguration. userrightmanageauditingandsecuritylogs 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/ManageAuditingAndSecurityLog

### <a name="windows10endpointprotectionconfigurationuserrightsmanagevolumes"></a>Windows10EndpointProtectionConfiguration. userrightionsmanagevolumes 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/ManageVolume

### <a name="windows10endpointprotectionconfigurationuserrightsmodifyfirmwareenvironment"></a>Windows10EndpointProtectionConfiguration. userrighungmodifyfirmwareenvironment 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/ModifyFirmwareEnvironment

### <a name="windows10endpointprotectionconfigurationuserrightsmodifyobjectlabels"></a>Windows10EndpointProtectionConfiguration. userrightmodifyobjectlabels 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/ModifyObjectLabel

### <a name="windows10endpointprotectionconfigurationuserrightsprofilesingleprocess"></a>Windows10EndpointProtectionConfiguration. userrightsprofilesingleprocess 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/ProfileSingleProcess

### <a name="windows10endpointprotectionconfigurationuserrightsregisterprocessasservice"></a>Windows10EndpointProtectionConfiguration. userrighzregisterprocessasservice 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/DenyLocalLogOn

### <a name="windows10endpointprotectionconfigurationuserrightsremotedesktopserviceslogon"></a>Windows10EndpointProtectionConfiguration. userrightremotedesktopserviceslogon 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/DenyRemoteDesktopServicesLogOn

### <a name="windows10endpointprotectionconfigurationuserrightsremoteshutdown"></a>Windows10EndpointProtectionConfiguration. userrighsiremoteshutdown 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/RemoteShutdown

### <a name="windows10endpointprotectionconfigurationuserrightsrestoredata"></a>Windows10EndpointProtectionConfiguration. userrighenrestoredata 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/RestoreFilesAndDirectories

### <a name="windows10endpointprotectionconfigurationuserrightstakeownership"></a>Windows10EndpointProtectionConfiguration. userrightstakeownership 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/UserRights/TakeOwnership

### <a name="windows10endpointprotectionconfigurationwindowsconnectionmanagerconnectiontonondomainnetworks"></a>Windows10EndpointProtectionConfiguration. windowsconnectionmanagerconnectiontonondomainnetworks 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsConnectionManager/ProhitConnectionToNonDomainNetworksWhenConnectedToDomainAuthenticatedNetwork

### <a name="windows10endpointprotectionconfigurationwindowslogonsigninlastinteractiveuseraftersysteminitiatedrestart"></a>Windows10EndpointProtectionConfiguration. windowslogonsigninlastinteractiveuseraftersysteminitiatedrestart 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsLogon/SignInLastInteractiveUserAutomaticallyAfterASystemInitiatedRestart

### <a name="windows10endpointprotectionconfigurationxboxservicesaccessorymanagementservicestartupmode"></a>Windows10EndpointProtectionConfiguration. xboxservicesaccessorymanagementservicestartupmode 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/SystemServices/ConfigureXboxAccessoryManagementServiceStartupMode

### <a name="windows10endpointprotectionconfigurationxboxservicesenablexboxgamesavetask"></a>Windows10EndpointProtectionConfiguration. xboxservicesenablexboxgamesavetask 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/TaskScheduler/EnableXboxGameSaveTask

### <a name="windows10endpointprotectionconfigurationxboxservicesliveauthmanagerservicestartupmode"></a>Windows10EndpointProtectionConfiguration. xboxservicesliveauthmanagerservicestartupmode 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/SystemServices/ConfigureXboxLiveAuthManagerServiceStartupMode

### <a name="windows10endpointprotectionconfigurationxboxserviceslivegamesaveservicestartupmode"></a>Windows10EndpointProtectionConfiguration. xboxserviceslivegamesaveservicestartupmode 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/SystemServices/XboxServicesLiveGameSaveServiceStartupMode

### <a name="windows10endpointprotectionconfigurationxboxserviceslivenetworkingservicestartupmode"></a>Windows10EndpointProtectionConfiguration. xboxserviceslivenetworkingservicestartupmode 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/SystemServices/ConfigureXboxLiveNetworkingServiceStartupMode

### <a name="windows10enterprisemodernappmanagementconfigurationuninstallbuiltinapps"></a>Windows10EnterpriseModernAppManagementConfiguration. uninstallbuiltinapps
**CSP**: n/a Graph-API reinen **Offset-URI**: n/a Graph-API nur Aufrufe

### <a name="windows10generalconfigurationaccountsblockaddingnonmicrosoftaccountemail"></a>Windows10GeneralConfiguration. accounffiblockaddingnonmicrosoftaccountemail 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Accounts/AllowAddingNonMicrosoftAccountsManually

### <a name="windows10generalconfigurationantitheftmodeblocked"></a>Windows10GeneralConfiguration. Anti-ftmodeblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Security/AntiTheftMode

### <a name="windows10generalconfigurationappmanagementmsiallowusercontroloverinstall"></a>Windows10GeneralConfiguration. appmanagementmsizuweisung wusercontroloverinstall 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/MSIAllowUserControlOverInstall

### <a name="windows10generalconfigurationappmanagementmsialwaysinstallwithelevatedprivileges"></a>Windows10GeneralConfiguration. appmanagementmsialwaysinstallwithelevatedprivileges 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges

### <a name="windows10generalconfigurationappsallowtrustedappssideloading"></a>Windows10GeneralConfiguration. appsallowtreuhändappssideloading 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/AllowAllTrustedApps

### <a name="windows10generalconfigurationappsblockwindowsstoreoriginatedapps"></a>Windows10GeneralConfiguration. appsblockwindowsstoreoriginatedapps 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/DisableStoreOriginatedApps

### <a name="windows10generalconfigurationappsmicrosoftaccountsoptional"></a>Windows10GeneralConfiguration. appsmicrosoftaccountoptional 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/AppRuntime/AllowMicrosoftAccountsToBeOptional

### <a name="windows10generalconfigurationassignedaccessmultimodeprofiles"></a>Windows10GeneralConfiguration. assignedaccessmultimodeprofiles 
**CSP**:./Device/Vendor/MSFT/AssignedAccess  
**Offset-URI**:/Konfiguration

### <a name="windows10generalconfigurationassignedaccesssinglemodeappusermodelid"></a>Windows10GeneralConfiguration. assignedaccesssinglemodeappusermodelid 
**CSP**:./Device/Vendor/MSFT/AssignedAccess  
**Offset-URI**:/Konfiguration

### <a name="windows10generalconfigurationassignedaccesssinglemodeusername"></a>Windows10GeneralConfiguration. assignedaccesssinglemudeusername 
**CSP**:./Device/Vendor/MSFT/AssignedAccess  
**Offset-URI**:/Konfiguration

### <a name="windows10generalconfigurationauthenticationallowfidodevice"></a>Windows10GeneralConfiguration. authenticationallowfdodevice 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/authentication/AllowFidoDeviceSignon

### <a name="windows10generalconfigurationauthenticationallowsecondarydevice"></a>Windows10GeneralConfiguration. authenticationallowsecondarydevice 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/authentication/AllowSecondaryAuthenticationDevice

### <a name="windows10generalconfigurationauthenticationpreferredazureadtenantdomainname"></a>Windows10GeneralConfiguration. authenticationpreferdomazuread tenantdomainname 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/authentication/PreferredAadTenantDomainName

### <a name="windows10generalconfigurationauthenticationwebsignin"></a>Windows10GeneralConfiguration. authenticationwebsignin 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/authentication/EnableWebSignIn

### <a name="windows10generalconfigurationautoplaydefaultautorunbehavior"></a>Windows10GeneralConfiguration. autoplaydefaultautor unbehavior 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/AutoPlay/SetDefaultAutoRunBehavior

### <a name="windows10generalconfigurationautoplayfornonvolumedevices"></a>Windows10GeneralConfiguration. autoplayfornonvolumedevices 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/AutoPlay/DisallowAutoplayForNonVolumeDevices

### <a name="windows10generalconfigurationautoplaymode"></a>Windows10GeneralConfiguration. autoplaymode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/AutoPlay/TurnOffAutoPlay

### <a name="windows10generalconfigurationbluetoothallowedservices"></a>Windows10GeneralConfiguration. bluetoothzuweisung 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Bluetooth/ServicesAllowedList

### <a name="windows10generalconfigurationbluetoothblockadvertising"></a>Windows10GeneralConfiguration. bluetoothblockadvertising 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Bluetooth/AllowAdvertising

### <a name="windows10generalconfigurationbluetoothblockdiscoverablemode"></a>Windows10GeneralConfiguration. bluetoothblockdiscoverablemode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Bluetooth/AllowDiscoverableMode

### <a name="windows10generalconfigurationbluetoothblocked"></a>Windows10GeneralConfiguration. bluetoothblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/AllowBluetooth

### <a name="windows10generalconfigurationbluetoothblockprepairing"></a>Windows10GeneralConfiguration. bluetoothblockprekopplung 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Bluetooth/AllowPrepairing

### <a name="windows10generalconfigurationbluetoothblockpromptedproximalconnections"></a>Windows10GeneralConfiguration. bluetoothblockpromptedproximalconnections 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Bluetooth/AllowPromptedProximalConnections

### <a name="windows10generalconfigurationbluetoothdevicename"></a>Windows10GeneralConfiguration. bluetoothdevicename 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Bluetooth/LocalDeviceName

### <a name="windows10generalconfigurationbootstartdriverinitialization"></a>windows10generalconfiguration. bootstartdriverinitialization 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/System/BootStartDriverInitialization

### <a name="windows10generalconfigurationcamerablocked"></a>Windows10GeneralConfiguration. camerablocked 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Camera/AllowCamera

### <a name="windows10generalconfigurationcellularblockdatawhenroaming"></a>Windows10GeneralConfiguration. cellularblockdata-Roaming 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/AllowCellularDataRoaming

### <a name="windows10generalconfigurationcellularblockvpn"></a>Windows10GeneralConfiguration. cellularblockvpn 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/AllowVPNOverCellular

### <a name="windows10generalconfigurationcellularblockvpnwhenroaming"></a>Windows10GeneralConfiguration. cellularblockvpndas Roaming 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/AllowVPNRoamingOverCellular

### <a name="windows10generalconfigurationcellulardata"></a>Windows10GeneralConfiguration. cellulardata 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/AllowCellularData

### <a name="windows10generalconfigurationcertificatesblockmanualrootcertificateinstallation"></a>Windows10GeneralConfiguration. Certifi-blockmanualrootcertifi-Installationsdatei 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Security/AllowManualRootCertificateInstallation

### <a name="windows10generalconfigurationconnecteddevicesserviceblocked"></a>Windows10GeneralConfiguration. connectedbinvicesserviceblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/AllowConnectedDevices

### <a name="windows10generalconfigurationcopypasteblocked"></a>Windows10GeneralConfiguration. copypasteblockiert 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowCopyPaste

### <a name="windows10generalconfigurationcortanablocked"></a>Windows10GeneralConfiguration. cortanablock 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/AboveLock/AllowCortanaAboveLock

### <a name="windows10generalconfigurationcryptographyallowfipsalgorithmpolicy"></a>Windows10GeneralConfiguration. cryptographyallowfpsalgorithmpolicy 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Cryptography/AllowFipsAlgorithmPolicy

### <a name="windows10generalconfigurationdataprotectionblockdirectmemoryaccess"></a>Windows10GeneralConfiguration. dataschutzblockdirectmemoryaccess 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DataProtection/AllowDirectMemoryAccess

### <a name="windows10generalconfigurationdefenderblockenduseraccess"></a>Windows10GeneralConfiguration. defenderblockenduseraccess 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowUserUIAccess

### <a name="windows10generalconfigurationdefenderblockonaccessprotection"></a>Windows10GeneralConfiguration. defenderblockonaccessprotection 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowOnAccessProtection

### <a name="windows10generalconfigurationdefendercloudblocklevel"></a>Windows10GeneralConfiguration. defendercloudblocklevel 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/CloudBlockLevel

### <a name="windows10generalconfigurationdefendercloudextendedtimeout"></a>Windows10GeneralConfiguration. defendercloudextendedtimeout 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/CloudExtendedTimeout

### <a name="windows10generalconfigurationdefendercloudextendedtimeoutinseconds"></a>Windows10GeneralConfiguration. defendercloudextendecodtimeoutinseconds 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/CloudExtendedTimeout

### <a name="windows10generalconfigurationdefenderdaysbeforedeletingquarantinedmalware"></a>Windows10GeneralConfiguration. defenderdaysbeforedelta etingquarantinedmalware 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/DaysToRetainCleanedMalware

### <a name="windows10generalconfigurationdefenderdetectedmalwareactions"></a>Windows10GeneralConfiguration. defenderdetectedmalwareactions 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/ThreatSeverityDefaultAction

### <a name="windows10generalconfigurationdefenderfileextensionstoexclude"></a>Windows10GeneralConfiguration. defenderfileextensionstoexclude 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/ExcludedExtensions

### <a name="windows10generalconfigurationdefenderfilesandfolderstoexclude"></a>Windows10GeneralConfiguration. defenderfilesandfolderstoexclude 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/ExcludedPaths

### <a name="windows10generalconfigurationdefendermonitorfileactivity"></a>Windows10GeneralConfiguration. defendermonitorfileactivity 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowRealtimeMonitoring

### <a name="windows10generalconfigurationdefenderpotentiallyunwantedappaction"></a>Windows10GeneralConfiguration. defenderpotenziallyunwantedappaction 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/PUAProtection

### <a name="windows10generalconfigurationdefenderpotentiallyunwantedappactionsetting"></a>Windows10GeneralConfiguration. defenderpotenziallyunwantedappaktionseinstellung 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/PUAProtection

### <a name="windows10generalconfigurationdefenderprocessestoexclude"></a>Windows10GeneralConfiguration. defenderprocessstoexclude 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/ExcludedProcesses

### <a name="windows10generalconfigurationdefenderpromptforsamplesubmission"></a>Windows10GeneralConfiguration. defenderpromptforsamplesubmission 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/SubmitSamplesConsent

### <a name="windows10generalconfigurationdefenderrequirebehaviormonitoring"></a>Windows10GeneralConfiguration. defenderrequirements verhalormonitoring 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowBehaviorMonitoring

### <a name="windows10generalconfigurationdefenderrequirecloudprotection"></a>Windows10GeneralConfiguration. defenderrequirecloudprotection 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowCloudProtection

### <a name="windows10generalconfigurationdefenderrequirenetworkinspectionsystem"></a>Windows10GeneralConfiguration. defenderrequunenetworkinspectionsystem 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowIntrusionPreventionSystem

### <a name="windows10generalconfigurationdefenderrequirerealtimemonitoring"></a>Windows10GeneralConfiguration. defenderrequnererealtimemonitoring 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowRealtimeMonitoring

### <a name="windows10generalconfigurationdefenderscanarchivefiles"></a>Windows10GeneralConfiguration. defenderscanarchivefiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowArchiveScanning

### <a name="windows10generalconfigurationdefenderscandownloads"></a>Windows10GeneralConfiguration. defenderscandownloads 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowIOAVProtection

### <a name="windows10generalconfigurationdefenderscanincomingmail"></a>Windows10GeneralConfiguration. defenderscanincomingmail 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowScanningNetworkFiles

### <a name="windows10generalconfigurationdefenderscanmappednetworkdrivesduringfullscan"></a>Windows10GeneralConfiguration. defenderscanmappednetworkdrivesduringfullscan 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowFullScanOnMappedNetworkDrives

### <a name="windows10generalconfigurationdefenderscanmaxcpu"></a>Windows10GeneralConfiguration. defenderscanmaxcpu 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AvgCPULoadFactor

### <a name="windows10generalconfigurationdefenderscannetworkfiles"></a>Windows10GeneralConfiguration. defenderscannetworkfiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowScanningNetworkFiles

### <a name="windows10generalconfigurationdefenderscanremovabledrivesduringfullscan"></a>Windows10GeneralConfiguration. defenderscanremovabledrivesduringfullscan 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowFullScanRemovableDriveScanning

### <a name="windows10generalconfigurationdefenderscanscriptsloadedininternetexplorer"></a>Windows10GeneralConfiguration. defenderscanscriptloadedininternetexplorer 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/AllowScriptScanning

### <a name="windows10generalconfigurationdefenderscantype"></a>Windows10GeneralConfiguration. defenderscantype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/ScanParameter

### <a name="windows10generalconfigurationdefenderscheduledquickscantime"></a>Windows10GeneralConfiguration. defenderscheduledquickscantime 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/ScheduleQuickScanTime

### <a name="windows10generalconfigurationdefenderscheduledscantime"></a>Windows10GeneralConfiguration. defenderscheduledscantime 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/ScheduleScanTime

### <a name="windows10generalconfigurationdefenderschedulescanday"></a>Windows10GeneralConfiguration. defenderschedulescanday 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/ScheduleScanDay

### <a name="windows10generalconfigurationdefendersignatureupdateintervalinhours"></a>Windows10GeneralConfiguration. defendersignatureupdateintervalinhours 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/SignatureUpdateInterval

### <a name="windows10generalconfigurationdefendersubmitsamplesconsenttype"></a>Windows10GeneralConfiguration. defendersubmitsampleseinvernehmtype 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/SubmitSamplesConsent

### <a name="windows10generalconfigurationdefendersystemscanschedule"></a>Windows10GeneralConfiguration. defendersystemscanschedule 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Defender/ScheduleScanDay

### <a name="windows10generalconfigurationdeveloperunlocksetting"></a>Windows10GeneralConfiguration. developerunlocksetting 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/AllowDeveloperUnlock

### <a name="windows10generalconfigurationdevicemanagementblockfactoryresetonmobile"></a>Windows10GeneralConfiguration. Geräte-Manager-Paket-Manager 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/System/AllowUserToResetPhone

### <a name="windows10generalconfigurationdevicemanagementblockmanualunenroll"></a>Windows10GeneralConfiguration. Debug-agementblockmanualdereroll 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowManualMDMUnenrollment

### <a name="windows10generalconfigurationdiagnosticsdatasubmissionmode"></a>Windows10GeneralConfiguration. diagnosticsdatasubmissionmode 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/System/AllowTelemetry

### <a name="windows10generalconfigurationdisplayapplistwithgdidpiscalingturnedoff"></a>Windows10GeneralConfiguration. displayapplistwithgdidpiscalingturnetdoff 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Display/TurnOffGdiDPIScalingForApps

### <a name="windows10generalconfigurationdisplayapplistwithgdidpiscalingturnedon"></a>Windows10GeneralConfiguration. displayapplistwithgdidpiscalingturnetdon 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Display/TurnOnGdiDPIScalingForApps

### <a name="windows10generalconfigurationedgeallowstartpagesmodification"></a>Windows10GeneralConfiguration. edgeallowstarttabgesmodifizierung 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/HomePages

### <a name="windows10generalconfigurationedgeblockaccesstoaboutflags"></a>Windows10GeneralConfiguration. edgeblockaccesstoaboutflags 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/PreventAccessToAboutFlagsInMicrosoftEdge

### <a name="windows10generalconfigurationedgeblockaddressbardropdown"></a>Windows10GeneralConfiguration. edgeblockaddressbardropdown 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowAddressBarDropdown

### <a name="windows10generalconfigurationedgeblockautofill"></a>Windows10GeneralConfiguration. edgeblockautofill 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowAutofill

### <a name="windows10generalconfigurationedgeblockcompatibilitylist"></a>Windows10GeneralConfiguration. edgeblockcompatibilitylist 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowMicrosoftCompatibilityList

### <a name="windows10generalconfigurationedgeblockdevelopertools"></a>Windows10GeneralConfiguration. edgeblockdevelopopertools 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowDeveloperTools

### <a name="windows10generalconfigurationedgeblocked"></a>Windows10GeneralConfiguration. edgeblocked 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowBrowser

### <a name="windows10generalconfigurationedgeblockeditfavorites"></a>Windows10GeneralConfiguration. edgeblockeditfavoriten 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/LockdownFavorites

### <a name="windows10generalconfigurationedgeblockextensions"></a>Windows10GeneralConfiguration. edgeblockextensions 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowExtensions

### <a name="windows10generalconfigurationedgeblockfullscreenmode"></a>Windows10GeneralConfiguration. edgeblockfullscreenmode 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowFullScreenMode

### <a name="windows10generalconfigurationedgeblockinprivatebrowsing"></a>Windows10GeneralConfiguration. edgeblockinprivatebrowsing 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowInPrivate

### <a name="windows10generalconfigurationedgeblocklivetiledatacollection"></a>Windows10GeneralConfiguration. edgeblocklivetiledatacollection 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/PreventLiveTileDataCollection

### <a name="windows10generalconfigurationedgeblockpasswordmanager"></a>Windows10GeneralConfiguration. edgeblockpasswordmanager 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowPasswordManager

### <a name="windows10generalconfigurationedgeblockpopups"></a>Windows10GeneralConfiguration. edgeblockpopups 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowPopups

### <a name="windows10generalconfigurationedgeblockprelaunch"></a>Windows10GeneralConfiguration. edgeblockprelaunch 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowPrelaunch

### <a name="windows10generalconfigurationedgeblockprinting"></a>Windows10GeneralConfiguration. edgeblockprinting 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowPrinting

### <a name="windows10generalconfigurationedgeblocksavinghistory"></a>Windows10GeneralConfiguration. edgeblocksavinghistory 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowSavingHistory

### <a name="windows10generalconfigurationedgeblocksearchsuggestions"></a>Windows10GeneralConfiguration. edgeblocksearchvorschläge 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowSearchSuggestionsinAddressBar

### <a name="windows10generalconfigurationedgeblocksendingdonottrackheader"></a>Windows10GeneralConfiguration. edgeblocksendingdonottrackheader 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowDoNotTrack

### <a name="windows10generalconfigurationedgeblocksendingintranettraffictointernetexplorer"></a>Windows10GeneralConfiguration. edgeblocksendingintranettrafficuminternetexplorer 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/SendIntranetTraffictoInternetExplorer

### <a name="windows10generalconfigurationedgeblocksideloadingextensions"></a>Windows10GeneralConfiguration. edgeblocksideloadingextensions 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowSideloadingOfExtensions

### <a name="windows10generalconfigurationedgeblocktabpreloading"></a>Windows10GeneralConfiguration. edgeblocktabpreload 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowTabPreloading

### <a name="windows10generalconfigurationedgeblockwebcontentonnewtabpage"></a>Windows10GeneralConfiguration. edgeblockwebcontentonnewtabpage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowWebContentOnNewTabPage

### <a name="windows10generalconfigurationedgeclearbrowsingdataonexit"></a>Windows10GeneralConfiguration. edgeclearbrowsingdataonexit 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/ClearBrowsingDataOnExit

### <a name="windows10generalconfigurationedgecookiepolicy"></a>Windows10GeneralConfiguration. edgecookiepolicy 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/allowCookies

### <a name="windows10generalconfigurationedgedisablefirstrunpage"></a>Windows10GeneralConfiguration. edgedisablefirstrauunpage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/PreventFirstRunPage

### <a name="windows10generalconfigurationedgeenterprisemodesitelistlocation"></a>Windows10GeneralConfiguration. edgeenterpriablagetelistlocation 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/EnterpriseSiteListServiceUrl

### <a name="windows10generalconfigurationedgefavoritesbarvisibility"></a>Windows10GeneralConfiguration. edgefavoritesbarvisibility 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/ConfigureFavoritesBar

### <a name="windows10generalconfigurationedgefavoriteslistlocation"></a>Windows10GeneralConfiguration. edgefavoriteslistlocation 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/ProvisionFavorites

### <a name="windows10generalconfigurationedgefirstrunurl"></a>Windows10GeneralConfiguration. edgefirstranunurl 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/FirstRunURL

### <a name="windows10generalconfigurationedgehomebuttonconfiguration"></a>Windows10GeneralConfiguration. edgehomebuttonconfiguration 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/SetHomeButtonURL

### <a name="windows10generalconfigurationedgehomebuttonconfigurationenabled"></a>Windows10GeneralConfiguration. edgehomebuttonconfigurationaktivierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/ConfigureHomeButton

### <a name="windows10generalconfigurationedgehomepageurls"></a>Windows10GeneralConfiguration. edgehomepageurls 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/SetHomeButtonURL

### <a name="windows10generalconfigurationedgenewtabpageurl"></a>Windows10GeneralConfiguration. edgenewtabpageurl 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/SetNewTabPageURL

### <a name="windows10generalconfigurationedgeopenswith"></a>Windows10GeneralConfiguration. edgeopenswith 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/ConfigureOpenMicrosoftEdgeWith

### <a name="windows10generalconfigurationedgepreventcertificateerroroverride"></a>Windows10GeneralConfiguration. edgepreventcertificateerroroverride 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/PreventCertErrorOverrides

### <a name="windows10generalconfigurationedgerequiresmartscreen"></a>Windows10GeneralConfiguration. edgerequiresmartscreen 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/AllowSmartScreen

### <a name="windows10generalconfigurationedgesearchengine"></a>Windows10GeneralConfiguration. edgesearchengine 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/SetDefaultSearchEngine

### <a name="windows10generalconfigurationedgesendintranettraffictointernetexplorer"></a>Windows10GeneralConfiguration. edgesendintranettrafficdeinternetexplorer 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/SendIntranetTraffictoInternetExplorer

### <a name="windows10generalconfigurationedgeshowmessagewhenopeninginternetexplorersites"></a>Windows10GeneralConfiguration. edgeshowmessagevon openinginternetexplorersites 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/ShowMessageWhenOpeningSitesInInternetExplorer

### <a name="windows10generalconfigurationedgesyncfavoriteswithinternetexplorer"></a>Windows10GeneralConfiguration. edgesyncfavoriteswithinternetexplorer 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/SyncFavoritesBetweenIEAndMicrosoftEdge

### <a name="windows10generalconfigurationedgetelemetryformicrosoft365analytics"></a>Windows10GeneralConfiguration.EdgeTelemetryForMicrosoft365Analytics 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/ConfigureTelemetryForMicrosoft365Analytics

### <a name="windows10generalconfigurationenableautomaticredeployment"></a>Windows10GeneralConfiguration. enableautomatikredeployment 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/CredentialProviders/DisableAutomaticReDeploymentCredentials

### <a name="windows10generalconfigurationenterprisecloudprintdiscoveryendpoint"></a>Windows10GeneralConfiguration. enterpritencloudprintdiscoveryendpoint 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint

### <a name="windows10generalconfigurationenterprisecloudprintdiscoverymaxlimit"></a>Windows10GeneralConfiguration. enterpriscloudprintdiscoverymaxlimit 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit

### <a name="windows10generalconfigurationenterprisecloudprintmopriadiscoveryresourceidentifier"></a>Windows10GeneralConfiguration. enterprigcloudprintmopriadiscoveryresourceidentifier 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/EnterpriseCloudPrint/MopriaDiscoveryResourceId

### <a name="windows10generalconfigurationenterprisecloudprintoauthauthority"></a>Windows10GeneralConfiguration. enterpriseemcloudprintoauthauthority 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/EnterpriseCloudPrint/CloudPrintOAuthAuthority

### <a name="windows10generalconfigurationenterprisecloudprintoauthclientidentifier"></a>Windows10GeneralConfiguration. enterprilcloudprintauthclientidentifier 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/EnterpriseCloudPrint/CloudPrintOAuthAuthority

### <a name="windows10generalconfigurationenterprisecloudprintresourceidentifier"></a>Windows10GeneralConfiguration. enterprigcloudprintresourceidentifier 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/EnterpriseCloudPrint/CloudPrintResourceId

### <a name="windows10generalconfigurationexperienceblockconsumerspecificfeatures"></a>Windows10GeneralConfiguration. experiendceblockconsumerspecificfeatures 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowWindowsConsumerFeatures

### <a name="windows10generalconfigurationexperienceblockdevicediscovery"></a>Windows10GeneralConfiguration. experierceblockdevicediscovery 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowDeviceDiscovery

### <a name="windows10generalconfigurationexperienceblockerrordialogwhennosim"></a>Windows10GeneralConfiguration. experierceblockerrordialogeinnosim 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowSIMErrorDialogPromptWhenNoSIM

### <a name="windows10generalconfigurationexperienceblocktaskswitcher"></a>Windows10GeneralConfiguration. experierceblocktaskswitcher 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowTaskSwitcher

### <a name="windows10generalconfigurationexperienceblockwindowsspotlight"></a>Windows10GeneralConfiguration. experierceblockwindowsspotlight 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowWindowsSpotlight

### <a name="windows10generalconfigurationexperiencedonotsyncbrowsersettings"></a>Windows10GeneralConfiguration. experiendcedonotsyncbrowsersettings 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/DoNotSyncBrowserSettings

### <a name="windows10generalconfigurationgamedvrblocked"></a>Windows10GeneralConfiguration. gamedvrblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/AllowGameDVR

### <a name="windows10generalconfigurationhardwaredeviceinstallationbydeviceidentifiers"></a>Windows10GeneralConfiguration. hardwaredeviceingestallationbydeviceidentifier 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceInstallation/PreventInstallationOfMatchingDeviceIDs

### <a name="windows10generalconfigurationhardwaredeviceinstallationbysetupclasses"></a>Windows10GeneralConfiguration. hardwaredeviceinstallationbysetupclasses 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceInstallation/PreventInstallationOfMatchingDeviceSetupClasses

### <a name="windows10generalconfigurationinkworkspaceaccess"></a>Windows10GeneralConfiguration. inkworkspaceaccess 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsInkWorkspace/AllowWindowsInkWorkspace

### <a name="windows10generalconfigurationinkworkspaceaccessstate"></a>Windows10GeneralConfiguration. inkworkspaceaccessstate 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsInkWorkspace/AllowWindowsInkWorkspace

### <a name="windows10generalconfigurationinkworkspaceblocksuggestedapps"></a>Windows10GeneralConfiguration. inkworkspaceblockvorschlags stedapps 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsInkWorkspace/AllowSuggestedAppsInWindowsInkWorkspace

### <a name="windows10generalconfigurationinternetexploreractivexcontrolsinprotectedmode"></a>Windows10GeneralConfiguration. internetexploreractivexcontrolsinprotectedmode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DoNotAllowActiveXControlsInProtectedMode

### <a name="windows10generalconfigurationinternetexplorerautocomplete"></a>Windows10GeneralConfiguration. internetexplorerautocomplete 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/AllowAutoComplete

### <a name="windows10generalconfigurationinternetexplorerblockoutdatedactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerblockoutdatedactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DoNotBlockOutdatedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerbypasssmartscreenwarnings"></a>Windows10GeneralConfiguration. internetexplorerbypasssmartscreenwarning 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DisableBypassOfSmartScreenWarnings

### <a name="windows10generalconfigurationinternetexplorerbypasssmartscreenwarningsaboutuncommonfiles"></a>Windows10GeneralConfiguration. internetexplorerbypasssmartscreenwarningsaboutuncommonfiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DisableBypassOfSmartScreenWarningsAboutUncommonFiles

### <a name="windows10generalconfigurationinternetexplorercertificateaddressmismatchwarning"></a>Windows10GeneralConfiguration. internetexplorercertificateaddressmismatchwarning 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/AllowCertificateAddressMismatchWarning

### <a name="windows10generalconfigurationinternetexplorercheckservercertificaterevocation"></a>Windows10GeneralConfiguration. internetexplorercheckservercertificaterevokation 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/CheckServerCertificateRevocation

### <a name="windows10generalconfigurationinternetexplorerchecksignaturesondownloadedprograms"></a>Windows10GeneralConfiguration. internetexplorerchecksignaturesondownloader-Programme 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/CheckSignaturesOnDownloadedPrograms

### <a name="windows10generalconfigurationinternetexplorercrashdetection"></a>Windows10GeneralConfiguration. internetexplorercrash-Erkennung 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DisableCrashDetection

### <a name="windows10generalconfigurationinternetexplorerdisableprocessesinenhancedprotectedmode"></a>Windows10GeneralConfiguration. internetexplorerdisableprocessesinenhancedprotectedmode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DisableProcessesInEnhancedProtectedMode

### <a name="windows10generalconfigurationinternetexplorerdownloadenclosures"></a>Windows10GeneralConfiguration. internetexplorerdownloader 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DisableEnclosureDownloading

### <a name="windows10generalconfigurationinternetexplorerencryptionsupport"></a>Windows10GeneralConfiguration. internetexplorerverschlüsseltionsupport 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DisableEncryptionSupport

### <a name="windows10generalconfigurationinternetexplorerenhancedprotectedmode"></a>Windows10GeneralConfiguration. internetexplorerenhancedprotectedmode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/AllowEnhancedProtectedMode

### <a name="windows10generalconfigurationinternetexplorerfallbacktossl3"></a>Windows10GeneralConfiguration.InternetExplorerFallbackToSsl3 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/AllowFallbackToSSL3

### <a name="windows10generalconfigurationinternetexplorerignorecertificateerrors"></a>Windows10GeneralConfiguration. internetexplorerignorecertificateerrors 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DisableIgnoringCertificateErrors

### <a name="windows10generalconfigurationinternetexplorerincludeallnetworkpaths"></a>Windows10GeneralConfiguration. internetexplorerincluentallnetworkpath 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/IncludeAllNetworkPaths

### <a name="windows10generalconfigurationinternetexplorerinternetzoneaccesstodatasources"></a>Windows10GeneralConfiguration. internetexplorerinternetoneaccesstodatasources 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowAccessToDataSources

### <a name="windows10generalconfigurationinternetexplorerinternetzoneallowonlyapproveddomainstouseactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerinternetzonezuweilyapproveddomainstoulactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowOnlyApprovedDomainsToUseActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzoneallowonlyapproveddomainstousetdcactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerinternetzoneexpwonlyapproveddomainstousetdcactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowOnlyApprovedDomainsToUseTDCActiveXControl

### <a name="windows10generalconfigurationinternetexplorerinternetzoneallowvbscripttorun"></a>Windows10GeneralConfiguration. internetexplorerinternetoneallowvbscripttorun 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowVBScriptToRunInInternetExplorer

### <a name="windows10generalconfigurationinternetexplorerinternetzoneautomaticpromptforfiledownloads"></a>Windows10GeneralConfiguration. internetexplorerinternetzoneautomaticpromptforfiledownloads 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowAutomaticPromptingForFileDownloads

### <a name="windows10generalconfigurationinternetexplorerinternetzonecopyandpasteviascript"></a>Windows10GeneralConfiguration. internetexplorerinternetzonecopyandpasteviascript 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowCopyPasteViaScript

### <a name="windows10generalconfigurationinternetexplorerinternetzonecrosssitescriptingfilter"></a>Windows10GeneralConfiguration. internetexplorerinternetrosssitescriptingfilter 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneEnableCrossSiteScriptingFilter

### <a name="windows10generalconfigurationinternetexplorerinternetzonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerinternetzonedonotrunantimalwareagainstactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonedotnetframeworkreliantcomponents"></a>Windows10GeneralConfiguration. internetexplorerinternetzonedotnetframeworkreliantcomponents 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowNETFrameworkReliantComponents

### <a name="windows10generalconfigurationinternetexplorerinternetzonedownloadsignedactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerinternetzdownloadsignedactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneDownloadSignedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonedownloadunsignedactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerinternetzdownloadunsignedactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneDownloadUnsignedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonedraganddroporcopyandpastefiles"></a>Windows10GeneralConfiguration. internetexplorerinternetzonedraganddroporcopyandpastefiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowDragAndDropCopyAndPasteFiles

### <a name="windows10generalconfigurationinternetexplorerinternetzonedragcontentfromdifferentdomainsacrosswindows"></a>Windows10GeneralConfiguration. internetexplorerinternetzonedragcontentfromdifferenentdomainsacrosswindows 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneEnableDraggingOfContentFromDifferentDomainsAcrossWindows

### <a name="windows10generalconfigurationinternetexplorerinternetzonedragcontentfromdifferentdomainswithinwindows"></a>Windows10GeneralConfiguration. internetexplorerinternetzonedragcontentfromdifferenentdomainswithinwindows 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneEnableDraggingOfContentFromDifferentDomainsWithinWindows

### <a name="windows10generalconfigurationinternetexplorerinternetzoneincludelocalpathwhenuploadingfilestoserver"></a>Windows10GeneralConfiguration. internetexplorerinternetzoneincludelta Server-Datei 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneIncludeLocalPathWhenUploadingFilesToServer

### <a name="windows10generalconfigurationinternetexplorerinternetzoneinitializeandscriptactivexcontrolsnotmarkedassafe"></a>Windows10GeneralConfiguration. internetexplorerinternetzoneinitializeandscriptactivexcontrolsnotmarkedassafe 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneInitializeAndScriptActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonejavapermissions"></a>Windows10GeneralConfiguration. internetexplorerinternetzonejavaberechtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneJavaPermissions


### <a name="windows10generalconfigurationinternetexplorerinternetzonelaunchapplicationsandfilesinaniframe"></a>Windows10GeneralConfiguration. internetexplorerinternetonelaunchapplicationsandfilesinaniframe 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneLaunchingApplicationsAndFilesInIFRAME

### <a name="windows10generalconfigurationinternetexplorerinternetzonelessprivilegedsites"></a>Windows10GeneralConfiguration. internetexplorerinternetzonelessprivilegedsites 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowLessPrivilegedSites

### <a name="windows10generalconfigurationinternetexplorerinternetzoneloadingofxamlfiles"></a>Windows10GeneralConfiguration. internetexplorerinternetzoneloadingofxamlfiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowLoadingOfXAMLFiles

### <a name="windows10generalconfigurationinternetexplorerinternetzonelogonoptions"></a>Windows10GeneralConfiguration. internetexplorerinternetzonelogonoptions 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneLogonOptions

### <a name="windows10generalconfigurationinternetexplorerinternetzonenavigatewindowsandframesacrossdifferentdomains"></a>Windows10GeneralConfiguration. internetexplorerinternetzonsavigatewindowsandframesacrossdifferenentdomains 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneNavigateWindowsAndFrames

### <a name="windows10generalconfigurationinternetexplorerinternetzonepopupblocker"></a>Windows10GeneralConfiguration. internetexplorerinternetzonepopupblocker 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneUsePopupBlocker

### <a name="windows10generalconfigurationinternetexplorerinternetzoneprotectedmode"></a>Windows10GeneralConfiguration. internetexplorerinternettedmode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneEnableProtectedMode

### <a name="windows10generalconfigurationinternetexplorerinternetzonerundotnetframeworkreliantcomponentssignedwithauthenticode"></a>Windows10GeneralConfiguration. internetexplorerinternetonerundotnetframeworkreliantcomponentssignedwithauthenticode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneRunNETFrameworkReliantComponentsSignedWithAuthenticode

### <a name="windows10generalconfigurationinternetexplorerinternetzonescriptingofwebbrowsercontrols"></a>Windows10GeneralConfiguration. internetexplorerinternetzonescriptingobwebbrowsercontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowScriptingOfInternetExplorerWebBrowserControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonescriptinitiatedwindows"></a>Windows10GeneralConfiguration. internetexplorerinternetonescriptinitiatedwindows 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowScriptInitiatedWindows

### <a name="windows10generalconfigurationinternetexplorerinternetzonescriptlets"></a>Windows10GeneralConfiguration. internetexplorerinternetz. criptlets 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowScriptlets

### <a name="windows10generalconfigurationinternetexplorerinternetzonesecuritywarningforpotentiallyunsafefiles"></a>Windows10GeneralConfiguration. internetexplorerinternetztenecuritywarningforpotenziallyunsafefiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneShowSecurityWarningForPotentiallyUnsafeFiles

### <a name="windows10generalconfigurationinternetexplorerinternetzonesmartscreen"></a>Windows10GeneralConfiguration. internetexplorerinternetonesmartscreen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowSmartScreenIE

### <a name="windows10generalconfigurationinternetexplorerinternetzoneupdatestostatusbarviascript"></a>Windows10GeneralConfiguration. internetexplorerinternetoneupdatestostatobarviascript 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowUpdatesToStatusBarViaScript

### <a name="windows10generalconfigurationinternetexplorerinternetzoneuserdatapersistence"></a>Windows10GeneralConfiguration. internetexplorerinternetzoneuserdatapersistenz 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/InternetZoneAllowUserDataPersistence

### <a name="windows10generalconfigurationinternetexplorerintranetzonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerintranetzonedonotrunantimalwareagainstactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/IntranetZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorerintranetzoneinitializeandscriptactivexcontrolsnotmarkedassafe"></a>Windows10GeneralConfiguration. internetexplorerintranetzoneinitializeandscriptactivexcontrolsnotmarkedassafe 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/IntranetZoneInitializeAndScriptActiveXControls

### <a name="windows10generalconfigurationinternetexplorerintranetzonejavapermissions"></a>Windows10GeneralConfiguration. internetexplorerintranetzonejavaberechtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/IntranetZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlocalmachinezonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerlocalmachinezonedonotrunantimalwareagainstactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/LocalMachineZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorerlocalmachinezonejavapermissions"></a>Windows10GeneralConfiguration. internetexplorerlocalmachinezonejavaberechtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/LocalMachineZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlockeddowninternetzonesmartscreen"></a>Windows10GeneralConfiguration. internetexplorerlockeddowninternetzonesmartscreen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/LockedDownInternetZoneAllowSmartScreenIE

### <a name="windows10generalconfigurationinternetexplorerlockeddownintranetzonejavapermissions"></a>Windows10GeneralConfiguration. internetexplorerlockeddownintranetzonejava-Berechtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/LockedDownIntranetJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlockeddownlocalmachinezonejavapermissions"></a>Windows10GeneralConfiguration. internetexplorerlockeddownloader calmachinezonejavaberechtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/LockedDownLocalMachineZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlockeddownrestrictedzonejavapermissions"></a>Windows10GeneralConfiguration. internetexplorerlockeddownrestrictedzonejavaberechtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/LockedDownRestrictedSitesZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlockeddownrestrictedzonesmartscreen"></a>Windows10GeneralConfiguration. internetexplorerlockeddownrestrictedzonesmartscreen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/LockedDownRestrictedSitesZoneAllowSmartScreenIE

### <a name="windows10generalconfigurationinternetexplorerlockeddowntrustedzonejavapermissions"></a>Windows10GeneralConfiguration. internetexplorerlockeddowntreuhänder-onejava-Berechtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/LockedDownTrustedSitesZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerpreventmanagingsmartscreenfilter"></a>Windows10GeneralConfiguration. internetexplorerpreventmanagingsmartscreenfilter 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/PreventManagingSmartScreenFilter

### <a name="windows10generalconfigurationinternetexplorerpreventperuserinstallationofactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerpreventperuserinstallationofaktivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/PreventPerUserInstallationOfActiveXControls

### <a name="windows10generalconfigurationinternetexplorerprocessesconsistentmimehandling"></a>Windows10GeneralConfiguration. internetexplorerprocesseskonsistentmimehandling 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/ConsistentMimeHandlingInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesmimesniffingsafetyfeature"></a>Windows10GeneralConfiguration. internetexplorerprocessesmimesniffingsafetyfeature 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/MimeSniffingSafetyFeatureInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesmkprotocolsecurityrestriction"></a>Windows10GeneralConfiguration. internetexplorerprocessesmkprotocolsecurityeinschränkung 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/MKProtocolSecurityRestrictionInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesnotificationbar"></a>Windows10GeneralConfiguration. internetexplorerprocessesnotificationbar 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/NotificationBarInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesprotectionfromzoneelevation"></a>Windows10GeneralConfiguration. internetexplorerprocessesschutzfromzoneelevation 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/ProtectionFromZoneElevationInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesrestrictactivexinstall"></a>Windows10GeneralConfiguration. internetexplorerprocessesrestrictactivexinstall 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictActiveXInstallInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesrestrictfiledownload"></a>Windows10GeneralConfiguration. internetexplorerprocessesrestrictfiledownload 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictFileDownloadInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesscriptedwindowsecurityrestrictions"></a>Windows10GeneralConfiguration. internetexplorerprocessesscriptedwindowsecurityrestrictions 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/ScriptedWindowSecurityRestrictionsInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerremoverunthistimebuttonforoutdatedactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerremoverunthistimebuttonforoutdatedactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RemoveRunThisTimeButtonForOutdatedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneaccesstodatasources"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneaccesstodatasources 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowAccessToDataSources

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneactivescripting"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneactivescripting 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowActiveScripting

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneallowonlyapproveddomainstouseactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneexpwonlyapproveddomainstoulactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowOnlyApprovedDomainsToUseActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneallowonlyapproveddomainstousetdcactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneexpwonlyapproveddomainstousetdcactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowOnlyApprovedDomainsToUseTDCActiveXControl

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneallowvbscripttorun"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneallowvbscripttorun 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowVBScriptToRunInInternetExplorer

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneautomaticpromptforfiledownloads"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneautomaticpromptforfiledownloads 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowAutomaticPromptingForFileDownloads

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonebinaryandscriptbehaviors"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonebinaryandscriptverhaltensweisen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowBinaryAndScriptBehaviors

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonecopyandpasteviascript"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonecopyandpasteviascript 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowCopyPasteViaScript

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonecrosssitescriptingfilter"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonecrosssitescriptingfilter 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneEnableCrossSiteScriptingFilter

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonedonotrunantimalwareagainstactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedotnetframeworkreliantcomponents"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonedotnetframeworkreliantcomponents 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowNETFrameworkReliantComponents

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedownloadsignedactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonedownloadsignedactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneDownloadSignedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedownloadunsignedactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonedownloadunsignedactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneDownloadUnsignedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedraganddroporcopyandpastefiles"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonedraganddroporcopyandpastefiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowDragAndDropCopyAndPasteFiles

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedragcontentfromdifferentdomainsacrosswindows"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonedragcontentfromdifferenentdomainsacrosswindows 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneEnableDraggingOfContentFromDifferentDomainsAcrossWindows

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedragcontentfromdifferentdomainswithinwindows"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonedragcontentfromdifferenentdomainswithinwindows 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneEnableDraggingOfContentFromDifferentDomainsWithinWindows

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonefiledownloads"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonefiledownloads 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowFileDownloads

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneincludelocalpathwhenuploadingfilestoserver"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneincludelta Server-Pfad 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneIncludeLocalPathWhenUploadingFilesToServer

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneinitializeandscriptactivexcontrolsnotmarkedassafe"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneinitializeandscriptactivexcontrolsnotmarkedassafe 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneInitializeAndScriptActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonejavapermissions"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonejavaberechtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonelaunchapplicationsandfilesinaniframe"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonelaunchapplicationsandfilesinaniframe 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneLaunchingApplicationsAndFilesInIFRAME

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonelessprivilegedsites"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonelessprivilegedsites 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowLessPrivilegedSites

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneloadingofxamlfiles"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneloadingofxamlfiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowLoadingOfXAMLFiles

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonelogonoptions"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonelogonoptions 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneLogonOptions

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonemetarefresh"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonemetarefresh 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowMETAREFRESH

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonenavigatewindowsandframesacrossdifferentdomains"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonsavigatewindowsandframesacrossdifferenentdomains 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneNavigateWindowsAndFrames

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonepopupblocker"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonepopupblocker 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneUsePopupBlocker

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneprotectedmode"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneprotectedmode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneTurnOnProtectedMode

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonerunactivexcontrolsandplugins"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonerunactivexcontrolsandplugins 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneRunActiveXControlsAndPlugins

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonerundotnetframeworkreliantcomponentssignedwithauthenticode"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonerundotnetframeworkreliantcomponentssignedwithauthenticode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneRunNETFrameworkReliantComponentsSignedWithAuthenticode

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptactivexcontrolsmarkedsafeforscripting"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonescriptactivexcontrolsmarkedsafeforscripting 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneScriptActiveXControlsMarkedSafeForScripting

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptingofjavaapplets"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonescriptingof JavaApplets 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneScriptingOfJavaApplets

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptingofwebbrowsercontrols"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonescriptingof webbrowsercontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowScriptingOfInternetExplorerWebBrowserControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptinitiatedwindows"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonescriptinitiatedwindows 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowScriptInitiatedWindows

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptlets"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonescriptlets 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowScriptlets

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonesecuritywarningforpotentiallyunsafefiles"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonesecuritywarningforpotenziallyunsafefiles 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneShowSecurityWarningForPotentiallyUnsafeFiles

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonesmartscreen"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzonesmartscreen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowSmartScreenIE

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneupdatestostatusbarviascript"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneupdatestostatus barviascript 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowUpdatesToStatusBarViaScript

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneuserdatapersistence"></a>Windows10GeneralConfiguration. internetexplorerrestrictedzoneuserdatapersistenz 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/RestrictedSitesZoneAllowUserDataPersistence

### <a name="windows10generalconfigurationinternetexplorersecuritysettingscheck"></a>Windows10GeneralConfiguration. internetexplorersecuritysettingscheck 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DisableSecuritySettingsCheck

### <a name="windows10generalconfigurationinternetexplorersecurityzonesuseonlymachinesettings"></a>Windows10GeneralConfiguration. internetexplorersecurityzonesuseonlymachinesettings 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/SecurityZonesUseOnlyMachineSettings

### <a name="windows10generalconfigurationinternetexplorersoftwarewhensignatureisinvalid"></a>Windows10GeneralConfiguration. internetexplorersoftware\signatureisinvalid 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/AllowSoftwareWhenSignatureIsInvalid

### <a name="windows10generalconfigurationinternetexplorertrustedzonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration. internetexplorertreuhänder-onedonotrunantimalwareagainstactivexcontrols 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/TrustedSitesZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorertrustedzoneinitializeandscriptactivexcontrolsnotmarkedassafe"></a>Windows10GeneralConfiguration. internetexplorertreuhänder-oneinitializeandscriptactivexcontrolsnotmarkedassafe 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/TrustedSitesZoneInitializeAndScriptActiveXControls

### <a name="windows10generalconfigurationinternetexplorertrustedzonejavapermissions"></a>Windows10GeneralConfiguration. internetexplorertreuhänder-onejava-Berechtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/TrustedSitesZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexploreruseactivexinstallerservice"></a>Windows10GeneralConfiguration. internetexploreruseactivexinstallerservice 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/SpecifyUseOfActiveXInstallerService

### <a name="windows10generalconfigurationinternetexplorerusersaddingsites"></a>Windows10GeneralConfiguration. internetexplorerusersaddingsites 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DoNotAllowUsersToAddSites

### <a name="windows10generalconfigurationinternetexploreruserschangingpolicies"></a>Windows10GeneralConfiguration. internetexploreruserschangingpolicies 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/InternetExplorer/DoNotAllowUsersToChangePolicies

### <a name="windows10generalconfigurationinternetsharingblocked"></a>Windows10GeneralConfiguration. internetsharingblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/WiFi/AllowInternetSharing

### <a name="windows10generalconfigurationlocationservicesblocked"></a>Windows10GeneralConfiguration. locationservicesblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/System/AllowLocation

### <a name="windows10generalconfigurationlockscreenallowtimeoutconfiguration"></a>Windows10GeneralConfiguration. lockscreenallowtimeoutconfiguration 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/AllowScreenTimeoutWhileLockedUser/config

### <a name="windows10generalconfigurationlockscreenblockactioncenternotifications"></a>Windows10GeneralConfiguration. lockscreenblockaktioncenterbenachrichtigungen 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/AboveLock/AllowActionCenterNotifications

### <a name="windows10generalconfigurationlockscreenblockcortana"></a>Windows10GeneralConfiguration. lockscreenblockcortana 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/AboveLock/AllowCortanaAboveLock

### <a name="windows10generalconfigurationlockscreenblocktoastnotifications"></a>Windows10GeneralConfiguration. lockscreenblockdeastbenachrichtigungen 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/AboveLock/AllowToasts

### <a name="windows10generalconfigurationlockscreencamera"></a>Windows10GeneralConfiguration. lockscreencamera 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/PreventEnablingLockScreenCamera

### <a name="windows10generalconfigurationlockscreenhidenetworkselectionui"></a>Windows10GeneralConfiguration. lockscreenhidenetworkselectionui 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsLogon/DontDisplayNetworkSelectionUI

### <a name="windows10generalconfigurationlockscreenslideshow"></a>Windows10GeneralConfiguration. lockscreenslide Show 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/PreventLockScreenSlideShow

### <a name="windows10generalconfigurationlockscreentimeoutinseconds"></a>Windows10GeneralConfiguration. lockscreentimeoutinseconds 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/ScreenTimeoutWhileLocked

### <a name="windows10generalconfigurationlogonblockfastuserswitching"></a>Windows10GeneralConfiguration. logonblockfastuserswitching 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsLogon/HideFastUserSwitching

### <a name="windows10generalconfigurationmessagingblockmms"></a>Windows10GeneralConfiguration. messagingblockmms 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Messaging/AllowMMS

### <a name="windows10generalconfigurationmessagingblockrichcommunicationservices"></a>Windows10GeneralConfiguration. messagingblockrichcommunicationservices 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Messaging/AllowRCS

### <a name="windows10generalconfigurationmessagingblocksync"></a>Windows10GeneralConfiguration. messagingblocksync 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Messaging/AllowMessageSync

### <a name="windows10generalconfigurationmicrosoftaccountblocked"></a>Windows10GeneralConfiguration. microsoftaccountblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Accounts/AllowMicrosoftAccountConnection

### <a name="windows10generalconfigurationmicrosoftaccountblocksettingssync"></a>Windows10GeneralConfiguration. microsoftaccountblocksettingssync 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowSyncMySettings

### <a name="windows10generalconfigurationmicrosoftaccountsigninassistantsettings"></a>Windows10GeneralConfiguration. microsoftaccountsigninassistantsettings 
**CSP**:./Device/Vendor/MSFT/Accounts  
**Offset-URI**:/AllowMicrosoftAccountSignInAssistant

### <a name="windows10generalconfigurationnetworkproxyapplysettingsdevicewide"></a>Windows10GeneralConfiguration. networkproxyapplysettingsdevicewide 
**CSP**:./Device/Vendor/MSFT/NetworkProxy  
**Offset-URI**:/ProxySettingsPerUser

### <a name="windows10generalconfigurationnetworkproxyautomaticconfigurationurl"></a>Windows10GeneralConfiguration. networkproxyautomaticconfigurationurl 
**CSP**:./Device/Vendor/MSFT/NetworkProxy  
**Offset-URI**:/SetupScriptUrl

### <a name="windows10generalconfigurationnetworkproxydisableautodetect"></a>Windows10GeneralConfiguration. networkproxydisableautodetect 
**CSP**:./Device/Vendor/MSFT/NetworkProxy  
**Offset-URI**:/Autodetect

### <a name="windows10generalconfigurationnetworkproxyserver"></a>Windows10GeneralConfiguration. networkproxyserver 
**CSP**:./Vendor/MSFT/NetworkProxy  
**Offset-URI**:/proxyAddress,/Exceptions und/UseProxyForLocalAddresses

### <a name="windows10generalconfigurationnfcblocked"></a>Windows10GeneralConfiguration. nfcblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/AllowNFC

### <a name="windows10generalconfigurationonedrivedisablefilesync"></a>Windows10GeneralConfiguration. onedrivedisablefilesync 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/System/DisableOneDriveFileSync

### <a name="windows10generalconfigurationpasswordblocksimple"></a>Windows10GeneralConfiguration. passwordblocksimple 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/AllowSimpleDevicePassword

### <a name="windows10generalconfigurationpasswordexpirationdays"></a>Windows10GeneralConfiguration. passwordexpirationdays 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/DevicePasswordExpiration

### <a name="windows10generalconfigurationpasswordminimumageindays"></a>Windows10GeneralConfiguration. passwordminimumageindays 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/MinimumPasswordAge

### <a name="windows10generalconfigurationpasswordminimumcharactersetcount"></a>Windows10GeneralConfiguration. passwordminimumcharakterisetcount 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/MinDevicePasswordComplexCharacters

### <a name="windows10generalconfigurationpasswordminimumlength"></a>Windows10GeneralConfiguration. passwordminimumlength 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/MinDevicePasswordLength

### <a name="windows10generalconfigurationpasswordminutesofinactivitybeforescreentimeout"></a>Windows10GeneralConfiguration. passwordminutesofinactivitybeforeskreentimeout 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/MaxInactivityTimeDeviceLock

### <a name="windows10generalconfigurationpasswordpreviouspasswordblockcount"></a>Windows10GeneralConfiguration. passwordpreviouspasswordblockcount 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/DevicePasswordHistory

### <a name="windows10generalconfigurationpasswordrequired"></a>Windows10GeneralConfiguration. PasswordRequired 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/DevicePasswordEnabled

### <a name="windows10generalconfigurationpasswordrequiredtype"></a>Windows10GeneralConfiguration. passwordrequiredtype 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/AlphanumericDevicePasswordRequired

### <a name="windows10generalconfigurationpasswordrequirewhenresumefromidlestate"></a>Windows10GeneralConfiguration. passwordrequire. resumefromittellestate 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/AllowIdleReturnWithoutPassword

### <a name="windows10generalconfigurationpasswordsigninfailurecountbeforefactoryreset"></a>Windows10GeneralConfiguration. passwordsigninfailurezähltbeforefacrenyreset 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceLock/MaxDevicePasswordFailedAttempts

### <a name="windows10generalconfigurationpersonalizationdesktopimageurl"></a>Windows10GeneralConfiguration. personalizationdesktopimageurl 
**CSP**:./Device/Vendor/MSFT/Personalization  
**Offset-URI**:/DesktopImageUrl

### <a name="windows10generalconfigurationpersonalizationlockscreenimageurl"></a>Windows10GeneralConfiguration. personalizationlockscreenimageurl 
**CSP**:./Device/Vendor/MSFT/Personalization  
**Offset-URI**:/LockScreenImageUrl

### <a name="windows10generalconfigurationpowerrequirepasswordonwakewhileonbattery"></a>Windows10GeneralConfiguration. powerrequirements passwordonwakewhileonakku 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Power/RequirePasswordWhenComputerWakesOnBattery

### <a name="windows10generalconfigurationpowerrequirepasswordonwakewhilepluggedin"></a>Windows10GeneralConfiguration. powerrequirements passwordonwakewhilepluggedin 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Power/RequirePasswordWhenComputerWakesPluggedIn

### <a name="windows10generalconfigurationpowerstandbystateswhensleepingwhileonbattery"></a>Windows10GeneralConfiguration. powerstandbystaatwhensleepingwhileonakku 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Power/AllowStandbyStatesWhenSleepingOnBattery

### <a name="windows10generalconfigurationpowerstandbystateswhensleepingwhilepluggedin"></a>Windows10GeneralConfiguration. powerstandbystaatwhensleepingwhilepluggedin 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Power/AllowStandbyWhenSleepingPluggedIn

### <a name="windows10generalconfigurationpreventinstallationofmatchingdeviceids"></a>windows10generalconfiguration. preventinstallationofmatchingtoviceids 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceInstallation/PreventInstallationOfMatchingDeviceIDs

### <a name="windows10generalconfigurationpreventinstallationofmatchingdevicesetupclasses"></a>windows10generalconfiguration. preventinstallationofmatchingbinvicesetupclasses 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeviceInstallation/PreventInstallationOfMatchingDeviceSetupClasses

### <a name="windows10generalconfigurationprinterblockaddition"></a>Windows10GeneralConfiguration. printerblockaddition 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Education/PreventAddingNewPrinters

### <a name="windows10generalconfigurationprinterdefaultname"></a>Windows10GeneralConfiguration. printerdefaultname 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Education/DefaultPrinterName

### <a name="windows10generalconfigurationprinternames"></a>Windows10GeneralConfiguration. printernames 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Education/PrinterNames

### <a name="windows10generalconfigurationprivacyadvertisingid"></a>Windows10GeneralConfiguration. privacywerbung 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Privacy/DisableAdvertisingID

### <a name="windows10generalconfigurationprivacyautoacceptpairingandconsentprompts"></a>Windows10GeneralConfiguration. privacyautoakzeptpaar autoingandzustimmungs Aufforderungen 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Privacy/AllowAutoAcceptPairingAndPrivacyConsentPrompts

### <a name="windows10generalconfigurationprivacyblockactivityfeed"></a>Windows10GeneralConfiguration. privacyblockactivityfeed 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Privacy/EnableActivityFeed

### <a name="windows10generalconfigurationprivacyblockinputpersonalization"></a>Windows10GeneralConfiguration. privacyblockinputpersonalization 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Privacy/AllowInputPersonalization

### <a name="windows10generalconfigurationprivacyblockpublishuseractivities"></a>Windows10GeneralConfiguration. privacyblockpublishuseractivities 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Privacy/PublishUserActivities

### <a name="windows10generalconfigurationsafesearchfilter"></a>Windows10GeneralConfiguration. safesearchfilter 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/SafeSearchPermissions

### <a name="windows10generalconfigurationscreencaptureblocked"></a>Windows10GeneralConfiguration. screencaptureblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowScreenCapture

### <a name="windows10generalconfigurationsearchblockdiacritics"></a>Windows10GeneralConfiguration. searchblockdiakritik 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/AllowUsingDiacritics

### <a name="windows10generalconfigurationsearchblockwebresults"></a>Windows10GeneralConfiguration. searchblockwebresults 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/DoNotUseWebResults

### <a name="windows10generalconfigurationsearchdisableautolanguagedetection"></a>Windows10GeneralConfiguration. searchdisableautolanguageerkennungs 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/AlwaysUseAutoLangDetection

### <a name="windows10generalconfigurationsearchdisableindexerbackoff"></a>Windows10GeneralConfiguration. searchdisableindexerbackoff 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/DisableBackoff

### <a name="windows10generalconfigurationsearchdisableindexingencrypteditems"></a>Windows10GeneralConfiguration. searchdisableindexingencrypteditems 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/AllowIndexingEncryptedStoresOrItems

### <a name="windows10generalconfigurationsearchdisableindexingremovabledrive"></a>Windows10GeneralConfiguration. searchdisableindexingremovabledrive 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/DisableRemovableDriveIndexing

### <a name="windows10generalconfigurationsearchdisablelocation"></a>Windows10GeneralConfiguration. searchdisableloation 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/AllowSearchToUseLocation

### <a name="windows10generalconfigurationsearchdisableuselocation"></a>Windows10GeneralConfiguration. searchdisableuselokation 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/AllowSearchToUseLocation

### <a name="windows10generalconfigurationsearchenableautomaticindexsizemanangement"></a>Windows10GeneralConfiguration. searchenableautomaticindexsizemanment 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/PreventIndexingLowDiskSpaceMB

### <a name="windows10generalconfigurationsearchenableremotequeries"></a>Windows10GeneralConfiguration. searchenableremotequeries 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Search/PreventRemoteQueries

### <a name="windows10generalconfigurationsecurityblockazureadjoineddevicesautoencryption"></a>Windows10GeneralConfiguration. securityblockazulesjoinedtovicesautoencryption 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices

### <a name="windows10generalconfigurationsettingsblockaccountspage"></a>Windows10GeneralConfiguration. settingsblockaccountspage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockaddprovisioningpackage"></a>Windows10GeneralConfiguration. settingsblockaddprovisioningpackage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Security/AllowAddProvisioningPackage

### <a name="windows10generalconfigurationsettingsblockappspage"></a>Windows10GeneralConfiguration. settingsblockappspage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockchangelanguage"></a>Windows10GeneralConfiguration. settingsblockchangelanguage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/AllowLanguage

### <a name="windows10generalconfigurationsettingsblockchangepowersleep"></a>Windows10GeneralConfiguration. settingsblockchangepowersleep 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/AllowPowerSleep

### <a name="windows10generalconfigurationsettingsblockchangeregion"></a>Windows10GeneralConfiguration. settingsblockchangeregion 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/AllowRegion

### <a name="windows10generalconfigurationsettingsblockchangesystemtime"></a>Windows10GeneralConfiguration. settingsblockchangesystemtime 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/AllowDateTime

### <a name="windows10generalconfigurationsettingsblockdevicespage"></a>Windows10GeneralConfiguration. settingsblockabvicespage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockeaseofaccesspage"></a>Windows10GeneralConfiguration. settingsblockeaseofakcesspage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockeditdevicename"></a>Windows10GeneralConfiguration. settingsblockeditdevicename 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/AllowEditDeviceName

### <a name="windows10generalconfigurationsettingsblockgamingpage"></a>Windows10GeneralConfiguration. settingsblockgamingpage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblocknetworkinternetpage"></a>Windows10GeneralConfiguration. settingsblocknetworkinternetpage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockpersonalizationpage"></a>Windows10GeneralConfiguration. settingsblockpersonalizationpage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockprivacypage"></a>Windows10GeneralConfiguration. settingsblockprivacypage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockremoveprovisioningpackage"></a>Windows10GeneralConfiguration. settingsblockremoveprovisioningpackage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Security/AllowRemoveProvisioningPackage

### <a name="windows10generalconfigurationsettingsblocksystempage"></a>Windows10GeneralConfiguration. settingsblocksystempage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblocktimelanguagepage"></a>Windows10GeneralConfiguration. settingsblocktimelanguagepage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockupdatesecuritypage"></a>Windows10GeneralConfiguration. settingsblockupdatesecuritypage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationshareduserappdataallowed"></a>Windows10GeneralConfiguration. shareduserappdataallowed 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/AllowSharedUserAppData

### <a name="windows10generalconfigurationsmartscreenblockpromptoverride"></a>Windows10GeneralConfiguration. smartscreenblockpromptopverride 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/PreventSmartScreenPromptOverride

### <a name="windows10generalconfigurationsmartscreenblockpromptoverrideforfiles"></a>Windows10GeneralConfiguration. smartscreenblockprompdeverrideforfiles 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/PreventSmartScreenPromptOverrideForFiles

### <a name="windows10generalconfigurationsmartscreenenableappinstallcontrol"></a>Windows10GeneralConfiguration. smartscreenenableappinstallcontrol 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/SmartScreen/EnableAppInstallControl

### <a name="windows10generalconfigurationstartblockunpinningappsfromtaskbar"></a>Windows10GeneralConfiguration. startblockunpinningappsfromtaskbar 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/NoPinningToTaskbar

### <a name="windows10generalconfigurationstartmenuapplistvisibility"></a>Windows10GeneralConfiguration. startmenuapplistvisibility 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideAppList

### <a name="windows10generalconfigurationstartmenuhidechangeaccountsettings"></a>Windows10GeneralConfiguration. startmenuhidechangeaccountsettings 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideChangeAccountSettings

### <a name="windows10generalconfigurationstartmenuhidefrequentlyusedapps"></a>Windows10GeneralConfiguration. startmenuhidefrequentlyusedapps 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideFrequentlyUsedApps

### <a name="windows10generalconfigurationstartmenuhidehibernate"></a>Windows10GeneralConfiguration. startmenuhidehibernate 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideHibernate

### <a name="windows10generalconfigurationstartmenuhidelock"></a>Windows10GeneralConfiguration. startmenuhidelta 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideLock

### <a name="windows10generalconfigurationstartmenuhidepowerbutton"></a>Windows10GeneralConfiguration. startmenuhidepowerbutton 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HidePowerButton

### <a name="windows10generalconfigurationstartmenuhiderecentjumplists"></a>Windows10GeneralConfiguration. startmenuhiderecentjumplists 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideRecentJumplists

### <a name="windows10generalconfigurationstartmenuhiderecentlyaddedapps"></a>Windows10GeneralConfiguration. startmenuhiderecentlyaddebug 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideRecentlyAddedApps

### <a name="windows10generalconfigurationstartmenuhiderestartoptions"></a>Windows10GeneralConfiguration. startmenuhiderestartoptions 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideRestart

### <a name="windows10generalconfigurationstartmenuhideshutdown"></a>Windows10GeneralConfiguration. startmenuhideshutdown 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideShutDown

### <a name="windows10generalconfigurationstartmenuhidesignout"></a>Windows10GeneralConfiguration. startmenuhidesignout 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideSignOut

### <a name="windows10generalconfigurationstartmenuhidesleep"></a>Windows10GeneralConfiguration. startmenuhidesleep 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideSleep

### <a name="windows10generalconfigurationstartmenuhideswitchaccount"></a>Windows10GeneralConfiguration. startmenuhideswitchaccount 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideSwitchAccount

### <a name="windows10generalconfigurationstartmenuhideusertile"></a>Windows10GeneralConfiguration. startmenuhideusertile 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/HideUserTile

### <a name="windows10generalconfigurationstartmenulayoutedgeassetsxml"></a>Windows10GeneralConfiguration. startmenulayoutedgeassetxml 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/ImportEdgeAssets

### <a name="windows10generalconfigurationstartmenulayoutxml"></a>Windows10GeneralConfiguration. startmenulayoutxml 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/StartLayout

### <a name="windows10generalconfigurationstartmenumode"></a>Windows10GeneralConfiguration. startmenumode 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/ForceStartSize

### <a name="windows10generalconfigurationstartmenupinnedfolderdocuments"></a>Windows10GeneralConfiguration. startmenupinnedfolderdocuments 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderDocuments

### <a name="windows10generalconfigurationstartmenupinnedfolderdownloads"></a>Windows10GeneralConfiguration. startmenupinnedfolderdownloads 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderDownloads

### <a name="windows10generalconfigurationstartmenupinnedfolderfileexplorer"></a>Windows10GeneralConfiguration. startmenupinnedfolderfileexplorer 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderFileExplorer

### <a name="windows10generalconfigurationstartmenupinnedfolderhomegroup"></a>Windows10GeneralConfiguration. startmenupinnedfolderhomegroup 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderHomeGroup

### <a name="windows10generalconfigurationstartmenupinnedfoldermusic"></a>Windows10GeneralConfiguration. startmenupinnedfoldermusic 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderMusic

### <a name="windows10generalconfigurationstartmenupinnedfoldernetwork"></a>Windows10GeneralConfiguration. startmenupinnedfoldernetwork 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderNetwork

### <a name="windows10generalconfigurationstartmenupinnedfolderpersonalfolder"></a>Windows10GeneralConfiguration. startmenupinnedfolderpersonalordner 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderPersonalFolder

### <a name="windows10generalconfigurationstartmenupinnedfolderpictures"></a>Windows10GeneralConfiguration. startmenupinnedfolderpictures 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderPictures

### <a name="windows10generalconfigurationstartmenupinnedfoldersettings"></a>Windows10GeneralConfiguration. startmenupinnedfoldersettings 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderSettings

### <a name="windows10generalconfigurationstartmenupinnedfoldervideos"></a>Windows10GeneralConfiguration. startmenupinnedfoldervideos 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Start/AllowPinnedFolderVideos

### <a name="windows10generalconfigurationstorageblockremovablestorage"></a>Windows10GeneralConfiguration. storageblockremovablestorage 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/System/AllowStorageCard

### <a name="windows10generalconfigurationstoragerequiremobiledeviceencryption"></a>Windows10GeneralConfiguration. storagerequiremobiledeviceencryption 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Security/RequireDeviceEncryption

### <a name="windows10generalconfigurationstoragerestrictappdatatosystemvolume"></a>Windows10GeneralConfiguration. storagerestrictappdatatosystemvolume 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/RestrictAppDataToSystemVolume

### <a name="windows10generalconfigurationstoragerestrictappinstalltosystemvolume"></a>Windows10GeneralConfiguration. storagerestrictappinstallatsystemvolume 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/RestrictAppToSystemVolume

### <a name="windows10generalconfigurationsystembootstartdriverinitialization"></a>Windows10GeneralConfiguration.Systembootstartdriverinitialization 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/System/BootStartDriverInitialization

### <a name="windows10generalconfigurationsystemtelemetryproxyserver"></a>Windows10GeneralConfiguration.Systemtelemetryproxyserver 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/System/TelemetryProxy

### <a name="windows10generalconfigurationtaskmanagerblockendtask"></a>Windows10GeneralConfiguration. taskmanagerblockendtask 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Taskmanager/AllowEndTask

### <a name="windows10generalconfigurationtenantlockdownrequirenetworkduringoutofboxexperience"></a>Windows10GeneralConfiguration. tenantlockdownrequuneinetworkduringoutof-Darstellung 
**CSP**:./Vendor/MSFT/TenantLockdown  
**Offset-URI**:/RequireNetworkInOOBE

### <a name="windows10generalconfigurationusbblocked"></a>Windows10GeneralConfiguration. Startblock 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Connectivity/AllowUSBConnection

### <a name="windows10generalconfigurationvoicerecordingblocked"></a>Windows10GeneralConfiguration. voicerecordingblockierte 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowVoiceRecording

### <a name="windows10generalconfigurationwebrtcblocklocalhostipaddress"></a>Windows10GeneralConfiguration. webrtcblocklocalhostipaddress 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/PreventUsingLocalHostIPAddressForWebRTC

### <a name="windows10generalconfigurationwifiblockautomaticconnecthotspots"></a>Windows10GeneralConfiguration. wifblockautomaticconnecthotspots 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/WiFi/AllowAutoConnectToWiFiSenseHotspots

### <a name="windows10generalconfigurationwifiblocked"></a>Windows10GeneralConfiguration. wiberblockierte 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WiFi/AllowWiFi

### <a name="windows10generalconfigurationwifiblockmanualconfiguration"></a>Windows10GeneralConfiguration. wifblockmanualconfiguration 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/WiFi/AllowManualWiFi/Configuration

### <a name="windows10generalconfigurationwifiscaninterval"></a>Windows10GeneralConfiguration. wifscaninterval 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/WiFi/WLANScanMode

### <a name="windows10generalconfigurationwindowslogonlocalusersondomainjoinedcomputers"></a>Windows10GeneralConfiguration. windowslogonlocalusersondomainjoinedcomputers 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/WindowsLogon/EnumerateLocalUsersOnDomainJoinedComputers

### <a name="windows10generalconfigurationwindowsspotlightblockconsumerspecificfeatures"></a>Windows10GeneralConfiguration. windowsspotlightblockconsumerspecificfeatures 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowWindowsConsumerFeatures

### <a name="windows10generalconfigurationwindowsspotlightblocked"></a>Windows10GeneralConfiguration. windowsspotlightblockierte 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowWindowsSpotlight

### <a name="windows10generalconfigurationwindowsspotlightblockonactioncenter"></a>Windows10GeneralConfiguration. windowsspotlightblockonaktioncenter 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowWindowsSpotlightOnActionCenter

### <a name="windows10generalconfigurationwindowsspotlightblocktailoredexperiences"></a>Windows10GeneralConfiguration. windowsspotlightblocktailoredexperiences 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowTailoredExperiencesWithDiagnosticData

### <a name="windows10generalconfigurationwindowsspotlightblockthirdpartynotifications"></a>Windows10GeneralConfiguration. windowsspotlightblockthirdpartybenachrichtigungen 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowThirdPartySuggestionsInWindowsSpotlight

### <a name="windows10generalconfigurationwindowsspotlightblockwelcomeexperience"></a>Windows10GeneralConfiguration. windowsspotlightblockwelcomeerlebnis 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowWindowsSpotlightWindowsWelcomeExperience

### <a name="windows10generalconfigurationwindowsspotlightblockwindowstips"></a>Windows10GeneralConfiguration. windowsspotlightblockwindowstips 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/AllowWindowsTips

### <a name="windows10generalconfigurationwindowsspotlightconfigureonlockscreen"></a>Windows10GeneralConfiguration. windowsspotlightkonfigurieinlockscreen 
**CSP**:./User/Vendor/MSFT/Policy  
**Offset-URI**:/config/Experience/ConfigureWindowsSpotlightOnLockScreen

### <a name="windows10generalconfigurationwindowsstoreblockautoupdate"></a>Windows10GeneralConfiguration. windowsstoreblockautoupdate 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/AllowAppStoreAutoUpdate

### <a name="windows10generalconfigurationwindowsstoreblocked"></a>Windows10GeneralConfiguration. windowsstoreblockierte 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/AllowStore

### <a name="windows10generalconfigurationwindowsstoreenableprivatestoreonly"></a>Windows10GeneralConfiguration. windowsstoreenableprivatestoreonly 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/ApplicationManagement/RequirePrivateStoreOnly

### <a name="windows10generalconfigurationwirelessdisplayblockprojectiontothisdevice"></a>Windows10GeneralConfiguration. wirelessdisplayblockprojectionrethisdevice 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/WirelessDisplay/AllowProjectionToPC

### <a name="windows10generalconfigurationwirelessdisplayblockuserinputfromreceiver"></a>Windows10GeneralConfiguration. wirelessdisplayblockuserinputfromreceiver 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver

### <a name="windows10generalconfigurationwirelessdisplayrequirepinforpairing"></a>Windows10GeneralConfiguration. wirelessdisplayrequirements pinforkopplung 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/WirelessDisplay/RequirePINForPairing

### <a name="windows10networkboundaryconfigurationwindowsnetworkisolationpolicy"></a>Windows10NetworkBoundaryConfiguration. windowsnetworkisolationpolicy 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/NetworkIsolation/EnterpriseCloudResources,/config/NetworkIsolation/EnterpriseIPRange,/config/NetworkIsolation/EnterpriseIPRangesAreAuthoritative,/config/NetworkIsolation/EnterpriseInternalProxyServers,/config/NetworkIsolation/EnterpriseNetworkDomainNames,/config/NetworkIsolation/EnterpriseProxyServers,/config/NetworkIsolation/EnterpriseProxyServersAreAuthoritative,/config/NetworkIsolation/NeutralResources

### <a name="windows10policyoverrideconfigurationprefermdmovergrouppolicy"></a>Windows10PolicyOverrideConfiguration. prefermdmugrouppolicy 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/ControlPolicyConflict/MDMWinsOverGP

### <a name="windows10secureassessmentconfigurationallowprinting"></a>Windows10SecureAssessmentConfiguration. allowprinting 
**CSP**:./Vendor/MSFT/SecureAssessment  
**Offset-URI**:/RequirePrinting

### <a name="windows10secureassessmentconfigurationallowscreencapture"></a>Windows10SecureAssessmentConfiguration. allowscreencapture 
**CSP**:./Vendor/MSFT/SecureAssessment  
**Offset-URI**:/AllowScreenMonitoring

### <a name="windows10secureassessmentconfigurationallowtextsuggestion"></a>Windows10SecureAssessmentConfiguration. allowtextvorschlag 
**CSP**:./Vendor/MSFT/SecureAssessment  
**Offset-URI**:/AllowTextSuggestions

### <a name="windows10secureassessmentconfigurationconfigurationaccount"></a>Urationaccount Windows10SecureAssessmentConfiguration.Config 
**CSP**:./Vendor/MSFT/SecureAssessment  
**Offset-URI**:/TesterAccount

### <a name="windows10secureassessmentconfigurationconfigurationaccounttype"></a>Windows10SecureAssessmentConfiguration.Configurationaccounttype 
**CSP**:./Vendor/MSFT/SecureAssessment  
**Offset-URI**:/TesterAccount

### <a name="windows10secureassessmentconfigurationlaunchuri"></a>Windows10SecureAssessmentConfiguration. launchuri 
**CSP**:./Vendor/MSFT/SecureAssessment  
**Offset-URI**:/LaunchURI

### <a name="windows10teamgeneralconfigurationazureoperationalinsightsblocktelemetry"></a>Windows10TeamGeneralConfiguration. azureoperationalinsighungblocktelemetrie 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/MOMAgent/WorkspaceID und/MOMAgent/WorkspaceKey

### <a name="windows10teamgeneralconfigurationazureoperationalinsightsworkspaceid"></a>Windows10TeamGeneralConfiguration. azureoperationalinsighungworkspaceid 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/MOMAgent/WorkspaceID

### <a name="windows10teamgeneralconfigurationazureoperationalinsightsworkspacekey"></a>Windows10TeamGeneralConfiguration. azureoperationalinsightworkspacekey 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/MOMAgent/WorkspaceKey

### <a name="windows10teamgeneralconfigurationconnectappblockautolaunch"></a>Windows10TeamGeneralConfiguration. connectappblockautolaunch 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/InBoxApps/Connect/AutoLaunch

### <a name="windows10teamgeneralconfigurationdeviceaccountblockexchangeservices"></a>Windows10TeamGeneralConfiguration. deviceaccountblockexchangeservices 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/DeviceAccount/Email

### <a name="windows10teamgeneralconfigurationdeviceaccountemailaddress"></a>Windows10TeamGeneralConfiguration. deviceaccountemailaddress 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/DeviceAccount/Email

### <a name="windows10teamgeneralconfigurationdeviceaccountexchangeserveraddress"></a>Windows10TeamGeneralConfiguration. deviceaccountexchangeserveraddress 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/DeviceAccount/ExchangeServer

### <a name="windows10teamgeneralconfigurationdeviceaccountrequirepasswordrotation"></a>Windows10TeamGeneralConfiguration. deviceaccountrequirepasswordrotation 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/DeviceAccount/PasswordRotationEnabled

### <a name="windows10teamgeneralconfigurationdeviceaccountsessioninitiationprotocoladdress"></a>Windows10TeamGeneralConfiguration. deviceaccounzessioninitiationprotocoladdress 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/DeviceAccount/SipAddress

### <a name="windows10teamgeneralconfigurationmaintenancewindowblocked"></a>Windows10TeamGeneralConfiguration. maintenancewindowblockierte 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/MaintenanceHoursSimple/Hours/Duration und/MaintenanceHoursSimple/Hours/StartTime

### <a name="windows10teamgeneralconfigurationmaintenancewindowdurationinhours"></a>Windows10TeamGeneralConfiguration. maintenancewindowdurationinhours 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/MaintenanceHoursSimple/Hours/Duration

### <a name="windows10teamgeneralconfigurationmaintenancewindowstarttime"></a>Windows10TeamGeneralConfiguration. maintenancewindowstarttime 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/MaintenanceHoursSimple/Hours/StartTime

### <a name="windows10teamgeneralconfigurationmiracastblocked"></a>Windows10TeamGeneralConfiguration. miracastblockiert 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/InBoxApps/WirelessProjection/Enabled

### <a name="windows10teamgeneralconfigurationmiracastchannel"></a>Windows10TeamGeneralConfiguration. miracastchannel 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/InBoxApps/WirelessProjection/Channel

### <a name="windows10teamgeneralconfigurationmiracastrequirepin"></a>Windows10TeamGeneralConfiguration. miracastrequirepin 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/InBoxApps/WirelessProjection/PINRequired

### <a name="windows10teamgeneralconfigurationsettingsblockmymeetingsandfiles"></a>Windows10TeamGeneralConfiguration. settingsblockmymeetingsandfiles 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/Properties/DoNotShowMyMeetingsAndFiles

### <a name="windows10teamgeneralconfigurationsettingsblocksessionresume"></a>Windows10TeamGeneralConfiguration. settingsblocksessionresume 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/Properties/AllowSessionResume

### <a name="windows10teamgeneralconfigurationsettingsblocksigninsuggestions"></a>Windows10TeamGeneralConfiguration. settingsblocksigninvorschlags 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/Properties/DisableSigninSuggestions

### <a name="windows10teamgeneralconfigurationsettingsdefaultvolume"></a>Windows10TeamGeneralConfiguration. settingsdefaultvolume 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/Properties/DefaultVolume

### <a name="windows10teamgeneralconfigurationsettingsscreentimeoutinminutes"></a>Windows10TeamGeneralConfiguration. settingsskreentimeoutinminutes 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/Properties/ScreenTimeout

### <a name="windows10teamgeneralconfigurationsettingssessiontimeoutinminutes"></a>Windows10TeamGeneralConfiguration. settingssessiontimeoutinminutes 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/Properties/SessionTimeout

### <a name="windows10teamgeneralconfigurationsettingssleeptimeoutinminutes"></a>Windows10TeamGeneralConfiguration. settingssleeptimeoutinminutes 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/Properties/SleepTimeout

### <a name="windows10teamgeneralconfigurationwelcomescreenbackgroundimageurl"></a>Windows10TeamGeneralConfiguration. welcomeskreenbackgroundimageurl 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/InBoxApps/Welcome/CurrentBackgroundPath

### <a name="windows10teamgeneralconfigurationwelcomescreenblockautomaticwakeup"></a>Windows10TeamGeneralConfiguration. welcomeskreenblockautomaticwakeup 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/InBoxApps/Welcome/AutoWakeScreen

### <a name="windows10teamgeneralconfigurationwelcomescreenmeetinginformation"></a>Windows10TeamGeneralConfiguration. welcomeskreenmeetinginformation 
**CSP**:./Vendor/MSFT/SurfaceHub  
**Offset-URI**:/InBoxApps/Welcome/MeetingInfoOption

### <a name="windowsdefenderadvancedthreatprotectionconfigurationadvancedthreatprotectionoffboardingblob"></a>Windowsdefenderadvancedagentschutzconfiguration. advancedbedrohlich Protection offboardingblob 
**CSP**:./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset-URI**:/Offboarding 

### <a name="windowsdefenderadvancedthreatprotectionconfigurationadvancedthreatprotectionoffboardingfilename"></a>Windowsdefenderadvancedagentschutzconfiguration. Advanced. schutzoffboardingfilename
**CSP**:./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset-URI**:/Offboarding 

### <a name="windowsdefenderadvancedthreatprotectionconfigurationadvancedthreatprotectiononboardingblob"></a>Windowsdefenderadvancederschutzconfiguration. advancedbedrohlich schutzonboardingblob 
**CSP**:./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset-URI**:/Onboarding 

### <a name="windowsdefenderadvancedthreatprotectionconfigurationadvancedthreatprotectiononboardingfilename"></a>Windowsdefenderadvancederschützschutzconfiguration. advancedbedrohlich schutzonboardingfilename 
**CSP**:./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset-URI**:/Onboarding 

### <a name="windowsdefenderadvancedthreatprotectionconfigurationallowsamplesharing"></a>Windowsdefenderadvancederschutzconfiguration. allowsamplesharing 
**CSP**:./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset-URI**:/Configuration/SampleSharing

### <a name="windowsdefenderadvancedthreatprotectionconfigurationenableexpeditedtelemetryreporting"></a>Windowsdefenderadvancedterischutzconfiguration. enablebeschleunigten tedtelemetryreporting 
**CSP**:./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset-URI**:/Configuration/TelemetryReportingFrequency

### <a name="windowsdeliveryoptimizationconfigurationdeliveryoptimizationmode"></a>Windowsdeliveryoptimizationconfiguration. deliveryoptimizationmode 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/DeliveryOptimization/DODownloadMode

### <a name="windowsidentityprotectionconfigurationenhancedantispoofingforfacialfeaturesenabled"></a>Windowsidentityschutzconfiguration. enhancedantispoofingforfakialfeaturesenabled 
**CSP**:./Device/Vendor/MSFT/PassportForWork  
**Offset-URI**:/Biometrics/FacialFeaturesUseEnhancedAntiSpoofing

### <a name="windowsidentityprotectionconfigurationpinexpirationindays"></a>Windowsidentityschutzconfiguration. pinexpirationindays 
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/PINComplexity/expiration

### <a name="windowsidentityprotectionconfigurationpinlowercasecharactersusage"></a>Windowsidentityschutzconfiguration. pinlowercasecharakterisusage 
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/PINComplexity/LowercaseLetters

### <a name="windowsidentityprotectionconfigurationpinmaximumlength"></a>Windowsidentityschutzconfiguration. pinmaximumlength 
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/PINComplexity/MaximumPINLength

### <a name="windowsidentityprotectionconfigurationpinminimumlength"></a>Windowsidentityschutzconfiguration. pinminimumlength 
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/PINComplexity/MinimumPINLength

### <a name="windowsidentityprotectionconfigurationpinpreviousblockcount"></a>Windowsidentityschutzconfiguration. pinpreviousblockcount 
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/PINComplexity/History

### <a name="windowsidentityprotectionconfigurationpinrecoveryenabled"></a>Windowsidentityschutzconfiguration. pinwiederherstellbar 
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/EnablePinRecovery

### <a name="windowsidentityprotectionconfigurationpinspecialcharactersusage"></a>Windowsidentityschutzconfiguration. pinspecialcharakterisusage 
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/PINComplexity/SpecialCharacters

### <a name="windowsidentityprotectionconfigurationpinuppercasecharactersusage"></a>Windowsidentityschutzconfiguration. pinuppercasecharakterisusage
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/PINComplexity/UppercaseLetters

### <a name="windowsidentityprotectionconfigurationsecuritydevicerequired"></a>Windowsidentityschutzconfiguration. securitydevicerequired 
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/RequireSecurityDevice

### <a name="windowsidentityprotectionconfigurationunlockwithbiometricsenabled"></a>Windowsidentityschutzconfiguration. unlockwithbiometricsenabled 
**CSP**:./Device/Vendor/MSFT/PassportForWork  
**Offset-URI**:/Biometrics/UseBiometrics

### <a name="windowsidentityprotectionconfigurationusecertificatesforonpremisesauthenabled"></a>Windowsidentityschutzconfiguration. usecertifigateesforonpremisesauthaktivierte 
**CSP**:./Device/Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/UseCertificateForOnPremAuth

### <a name="windowsidentityprotectionconfigurationwindowshelloforbusinessblocked"></a>Windowsidentityschutzconfiguration. windowshelloforbusinessblockierte 
**CSP**:./Vendor/MSFT/PassportForWork  
**Offset-URI**:/{AADTenantId}/Policies/UsePassportForWork

### <a name="windowskioskconfigurationedgekioskenablepublicbrowsing"></a>Windowskioskconfiguration. edgekioskenablepublicbrowsing 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/ConfigureKioskMode

### <a name="windowskioskconfigurationedgekioskresetafteridletimeinminutes"></a>Windowskioskconfiguration. edgekioskrelog TAF 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Browser/ConfigureKioskResetAfterIdleTimeout

### <a name="windowskioskconfigurationkioskbrowserblockedurlexceptions"></a>Windowskioskconfiguration. kioskbrowserblockedurlexceptions 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/KioskBrowser/BlockedUrlExceptions

### <a name="windowskioskconfigurationkioskbrowserblockedurls"></a>Windowskioskconfiguration. kioskbrowserblockedurls 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/KioskBrowser/BlockedUrls

### <a name="windowskioskconfigurationkioskbrowserdefaulturl"></a>Windowskioskconfiguration. kioskbrowserdefaulturl 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/KioskBrowser/DefaultUrl

### <a name="windowskioskconfigurationkioskbrowserenableendsessionbutton"></a>Windowskioskconfiguration. kioskbrowserenableendsessionbutton 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/KioskBrowser/EnableEndSessionButton

### <a name="windowskioskconfigurationkioskbrowserenablehomebutton"></a>Windowskioskconfiguration. kioskbrowserenablehomebutton 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/KioskBrowser/EnableHomeButton

### <a name="windowskioskconfigurationkioskbrowserenablenavigationbuttons"></a>Windowskioskconfiguration. kioskbrowserenablenavigationbuttons 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/KioskBrowser/EnableNavigationButtons

### <a name="windowskioskconfigurationkioskbrowserrestartonidletimeinminutes"></a>Windowskioskconfiguration. kioskbrowserrestartondletimumminutes 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/KioskBrowser/KioskBrowserRestartOnIdleTimeInMinutes

### <a name="windowsupdateforbusinessconfigurationautomaticupdatemode"></a>Windowsupdateforbusinessconfiguration. automaticupdatemode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/AllowAutoUpdate

### <a name="windowsupdateforbusinessconfigurationautorestartnotificationdismissal"></a>Windowsupdateforbusinessconfiguration. autorestartnotificationentlassung 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/AutoRestartRequiredNotificationDismissal

### <a name="windowsupdateforbusinessconfigurationbusinessreadyupdatesonly"></a>Windowsupdateforbusinessconfiguration. businessleseryupdatesonly 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/BranchReadinessLevel

### <a name="windowsupdateforbusinessconfigurationdeliveryoptimizationmode"></a>Windowsupdateforbusinessconfiguration. deliveryoptimizationmode 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/DeliveryOptimization/DODownloadMode

### <a name="windowsupdateforbusinessconfigurationdriversexcluded"></a>Windowsupdateforbusinessconfiguration. driversexcluded 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/ExcludeWUDriversInQualityUpdate

### <a name="windowsupdateforbusinessconfigurationengagedrestartdeadlineforfeatureupdatesindays"></a>Windowsupdateforbusinessconfiguration. engagedrestartdeadlineforfeatureupdatesindays 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/EngagedRestartDeadlineForFeatureUpdates

### <a name="windowsupdateforbusinessconfigurationengagedrestartdeadlineindays"></a>Windowsupdateforbusinessconfiguration. engagedrestartdeadlineindays 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/EngagedRestartDeadline

### <a name="windowsupdateforbusinessconfigurationengagedrestartsnoozescheduleforfeatureupdatesindays"></a>Windowsupdateforbusinessconfiguration. engagedrestartnoozescheduleforfeatureupdatesindays 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/EngagedRestartSnoozeScheduleForFeatureUpdates

### <a name="windowsupdateforbusinessconfigurationengagedrestartsnoozescheduleindays"></a>Windowsupdateforbusinessconfiguration. engagedrestartnoozescheduleindays 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/EngagedRestartSnoozeSchedule

### <a name="windowsupdateforbusinessconfigurationengagedrestarttransitionscheduleforfeatureupdatesindays"></a>Windowsupdateforbusinessconfiguration. engagedrestarttransitionscheduleforfeatureupdatesindays 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/EngagedRestartTransitionScheduleForFeatureUpdates

### <a name="windowsupdateforbusinessconfigurationengagedrestarttransitionscheduleindays"></a>Windowsupdateforbusinessconfiguration. engagedrestarttransitionscheduleindays 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/EngagedRestartTransitionSchedule

### <a name="windowsupdateforbusinessconfigurationfeatureupdatesdeferralperiodindays"></a>Windowsupdateforbusinessconfiguration. featureupdatesdeferralperiodindays 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/DeferFeatureUpdatesPeriodInDays

### <a name="windowsupdateforbusinessconfigurationfeatureupdatespaused"></a>Windowsupdateforbusinessconfiguration. featureupdatesamp; quot; angehalten 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/PauseFeatureUpdates

### <a name="windowsupdateforbusinessconfigurationfeatureupdatespausestartdatetime"></a>Windowsupdateforbusinessconfiguration. featureupdatespausestartdatetime 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/PauseFeatureUpdatesStartTime

### <a name="windowsupdateforbusinessconfigurationfeatureupdatesrollbackstartdatetime"></a>Windowsupdateforbusinessconfiguration. featureupdatesrollbackstartdatetime
**CSP**: n/a-Graph-API nur **Offset-URI**: n/a-Graph-API

### <a name="windowsupdateforbusinessconfigurationfeatureupdateswillberolledback"></a>Windowsupdateforbusinessconfiguration. featureupdateswillberolledback 
**CSP**: n/a-Graph-API nur **Offset-URI**: n/a-Graph-API

### <a name="windowsupdateforbusinessconfigurationfeatureupdatesrollbackwindowindays"></a>Windowsupdateforbusinessconfiguration. featureupdatesrollbackwindowindays
**CSP**: n/a-Graph-API nur **Offset-URI**: n/a-Graph-API

### <a name="windowsupdateforbusinessconfigurationinstallationschedule"></a>Windowsupdateforbusinessconfiguration. installationschedule
**CSP**:./Device/Vendor/MSFT/Policy **Offset-URI**:/config/Update/ActiveHoursStart,/config/Update/ActiveHoursEnd,/config/Update/ScheduledInstallDay,/config/Update/ScheduledInstallTime

### <a name="windowsupdateforbusinessconfigurationmicrosoftupdateserviceallowed"></a>Windowsupdateforbusinessconfiguration. mikrosoftupdateserviceallowed 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/AllowMUUpdateService

### <a name="windowsupdateforbusinessconfigurationpreviewbuildsetting"></a>Windowsupdateforbusinessconfiguration. previewbuildsetting 
**CSP**:./Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/ManagePreviewBuilds

### <a name="windowsupdateforbusinessconfigurationqualityupdatesdeferralperiodindays"></a>Windowsupdateforbusinessconfiguration. qualityupdatesdeferralperiodindays 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/DeferQualityUpdatesPeriodInDays

### <a name="windowsupdateforbusinessconfigurationqualityupdatespaused"></a>Windowsupdateforbusinessconfiguration. qualityupdatespaused 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/PauseQualityUpdates

### <a name="windowsupdateforbusinessconfigurationqualityupdatespausestartdatetime"></a>Windowsupdateforbusinessconfiguration. qualityupdatespausestartdatetime 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/PauseQualityUpdatesStartTime

### <a name="windowsupdateforbusinessconfigurationqualityupdatesrollbackstartdatetime"></a>Windowsupdateforbusinessconfiguration. qualityupdatesrollbackstartdatetime
**CSP**: n/a-Graph-API nur **Offset-URI**: n/a-Graph-API

### <a name="windowsupdateforbusinessconfigurationqualityupdateswillberolledback"></a>Windowsupdateforbusinessconfiguration. qualityupdateswillberolledback 
**CSP**: n/a-Graph-API nur **Offset-URI**: n/a-Graph-API

### <a name="windowsupdateforbusinessconfigurationscheduleimminentrestartwarninginminutes"></a>Windowsupdateforbusinessconfiguration. scheduleimminentrestartwarninginminutes 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/ScheduleImminentRestartWarning

### <a name="windowsupdateforbusinessconfigurationschedulerestartwarninginhours"></a>Windowsupdateforbusinessconfiguration. schedulerestartwarninginhours 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/ScheduleRestartWarning

### <a name="windowsupdateforbusinessconfigurationskipchecksbeforerestart"></a>Windowsupdateforbusinessconfiguration. skipchecksbeforerestart 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/SetEDURestart

### <a name="windowsupdateforbusinessconfigurationupdateweeks"></a>Windowsupdateforbusinessconfiguration. updateweeks 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/ScheduledInstallEveryWeek,/config/Update/ScheduledInstallFirstWeek,/config/Update/ScheduledInstallFourthWeek,/config/Update/ScheduledInstallSecondWeek,/config/Update/ScheduledInstallThirdWeek

### <a name="windowsupdateforbusinessconfigurationuserpauseaccess"></a>Windowsupdateforbusinessconfiguration. userpaulaccess 
**CSP**:./Device/Vendor/MSFT/Policy  
**Offset-URI**:/config/Update/SetDisablePauseUXAccess


## <a name="next-steps"></a>Nächste Schritte

- [Übersicht: Gerätekonfiguration](../configuration/device-profiles.md)
- [Referenz zum Konfigurations Dienstanbieter](/windows/client-management/mdm/configuration-service-provider-reference) (öffnet eine andere Dokumentations Website)