---
title: "StrongNameCompareAssemblies 函式"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: StrongNameCompareAssemblies
api_location: mscoree.dll
api_type: DLLExport
f1_keywords: StrongNameCompareAssemblies
helpviewer_keywords: StrongNameCompareAssemblies function [.NET Framework strong naming]
ms.assetid: 763f2375-efc6-4219-8806-a3b0567ef72b
topic_type: apiref
caps.latest.revision: "17"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 1ed98b1713427a71c73c30ddd64188f61d51045c
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="strongnamecompareassemblies-function"></a>StrongNameCompareAssemblies 函式
判斷兩個組件是否只有其強式名稱簽章不同。  
  
 此函式已被取代。 使用[iclrstrongname:: Strongnamecompareassemblies](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamecompareassemblies-method.md)方法改為。  
  
## <a name="syntax"></a>語法  
  
```  
BOOLEAN StrongNameCompareAssemblies (  
    [in]  LPCWSTR   wszAssembly1,  
    [in]  LPCWSTR   wszAssembly2,  
    [out] DWORD     *pdwResult  
);  
```  
  
#### <a name="parameters"></a>參數  
 `wszAssembly1`  
 [in]第一個組件的路徑。  
  
 `wszAssembly2`  
 [in]第二個組件的路徑。  
  
 `pdwResult`  
 [out]下列值之一：  
  
-   `SN_CMP_DIFFERENT`(0)-指定的組件包含不同的資料。  
  
-   `SN_CMP_IDENTICAL`(1)-指定的組件完全相同，包括其簽章與總和檢查碼。  
  
-   `SN_CMP_SIGONLY`(2)-指定只要簽章與總和檢查碼不同組件。  
  
## <a name="return-value"></a>傳回值  
 `true`如果成功地完成。否則， `false`。  
  
## <a name="requirements"></a>需求  
 **平台：**看到[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** StrongName.h  
  
 **程式庫：**包含做為 MsCorEE.dll 中的資源  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="remarks"></a>備註  
 組件的強式名稱簽章包含組件的文字名稱、 版本、 文化特性和公開金鑰語彙基元。  
  
 如果`StrongNameCompareAssemblies`函式未順利完成，請呼叫[StrongNameErrorInfo](../../../../docs/framework/unmanaged-api/strong-naming/strongnameerrorinfo-function.md)函式可擷取的最後一個產生的錯誤。  
  
## <a name="see-also"></a>請參閱  
 [StrongNameCompareAssemblies 方法](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamecompareassemblies-method.md)  
 [ICLRStrongName 介面](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
