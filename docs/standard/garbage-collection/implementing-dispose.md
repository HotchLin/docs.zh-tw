---
title: "實作 Dispose 方法 | Microsoft Docs"
ms.custom: ""
ms.date: "04/07/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Dispose 方法"
  - "記憶體回收，Dispose 方法"
ms.assetid: eb4e1af0-3b48-4fbc-ad4e-fc2f64138bf9
caps.latest.revision: 44
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 44
---
# 實作 Dispose 方法
您實作 <xref:System.IDisposable.Dispose%2A> 方法，以釋放您的應用程式所使用的 Unmanaged 資源。 .NET Framework 記憶體回收行程不會配置或釋放 Unmanaged 記憶體。  
  
 處置物件的模式稱為[處置模式](../../../docs/standard/design-guidelines/dispose-pattern.md)，會在物件存留期上安排順序。 處置模式僅適用於存取 Unmanaged 資源的物件，例如檔案和管道控制碼、註冊控制代碼、等候控制代碼，或是 Unmanaged 記憶體區塊的指標。 這是因為記憶體回收行程在回收未使用的 Managed 物件方面相當有效率，但是它無法回收 Unmanaged 物件。  
  
 處置模式有兩種：  
  
-   將類型使用的每一種 Unmanaged 資源包裝在安全控制代碼中 (也就是在衍生自 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName> 的類別中)。 在這種情況下，請實作 <xref:System.IDisposable> 介面和額外的 `Dispose(Boolean)` 方法。 這是建議的做法，這種做法不需要覆寫 <xref:System.Object.Finalize%2A?displayProperty=fullName> 方法。  
  
    > [!NOTE]
    >  <xref:Microsoft.Win32.SafeHandles?displayProperty=fullName> 命名空間會提供一組衍生自 <xref:System.Runtime.InteropServices.SafeHandle> 的類別，[使用安全控制代碼](#SafeHandles)一節將列出這些類別。 如果您找不到適合釋放 Unmanaged 資源的類別，可以實作自有的 <xref:System.Runtime.InteropServices.SafeHandle> 子類別。  
  
-   您實作<xref:System.IDisposable>介面和額外`Dispose(Boolean)`方法之外，也會覆寫<xref:System.Object.Finalize%2A?displayProperty=fullName>方法。 您必須覆寫 <xref:System.Object.Finalize%2A>，才能確保類型消費者未呼叫您的 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 實作時，Unmanaged 資源仍會獲得處置。 如果您採用前一項所討論的建議技術，<xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName> 類別會自動為您完成這項作業。  
  
 若要確保資源永遠都能適當清除，<xref:System.IDisposable.Dispose%2A> 方法應該能夠被呼叫多次而不會擲回例外狀況。  
  
> [!IMPORTANT]
>  如果您是 c + + 程式設計人員，請勿實作<xref:System.IDisposable.Dispose%2A>方法。 相反地，請依照 \< 解構函式和完成項 > 一節中的指示[How to︰ 定義和使用類別和結構 (C + + /cli CLI)](../Topic/How%20to:%20Define%20and%20Consume%20Classes%20and%20Structs%20\(C++-CLI\).md)。 從.NET Framework 2.0 開始，c + + 編譯器支援決定性的資源處置，而且不允許直接實作<xref:System.IDisposable.Dispose%2A>方法。  
  
 提供的 <xref:System.GC.KeepAlive%2A?displayProperty=fullName> 方法程式碼範例示範積極記憶體回收如何在被回收的物件仍在執行時，即讓完成項開始執行。 它是個不錯的主意呼叫<xref:System.GC.KeepAlive%2A>方法結尾的冗長<xref:System.IDisposable.Dispose%2A>方法。  
  
<a name="Dispose2"></a>   
## <a name="dispose-and-disposeboolean"></a>Dispose() 和 Dispose(Boolean)  
 <xref:System.IDisposable> 介面要求實作單一無參數方法 <xref:System.IDisposable.Dispose%2A>。 不過，處置模式要求實作兩種 `Dispose` 方法：  
  
-   公用非虛擬 (在 Visual Basic 中為 `NonInheritable`) 的 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 實作，而且沒有任何參數。  
  
-   受保護的虛擬 (Visual Basic 中為 `Overridable`) `Dispose` 方法，其簽章為：  
  
     [!code-csharp[Conceptual.Disposable#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#8)]
     [!code-vb[Conceptual.Disposable#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#8)]  
  
### <a name="the-dispose-overload"></a>Dispose() 多載  
 由於這個公用、非虛擬 (在 Visual Basic 中為 `NonInheritable`)、無參數的 `Dispose` 方法是由類型消費者所呼叫，其用途是釋放 Unmanaged 資源並指出完成項 (如果有的話) 不需要執行。 因此，它擁有標準實作：  
  
 [!code-csharp[Conceptual.Disposable#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#7)]
 [!code-vb[Conceptual.Disposable#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#7)]  
  
 `Dispose` 方法會執行所有物件清除，所以記憶體回收行程不需要再呼叫物件的 <xref:System.Object.Finalize%2A?displayProperty=fullName> 覆寫。 因此，呼叫<xref:System.GC.SuppressFinalize%2A>方法會防止記憶體回收行程執行完成項。 型別是否具有沒有完成項呼叫<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>沒有任何作用。 請注意，實際釋放 Unmanaged 資源的工作是由 `Dispose` 方法的第二個多載執行。  
  
### <a name="the-disposeboolean-overload"></a>Dispose(Boolean) 多載  
 在第二個多載，`disposing`參數是<xref:System.Boolean>，指出方法呼叫是來自<xref:System.IDisposable.Dispose%2A>方法 (其值是`true`) 或是來自完成項 (其值是`false`)。  
  
 方法的主體是由兩個程式碼區塊所構成：  
  
-   釋放 Unmanaged 資源的區塊。 不論 `disposing` 參數的值為何，這個區塊都會執行。  
  
-   釋放 Managed 資源的條件性區塊。 如果 `disposing` 的值為 `true`，這個區塊就會執行。 它所釋放的 Managed 資源可能包括：  
  
     **受管理物件實作<xref:System.IDisposable>。**  
     條件式區塊可以用來呼叫其 <xref:System.IDisposable.Dispose%2A> 實作。 如果您已使用安全控制代碼包裝 unmanaged 的資源，您應該呼叫<xref:System.Runtime.InteropServices.SafeHandle.Dispose%28System.Boolean%29?displayProperty=fullName>此處的實作。  
  
     **耗用大量記憶體或耗用少量資源的 Managed 物件。**  
     如果它們是之非由記憶體回收行程，在 `Dispose` 方法中明確釋放這些物件的速度，會比由記憶體回收行程以非決定性的方式回收來得快。  
  
 如果方法呼叫來自完成項 (也就是如果 `disposing` 為 `false`)，則只會執行釋放 Unmanaged 資源的程式碼。 由於記憶體回收行程在最終處理期間終結 Managed 物件的順序並未定義，使用 `Dispose` 值呼叫此 `false` 多載可防止完成項嘗試釋放可能已經回收的 Managed 資源。  
  
## <a name="implementing-the-dispose-pattern-for-a-base-class"></a>實作基底類別的處置模式  
 如果您實作基底類別的處置模式，則必須提供下列項目：  
  
> [!IMPORTANT]
>  您應該實作此模式的所有基底類別實作<xref:System.IDisposable> ，並非`sealed`(`NotInheritable`在 Visual Basic 中)。  
  
-   呼叫 <xref:System.IDisposable.Dispose%2A> 方法的 `Dispose(Boolean)` 實作。  
  
-   實際釋放資源的 `Dispose(Boolean)` 方法。  
  
-   衍生自包裝您的 Unmanaged 資源之 <xref:System.Runtime.InteropServices.SafeHandle> 的類別 (建議使用)，或是 <xref:System.Object.Finalize%2A?displayProperty=fullName> 方法的覆寫。 <xref:System.Runtime.InteropServices.SafeHandle> 類別會提供完成項，讓您不必自行撰寫程式碼。  
  
 以下一般模式將會實作使用安全控制代碼之基底類別的處置模式。  
  
 [!code-csharp[System.IDisposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base1.cs#3)]
 [!code-vb[System.IDisposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base1.vb#3)]  
  
> [!NOTE]
>  上一個範例使用 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 物件來說明模式；可改用任何衍生自 <xref:System.Runtime.InteropServices.SafeHandle> 的物件。 請注意，該範例未正確地執行個體化其 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 物件。  
  
 以下一般模式將會實作覆寫 <xref:System.Object.Finalize%2A?displayProperty=fullName> 之基底類別的處置模式。  
  
 [!code-csharp[System.IDisposable#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base2.cs#5)]
 [!code-vb[System.IDisposable#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base2.vb#5)]  
  
> [!NOTE]
>  在 C# 中，您覆寫<xref:System.Object.Finalize%2A?displayProperty=fullName>藉由定義[解構函式](../Topic/Destructors%20\(C%23%20Programming%20Guide\).md)。  
  
## <a name="implementing-the-dispose-pattern-for-a-derived-class"></a>實作衍生類別的處置模式  
 從實作 <xref:System.IDisposable> 介面的類別衍生的類別不應該實作 <xref:System.IDisposable>，因為 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 的基底類別實作會由其衍生類別繼承。 因此，若要實作衍生類別的處置模式，請改為提供下列項目：  
  
-   覆寫基底類別方法及實際釋放衍生類別之資源的 `protected``Dispose(Boolean)` 方法。 這個方法也應該呼叫基底類別的 `Dispose(Boolean)` 方法，並且傳遞 `true` 做為其 `disposing` 引數的值。  
  
-   衍生自包裝您的 Unmanaged 資源之 <xref:System.Runtime.InteropServices.SafeHandle> 的類別 (建議使用)，或是 <xref:System.Object.Finalize%2A?displayProperty=fullName> 方法的覆寫。 <xref:System.Runtime.InteropServices.SafeHandle> 類別會提供完成項，讓您不必自行撰寫程式碼。 如果您提供完成項，則它應該呼叫 `Dispose(Boolean)` 多載且 `disposing` 引數為 `false`。  
  
 以下一般模式將會實作使用安全控制代碼之衍生類別的處置模式：  
  
 [!code-csharp[System.IDisposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived1.cs#4)]
 [!code-vb[System.IDisposable#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived1.vb#4)]  
  
> [!NOTE]
>  上一個範例使用 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 物件來說明模式；可改用任何衍生自 <xref:System.Runtime.InteropServices.SafeHandle> 的物件。 請注意，該範例未正確地執行個體化其 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 物件。  
  
 以下一般模式將會實作覆寫 <xref:System.Object.Finalize%2A?displayProperty=fullName> 之衍生類別的處置模式：  
  
 [!code-csharp[System.IDisposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived2.cs#6)]
 [!code-vb[System.IDisposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived2.vb#6)]  
  
> [!NOTE]
>  在 C# 中，您覆寫<xref:System.Object.Finalize%2A?displayProperty=fullName>藉由定義[解構函式](../Topic/Destructors%20\(C%23%20Programming%20Guide\).md)。  
  
<a name="SafeHandles"></a>   
## <a name="using-safe-handles"></a>使用安全控制代碼  
 撰寫物件完成項的程式碼是一項複雜的工作，若未正確撰寫，可能會造成問題。 因此，建議您建構 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName> 物件，而不要實作完成項。  
  
 衍生自 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName> 類別的類別會在不受干擾的情況下，藉由指派和釋放控制代碼的方式簡化物件存留期的問題。 這些類別包含重要的完成項，該完成項保證會在應用程式定義域卸載時執行。 使用安全控制代碼的優點的相關資訊，請參閱<xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName>。 <xref:Microsoft.Win32.SafeHandles> 命名空間中的下列衍生類別會提供安全控制代碼：  
  
-   <xref:Microsoft.Win32.SafeHandles.SafeFileHandle>、<xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedFileHandle> 和 <xref:Microsoft.Win32.SafeHandles.SafePipeHandle> 類別，適用於檔案、記憶體對應檔案和管道。  
  
-   <xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedViewHandle> 類別，適用於記憶體檢視。  
  
-   <xref:Microsoft.Win32.SafeHandles.SafeNCryptKeyHandle>、<xref:Microsoft.Win32.SafeHandles.SafeNCryptProviderHandle> 和 <xref:Microsoft.Win32.SafeHandles.SafeNCryptSecretHandle> 類別，適用於加密建構。  
  
-   <xref:Microsoft.Win32.SafeHandles.SafeRegistryHandle> 類別，適用於登錄機碼。  
  
-   <xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> 類別，適用於等候控制代碼。  
  
<a name="base"></a>   
## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-base-class"></a>使用安全控制代碼實作基底類別的處置模式  
 下列範例將說明使用安全控制代碼封裝 Unmanaged 資源之基底類別 `DisposableStreamResource` 的處置模式。 它會定義 `DisposableResource` 類別，該類別使用 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 包裝代表開啟檔案的 <xref:System.IO.Stream> 物件。 `DisposableResource` 方法還包含單一屬性 `Size`，該屬性會傳回檔案資料流中的位元組總數。  
  
 [!code-csharp[Conceptual.Disposable#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/base1.cs#9)]
 [!code-vb[Conceptual.Disposable#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/base1.vb#9)]  
  
<a name="derived"></a>   
## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-derived-class"></a>使用安全控制代碼實作衍生類別的處置模式  
 下列範例將說明衍生類別 `DisposableStreamResource2` 的處置模式，該類別繼承自上述範例中顯示的 `DisposableStreamResource` 類別。 這個類別會新增額外的方法 `WriteFileInfo`，並使用 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 物件包裝可寫入檔案的控制代碼。  
  
 [!code-csharp[Conceptual.Disposable#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/derived1.cs#10)]
 [!code-vb[Conceptual.Disposable#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/derived1.vb#10)]  
  
## <a name="see-also"></a>另請參閱  
 <xref:System.GC.SuppressFinalize%2A>   
 <xref:System.IDisposable>   
 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName>   
 <xref:Microsoft.Win32.SafeHandles>   
 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName>   
 <xref:System.Object.Finalize%2A?displayProperty=fullName>   
 [如何︰ 定義和使用類別和結構 (C + + /cli CLI)](../Topic/How%20to:%20Define%20and%20Consume%20Classes%20and%20Structs%20\(C++-CLI\).md)   
 [處置模式](../../../docs/standard/design-guidelines/dispose-pattern.md)