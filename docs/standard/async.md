---
title: "非同步總覽"
description: "了解非同步程式設計此一重要技術，如何讓您更容易處理對多個核心的封鎖 I/O 和並行作業。"
keywords: .NET, .NET Core
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 1e38e9d9-8284-46ee-a15f-199adc4f26f4
ms.openlocfilehash: bf0cc4ed21c92a57f3f5b2cfa27ac1f054e15172
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/18/2017
---
# <a name="async-overview"></a>非同步總覽

不久之前，只要購買較新的電腦或伺服器，應用程式的執行速度就會更快，然後逐漸停止。 這事實上相反。 具有 1ghz 單一核心 ARM 晶片和伺服器工作負載的行動電話已轉換為 VM。 使用者仍然想要回應式 UI，而且企業擁有者想要擁有隨其業務調整的伺服器。 行動和雲端以及已連接網際網路母體 >3B 使用者的轉換已導致新的一組軟體模式。 

* 用戶端應用程式應該一律啟動、一律連線，並持續回應使用者互動 (例如觸控)，而且在應用程式市集具有高評價！
* 服務應該透過正常相應增加和相應減少來處理流量暴增情況。 

非同步程式設計是一項重要技術，可讓您更容易處理對多個核心的封鎖 I/O 和並行作業。 .NET 提供使用 C#、VB 和 F# 的易用語言層級非同步程式設計模型，讓應用程式和服務具備回應性與彈性的功能。

## <a name="why-write-async-code"></a>為什麼撰寫非同步程式碼？

現代應用程式大量使用檔案和網路 I/O。 除非您想要學習和使用具挑戰性的模式，否則 I/O API 傳統上預設會進行封鎖，進而導致不佳的使用者經驗和硬體使用。 工作架構非同步 API 和語言層級非同步程式設計模型則與此模型相反，只要學習幾個新的概念就可讓非同步執行成為預設值。

非同步程式碼具有下列特性：

* 處理更多的伺服器要求，方法是在等候傳回 I/O 要求時產生執行緒以處理更多的要求。
* 讓 UI 更具回應性，方法是在等候 I/O 要求時產生 UI 互動的執行緒，以及將長時間執行的工作轉換成其他 CPU 核心。
* 許多較新的 .NET API 都是非同步的。
* 輕鬆地在 .NET 中撰寫非同步程式碼！

## <a name="whats-next"></a>後續步驟

若要深入探討非同步概念和程式設計，請參閱[深入了解非同步](async-in-depth.md)和[工作架構非同步程式設計](~/docs/standard/parallel-programming/task-based-asynchronous-programming.md)。
