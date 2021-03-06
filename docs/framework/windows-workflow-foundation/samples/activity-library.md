---
title: "活動程式庫"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5323e9d4-71d6-47eb-bfa6-31feac62044d
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 99d8fba848129156d94e54d1da7d08122ccfa735
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="activity-library"></a>活動程式庫
本節中的範例示範如何建立 [!INCLUDE[wf](../../../../includes/wf-md.md)] 進階自訂活動。  
  
## <a name="in-this-section"></a>本節內容  
 [.NET Framework 4.5 中的原則活動](../../../../docs/framework/windows-workflow-foundation/samples/policy-activity-in-net-framework-4-5.md)  
 示範 Policy4 活動如何直接使用 WF 3.5 隨附的規則引擎，在 [!INCLUDE[wf2](../../../../includes/wf2-md.md)][!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] (WF 4.5) 中使用 <xref:System.Workflow.Activities.Rules.RuleSet>[!INCLUDE[wf2](../../../../includes/wf2-md.md)] (WF 3.5) [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 物件。  
  
 [自訂活動以切換到值的範圍](../../../../docs/framework/windows-workflow-foundation/samples/custom-activity-to-switch-on-a-range-of-values.md)  
 示範如何建立可擴充 <xref:System.Activities.Statements.Switch%601> 用法的自訂活動。  
  
 [LINQ to Objects 活動](../../../../docs/framework/windows-workflow-foundation/samples/linq-to-objects-activity.md)  
 示範如何建立活動，以使用 LINQ to Objects 查詢集合項目。  
  
 [LINQ to SQL 範例](../../../../docs/framework/windows-workflow-foundation/samples/linq-to-sql-sample.md)  
 示範如何建立活動，以使用 SQL Server 資料庫資料表中的 LINQ to SQL 查詢實體。  
  
 [使用 InvokePowerShell 活動](../../../../docs/framework/windows-workflow-foundation/samples/using-the-invokepowershell-activity.md)  
 示範如何使用 InvokePowerShell 活動叫用 Windows PowerShell 命令。  
  
 [RangeEnumeration 活動](../../../../docs/framework/windows-workflow-foundation/samples/rangeenumeration-activity.md)  
 示範如何建立可逐一查看數字集合的自訂活動。  
  
 [規則運算式活動](../../../../docs/framework/windows-workflow-foundation/samples/regular-expression-activities.md)  
 示範如何建立可公開 <xref:System.Text.RegularExpressions> 命名空間規則運算式功能的一組活動。  
  
 [SendMail 自訂活動](../../../../docs/framework/windows-workflow-foundation/samples/sendmail-custom-activity.md)  
 示範如何建立衍生自 <xref:System.Activities.AsyncCodeActivity> 的自訂活動，以使用 SMTP 來傳送郵件，供工作流程應用程式使用。  
  
 [針對活動](../../../../docs/framework/windows-workflow-foundation/samples/for-activity.md)  
 示範如何建置繼承自 <xref:System.Activities.NativeActivity> 的自訂活動，以及在工作流程中使用它來逐一查看值範圍。  
  
 [等候輸入活動](../../../../docs/framework/windows-workflow-foundation/samples/wait-for-input-activity.md)  
 示範如何在工作流程中建立命名書籤。  
  
 [節流平行 ForEach](../../../../docs/framework/windows-workflow-foundation/samples/throttled-parallel-foreach.md)  
 示範 `ThrottleParallelForEach` 活動與 <xref:System.Activities.Statements.ParallelForEach%601> 活動如何類似，唯一的例外是它允許設定並行因數來限制同時執行的分支數目。  
  
 [實體活動](../../../../docs/framework/windows-workflow-foundation/samples/entity-activities.md)  
 示範如何與 [!INCLUDE[wf2](../../../../includes/wf2-md.md)] 搭配使用 ADO.NET Entity Framework，以簡化資料存取。  
  
 [資料庫存取活動](../../../../docs/framework/windows-workflow-foundation/samples/database-access-activities.md)  
 示範如何建立活動，可讓您存取資料庫以擷取或修改資訊並使用[ADO.NET](http://go.microsoft.com/fwlink/?LinkId=166081)來存取資料庫。  
  
 [CommentOut 活動](../../../../docs/framework/windows-workflow-foundation/samples/commentout-activity.md)  
 示範如何撰寫可從執行路徑移除其他活動的自訂活動，實際上將這些活動標記為註解。  
  
 [.NET Framework 4.5 中的外顯化原則活動](../../../../docs/framework/windows-workflow-foundation/samples/externalized-policy-activity-in-net-framework-4-5.md)  
 示範 ExternalizedPolicy4 活動如何直接使用 WF 3.5 隨附的規則引擎，以便在 [!INCLUDE[wf2](../../../../includes/wf2-md.md)][!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] (WF 4.5) 中執行現有的 <xref:System.Workflow.Activities.Rules.RuleSet>[!INCLUDE[wf2](../../../../includes/wf2-md.md)] (WF 3.5) [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 物件。  
  
 [NoPersistScope 活動](../../../../docs/framework/windows-workflow-foundation/samples/nopersistscope-activity.md)  
 示範如何在工作流程中操作不可序列化且可處置的狀態。  
  
 [非泛型 ForEach](../../../../docs/framework/windows-workflow-foundation/samples/non-generic-foreach.md)  
 示範如何建立非泛型 <xref:System.Activities.Statements.ForEach%601> 活動版本。  
  
 [非泛型 ParallelForEach](../../../../docs/framework/windows-workflow-foundation/samples/non-generic-parallelforeach.md)  
 示範如何建立非泛型 <xref:System.Activities.Statements.ParallelForEach%601> 活動版本。  
  
 [取得 WorkflowInstanceId](../../../../docs/framework/windows-workflow-foundation/samples/get-workflowinstanceid.md)  
 示範如何使用 `GetWorkflowInstanceId` 自訂活動傳回工作流程執行個體識別碼。
