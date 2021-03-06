---
title: "如何：使用支援事件架構非同步模式的元件"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 35e9549c-1568-4768-ad07-17cc6dff11e1
caps.latest.revision: "15"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 49e03a8d886ccd4ed6e4b2a19692c1874f5928ec
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-use-components-that-support-the-event-based-asynchronous-pattern"></a>如何：使用支援事件架構非同步模式的元件
許多元件可讓您選擇以非同步方式執行其工作。 <xref:System.Media.SoundPlayer>和<xref:System.Windows.Forms.PictureBox>元件，例如，啟用您載入音效和您的主執行緒繼續沒有中斷的情況下執行的同時，「 在背景 」 映像。  
  
 支援的類別上使用非同步方法[事件架構非同步模式概觀](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)可以附加至元件的事件處理常式一樣簡單*MethodName* `Completed`事件，就如同任何其他事件。 當您呼叫*MethodName* `Async`方法，您的應用程式仍會繼續執行，而不會中斷，直到*MethodName* `Completed`就會引發事件。 在您的事件處理常式，您可以檢查<xref:System.ComponentModel.AsyncCompletedEventArgs>參數來判斷是否已成功完成非同步作業，或已取消。  
  
 如需有關如何使用事件處理常式的詳細資訊，請參閱[事件處理常式概觀](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)。  
  
 下列程序示範如何使用非同步影像載入功能的<xref:System.Windows.Forms.PictureBox>控制項。  
  
### <a name="to-enable-a-picturebox-control-to-asynchronously-load-an-image"></a>若要啟用非同步載入影像的 PictureBox 控制項  
  
1.  建立的執行個體<xref:System.Windows.Forms.PictureBox>表單中的元件。  
  
2.  指定事件處理常式<xref:System.Windows.Forms.PictureBox.LoadCompleted>事件。  
  
     請檢查有任何非同步下載期間可能發生的錯誤。 這也是在您檢查取消。  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#2)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#5)]  
  
3.  加入兩個按鈕，稱為`loadButton`和`cancelLoadButton`，加入至表單。 新增<xref:System.Windows.Forms.Control.Click>事件處理常式，啟動和取消下載。  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#4)]  
  
4.  執行應用程式。  
  
     映像下載進行時，您可以自由移動表單、 降至最低，並將它最大化。  
  
## <a name="see-also"></a>另請參閱  
 [操作說明：在背景執行作業](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)  
 [事件架構非同步模式概觀](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)  
 [不在組建中： Visual Basic 中的多執行緒](http://msdn.microsoft.com/en-us/c731a50c-09c1-4468-9646-54c86b75d269)
