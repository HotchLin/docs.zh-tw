---
title: "IMetaDataTables::GetTableInfo 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataTables.GetTableInfo
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataTables::GetTableInfo
helpviewer_keywords:
- IMetaDataTables::GetTableInfo method [.NET Framework metadata]
- GetTableInfo method [.NET Framework metadata]
ms.assetid: 50cbe557-2322-41aa-8e0d-f967602eaa0f
topic_type: apiref
caps.latest.revision: "13"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 9ce9e3beb15724c7d7ddf02cbe7f83795d474139
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="imetadatatablesgettableinfo-method"></a>IMetaDataTables::GetTableInfo 方法
取得名稱、 資料列大小、 資料列數目、 資料行數與指定之資料表的索引鍵資料行索引。  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT GetTableInfo (  
    [in]  ULONG       ixTbl,  
    [out] ULONG       *pcbRow,  
    [out] ULONG       *pcRows,  
    [out] ULONG       *pcCols,  
    [out] ULONG       *piKey,  
    [out] const char  **ppName  
);  
```  
  
#### <a name="parameters"></a>參數  
 `ixTbl`  
 [in]資料表的識別項来傳回其屬性。  
  
 `pcbRow`  
 [out]大小，以位元組為單位的資料表資料列的指標。  
  
 `pcRows`  
 [out]資料表中的資料列號碼的指標。  
  
 `pcCols`  
 [out]資料表中的資料行編號的指標。  
  
 `piKey`  
 [out]指向的索引鍵資料行或-1，如果資料表沒有索引鍵資料行的索引。  
  
 `ppName`  
 [out]指向資料表名稱的指標。  
  
## <a name="requirements"></a>需求  
 **平台：**看到[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Cor.h  
  
 **程式庫：**做為 MsCorEE.dll 中的資源  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>請參閱  
 [IMetaDataTables 介面](../../../../docs/framework/unmanaged-api/metadata/imetadatatables-interface.md)  
 [IMetaDataTables2 介面](../../../../docs/framework/unmanaged-api/metadata/imetadatatables2-interface.md)
