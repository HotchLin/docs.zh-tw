---
title: "自訂 TimeSpan 格式字串"
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
- format spexifiers, custom time interval
- format strings
- formatting [.NET Framework], time interval
- custom time interval format strings
- formatting [.NET Framework], time
- custom TimeSpan format strings
ms.assetid: a63ebf55-7269-416b-b4f5-286f6c03bf0e
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 7302b17beb5ce20ec2bd8865149fe2e0bae9cee4
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="custom-timespan-format-strings"></a>自訂 TimeSpan 格式字串
A<xref:System.TimeSpan>格式字串會定義的字串表示<xref:System.TimeSpan>格式化作業所產生的值。 自訂格式字串所組成一或多個自訂<xref:System.TimeSpan>格式規範，以及任何數目的常值字元。 不是任何字串[標準 TimeSpan 格式字串](../../../docs/standard/base-types/standard-timespan-format-strings.md)解譯為自訂<xref:System.TimeSpan>格式字串。  
  
> [!IMPORTANT]
>  自訂<xref:System.TimeSpan>格式規範不包括預留位置分隔符號符號，例如天分開小時、 分鐘、 小時或小數秒數的秒數的符號。 相反地，這些符號必須包含在自訂格式字串中作為字串常值。 例如，`"dd\.hh\:mm"` 會定義句號 (.) 作為天與小時之間的分隔符號，並定義冒號 (:) 作為小時與分鐘之間的分隔符號。  
>   
>  自訂 <xref:System.TimeSpan> 格式規範也不包括讓您區分正負時間間隔的正負號。 若要包括正負號，您必須使用條件邏輯建構格式字串。 [其他字元](#Other)一節中將提供範例。  
  
 字串表示<xref:System.TimeSpan>值的多載的呼叫所產生<xref:System.TimeSpan.ToString%2A?displayProperty=nameWithType>方法，以及方法，可支援複合格式，例如<xref:System.String.Format%2A?displayProperty=nameWithType>。 如需詳細資訊，請參閱[格式化類型](../../../docs/standard/base-types/formatting-types.md)和[複合格式設定](../../../docs/standard/base-types/composite-formatting.md)。 下列範例說明使用的自訂格式字串在格式化作業中。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customformatexample1.cs#1)]
 [!code-vb[Conceptual.TimeSpan.Custom#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customformatexample1.vb#1)]  
  
 自訂<xref:System.TimeSpan>格式字串也會使用<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>和<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法來定義所需的格式輸入字串的剖析作業。 (剖析會將值的字串表示轉換成該值)。下列範例說明剖析作業中標準格式字串的用法。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customparseexample1.cs#2)]
 [!code-vb[Conceptual.TimeSpan.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customparseexample1.vb#2)]  
  
<a name="table"></a>下表描述自訂日期和時間格式規範。  
  
|格式規範|描述|範例|  
|----------------------|-----------------|-------------|  
|"d"、"%d"|時間間隔中的完整天數。<br /><br /> 詳細資訊：["d" 自訂格式規範](#dSpecifier)。|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%d` --> "6"<br /><br /> `d\.hh\:mm` --> "6.14:32"|  
|"dd"-"dddddddd"|時間間隔中的完整天數，視需要填補前置零。<br /><br /> 更多資訊： ["dd"-"dddddddd"自訂格式規範](#ddSpecifier)。|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `ddd` --> "006"<br /><br /> `dd\.hh\:mm` --> "06.14:32"|  
|"h"、"%h"|時間間隔中未計入天數部分的完整時數。 一位數的小時不會有前置零。<br /><br /> 詳細資訊：["h" 自訂格式規範](#hSpecifier)。|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%h` --> "14"<br /><br /> `hh\:mm` --> "14:32"|  
|"hh"|時間間隔中未計入天數部分的完整時數。 一位數的小時有前置零。<br /><br /> 詳細資訊：["hh" 自訂格式規範](#hhSpecifier)。|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `hh` --> "14"<br /><br /> `new TimeSpan(6, 8, 32, 17, 685):`<br /><br /> `hh` --> 08|  
|"m"、"%m"|時間間隔中未納入時數或天數部分的完整分鐘數。 一位數的分鐘不會有前置零。<br /><br /> 詳細資訊：["m" 自訂格式規範](#mSpecifier)。|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `%m` --> "8"<br /><br /> `h\:m` --> "14:8"|  
|"mm"|時間間隔中未納入時數或天數部分的完整分鐘數。 一位數的分鐘有前置零。<br /><br /> 詳細資訊：["mm" 自訂格式規範](#mmSpecifier)。|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `mm` --> "08"<br /><br /> `new TimeSpan(6, 8, 5, 17, 685):`<br /><br /> `d\.hh\:mm\:ss` --> 6.08:05:17|  
|"s"、"%s"|時間間隔中未納入時數、天數或分鐘數部分的完整秒數。 一位數的秒不會有前置零。<br /><br /> 詳細資訊：["s" 自訂格式規範](#sSpecifier)。|`TimeSpan.FromSeconds(12.965)`：<br /><br /> `%s` --> 12<br /><br /> `s\.fff` --> 12.965|  
|"ss"|時間間隔中未納入時數、天數或分鐘數部分的完整秒數。  一位數的秒有前置零。<br /><br /> 詳細資訊：["ss" 自訂格式規範](#ssSpecifier)。|`TimeSpan.FromSeconds(6.965)`：<br /><br /> `ss` --> 06<br /><br /> `ss\.fff` --> 06.965|  
|"f"、"%f"|時間間隔中的十分之一秒。<br /><br /> 詳細資訊：["f" 自訂格式規範](#fSpecifier)。|`TimeSpan.FromSeconds(6.895)`：<br /><br /> `f` --> 8<br /><br /> `ss\.f` --> 06.8|  
|"ff"|時間間隔中的百分之一秒。<br /><br /> 更多資訊：["Ff"自訂格式規範](#ffSpecifier)。|`TimeSpan.FromSeconds(6.895)`：<br /><br /> `ff` --> 89<br /><br /> `ss\.ff` --> 06.89|  
|"fff"|時間間隔中的毫秒。<br /><br /> 詳細資訊：["fff" 自訂格式規範](#f3Specifier)。|`TimeSpan.FromSeconds(6.895)`：<br /><br /> `fff` --> 895<br /><br /> `ss\.fff` --> 06.895|  
|"ffff"|時間間隔中的萬分之一秒。<br /><br /> 詳細資訊：["ffff" 自訂格式規範](#f4Specifier)。|`TimeSpan.Parse("0:0:6.8954321")`：<br /><br /> `ffff` --> 8954<br /><br /> `ss\.ffff` --> 06.8954|  
|"fffff"|時間間隔中的十萬分之一秒。<br /><br /> 詳細資訊：["fffff" 自訂格式規範](#f5Specifier)。|`TimeSpan.Parse("0:0:6.8954321")`：<br /><br /> `fffff` --> 89543<br /><br /> `ss\.fffff` --> 06.89543|  
|"ffffff"|時間間隔中的百萬分之一秒。<br /><br /> 詳細資訊：["ffffff" 自訂格式規範](#f6Specifier)。|`TimeSpan.Parse("0:0:6.8954321")`：<br /><br /> `ffffff` --> 895432<br /><br /> `ss\.ffffff` --> 06.895432|  
|"fffffff"|時間間隔中的千萬分之一秒 (或小數刻度)。<br /><br /> 詳細資訊：["fffffff" 自訂格式規範](#f7Specifier)。|`TimeSpan.Parse("0:0:6.8954321")`：<br /><br /> `fffffff` --> 8954321<br /><br /> `ss\.fffffff` --> 06.8954321|  
|"F"、"%F"|時間間隔中的十分之一秒。 如果數字為零，則不會顯示任何內容。<br /><br /> 詳細資訊：["F" 自訂格式規範](#F_Specifier)。|`TimeSpan.Parse("00:00:06.32")`：<br /><br /> `%F`: 3<br /><br /> `TimeSpan.Parse("0:0:3.091")`:<br /><br /> `ss\.F`: 03.|  
|"FF"|時間間隔中的百分之一秒。 不包含小數點後的零或兩位數都是零的數字。<br /><br /> 詳細資訊：["FF" 自訂格式規範](#FF_Specifier)。|`TimeSpan.Parse("00:00:06.329")`：<br /><br /> `FF`: 32<br /><br /> `TimeSpan.Parse("0:0:3.101")`:<br /><br /> `ss\.FF`: 03.1|  
|"FFF"|時間間隔中的毫秒。 不包含小數點後的零。<br /><br /> 詳細資訊：|`TimeSpan.Parse("00:00:06.3291")`:<br /><br /> `FFF`: 329<br /><br /> `TimeSpan.Parse("0:0:3.1009")`:<br /><br /> `ss\.FFF`: 03.1|  
|"FFFF"|時間間隔中的萬分之一秒。 不包含小數點後的零。<br /><br /> 詳細資訊：["FFFF" 自訂格式規範](#F4_Specifier)。|`TimeSpan.Parse("00:00:06.32917")`：<br /><br /> `FFFFF`: 3291<br /><br /> `TimeSpan.Parse("0:0:3.10009")`:<br /><br /> `ss\.FFFF`: 03.1|  
|"FFFFF"|時間間隔中的十萬分之一秒。 不包含小數點後的零。<br /><br /> 詳細資訊：["FFFFF" 自訂格式規範](#F5_Specifier)。|`TimeSpan.Parse("00:00:06.329179")`：<br /><br /> `FFFFF`: 32917<br /><br /> `TimeSpan.Parse("0:0:3.100009")`:<br /><br /> `ss\.FFFFF`: 03.1|  
|"FFFFFF"|時間間隔中的百萬分之一秒。 不顯示小數點後的零。<br /><br /> 詳細資訊：["FFFFFF" 自訂格式規範](#F6_Specifier)。|`TimeSpan.Parse("00:00:06.3291791")`：<br /><br /> `FFFFFF`: 329179<br /><br /> `TimeSpan.Parse("0:0:3.1000009")`:<br /><br /> `ss\.FFFFFF`: 03.1|  
|"FFFFFFF"|時間間隔中的千萬分之一秒。 不顯示小數點後的零或七位數都是零。<br /><br /> 詳細資訊：["FFFFFFF" 自訂格式規範](#F7_Specifier)。|`TimeSpan.Parse("00:00:06.3291791")`：<br /><br /> `FFFFFF`: 3291791<br /><br /> `TimeSpan.Parse("0:0:3.1900000")`:<br /><br /> `ss\.FFFFFF`: 03.19|  
|*' 字串*'|常值字串分隔符號。<br /><br /> 更多資訊：[其他字元](#Other)。|`new TimeSpan(14, 32, 17):`<br /><br /> `hh':'mm':'ss` --> "14:32:17"|  
|\|逸出字元。<br /><br /> 更多資訊：[其他字元](#Other)。|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` --> "14:32:17"|  
|任意字元|其他任何未逸出字元都會解譯為自訂格式規範。<br /><br /> 更多資訊：[其他字元](#Other)。|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` --> "14:32:17"|  
  
<a name="dSpecifier"></a>   
## <a name="the-d-custom-format-specifier"></a>"d" 自訂格式規範  
 "D"自訂格式規範輸出的值<xref:System.TimeSpan.Days%2A?displayProperty=nameWithType>屬性，代表整日天數中的時間間隔。 它會輸出中的完整天數<xref:System.TimeSpan>值，即使值有一個以上的數字。 如果值<xref:System.TimeSpan.Days%2A?displayProperty=nameWithType>屬性為零，規範輸出"0"。  
  
 如果單獨使用 "d" 自訂格式規範，請指定 "%d"，以免被錯誤解譯為標準格式字串。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#3)]
 [!code-vb[Conceptual.TimeSpan.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#3)]  
  
 下列範例說明如何使用 "d" 自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#4)]
 [!code-vb[Conceptual.TimeSpan.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#4)]  
  
 [回到表格](#table)  
  
<a name="ddSpecifier"></a>   
## <a name="the-dd-dddddddd-custom-format-specifiers"></a>"dd"-"dddddddd" 自訂格式規範  
 "Dd"、"ddd"、"dddd"、"ddddd"、"dddddd"、"ddddddd 」 和 「 dddddddd"自訂格式規範輸出的值<xref:System.TimeSpan.Days%2A?displayProperty=nameWithType>屬性，代表整日天數中的時間間隔。  
  
 輸出字串會包含格式規範中 "d" 字元數所指定的最少位數，並且視需要填補前置零。 如果天數位數超過格式規範中的 "d" 字元數，則結果字串中的輸出會是完整天數。  
  
 下列範例會使用這些格式規範來顯示兩個字串表示<xref:System.TimeSpan>值。 第一個時間間隔的天數部分值為零，第二個時間間隔的天數部分值為 365。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#5)]
 [!code-vb[Conceptual.TimeSpan.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#5)]  
  
 [回到表格](#table)  
  
<a name="hSpecifier"></a>   
## <a name="the-h-custom-format-specifier"></a>"h" 自訂格式規範  
 "H"自訂格式規範輸出的值<xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType>屬性，代表不會計入為其日期元件的一部分的時間間隔內的整個小時數。 如果，則會傳回一個數字的字串值的值<xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType>屬性是 0 到 9，且如果，則會傳回兩個位數的字串值的值<xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType>屬性範圍是從 10 到 23。  
  
 如果單獨使用 "h" 自訂格式規範，請指定 "%h"，以免被錯誤解譯為標準格式字串。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
 [!code-vb[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]  
  
 通常在剖析作業中，只包含單一數字的輸入字串會解譯為天數。 您可以改用 "%h" 自訂格式規範會，將數值字串解譯為時數。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#8)]
 [!code-vb[Conceptual.TimeSpan.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#8)]  
  
 下列範例說明如何使用 "h" 自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#7)]
 [!code-vb[Conceptual.TimeSpan.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#7)]  
  
 [回到表格](#table)  
  
<a name="hhSpecifier"></a>   
## <a name="the-hh-custom-format-specifier"></a>"hh" 自訂格式規範  
 "Hh"自訂格式規範輸出的值<xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType>屬性，代表不會計入為其日期元件的一部分的時間間隔內的整個小時數。 對於從 0 到 9 的值，輸出字串會包含前置零。  
  
 通常在剖析作業中，只包含單一數字的輸入字串會解譯為天數。 您可以改用 "hh" 自訂格式規範，將數值字串解譯為時數。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#9)]
 [!code-vb[Conceptual.TimeSpan.Custom#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#9)]  
  
 下列範例說明如何使用 "hh" 自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#10)]
 [!code-vb[Conceptual.TimeSpan.Custom#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#10)]  
  
 [回到表格](#table)  
  
<a name="mSpecifier"></a>   
## <a name="the-m-custom-format-specifier"></a>"m" 自訂格式規範  
 "M"自訂格式規範輸出的值<xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType>屬性，代表整數分鐘數，就不會計算其日期元件的一部分的時間間隔內。 如果，則會傳回一個數字的字串值的值<xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType>屬性是 0 到 9，且如果，則會傳回兩個位數的字串值的值<xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType>屬性範圍是從 10 到 59 之間。  
  
 如果單獨使用 "m" 自訂格式規範，請指定 "%m"，以免被錯誤解譯為標準格式字串。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
 [!code-vb[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]  
  
 通常在剖析作業中，只包含單一數字的輸入字串會解譯為天數。 您可以改用 "%m" 自訂格式規範，將數值字串解譯為分鐘數。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#11)]
 [!code-vb[Conceptual.TimeSpan.Custom#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#11)]  
  
 下列範例說明如何使用 "m" 自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#12)]
 [!code-vb[Conceptual.TimeSpan.Custom#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#12)]  
  
 [回到表格](#table)  
  
<a name="mmSpecifier"></a>   
## <a name="the-mm-custom-format-specifier"></a>"mm" 自訂格式規範  
 "Mm"自訂格式規範輸出的值<xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType>屬性，代表整數分鐘數，就不會包含在其小時或天元件的時間間隔內。 對於從 0 到 9 的值，輸出字串會包含前置零。  
  
 通常在剖析作業中，只包含單一數字的輸入字串會解譯為天數。 您可以改用 "mm" 自訂格式規範，將數值字串解譯為分鐘數。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#13)]
 [!code-vb[Conceptual.TimeSpan.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#13)]  
  
 下列範例說明如何使用 "mm" 自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#14)]
 [!code-vb[Conceptual.TimeSpan.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#14)]  
  
 [回到表格](#table)  
  
<a name="sSpecifier"></a>   
## <a name="the-s-custom-format-specifier"></a>"s" 自訂格式規範  
 "S"自訂格式規範輸出的值<xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType>屬性，代表不是其小時、 天數或分鐘數元件的一部分的時間間隔中的完整秒數數目。 如果，則會傳回一個數字的字串值的值<xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType>屬性是 0 到 9，且如果，則會傳回兩個位數的字串值的值<xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType>屬性範圍是從 10 到 59 之間。  
  
 如果單獨使用 "s" 自訂格式規範，請指定 "%s"，以免被錯誤解譯為標準格式字串。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#15)]
 [!code-vb[Conceptual.TimeSpan.Custom#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#15)]  
  
 通常在剖析作業中，只包含單一數字的輸入字串會解譯為天數。 您可以改用 "%s" 自訂格式規範，將數值字串解譯為秒數。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#17)]
 [!code-vb[Conceptual.TimeSpan.Custom#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#17)]  
  
 下列範例說明如何使用 "s" 自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#16)]
 [!code-vb[Conceptual.TimeSpan.Custom#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#16)]  
  
 [回到表格](#table)  
  
<a name="ssSpecifier"></a>   
## <a name="the-ss-custom-format-specifier"></a>"ss" 自訂格式規範  
 "Ss"自訂格式規範輸出的值<xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType>屬性，代表不是其小時、 天數或分鐘數元件的一部分的時間間隔中的完整秒數數目。 對於從 0 到 9 的值，輸出字串會包含前置零。  
  
 通常在剖析作業中，只包含單一數字的輸入字串會解譯為天數。 您可以改用 "ss" 自訂格式規範，將數值字串解譯為秒數。 下列範例提供一個實例。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#18)]
 [!code-vb[Conceptual.TimeSpan.Custom#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#18)]  
  
 下列範例說明如何使用 "ss" 自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#19)]
 [!code-vb[Conceptual.TimeSpan.Custom#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#19)]  
  
 [回到表格](#table)  
  
<a name="fSpecifier"></a>   
## <a name="thef-custom-format-specifier"></a>"F"自訂格式規範  
 "f" 自訂格式規範會輸出時間間隔中的十分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法中，輸入的字串必須包含剛好一個小數位數。  
  
 如果單獨使用 "f" 自訂格式規範，請指定 "%f"，以免被錯誤解譯為標準格式字串。  
  
 下列範例使用"f"自訂格式規範來顯示的十分之一秒中<xref:System.TimeSpan>值。 首先會使用 "f" 作為唯一的格式規範，然後再放在自訂格式字串中與 "s" 規範結合。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [回到表格](#table)  
  
<a name="ffSpecifier"></a>   
## <a name="the-ff-custom-format-specifier"></a>"ff" 自訂格式規範  
 "ff" 自訂格式規範會輸出時間間隔中的百分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法中，輸入的字串必須包含兩個小數。  
  
 下列範例使用"ff"自訂格式規範來顯示百分之一秒<xref:System.TimeSpan>值。 首先會使用 "ff" 作為唯一的格式規範，然後再放在自訂格式字串中與 "s" 規範結合。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [回到表格](#table)  
  
<a name="f3Specifier"></a>   
## <a name="the-fff-custom-format-specifier"></a>"fff" 自訂格式規範  
 "fff" 自訂格式規範 (有三個 "f" 字元) 會輸出時間間隔中的毫秒。 在格式化作業中，會截斷其餘任何小數位數。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法中，輸入的字串必須包含剛好三個小數。  
  
 下列範例使用"fff"自訂格式規範來顯示中的千分之一秒<xref:System.TimeSpan>值。 首先會使用 "fff" 作為唯一的格式規範，然後再放在自訂格式字串中與 "s" 規範結合。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [回到表格](#table)  
  
<a name="f4Specifier"></a>   
## <a name="the-ffff-custom-format-specifier"></a>"ffff" 自訂格式規範  
 "ffff" 自訂格式規範 (有四個 "f" 字元) 會輸出時間間隔中的萬分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法中，輸入的字串必須包含四個小數。  
  
 下列範例使用"ffff"自訂格式規範來顯示在第二個則萬分之一<xref:System.TimeSpan>值。 首先會使用 "ffff" 作為唯一的格式規範，然後再放在自訂格式字串中與 "s" 規範結合。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [回到表格](#table)  
  
<a name="f5Specifier"></a>   
## <a name="the-fffff-custom-format-specifier"></a>"fffff" 自訂格式規範  
 "fffff" 自訂格式規範 (有五個 "f" 字元) 會輸出時間間隔中的十萬分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法中，輸入的字串必須包含剛好 5 個小數。  
  
 下列範例使用"fffff"自訂格式規範來顯示在第二個則十萬分之一<xref:System.TimeSpan>值。 首先會使用 "fffff" 作為唯一的格式規範，然後再放在自訂格式字串中與 "s" 規範結合。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [回到表格](#table)  
  
<a name="f6Specifier"></a>   
## <a name="the-ffffff-custom-format-specifier"></a>"ffffff" 自訂格式規範  
 "ffffff" 自訂格式規範 (有六個 "f" 字元) 會輸出時間間隔中的百萬分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法中，輸入的字串必須包含剛好六個小數點後數字。  
  
 下列範例使用"ffffff"自訂格式規範來顯示在第二個百萬分之一<xref:System.TimeSpan>值。 首先會使用它作為唯一的格式規範，然後再放在自訂格式字串中與 "s" 規範結合。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [回到表格](#table)  
  
<a name="f7Specifier"></a>   
## <a name="the-fffffff-custom-format-specifier"></a>"fffffff" 自訂格式規範  
 "fffffff" 自訂格式規範 (有七個 "f" 字元) 會輸出時間間隔中的千萬分之一秒 (或刻度的小數值)。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法中，輸入的字串必須包含剛好七個小數。  
  
 下列範例使用"fffffff"自訂格式規範來小數的數字中的刻度顯示<xref:System.TimeSpan>值。 首先會使用它作為唯一的格式規範，然後再放在自訂格式字串中與 "s" 規範結合。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [回到表格](#table)  
  
<a name="F_Specifier"></a>   
## <a name="the-f-custom-format-specifier"></a>"F" 自訂格式規範  
 "F" 自訂格式規範會輸出時間間隔中的十分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 如果時間間隔十分之一秒的值為零，它就不會包含在結果字串中。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法，第二個位數的十分之一與否是選擇性的。  
  
 如果單獨使用 "F" 自訂格式規範，請指定 "%F"，以免被錯誤解譯為標準格式字串。  
  
 下列範例使用"F"自訂格式規範來顯示的十分之一秒中<xref:System.TimeSpan>值。 它也會在剖析作業中使用此自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#21)]
 [!code-vb[Conceptual.TimeSpan.Custom#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#21)]  
  
 [回到表格](#table)  
  
<a name="FF_Specifier"></a>   
## <a name="the-ff-custom-format-specifier"></a>"FF" 自訂格式規範  
 "FF" 自訂格式規範會輸出時間間隔中的百分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 如果小數點後有任何零，這些零不會包含在結果字串中。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法，十分之一的存在和第二位數百分之一是選擇性的。  
  
 下列範例使用"FF"自訂格式規範來顯示百分之一秒<xref:System.TimeSpan>值。 它也會在剖析作業中使用此自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#22)]
 [!code-vb[Conceptual.TimeSpan.Custom#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#22)]  
  
 [回到表格](#table)  
  
<a name="F3_Specifier"></a>   
## <a name="the-fff-custom-format-specifier"></a>"FFF" 自訂格式規範  
 "FFF" 自訂格式規範 (有三個 "F" 字元) 會輸出時間間隔中的毫秒。 在格式化作業中，會截斷其餘任何小數位數。 如果小數點後有任何零，這些零不會包含在結果字串中。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法，在出現十分之一、 百分之一，與第二個位數的千分之一是選擇性的。  
  
 下列範例使用"FFF"自訂格式規範來顯示在第二個千分之一<xref:System.TimeSpan>值。 它也會在剖析作業中使用此自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#23)]
 [!code-vb[Conceptual.TimeSpan.Custom#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#23)]  
  
 [回到表格](#table)  
  
<a name="F4_Specifier"></a>   
## <a name="the-ffff-custom-format-specifier"></a>"FFFF" 自訂格式規範  
 "FFFF" 自訂格式規範 (有四個 "F" 字元) 會輸出時間間隔中的萬分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 如果小數點後有任何零，這些零不會包含在結果字串中。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法，在出現十分之一、 百分之一、 千分之一，與第二個位數的萬分之一是選擇性的。  
  
 下列範例使用"FFFF"自訂格式規範來顯示在第二個則萬分之一<xref:System.TimeSpan>值。 它也會在剖析作業中使用 "FFFF" 自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#24](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#24)]
 [!code-vb[Conceptual.TimeSpan.Custom#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#24)]  
  
 [回到表格](#table)  
  
<a name="F5_Specifier"></a>   
## <a name="the-fffff-custom-format-specifier"></a>"FFFFF" 自訂格式規範  
 "FFFFF" 自訂格式規範 (有五個 "F" 字元) 會輸出時間間隔中的十萬分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 如果小數點後有任何零，這些零不會包含在結果字串中。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法，在出現十分之一、 百分之一、 千分之一、 萬分之一，與第二個數字的五位數是選擇性的。  
  
 下列範例使用"FFFFF"自訂格式規範來顯示在第二個則十萬分之一<xref:System.TimeSpan>值。 它也會在剖析作業中使用 "FFFFF" 自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#25](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#25)]
 [!code-vb[Conceptual.TimeSpan.Custom#25](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#25)]  
  
 [回到表格](#table)  
  
<a name="F6_Specifier"></a>   
## <a name="the-ffffff-custom-format-specifier"></a>"FFFFFF" 自訂格式規範  
 "FFFFFF" 自訂格式規範 (有六個 "F" 字元) 會輸出時間間隔中的百萬分之一秒。 在格式化作業中，會截斷其餘任何小數位數。 如果小數點後有任何零，這些零不會包含在結果字串中。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法，在出現十分之一、 百分之一、 千分之一、 萬分之一、 十萬分之一，與第二個位數的百萬分之一是選擇性的。  
  
 下列範例使用"FFFFFF"自訂格式規範來顯示在第二個百萬分之一<xref:System.TimeSpan>值。 它也會在剖析作業中使用此自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#26](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#26)]
 [!code-vb[Conceptual.TimeSpan.Custom#26](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#26)]  
  
 [回到表格](#table)  
  
<a name="F7_Specifier"></a>   
## <a name="the-fffffff-custom-format-specifier"></a>"FFFFFFF" 自訂格式規範  
 "FFFFFFF" 自訂格式規範 (有七個 "F" 字元) 會輸出時間間隔中的千萬分之一秒 (或刻度的小數值)。 如果小數點後有任何零，這些零不會包含在結果字串中。 在剖析作業中呼叫<xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType>或<xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType>方法，七個小數的數字，輸入字串中的目前狀態是選擇性的。  
  
 下列範例使用"FFFFFFF"自訂格式規範來顯示秒的小數部分<xref:System.TimeSpan>值。 它也會在剖析作業中使用此自訂格式規範。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#27](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#27)]
 [!code-vb[Conceptual.TimeSpan.Custom#27](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#27)]  
  
 [回到表格](#table)  
  
<a name="Other"></a>   
## <a name="other-characters"></a>其他字元  
 格式字串中任何其他未逸出的字元 (包括空白字元)，都會解譯為自訂格式規範。 在大部分情況下，是否存在的任何其他未逸出方式字元導致<xref:System.FormatException>。  
  
 有兩個方式可以在格式字串中納入常值字元：  
  
-   用單引號 (常值字串分隔符號) 括住字元。  
  
-   在其前面加一個反斜線 ("\\")，它解譯為逸出字元。 亦即在 C# 中，格式字串必須括以 @-quoted，或必須在常值字元前額外加上一道反斜線。  
  
     在某些情況下，您可能需要使用條件邏輯，才能在格式字串中包含逸出的常值。 下列範例將使用條件邏輯包含代表負時間間隔的正負號。  
  
     [!code-csharp[Conceptual.TimeSpan.Custom#29](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/negativevalues1.cs#29)]
     [!code-vb[Conceptual.TimeSpan.Custom#29](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/negativevalues1.vb#29)]  
  
 .NET 不會定義時間間隔中分隔符號的文法。 這表示天與小時、小時與分鐘、分鐘與秒以及秒與小數秒之間的分隔符號，都必須以格式字串中的字元常值方式處理。  
  
 下列範例使用逸出字元和單引號，定義會在輸出字串中加上 "minutes" 一詞的自訂格式字串。  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#28](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/literal1.cs#28)]
 [!code-vb[Conceptual.TimeSpan.Custom#28](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/literal1.vb#28)]  
  
 [回到表格](#table)  
  
## <a name="see-also"></a>另請參閱  
 [格式化類型](../../../docs/standard/base-types/formatting-types.md)  
 [標準 TimeSpan 格式字串](../../../docs/standard/base-types/standard-timespan-format-strings.md)
