---
title: "如何：使用 Windows Form NumericUpDown 控制項設定和傳回數值"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- numeric values [Windows Forms], Windows Forms
- Windows Forms, numeric values
- Windows Forms controls, NumericUpDown
- NumericUpDown control [Windows Forms], setting and returning values
ms.assetid: 5bd8f8cd-4c12-49ea-9cc3-2a647d064689
caps.latest.revision: "14"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: f31f0b247c882b8ccba84930f7e21f5eea088a35
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-set-and-return-numeric-values-with-the-windows-forms-numericupdown-control"></a>如何：使用 Windows Form NumericUpDown 控制項設定和傳回數值
Windows Form 的數值<xref:System.Windows.Forms.NumericUpDown>控制項由其<xref:System.Windows.Forms.NumericUpDown.Value%2A>屬性。 您可以如同任何其他屬性撰寫條件測試控制項的值。 一次<xref:System.Windows.Forms.NumericUpDown.Value%2A>屬性設定，您可以調整它直接撰寫程式碼執行作業，或可以呼叫<xref:System.Windows.Forms.NumericUpDown.UpButton%2A>和<xref:System.Windows.Forms.NumericUpDown.DownButton%2A>方法。  
  
### <a name="to-set-the-numeric-value"></a>若要設定的數值  
  
1.  指派值給<xref:System.Windows.Forms.NumericUpDown.Value%2A>在程式碼，或在 [屬性] 視窗中的屬性。  
  
    ```vb  
    NumericUpDown1.Value = 55  
    ```  
  
    ```csharp  
    numericUpDown1.Value = 55;  
    ```  
  
    ```cpp  
    numericUpDown1->Value = 55;  
    ```  
  
     -或-  
  
2.  呼叫<xref:System.Windows.Forms.NumericUpDown.UpButton%2A>或<xref:System.Windows.Forms.NumericUpDown.DownButton%2A>方法，以增加或減少值中指定的數量<xref:System.Windows.Forms.NumericUpDown.Increment%2A>屬性。  
  
    ```vb  
    NumericUpDown1.UpButton()  
    ```  
  
    ```csharp  
    numericUpDown1.UpButton();  
    ```  
  
    ```cpp  
    numericUpDown1->UpButton();  
    ```  
  
### <a name="to-return-the-numeric-value"></a>要傳回的數值  
  
-   存取<xref:System.Windows.Forms.NumericUpDown.Value%2A>程式碼中的屬性。  
  
    ```vb  
    If NumericUpDown1.Value >= 65 Then  
       MessageBox.Show("Age is: " & NumericUpDown1.Value.ToString)  
    Else  
       MessageBox.Show("The customer is ineligible for a senior citizen discount.")  
    End If  
    ```  
  
    ```csharp  
    if(numericUpDown1.Value >= 65)  
    {  
       MessageBox.Show("Age is: " + numericUpDown1.Value.ToString());  
    }  
    else  
    {  
       MessageBox.Show("The customer is ineligible for a senior citizen discount.");  
    }  
    ```  
  
    ```cpp  
    if(numericUpDown1->Value >= 65)  
    {  
       MessageBox::Show(String::Concat("Age is: ",  
          numericUpDown1->Value.ToString()));  
    }  
    else  
    {  
       MessageBox::Show  
          ("The customer is ineligible for a senior citizen discount.");  
    }  
    ```  
  
## <a name="see-also"></a>請參閱  
 <xref:System.Windows.Forms.NumericUpDown>  
 <xref:System.Windows.Forms.NumericUpDown.Value%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.NumericUpDown.Increment%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.NumericUpDown.UpButton%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.NumericUpDown.DownButton%2A?displayProperty=nameWithType>  
 [NumericUpDown 控制項](../../../../docs/framework/winforms/controls/numericupdown-control-windows-forms.md)  
 [NumericUpDown 控制項概觀](../../../../docs/framework/winforms/controls/numericupdown-control-overview-windows-forms.md)
