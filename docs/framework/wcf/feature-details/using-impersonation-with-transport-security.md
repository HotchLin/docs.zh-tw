---
title: "使用模擬搭配傳輸安全性"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 426df8cb-6337-4262-b2c0-b96c2edf21a9
caps.latest.revision: "12"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: 57b40493d0e9bcbbaaf1366c74ff116343f6ee96
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="using-impersonation-with-transport-security"></a>使用模擬搭配傳輸安全性
*模擬*是上的用戶端識別讓伺服器應用程式的能力。 對服務而言，驗證存取資源時使用模擬是很常見的。 伺服器應用程式使用服務帳戶執行，但是伺服器在接受用戶端連線會模擬用戶端，藉此使用用戶端的認證執行存取檢查。 傳輸安全性是一種用於傳遞認證與使用該認證保護通訊安全性的機制。 本主題說明如何搭配模擬功能來使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的傳輸安全性。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]模擬使用訊息安全性，請參閱[委派和模擬](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)。  
  
## <a name="five-impersonation-levels"></a>五個模擬等級  
 傳輸安全性運用如下表所述的五種模擬等級。  
  
|模擬等級|描述|  
|-------------------------|-----------------|  
|無|伺服器不嘗試模擬用戶端。|  
|匿名|伺服器應用程式可以根據用戶端的認證執行存取檢查，但不會接收任何有關用戶端身分識別的資訊。 模擬等級只對電腦上的通訊有意義，例如具名管道。 使用 `Anonymous` 搭配遠端連線將模擬等級提升至識別。|  
|識別|伺服器應用程式知道用戶端的身分，而且可以根據用戶端的認證執行存取驗證，但無法模擬用戶端。 若權杖提供者未提供不同的模擬等級，則識別是 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中搭配 SSPI 認證使用的預設模擬等級。|  
|Impersonate|除了執行存取檢查外，伺服器應用程式可以存取做為用戶端的伺服器電腦上的資源。 伺服器應用程式無法使用用戶端識別存取遠端電腦上的資源，因為模擬的權杖沒有網路認證。|  
|Delegate - 委派|除了擁有與 `Impersonate` 相同的功能外，「委派」模擬等級也可以使用用戶端識別讓伺服器應用程式存取遠端電腦上的資訊，並且將識別傳遞到其他應用程式。<br /><br /> **重要**伺服器網域帳戶必須標示為受信任可以委派的網域控制站，才能使用這些額外的功能。 這個模擬等級無法搭配標示為敏感的用戶端網域帳戶使用。|  
  
 最常搭配傳輸安全性層級為`Identify`和`Impersonate`。 不建議將 `None` 和 `Anonymous` 等級使用於一般用途，而且很多傳輸不支援使用這些等級進行驗證。 請小心使用 `Delegate` 等級的強大功能， 僅將委派憑證的使用權限提供給受信任的伺服器應用程式。  
  
 伺服器應用程式需要有 `Impersonate` 權限，才能在 `Delegate` 或 `SeImpersonatePrivilege` 等級使用模擬。 如果應用程式在管理員群組或有服務 SID (網路服務、本機服務或本機系統) 的帳戶上執行，該應用程式預設為擁有此權限。 伺服器不需要用戶端和伺服器的相互驗證。 有些支援模擬的驗證配置 (例如 NTLM) 無法搭配相互驗證使用。  
  
## <a name="transport-specific-issues-with-impersonation"></a>模擬的特定傳輸問題  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的傳輸選擇會影響模擬的可能選擇。 本節描述影響 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中標準 HTTP 與具名管道的問題。 自訂傳輸在支援模擬上有其限制。  
  
### <a name="named-pipe-transport"></a>具名管道傳輸  
 下列項目會與具名管道傳輸一併使用：  
  
-   命名管道傳輸僅供在本機電腦上使用。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的具名管道明確不允許跨電腦連接。  
  
-   具名管道無法搭配 `Impersonate` 或 `Delegate` 模擬等級使用。 具名管道無法在這些模擬等級強制執行電腦保證。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]具名管道，請參閱[選擇傳輸](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)。  
  
### <a name="http-transport"></a>HTTP 傳輸  
 使用 HTTP 傳輸的繫結 (<xref:System.ServiceModel.WSHttpBinding>和<xref:System.ServiceModel.BasicHttpBinding>) 中所述，支援數種驗證配置，[了解 HTTP 驗證](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)。 支援的模擬等級視驗證配置而定。 下列項目會與 HTTP 傳輸一併使用：  
  
-   `Anonymous` 驗證配置會忽略模擬。  
  
-   `Basic`驗證配置僅支援`Delegate`層級。 所有較低的模擬等級都會進行升級。  
  
-   `Digest` 驗證配置僅支援 `Impersonate` 和 `Delegate` 等級。  
  
-   可直接選擇或透過交涉選擇的 `NTLM` 驗證配置僅支援本機電腦上的 `Delegate` 等級。  
  
-   只能夠透過交涉選擇的 Kerberos 驗證配置可以搭配任何支援的模擬等級使用。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]HTTP 傳輸，請參閱[選擇傳輸](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)。  
  
## <a name="see-also"></a>請參閱  
 [委派和模擬](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)  
 [授權](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)  
 [如何：在服務上模擬用戶端](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)  
 [了解 HTTP 驗證](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)
