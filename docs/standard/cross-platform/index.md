---
title: "使用 .NET Framework 進行多平台開發"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b153baaa-130c-4169-860b-e580591de91e
caps.latest.revision: "13"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 9acceb04ea48ef7d9a99d8a82c63090ee344ea54
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/23/2017
---
# <a name="developing-for-multiple-platforms-with-the-net-framework"></a>使用 .NET Framework 進行多平台開發
您可以使用 .NET Framework 和 Visual Studio，針對 Microsoft 和非 Microsoft 平台來開發應用程式。  
  
## <a name="options-for-cross-platform-development"></a>跨平台開發的選項  
 若要針對多重平台進行開發，您可以共用原始程式碼或二進位檔，並且可以在 .NET Framework 程式碼與 Windows 執行階段 API 之間進行呼叫。  
  
|如果您想要...|請使用...|  
|-----------------------|------------|  
|在 Windows Phone 8.1 與 Windows 8.1 應用程式之間共用原始程式碼|**共用的專案**（在 Visual Studio 2013 Update 2 中的通用應用程式範本）。<br /><br /> -目前沒有 Visual Basic 支援。<br />-您可以使用 # 來分隔平台專屬程式碼`if`陳述式。<br /><br /> 如需詳細資訊，請參閱：<br /><br /> -   [建置以 Windows 和 Windows Phone 為目標使用 Visual Studio 的應用程式](http://msdn.microsoft.com/library/windows/apps/dn609832.aspx)（MSDN 文章）<br />-   [使用 Visual Studio 建置通用 XAML 應用程式](http://blogs.msdn.com/b/visualstudio/archive/2014/04/14/using-visual-studio-to-build-universal-xaml-apps.aspx)（部落格文章）<br />-   [使用 Visual Studio 建立 XAML 交集應用程式，](http://channel9.msdn.com/Events/Build/2014/3-591) （影片）|  
|在目標為不同平台的應用程式之間共用二進位檔|**可攜式類別庫專案**是無從驗證平台的程式碼。<br /><br /> -這種方法通常用於實作商業邏輯的程式碼。<br />-您可以使用 Visual Basic 或 C#。<br />-應用程式開發介面支援因平台。<br />-Windows 8.1 和 Windows Phone 8.1 為目標的可攜式類別庫專案支援 Windows 執行階段 Api 和 XAML。 舊版可攜式類別程式庫中沒有提供這些功能。<br />-如果有需要您可以使用介面或抽象類別來擷取平台專屬程式碼。<br /><br /> 如需詳細資訊，請參閱：<br /><br /> -   [可攜式類別庫](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)（MSDN 文章）<br />-   [如何讓可攜式類別程式庫工作讓您](http://blogs.msdn.com/b/dsplaisted/archive/2012/08/27/how-to-make-portable-class-libraries-work-for-you.aspx)（部落格文章）<br />-   [搭配 MVVM 使用可攜式類別庫](../../../docs/standard/cross-platform/using-portable-class-library-with-model-view-view-model.md)（MSDN 文章）<br />-   [程式庫，目標多個平台的應用程式資源](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md)（MSDN 文章）<br />-   [.NET portability Analyzer](http://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b) （Visual Studio 擴充功能）|  
|針對非 Windows 8.1 和 Windows Phone 8.1 的平台共用原始程式碼|**加入連結**功能。<br /><br /> -此方法是適用於這兩個應用程式常用但可攜性，是因為某些原因的應用程式邏輯。 您可以將此功能用於 C# 或 Visual Basic 程式碼。<br />     例如，Windows Phone 8 和 Windows 8 共用 Windows 執行階段 API，但可攜式類別庫不支援那些平台的 Windows 執行階段。 您可以使用 `Add as link`，在 Windows Phone 8 應用程式與目標為 Windows 8 的 Windows 市集應用程式之間，共用一般 Windows 執行階段程式碼。<br /><br /> 如需詳細資訊，請參閱：<br /><br /> -   [與加入連結共用程式碼](http://msdn.microsoft.com/library/windowsphone/develop/jj714082\(v=vs.105\).aspx)（MSDN 文章）<br />-   [如何： 將現有的項目加入專案](http://msdn.microsoft.com/library/vstudio/9f4t9t92\(v=vs.100\).aspx)（MSDN 文章）|  
|使用 .NET Framework 或從 .NET Framework 程式碼呼叫 Windows 執行階段 API，以撰寫 Windows 市集應用程式|**Windows 執行階段 Api**從您的.NET Framework C# 或 Visual Basic 程式碼，並使用.NET Framework 來建立 Windows 市集應用程式。 請注意這兩個平台之間的 API 差異。 不過，有類別可以幫助您處理這些差異。<br /><br /> 如需詳細資訊，請參閱：<br /><br /> -   [.NET framework 支援的 Windows 市集應用程式和 Windows 執行階段](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)（MSDN 文章）<br />-   [傳遞 URI 給 Windows 執行階段](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)（MSDN 文章）<br />-   <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions>-->`System.IO.WindowsRuntimeStreamExtensions` （MSDN API 參考頁面）<br />-   <!--zz <xref:System.WindowsRuntimeSystemExtensions>-->`System.WindowsRuntimeSystemExtensions` （MSDN API 參考頁面）|  
|針對非 Microsoft 平台建立 .NET Framework 應用程式|**可攜式類別庫參考組件**在.NET Framework 和 Visual Studio 擴充功能或協力廠商工具，例如： Xamarin。<br /><br /> 如需詳細資訊，請參閱：<br /><br /> -   [可攜式類別程式庫現在適用於所有平台。](http://blogs.msdn.com/b/dotnet/archive/2013/10/14/portable-class-library-pcl-now-available-on-all-platforms.aspx) (部落格文章)<br />-   [Xamarin](http://xamarin.com/visual-studio) （Xamarin 網站）|  
|使用 JavaScript 和 HTML 進行跨平台開發|**通用應用程式範本**在 Visual Studio 2013 中，更新 2，以針對 Windows 8.1 和 Windows Phone 8.1 開發 Windows 執行階段 Api。 目前，您無法使用 JavaScript 和 HTML 搭配 .NET Framework API 來開發跨平台應用程式。<br /><br /> 如需詳細資訊，請參閱：<br /><br /> -   [JavaScript 專案範本](http://msdn.microsoft.com/library/windows/apps/hh758331.aspx)<br />-   [使用 JavaScript 為 Windows Phone 的 Windows 執行階段應用程式移植](http://msdn.microsoft.com/library/windows/apps/dn636144.aspx)|
