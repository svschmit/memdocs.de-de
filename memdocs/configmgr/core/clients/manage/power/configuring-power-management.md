---
title: Konfigurieren der Energieverwaltung
titleSuffix: Configuration Manager
description: Einrichten der Energieverwaltung in Configuration Manager
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3146c753e2d84001c162c653cc09af654e6a170a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696598"
---
# <a name="configure-power-management-in-configuration-manager"></a>Konfigurieren der Energieverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel wird erläutert, wie Sie die Energieverwaltung in Configuration Manager einrichten können.

## <a name="enable-and-configure-client-settings"></a>Aktivieren und Konfigurieren von Clienteinstellungen

Mithilfe dieses Verfahrens werden die *Standardclienteinstellungen* für die Energieverwaltung konfiguriert. Sie gilt für alle Computer in Ihrer Hierarchie.

Wenn diese Einstellungen nur auf manche Clients angewendet werden sollen, erstellen Sie eine *benutzerdefinierte Geräteclienteinstellung* Weisen Sie diese dann einer Sammlung zu, die die Computer für die Energieverwaltung enthält. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../../deploy/configure-client-settings.md).  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und klicken Sie erst auf den Knoten **Clienteinstellungen** und dann auf **Clientstandardeinstellungen**.

1. Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

1. Klicken Sie auf die Gruppe **Energieverwaltung**.  

1. Aktivieren Sie die Clienteinstellung, um die **Energieverwaltung von Geräten zuzulassen**.

1. Konfigurieren Sie alle weiteren erforderlichen Clienteinstellungen. Weitere Informationen finden Sie unter [Informationen zu Clienteinstellungen – Energieverwaltung](../../deploy/about-client-settings.md#power-management).  

Die Clients werden beim nächsten Download der Clientrichtlinie mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [How to manage Clients (Verwalten von Clients)](../manage-clients.md#BKMK_PolicyRetrieval).  

## <a name="exclude-computers"></a>Ausschließen von Computern

Sie können verhindern, dass von Computersammlungen Energieverwaltungseinstellungen empfangen werden. Wenn ein Computer Mitglied *einer* Sammlung ist, die Sie aus den Energieverwaltungseinstellungen ausschließen, wendet dieser Computer keine Energieverwaltungseinstellungen an. Dieses Verhalten wird auch dann angewendet, wenn es sich um ein Mitglied einer anderen Sammlung handelt, die Energieverwaltungseinstellungen anwendet.  

Möglicherweise möchten Sie Computer aus folgenden Gründen aus der Energieverwaltung ausschließen:  

- Aufgrund einer Unternehmensanforderung müssen Computer ständig eingeschaltet sein.  

- Sie verfügen über eine Kontrollsammlung von Computern, auf die Sie keine Energieverwaltungseinstellungen anwenden möchten.  

- Bei einigen Computern ist es nicht möglich, Energieverwaltungseinstellungen anzuwenden.  

- Sie möchten Computer, auf denen Windows Server ausgeführt wird, aus der Energieverwaltung ausschließen.  

> [!NOTE]  
> Wenn Sie die Clienteinstellung auf **Benutzern das Ausschließen ihres Geräts aus der Energieverwaltung gestatten** festgelegt haben, können Benutzer ihre Computer über das Softwarecenter aus der Energieverwaltung ausschließen.  

Führen Sie den Bericht **Computers Excluded** (Ausgeschlossene Computer) aus, um herauszufinden, welche Computer aus der Energieverwaltung ausgeschlossen wurden. Weitere Informationen zu diesem Bericht finden Sie unter [Überwachen und Planen der Energieverwaltung](monitor-and-plan-for-power-management.md#BKMK_Excluded).  

> [!IMPORTANT]  
> Wenn ein Computer aus der Energieverwaltung ausgeschlossen wird, werden sämtliche Energieeinstellungen auf ihre ursprünglichen Werte zurückgesetzt. Es können keine einzelnen Energieeinstellungen auf ihre ursprünglichen Werte zurückgesetzt werden.  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>So schließen Sie eine Sammlung von Computern aus der Energieverwaltung aus  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, und wählen Sie den Knoten **Gerätesammlungen** aus.  

1. Wählen Sie die Sammlung aus, die Sie aus der Energieverwaltung ausschließen möchten. Klicken Sie auf dem Menüband auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

1. Navigieren Sie zur Registerkarte**Energieverwaltung**, und klicken Sie auf **Energieverwaltungseinstellungen nie auf Computer in dieser Sammlung anwenden**.  

## <a name="next-steps"></a>Nächste Schritte

[Erstellen und Anwenden von Energiesparplänen](create-and-apply-power-plans.md)

[Überwachen und Planen der Energieverwaltung](monitor-and-plan-for-power-management.md)
