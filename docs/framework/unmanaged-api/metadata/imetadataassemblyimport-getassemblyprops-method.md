---
title: "IMetaDataAssemblyImport::GetAssemblyProps 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataAssemblyImport.GetAssemblyProps
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataAssemblyImport::GetAssemblyProps
helpviewer_keywords:
- GetAssemblyProps method [.NET Framework metadata]
- IMetaDataAssemblyImport::GetAssemblyProps method [.NET Framework metadata]
ms.assetid: 0eaa4aa9-9441-444a-920c-e4b2a2db899e
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 6e99474fea329f53286d698d0e1a302909d5cc65
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="imetadataassemblyimportgetassemblyprops-method"></a>IMetaDataAssemblyImport::GetAssemblyProps 方法
取得具有指定的中繼資料簽章的組件的屬性集。  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT GetAssemblyProps (  
    [in]  mdAssembly          mda,  
    [out] const void          **ppbPublicKey,   
    [out] ULONG               *pcbPublicKey,  
    [out] ULONG               *pulHashAlgId,  
    [out] LPWSTR              szName,  
    [in] ULONG                cchName,  
    [out] ULONG               *pchName,  
    [out] ASSEMBLYMETADATA    *pMetaData,  
    [out] DWORD               *pdwAssemblyFlags  
);  
```  
  
#### <a name="parameters"></a>參數  
 `mda`  
 [in]。 `mdAssembly`代表要取得屬性的組件的中繼資料語彙基元。  
  
 `ppbPublicKey`  
 [out]公開金鑰或中繼資料語彙基元的指標。  
  
 `pcbPublicKey`  
 [out]在傳回的公開金鑰的位元組數目。  
  
 `pulHashAlgId`  
 [out]指標，用來雜湊中的組件檔案的演算法。  
  
 `szName`  
 [out]組件的簡單名稱。  
  
 `cchName`  
 [in]大小，以寬字元的`szName`。  
  
 `pchName`  
 [out]中實際傳回的寬字元數目`szName`。  
  
 `pMetaData`  
 [out]ASSEMBLYMETADATA 結構，其中包含組件中繼資料指標。  
  
 `pdwAssemblyFlags`  
 [out]描述套用至組件的中繼資料的旗標。 這個值是一或多個組合[CorAssemblyFlags](../../../../docs/framework/unmanaged-api/metadata/corassemblyflags-enumeration.md)值。  
  
## <a name="requirements"></a>需求  
 **平台：**看到[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Cor.h  
  
 **程式庫：**做為 MsCorEE.dll 中的資源  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>請參閱  
 [IMetaDataAssemblyImport 介面](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md)
