---
title: レポートでの式の使用 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- expressions [Reporting Services], about expressions
ms.assetid: 76b9ed31-5aec-40fc-bb88-a1c1b0ab3fc3
caps.latest.revision: 57
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ecdadef4e49f3630c78fc33c1c6f490deda26b5f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274748"
---
# <a name="expression-uses-in-reports-report-builder-and-ssrs"></a>レポートでの式の使用 (レポート ビルダーおよび SSRS)
  パラメーター、クエリ、フィルター、レポート アイテムのプロパティ、グループ化と並べ替え定義、テキスト ボックスのプロパティ、ブックマーク、ドキュメント マップ、ページ ヘッダーとページ フッターの動的なコンテンツ、画像、および動的データ ソース定義の値を指定または計算するために、レポート定義には随所に式が使用されています。 このトピックでは、レポートの内容と外観を変更するために式を使用できるさまざまな場所の例を示します。 この一覧がすべてではありません。 式 (**[fx]**) ボタンが表示されるダイアログ ボックスや、**[\<式...>]** が表示されるドロップダウン リストで、あらゆるプロパティに式を設定できます。  
  
 式には単純式と複合式があります。 *単純式* には、1 つのデータセット フィールド、パラメーター、または組み込みフィールドへの参照が含まれます。 複合式には、複数の組み込み参照、演算子、および関数呼び出しを含めることができます。 たとえば、複合式には売上フィールドに適用される Sum 関数が含まれる場合があります。  
  
 式は [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]に書き込まれます。 式は等号 (=) で始まり、データセット フィールドとパラメーター、定数、関数、および演算子などの組み込みコレクションへの参照が後に続きます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Simple"></a> 単純式の使用  
 単純式は、角かっこで囲まれたデザイン画面やダイアログ ボックスに表示されます。たとえば、データセット フィールドは `[ProductID]`と表示されます。 単純式は、データセットからフィールドをテキスト ボックスにドラッグすると自動的に作成されます。 プレースホルダーが作成され、式により基になる値が定義されます。 デザイン画面とダイアログ ボックスでは、データ領域のセルかテキスト ボックスに式を直接入力することもできます (たとえば、 `[ProductID]`)。  
  
 次の表は、単純式の使用例を示します。 機能、設定プロパティ、プロパティの設定に通常使用するダイアログ ボックス、およびプロパティの値を示しています。 あらゆる式と同様に、デザイン画面、ダイアログ ボックス、プロパティ ペインに直接単純式を入力したり、[式] ダイアログ ボックスで単純式を編集できます。  
  
