---
title: "COR_IL_MAP 結構"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: COR_IL_MAP
api_location: mscordbi.dll
api_type: COM
f1_keywords: COR_IL_MAP
helpviewer_keywords: COR_IL_MAP structure [.NET Framework debugging]
ms.assetid: 534ebc17-963d-4b26-8375-8cd940281db3
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 2e2772833d75ced2209896ca37cf6cf37fb965f1
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="corilmap-structure"></a>COR_IL_MAP 結構
指定函式相關位移中的變更。  
  
## <a name="syntax"></a>語法  
  
```  
typedef struct _COR_IL_MAP {  
    ULONG32 oldOffset;   
    ULONG32 newOffset;   
    BOOL    fAccurate;  
} COR_IL_MAP;  
```  
  
## <a name="members"></a>成員  
  
|成員|描述|  
|------------|-----------------|  
|`oldOffset`|舊 Microsoft 中繼語言 (MSIL) 位移相對於函式的開頭。|  
|`newOffset`|新的 MSIL 位移相對於函式的開頭。|  
|`fAccurate`|`true`如果對應是否已知為精確;否則， `false`。|  
  
## <a name="remarks"></a>備註  
 對應的格式如下所示： 偵錯工具會假設`oldOffset`指的是在原始、 未修改 MSIL 程式碼的 MSIL 位移。 `newOffset`參數是指在新的已檢測的程式碼中對應的 MSIL 位移。  
  
 逐步執行才能正常運作，應該符合下列需求：  
  
-   此對應應該以遞增順序排序。  
  
-   已檢測的 MSIL 程式碼不應該重新排列。  
  
-   不應該移除原始的 MSIL 程式碼。  
  
-   此對應應該包含對應程式資料庫 (PDB) 檔案中的所有序列點的項目。  
  
 對應不會不進行插補遺漏的項目。 下列範例顯示的地圖與它的結果。  
  
 對應：  
  
-   舊的位移 0，0 新位移  
  
-   舊的位移 5、 10 個新的位移  
  
-   舊的位移 9、 20 新位移  
  
 結果：  
  
-   0、 1、 2、 3 或 4 的舊位移會對應為新的位移為 0。  
  
-   5、 6、 7 或 8 的舊位移會對應至新的位移 10。  
  
-   9 或更高版本的舊位移會對應至新的位移 20。  
  
-   0、 1、 2、 3、 4、 5、 6、 7、 8 或 9 的新位移會對應至舊的位移 0。  
  
-   為新的位移 10、 11、 12、 13、 14、 15、 16、 17、 18 或 19 的會對應至舊的位移 5。  
  
-   20 或更高版本的新位移會對應至舊的位移 9。  
  
## <a name="requirements"></a>需求  
 **平台：**看到[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、 CorProf.idl  
  
 **程式庫：** CorGuids.lib  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>請參閱  
 [偵錯結構](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)  
 [偵錯](../../../../docs/framework/unmanaged-api/debugging/index.md)
