---
title: "ICorProfilerInfo::GetModuleInfo 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo.GetModuleInfo
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo::GetModuleInfo
helpviewer_keywords:
- GetModuleInfo method [.NET Framework profiling]
- ICorProfilerInfo::GetModuleInfo method [.NET Framework profiling]
ms.assetid: 5a90d16f-7929-4987-8f83-a631becf564d
topic_type: apiref
caps.latest.revision: "20"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: a8309b57f2940805e23010feac17b6d37f1a58af
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="icorprofilerinfogetmoduleinfo-method"></a>ICorProfilerInfo::GetModuleInfo 方法
根據模組 ID，傳回模組的檔案名稱和模組的父組件 ID。  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT GetModuleInfo(  
    [in]  ModuleID   moduleId,  
    [out] LPCBYTE    *ppBaseLoadAddress,  
    [in]  ULONG      cchName,  
    [out] ULONG      *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
          WCHAR      szName[] ,  
    [out] AssemblyID *pAssemblyId);  
```  
  
#### <a name="parameters"></a>參數  
 `moduleId`  
 [in] 將被擷取資訊的模組 ID。  
  
 `ppBaseLoadAddress`  
 [out] 載入模組的基底位址。  
  
 `cchName`  
 [in] `szName` 傳回緩衝區的長度 (以字元為單位)。  
  
 `pcchName`  
 [out] 所傳回的模組檔案名稱之總字元長度的指標。  
  
 `szName`  
 [out] 呼叫端提供的寬字元緩衝區。 當方法傳回時，這個緩衝區會包含模組的檔案名稱。  
  
 `pAssemblyId`  
 [out] 模組父組件之 ID 的指標。  
  
## <a name="remarks"></a>備註  
 若為動態模組，則 `szName` 參數為空字串，且基底位址為 0 (零)。  
  
 雖然`GetModuleInfo`可以呼叫方法，只要有模組 ID，無法使用的父組件的識別碼，直到分析工具收到[icorprofilercallback:: Moduleattachedtoassembly](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleattachedtoassembly-method.md)回呼。  
  
 當 `GetModuleInfo` 傳回時，您必須確認 `szName` 緩衝區的大小足以包含模組的完整檔案名稱。 若要執行這項作業，請比較 `pcchName` 指向的值和 `cchName` 參數的值。 如果 `pcchName` 指向大於 `cchName` 的值，請配置較大的 `szName` 緩衝區，並以較大的大小來更新 `cchName`，然後再次呼叫 `GetModuleInfo`。  
  
 此外，您可以先使用長度為零的 `szName` 緩衝區來呼叫 `GetModuleInfo`，以取得正確的緩衝區大小。 接著您就可以將緩衝區大小設定為 `pcchName` 中傳回的值，並再次呼叫 `GetModuleInfo`。  
  
## <a name="requirements"></a>需求  
 **平台：**看到[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>請參閱  
 [ICorProfilerInfo 介面](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)  
 [分析介面](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [程式碼剖析](../../../../docs/framework/unmanaged-api/profiling/index.md)  
 [GetModuleInfo2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getmoduleinfo2-method.md)