|機能|プロパティ、コンテキスト、およびダイアログ ボックス|プロパティ値|  
|-------------------|---------------------------------------|--------------------|  
|テキスト ボックスを表示するデータセット フィールドを指定します。|テキスト ボックス内のプレースホルダーの Value プロパティ。 [プレースホルダーのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`[Sales]`|  
|グループの集計値。|Tablix グループに関連付けられた行内のプレースホルダーの Value プロパティ。 **[テキスト ボックスのプロパティ]** ダイアログ ボックスを使用します。|`[Sum(Sales)]`|  
|ページ番号が含まれます。|ページ ヘッダーに配置されるテキスト ボックス内のプレースホルダーの Value プロパティ。 [テキスト ボックスのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`[&PageNumber]`|  
|選択したパラメーター値を表示します。|デザイン画面のテキスト ボックス内のプレースホルダーの Value プロパティ。 [テキスト ボックスのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`[@SalesThreshold]`|  
|データ領域のグループ定義を指定します。|Tablix グループのグループ式。 [Tablix グループのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`[Category]`|  
|特定のフィールドの値をテーブルから除外します。|Tablix の式にフィルターを適用します。 [Tablix のプロパティ] ダイアログ ボックスの **[フィルター]** を使用します。|データ型には、 **[整数]** を選択します。<br /><br /> `[Quantity]`<br /><br /> `>`<br /><br /> `100`|  
|グループ フィルターの特定の値のみが含まれます。|Tablix グループの式にフィルターを適用します。 [Tablix グループのプロパティ] ダイアログ ボックスの **[フィルター]** を使用します。|`[Category]`<br /><br /> `=`<br /><br /> `Clothing`|  
|複数のフィールドの特定の値をデータセットから除外します。|Tablix のグループの式にフィルターを適用します。 [Tablix のプロパティ] ダイアログ ボックスの **[フィルター]** を使用します。|`=[Color]`<br /><br /> `<>`<br /><br /> `Red`<br /><br /> `=[Color]`<br /><br /> `<>`<br /><br /> `Blue`|  
|テーブル内の既存のフィールドに基づいて並べ替え順を指定します。|Tablix の式を並べ替えます。 [Tablix のプロパティ] ダイアログ ボックスの **[並べ替え]** を使用します。|`[SizeSortOrder]`|  
|レポート パラメーターにクエリ パラメーターをリンクします。|データセットのパラメーター コレクション。 [データセットのプロパティ] ダイアログ ボックスの **[パラメーター]** を使用します。|`[@Category]`<br /><br /> `[@Category]`|  
|パラメーターをメイン レポートからサブレポートに渡します。|サブレポートのパラメーター コレクション。 [サブレポートのプロパティ] ダイアログ ボックスの **[パラメーター]** を使用します。|`[@Category]`<br /><br /> `[@Category]`|  
  
 
  
##  <a name="Complex"></a> 複合式の使用  
 複合式には、複数の組み込み参照、演算子、関数呼び出しを含めることができ、デザイン画面には `<<Expr>>`として表示されます。 式のテキストを表示、または変更するには、 **[式]** ダイアログ ボックスを開くか、プロパティ ペインに直接入力する必要があります。 次の表には、設定プロパティ、プロパティの設定に通常使用するダイアログ ボックス、およびプロパティの値など、複合式を使用してデータを表示または編成したり、レポートの外観を変更したりする方法を示します。 ダイアログ ボックス、デザイン画面、またはプロパティ ペインに直接式を入力できます。  
  
|機能|プロパティ、コンテキスト、およびダイアログ ボックス|プロパティ値|  
|-------------------|---------------------------------------|--------------------|  
|データセットの集計値を計算します。|テキスト ボックス内のプレースホルダーの Value プロパティ。 [プレースホルダーのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`=First(Fields!Sales.Value,"DataSet1")`|  
|同じテキスト ボックス内のテキストと式を連結します。|ページ ヘッダーまたはページ フッターに配置されるテキスト ボックス内のプレースホルダーの値。 [プレースホルダーのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`="This report began processing at " & Globals!ExecutionTime`|  
|異なるスコープ内のデータセットの集計値を計算します。|Tablix グループに配置されるテキスト ボックス内のプレースホルダーの値。 [プレースホルダーのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`=Max(Fields!Total.Value,"DataSet2)`|  
|値に応じてテキスト ボックス内のデータを書式設定します。|Tablix の詳細行のテキスト ボックス内のプレースホルダーの色。 [テキスト ボックスのプロパティ] ダイアログ ボックスの **[フォント]** を使用します。|`=IIF(Fields!TotalDue.Value < 10000,"Red","Black")`|  
|レポート全体で参照される値を 1 回計算します。|レポート変数の値。 [レポートのプロパティ] ダイアログ ボックスの **[変数]** を使用します。|`=Variables!MyCalculation.Value`|  
|データセットからの複数のフィールドの特定の値が含まれます。|Tablix のグループの式にフィルターを適用します。 [Tablix のプロパティ] ダイアログ ボックスの **[フィルター]** を使用します。|データ型には、 **[ブール]** を選択します。<br /><br /> `=IIF(InStr(Fields!Subcat.Value,"Shorts")=0 AND (Fields!Size.Value="M" OR Fields!Size.Value="S"),TRUE, FALSE)`<br /><br /> `=`<br /><br /> `TRUE`|  
|デザイン画面のテキスト ボックスを非表示にします。これは *Show*というブール型パラメーターを使用して切り替えることができます。|テキスト ボックスの Hidden プロパティ。 [テキスト ボックスのプロパティ] ダイアログ ボックスの **[表示]** を使用します。|`=Not Parameters!` *Show\<ブール型パラメーター>* `.Value`|  
|ページ ヘッダーまたはページ フッターの動的なコンテンツを指定します。|ページ ヘッダーまたはページ フッターに配置されるテキスト ボックス内のプレースホルダーの値。|`="Page " & Globals!PageNumber & " of "  & Globals!TotalPages`|  
|パラメーターを使用してデータ ソースを動的に指定します。|データ ソースの接続文字列。 [データ ソースのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`="Data Source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks2012"`|  
|ユーザーが選択した複数値パラメーターのすべての値を識別します。|テキスト ボックス内のプレースホルダーの値。 [Tablix のプロパティ] ダイアログ ボックスの **[フィルター]** を使用します。|`=Join(Parameters!MyMultivalueParameter.Value,", ")`|  
|他のグループがない Tablix に 20 行ごとに改ページを指定します。|Tablix のグループのグループ式。 [Tablix グループのプロパティ] ダイアログ ボックスの **[改ページ]** を使用します。 **[グループの各インスタンスの間]** を選択します。|`=Ceiling(RowNumber(Nothing)/20)`|  
|パラメーターに基づいて条件付き表示を指定します。|Tablix の Hidden プロパティ。 [Tablix のプロパティ] ダイアログ ボックスの **[表示]** を使用します。|`=Not Parameters!<` *ブール型パラメーター* `>.Value`|  
|特定のカルチャの書式に設定された日付を指定します。|データ領域のテキスト ボックス内のプレースホルダーの値。 [テキスト ボックスのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`=Fields!OrderDate.Value.ToString(System.Globalization.CultureInfo.CreateSpecificCulture("de-DE"))`|  
|文字列と小数点 2 桁のパーセンテージとして書式設定された数を連結します。|データ領域のテキスト ボックス内のプレースホルダーの値。 [テキスト ボックスのプロパティ] ダイアログ ボックスの **[全般]** を使用します。|`="Growth Percent: " & Format(Fields!Growth.Value,"p2")`|  
  
 
  
## <a name="see-also"></a>参照  
 [式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](report-parameters-report-builder-and-report-designer.md)   
 [フィルター式の例&#40;レポート ビルダーおよび SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [ページ ヘッダーとページ フッター&#40;レポート ビルダーおよび SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)   
 [テキストとプレース ホルダーの書式設定&#40;レポート ビルダーおよび SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [アイテムを非表示にする (レポート ビルダーおよび SSRS)](../report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  