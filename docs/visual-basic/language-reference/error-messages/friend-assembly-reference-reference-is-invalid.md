---
title: "Friend 組件參考&lt;參考&gt;無效"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc31535
- bc31535
helpviewer_keywords: BC31535
ms.assetid: 6540c1d0-bb19-4051-a579-2e4f9094585e
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: ab1c7c5cc7a7f4ad899df7722769238e05d96e6b
ms.sourcegitcommit: 34ec7753acf76f90a0fa845235ef06663dc9e36e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="friend-assembly-reference-ltreferencegt-is-invalid"></a>Friend 組件參考&lt;參考&gt;無效
Friend 組件參考\<參考 > 無效。 以強式名稱簽署的組件必須在其 InternalsVisibleTo 宣告中指定公開金鑰。  
  
 組件名稱傳遞給<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>屬性建構函式識別是強式名稱組件，但它不包含`PublicKey`屬性。  
  
 **錯誤 ID:** BC31535  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
1.  判斷公開金鑰的強式名稱的 friend 組件。 包含公開金鑰，因為組件名稱的一部分傳遞至<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>屬性建構函式使用`PublicKey`屬性。  
  
## <a name="see-also"></a>請參閱  
 <xref:System.Reflection.AssemblyName>  
 [Friend 組件](../../programming-guide/concepts/assemblies-gac/friend-assemblies.md)  
 

