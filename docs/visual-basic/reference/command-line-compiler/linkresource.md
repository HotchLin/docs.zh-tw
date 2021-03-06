---
title: /linkresource (Visual Basic)
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- /linkresource compiler option [Visual Basic]
- -linkresource compiler option [Visual Basic]
- linkresource compiler option [Visual Basic]
- /linkres compiler option [Visual Basic]
- linkres compiler option [Visual Basic]
- -linkres compiler option [Visual Basic]
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 4e51f844695985485210a1e4bedfef7ac968326c
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="linkresource-visual-basic"></a>/linkresource (Visual Basic)
建立與 Managed 資源的連結。  
  
## <a name="syntax"></a>語法  
  
```  
/linkresource:filename[,identifier[,public|private]]  
' -or-  
/linkres:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>引數  
 `filename`  
 必要項。 要連結至組件的資源檔。 如果檔案名稱包含空格，將名稱括在引號 ("")。  
  
 `identifier`  
 選擇項。 資源的邏輯名稱。 用來載入資源的名稱。 預設值是檔案的名稱。 您可以選擇性地指定檔案是否公用或私用組件資訊清單中，例如： `/linkres:filename.res,myname.res,public`。 根據預設，`filename`是公用的組件中。  
  
## <a name="remarks"></a>備註  
 `/linkresource`選項不會在輸出檔中內嵌資源檔; 使用`/resource`選項來執行這項操作。  
  
 `/linkresource`選項需要一個`/target`選項以外`/target:module`。  
  
 如果`filename`是[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]建立資源檔，例如，藉由[Resgen.exe （資源檔產生器）](http://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4) ，或是在開發環境中，它可以存取與其中成員保持<xref:System.Resources>命名空間。 (如需詳細資訊，請參閱 <xref:System.Resources.ResourceManager>)。若要在執行階段存取所有其他資源，可使用的方式開頭`GetManifestResource`中<xref:System.Reflection.Assembly>類別。  
  
 檔案名稱可以是任何檔案格式。 例如，您可能需要產生組件的原生 DLL 部分，以便安裝到全域組件快取中，並從組件的 Managed 程式碼存取。  
  
 `/linkresource` 的簡短形式為 `/linkres`。  
  
> [!NOTE]
>  `/linkresource`選項不可以從 Visual Studio 開發環境，則可以使用只有當您編譯從命令列。  
  
## <a name="example"></a>範例  
 下列程式碼編譯`In.vb`以及資源檔連結`Rf.resource`。  
  
```  
vbc /linkresource:rf.resource in.vb  
```  
  
## <a name="see-also"></a>另請參閱  
 [Visual Basic 命令列編譯器](../../../visual-basic/reference/command-line-compiler/index.md)  
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)  
 [/resource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md)  
 [編譯命令列範例](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
