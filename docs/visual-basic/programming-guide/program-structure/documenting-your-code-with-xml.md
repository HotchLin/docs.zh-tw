---
title: "使用 XML 在程式碼中加入文件 (Visual Basic)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- XML [Visual Basic], documenting code
- XML comments, Visual Basic
- Visual Basic code, documenting with XML
ms.assetid: a0d35dc7-c5f9-4d74-92ff-a1c6f28d5235
caps.latest.revision: "17"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: ddb1f366002c4f0c675c591d83aab1b31ef8f602
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="documenting-your-code-with-xml-visual-basic"></a>使用 XML 在程式碼中加入文件 (Visual Basic)
在[!INCLUDE[vbprvb](~/includes/vbprvb-md.md)]，您可以將您的程式碼使用 XML 文件  
  
## <a name="xml-documentation-comments"></a>XML 文件註解  
 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)]提供簡單的方法來自動建立專案的 XML 文件。 您可以自動產生的 XML 基本架構型別和成員，然後再提供摘要、 描述性的文件每個參數，以及其他備註。 適當的安裝程式，XML 文件，就會自動發出到 XML 檔案具有相同名稱做為副檔名為.xml 和您的專案。 如需詳細資訊，請參閱 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)。  
  
 可以使用或操作為 XML 的 XML 檔案。 這個檔案位於相同的目錄與您的專案輸出.exe 或.dll 檔中。  
  
 XML 文件開頭`'''`。 這些註解在處理時有一些限制：  
  
-   文件必須是語式正確的 XML。 如果 XML 的格式不正確，則會產生警告，而且文件檔案包含註解指出發生錯誤。  
  
-   開發人員可以自由建立自己的標記集合。 沒有一組建議的標記 （請參閱本主題中的 < 相關章節 >）。 其中一些建議的標記具有特殊意義：  
  
    -   \<param> 標記是用來描述參數。 如果使用，編譯器會驗證參數存在，而且所有參數在文件中都有描述。 如果驗證失敗，則編譯器會發出警告。  
  
    -   `cref` 屬性可以附加至任何標記，以提供程式碼項目的參考。 編譯器會驗證此程式碼項目存在。 如果驗證失敗，則編譯器會發出警告。 編譯器也會遵守任何`Imports`陳述式時搜尋類型中所述`cref`屬性。  
  
    -   \<摘要 > 標記中的 IntelliSense 即可使用[!INCLUDE[vsprvs](~/includes/vsprvs-md.md)]以顯示類型或成員的其他資訊。  
  
## <a name="related-sections"></a>相關章節  
 如需建立文件註解的 XML 檔案的詳細資訊，請參閱下列主題：  
  
-   [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)  
  
-   [XML 註解標記](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)  
  
-   [處理 XML 檔案](../../../visual-basic/programming-guide/program-structure/processing-the-xml-file.md)  
  
-   [如何：建立 XML 文件](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)  
  
-   [Visual Studio 中的 XML 工具](/visualstudio/xml-tools/xml-tools-in-visual-studio)  
  
## <a name="see-also"></a>另請參閱  
 [使用 Visual Basic 開發應用程式](../../../visual-basic/developing-apps/index.md)  
 [Visual Basic 程式設計手冊](../../../visual-basic/programming-guide/index.md)
