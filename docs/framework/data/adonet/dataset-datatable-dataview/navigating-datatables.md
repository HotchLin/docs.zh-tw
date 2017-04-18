---
title: "巡覽 DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 202026a1-ec79-435e-b507-12a77f5011b2
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 巡覽 DataTable
<xref:System.Data.DataTableReader> 會以一或多個唯讀、順向結果集的形式，取得一或多個 <xref:System.Data.DataTable> 物件的內容。  
  
 如果 <xref:System.Data.DataTableReader> 是使用 <xref:System.Data.DataSet.CreateDataReader%2A> 方法而建立，則可能包含多個結果集。  有多個結果集時，<xref:System.Data.DataTableReader.NextResult%2A> 方法會將游標移到下一個結果集。  這是順向的處理序。  且不可能返回前一個結果集。  
  
## 範例  
 在下列範例中，`TestConstructor` 方法會建立兩個 <xref:System.Data.DataTable> `` 執行個體。  為了示範 <xref:System.Data.DataTableReader> 類別 \(Class\) 的這個建構函式 \(Constructor\)，此範例會根據內含兩個 **DataTables** 的陣列建立新的 **DataTableReader**，並執行簡單的作業，將前幾行資料行的內容列印到主控台視窗。  
  
 [!code-csharp[DataWorks DataTableReader.NextResult#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTableReader.NextResult/CS/source.cs#1)]
 [!code-vb[DataWorks DataTableReader.NextResult#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTableReader.NextResult/VB/source.vb#1)]  
  
## 請參閱  
 [DataTableReader](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatablereaders.md)   
 [ADO.NET Managed 提供者和資料集開發人員中心](http://go.microsoft.com/fwlink/?LinkId=217917)