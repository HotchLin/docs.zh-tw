---
title: '&lt;serviceSecurityAudit&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba517369-a034-4f8e-a2c4-66517716062b
caps.latest.revision: "17"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: e36019cd6d010e25292fa50ed3bf795dfca15f73
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="ltservicesecurityauditgt"></a>&lt;serviceSecurityAudit&gt;
指定在服務作業期間啟用安全性事件稽核的設定。  
  
 \<系統。ServiceModel >  
\<行為 >  
\<serviceBehaviors >  
\<行為 >  
\<serviceSecurityAudit >  
  
## <a name="syntax"></a>語法  
  
```xml  
<serviceSecurityAudit   
   auditLogLocation="Default/Application/Security"  
   messageAuthenticationAuditLevel= None/Success/Failure/SuccessAndFailure"   serviceAuthorizationAuditLevel="None/Success/Failure/SuccessAndFailure"  
   suppressAuditFailure="Boolean"  
/>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子項目和父項目。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|auditLogLocation|指定稽核記錄檔的位置。 有效值包括以下的值：<br /><br /> 預設： 安全性事件會寫入應用程式記錄檔到事件記錄檔的 Windows XP 和 Windows Server 2003 和 Windows Vista 上。<br />應用程式： 稽核事件會寫入應用程式記錄檔。<br />安全性： 稽核事件會寫入安全性記錄檔。<br /><br /> 預設值為 Default。 如需詳細資訊，請參閱<xref:System.ServiceModel.AuditLogLocation>。|  
|suppressAuditFailure|布林值，指定隱藏寫入稽核記錄檔錯誤的行為。<br /><br /> 應用程式應會收到稽核記錄檔寫入失敗的通知。 如果您的應用程式不是設計用來處理稽核失敗，應使用這個屬性來隱藏稽核記錄檔的寫入失敗。<br /><br /> 如果這個屬性是 `true`，則 OutOfMemoryException、StackOverFlowException、ThreadAbortException 和 ArgumentException 以外的例外狀況會由系統處理，而不會傳播至應用程式；這些例外狀況是因為嘗試寫入稽核事件所造成的。 如果這個屬性是 `false`，則所有因嘗試寫入稽核事件而造成的例外狀況都會向上傳遞至應用程式。<br /><br /> 預設為 `true`。|  
|serviceAuthorizationAuditLevel|指定記錄在稽核記錄檔中的授權事件類型。 有效值包括以下的值：<br /><br /> -無： 服務授權事件的稽核不會執行。<br />-Success： 只成功的服務授權稽核事件。<br />失敗： 只失敗服務授權稽核事件。<br />-： Successandfailure 成功和失敗的服務授權事件進行稽核。<br /><br /> 預設值為 None。 如需詳細資訊，請參閱<xref:System.ServiceModel.AuditLevel>。|  
|messageAuthenticationAuditLevel|指定稽核事件記錄的訊息驗證類型。 有效值包括以下的值：<br /><br /> -無： 稽核會產生任何事件。<br />-Success： 記錄成功的安全性 （完整驗證，包括訊息簽章驗證、 cipher 和權杖驗證） 事件。<br />失敗： 只失敗記錄事件。<br />-： Successandfailure 成功和失敗的事件會記錄。<br /><br /> 預設值為 None。 如需詳細資訊，請參閱<xref:System.ServiceModel.AuditLevel>。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<行為 >](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|指定行為項目。|  
  
## <a name="remarks"></a>備註  
 這個組態項目會用來稽核 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 驗證事件。 啟用稽核時，可以稽核成功或失敗的驗證嘗試 (或兩者)。 事件會寫入三個事件記錄檔之一：應用程式、安全性或作業系統版本的預設記錄檔。 使用 Windows 事件檢視器，即可檢視所有的事件記錄。  
  
 使用這個組態項目詳細範例，請參閱[服務稽核行為](../../../../../docs/framework/wcf/samples/service-auditing-behavior.md)。  
  
 根據預設，在 Windows XP 中，您可以在應用程式記錄檔中查看稽核事件，在 Windows Server 2003 和 Windows Vista 中，則可以在安全性記錄檔中查看稽核事件。 將 `auditLogLocation` 屬性設定為 'Application' 或 'Security'，即可指定稽核事件的位置。 如需詳細資訊，請參閱[How to： 稽核安全性事件](../../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)。 如果事件要寫入安全性記錄檔，則 LocalSecurityPolicy-> Enable Object Access 應設為 "Success" 和 "Failure"。  
  
 在查看事件記錄檔時，稽核事件的來源為 "ServiceModel Audit 3.0.0.0"。 訊息驗證稽核記錄的分類為 "MessageAuthentication"，而服務驗證稽核記錄的分類則為 'ServiceAuthorization'。  
  
 訊息驗證稽核事件的涵蓋範圍包括訊息是否遭人竄改、訊息是否已過期，以及用戶端是否可驗證服務。 這些事件可提供驗證是否成功或失敗、以及用戶端的身分識别、訊息傳送的目的端點，以及與訊息關聯的動作等相關訊息。  
  
 服務授權稽核事件的涵蓋範圍則是服務授權管理員決定的授權。 這些事件提供的訊息是關於授權是否成功或失敗以及用戶端的身分識别、訊息傳送的目的端點、與訊息相關聯的動作、由傳入訊息產生的授權內容識別碼，以及做出存取決策的授權管理員類型。  
  
## <a name="example"></a>範例  
  
```xml  
<system.serviceModel>  
   <serviceBehaviors>  
      <behavior name="NewBehavior">  
         <serviceSecurityAudit auditLogLocation="Application"   
             suppressAuditFailure="true"  
             serviceAuthorizationAuditLevel="Success"   
             messageAuthenticationAuditLevel="Success" />  
      </behavior>  
   </serviceBehaviors>  
</behaviors>  
```  
  
## <a name="see-also"></a>請參閱  
 <xref:System.ServiceModel.Configuration.ServiceSecurityAuditElement>  
 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>  
 [安全性行為](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)  
 [稽核](../../../../../docs/framework/wcf/feature-details/auditing-security-events.md)  
 [如何：稽核安全性事件](../../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)  
 [服務稽核行為](../../../../../docs/framework/wcf/samples/service-auditing-behavior.md)
