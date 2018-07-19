---
title: データセット フィールド コレクションの参照 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 006c6bd3-d776-4c20-9092-32e40688ac49
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: dab153b8d5047f73b337e5647fdb25d3b36d9705
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248072"
---
# <a name="dataset-fields-collection-references-report-builder-and-ssrs"></a>データセット フィールド コレクションの参照 (レポート ビルダーおよび SSRS)
  レポート内の各データセットには、1 つのフィールド コレクションが含まれます。 フィールド コレクションは、データセット クエリによって指定されるフィールドと、ユーザーが作成する追加の計算フィールドのセットです。 データセットを作成すると、フィールド コレクションが **[レポート データ]** ペインに表示されます。  
  
 式内の単純なフィールド参照は、デザイン画面に単純な式として表示されます。 たとえば、フィールド `Sales` をレポート データ ペインからデザイン画面のテーブル セルにドラッグすると、 `[Sales]` が表示されます。 この式は、テキスト ボックスの Value プロパティに対して設定されている基本となる式 `=Fields!Sales.Value` を表しています。 レポートが実行されると、レポート プロセッサによってこの式が評価され、テーブル セルのテキスト ボックスにデータ ソースの実際のデータが表示されます。 詳細については、「[式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)」および「[データセット フィールド コレクション &#40;レポート ビルダーおよび SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-the-field-collection-for-a-dataset"></a>データセットのフィールド コレクションの表示  
 フィールド コレクションの個々の値を表示するには、各フィールドをテーブル詳細行にドラッグして、レポートを実行します。 フィールド参照がテーブル データ領域または一覧データ領域の詳細行に含まれている場合は、データセットの行ごとの値が表示されます。  
  
 フィールドの集約値を表示するには、各数値フィールドをマトリックスのデータ領域にドラッグします。 行の総数を計算する既定の集計関数は、 `=Sum(Fields!Sales.Value)`などの Sum 関数です。 既定の関数を変更して、別の合計を計算することもできます。 詳細については、「 [集計関数リファレンス (レポート ビルダーおよび SSRS)](report-builder-functions-aggregate-functions-reference.md)」を参照してください。  
  
 テキスト ボックス内のフィールド コレクションに関する集約値を (データ領域の一部ではなく) デザイン画面に直接表示するには、集計関数のスコープとしてデータセット名を指定する必要があります。 たとえば、 `SalesData`という名前のデータセットの場合は、 `Sales`という式によってフィールド `=Sum(Fields!Sales,"SalesData")`のすべての値の合計が指定されます。  
  
 **[式]** ダイアログ ボックスを使用して単純なフィールド参照を定義する場合は、カテゴリ ペインでフィールド コレクションを選択して、使用可能なフィールドの一覧を **フィールド** ペインに表示できます。 各フィールドには、Value や IsMissing などのいくつかのプロパティがあります。 残りのプロパティは、データ ソースの種類によってはデータセットで使用できる場合がある、定義済みの拡張フィールド プロパティです。  
  
### <a name="detecting-nulls-for-a-dataset-field"></a>値が NULL であるデータセット フィールドの検出  
 NULL ([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] では `Nothing`) であるフィールド値を検出するには、関数 `IsNothing` を使用します。 次の式をテーブル詳細行のテキスト ボックスに配置すると、フィールド `MiddleName` がテストされ、値が NULL の場合は "No Middle Name" という文字列、値が NULL 以外の場合はフィールド値そのもので置き換えられます。  
  
 `=IIF(IsNothing(Fields!MiddleName.Value),"No Middle Name",Fields!MiddleName.Value)`  
  
### <a name="detecting-missing-fields-for-dynamic-queries-at-run-time"></a>実行時の動的クエリにおける存在しないフィールドの検出  
 既定では、フィールド コレクションのアイテムには、Value および IsMissing という 2 つのプロパティがあります。 IsMissing プロパティは、デザイン時にデータセットに対して定義されているフィールドが、実行時に取得されたフィールドに存在するかどうかを示します。 たとえば、クエリには、入力パラメーターによって結果セットの異なるストアド プロシージャを呼び出すものや、テーブル定義が変更された場合に `SELECT * FROM` *\<table>* を照会するものがあります。  
  
> [!NOTE]  
>  IsMissing は、任意の種類のデータ ソースに関して、デザイン時と実行時の間にデータセット スキーマに加えられた変更を検出します。 IsMissing は、多次元キューブで空のメンバーを検出するために使用することはできませんし、MDX クエリ言語の概念に関連しない`EMPTY`と`NON EMPTY`します。  
  
 IsMissing プロパティをカスタム コードでテストすると、結果セットにフィールドが含まれているかどうかを判断できます。 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 関数では、関数の呼び出しに含まれているすべてのパラメーターが評価されるので、存在しないパラメーターへの参照が評価されたときにエラーが返されます。そのため、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 関数の呼び出しで `IIF` や `SWITCH` などの式を使用してフィールドの有無をテストすることはできません。  
  
#### <a name="example-for-controlling-the-visibility-of-a-dynamic-column-for-a-missing-field"></a>存在しないフィールド用の動的列の表示を制御する例  
 データセット内のフィールドを表示する列の表示を制御するための式を設定するには、まず、フィールドの有無に基づいてブール値を返すカスタム コード関数を定義しておく必要があります。 たとえば、次のカスタム コード関数では、フィールドが存在しない場合に true、フィールドが存在する場合に false が返されます。  
  
```  
Public Function IsFieldMissing(field as Field) as Boolean  
 If (field.IsMissing) Then  
 Return True  
  Else   
  Return False  
 End If  
End Function  
```  
  
 この関数を使用して列の表示を制御するには、列の Hidden プロパティを次の式に設定します。  
  
 `=Code.IsFieldMissing(Fields!FieldName)`  
  
 フィールドが存在しない場合、列は非表示になります。  
  
#### <a name="example-for-controlling-the-text-box-value-for-a-missing-field"></a>存在しないフィールドのテキスト ボックス値を制御する例  
 存在しないフィールドの値を指定文字列で置き換えるには、カスタム コードを作成して、フィールドが存在しない場合にそのフィールド値の代わりに使用できる文字列が返されるようにする必要があります。 たとえば、次のカスタム コード関数を実行すると、フィールドが存在する場合はフィールドの値が返され、フィールドが存在しない場合は 2 番目のパラメーターとして指定したメッセージが返されます。  
  
```  
Public Function IsFieldMissingThenString(field as Field, strMessage as String) as String  
 If (field.IsMissing) Then  
  Return strMessage  
 Else   
  Return field.Value  
  End If  
End Function  
```  
  
 この関数をテキスト ボックスで使用するには、次の式を Value プロパティに追加します。  
  
 `=Code.IsFieldMissingThenString(Fields!FieldName,"Missing")`  
  
 テキスト ボックスには、フィールド値または指定した文字列が表示されます。  
  
### <a name="using-extended-field-properties"></a>拡張フィールド プロパティの使用  
 拡張フィールド プロパティは、データ処理拡張機能によってフィールドに定義された追加プロパティであり、データセットのデータ ソースの種類に基づいて決定されます。 拡張フィールド プロパティには、定義済みのものと、データ ソースの種類に固有のものがあります。 詳細については、「[Analysis Services データベースに対する拡張フィールド プロパティ &#40;SSRS&#41;](../report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)」を参照してください。  
  
 式の評価がそのフィールドに対してサポートされていないプロパティを指定する場合`null`(`Nothing`で[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])。 データ プロバイダーが拡張フィールド プロパティをサポートしていないか、クエリを実行すると、フィールドが検出されなかった場合、プロパティの値は場合`null`(`Nothing`で[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) 型のプロパティの`String`と`Object`と型のプロパティのゼロ (0)`Integer`します。 データ処理拡張機能は、この構文を含むクエリを最適化することにより、定義済みのプロパティを利用する場合があります。  
  
## <a name="see-also"></a>参照  
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](../report-data/report-datasets-ssrs.md)  
  
  