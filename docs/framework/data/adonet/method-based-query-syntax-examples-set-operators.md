---
title: メソッド ベースのクエリ構文例:セット演算子 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fa93af15-28af-4b5e-846b-897308410edb
ms.openlocfilehash: 48aa6044f39be93f144b6c4af5137b131dda0b30
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61772139"
---
# <a name="method-based-query-syntax-examples-set-operators-linq-to-dataset"></a>メソッド ベースのクエリ構文例:セット演算子 (LINQ to DataSet)
このトピックの例では、使用する方法を示します、 <xref:System.Linq.Enumerable.Distinct%2A>、 <xref:System.Linq.Enumerable.Except%2A>、 <xref:System.Linq.Enumerable.Intersect%2A>、および<xref:System.Linq.Enumerable.Union%2A>データ行の集合に対する値ベースの比較操作を実行する演算子[。データセットにデータを読み込んで](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md)を参照してください[Datarow の比較](../../../../docs/framework/data/adonet/comparing-datarows-linq-to-dataset.md)の詳細については<xref:System.Data.DataRowComparer>します。  
  
 `FillDataSet`でこれらの例で使用されるメソッドが指定された[をデータセットにデータを読み込む](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md)します。  
  
 このトピックの例には、AdventureWorks サンプル データベースの Contact、Address、Product、SalesOrderHeader、SalesOrderDetail の各テーブルが使用されています。  
  
 このトピックの例では、次を使用して`using` / `Imports`ステートメント。  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 詳細については、「[方法 :Visual Studio での LINQ to DataSet プロジェクトの作成](../../../../docs/framework/data/adonet/how-to-create-a-linq-to-dataset-project-in-vs.md)です。  
  
## <a name="distinct"></a>Distinct  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.Distinct%2A> メソッドを使用してシーケンス内の重複する要素を削除します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#DistinctRows](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#distinctrows)]
 [!code-vb[DP LINQ to DataSet Examples#DistinctRows](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#distinctrows)]  
  
## <a name="except"></a>除く  
  
### <a name="example"></a>例  
 この例では、最初のテーブルにのみ存在し、かつ 2 つ目のテーブルには存在しない連絡先だけを、<xref:System.Linq.Enumerable.Except%2A> メソッドを使用して取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#Except2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#except2)]
 [!code-vb[DP LINQ to DataSet Examples#Except2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#except2)]  
  
## <a name="intersect"></a>交差  
  
### <a name="example"></a>例  
 この例では、両方のテーブルに存在する連絡先を <xref:System.Linq.Enumerable.Intersect%2A> メソッドを使用して取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#intersect2)]
 [!code-vb[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#intersect2)]  
  
## <a name="union"></a>和集合  
  
### <a name="example"></a>例  
 この例では、<xref:System.Linq.Enumerable.Union%2A> メソッドを使用して、2 つのテーブルのいずれかから一意の連絡先を取得します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#Union2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#union2)]
 [!code-vb[DP LINQ to DataSet Examples#Union2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#union2)]  
  
## <a name="see-also"></a>関連項目

- [DataSet へのデータの読み込み](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md)
- [LINQ to DataSet の例](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)
- [標準クエリ演算子の概要 (C#)](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [標準クエリ演算子の概要 (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
