---
title: Oracle スキーマ (OracleToSQL) の変換 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 638c16de8312456410c14e38fa632085e504913e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266154"
---
# <a name="converting-oracle-schemas-oracletosql"></a>Oracle スキーマの変換 (OracleToSQL)
Oracle に接続すると後に、接続されている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、プロジェクトの設定とデータ マッピング オプションでは、Oracle データベースのオブジェクトを変換できますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース オブジェクト。  
  
## <a name="the-conversion-process"></a>変換プロセス  
Oracle からオブジェクトの定義は、データベース オブジェクトの変換と同様に変換して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト、および SSMA メタデータにこの情報を読み込みます。 インスタンスに情報は読み込まれません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 使用して、オブジェクトとそのプロパティを表示することができますし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラー。  
  
変換中は、SSMA は、出力ウィンドウに出力メッセージとエラー一覧 ウィンドウにエラー メッセージを出力します。 出力とエラー情報を使用して、Oracle データベース、または必要な変換の結果を得るため、変換プロセスを変更しているかどうかを確認します。  
  
## <a name="setting-conversion-options"></a>変換オプションの設定  
オブジェクトを変換する前に、プロジェクトの変換オプションを確認して、**プロジェクト設定** ダイアログ ボックス。 このダイアログ ボックスを使用すると、SSMA が関数とグローバル変数に変換する方法を設定できます。 詳細については、次を参照してください。[プロジェクト設定&#40;変換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)します。  
  
## <a name="conversion-results"></a>変換結果  
次の表は、変換されますが、Oracle のオブジェクトし、その結果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト。  
  
|||  
|-|-|  
|Oracle オブジェクト|SQL Server オブジェクトの結果として得られる|  
|関数|関数を直接変換できる場合[!INCLUDE[tsql](../../includes/tsql-md.md)]、SSMA 関数を作成します。<br /><br />場合によっては、関数は、ストアド プロシージャに変換する必要があります。 この場合は、SSMA では、ストアド プロシージャおよびストアド プロシージャを呼び出す関数を作成します。|  
|手順|プロシージャを直接変換できる場合[!INCLUDE[tsql](../../includes/tsql-md.md)]SSMA は、ストアド プロシージャを作成します。<br /><br />場合によっては、自律的なトランザクションでストアド プロシージャを呼び出す必要があります。 この場合は、SSMA が 2 つのストアド プロシージャを作成します: ストアド プロシージャのいずれかの手順と、実装を呼び出すために使用する別の実装します。|  
|パッケージ|SSMA では、一連のストアド プロシージャと関数のようなオブジェクト名では統合を作成します。|  
|シーケンス|SSMA は (SQL Server 2012 または SQL Server 2014) のシーケンス オブジェクトを作成または Oracle のシーケンスをエミュレートします。|  
|インデックスおよびトリガーなどの依存オブジェクトを持つテーブル|SSMA は、依存オブジェクトをテーブルを作成します。|  
|トリガーなどの依存オブジェクトを見る|SSMA では、依存オブジェクトをビューを作成します。|  
|具体化されたビュー|**SSMA では、いくつかの例外で SQL server にインデックス付きビューを作成します。具体化されたビューには、次の構成要素の 1 つ以上が含まれている場合、変換は失敗します。**<br /><br />ユーザー定義関数<br /><br />不明確フィールド/[関数/式の選択] で、または GROUP BY 句<br /><br />Float 列で SELECT * の使用法、または GROUP BY 句 (前の問題の特殊なケース)<br /><br />カスタム データ型の (税込入れ子になったテーブル)<br /><br />COUNT (distinct&lt;フィールド&gt;)<br /><br />FETCH<br /><br />外部結合 (LEFT、RIGHT、または FULL)<br /><br />サブクエリでは、その他のビュー<br /><br />ランク付け、潜在顧客、ログインが、<br /><br />MIN、MAX<br /><br />UNION、マイナス、INTERSECT します。<br /><br />HAVING|  
|トリガー|**SSMA では、次の規則に基づくトリガーが作成されます。**<br /><br />前に、トリガーは、INSTEAD of トリガーに変換されます。<br /><br />トリガーは AFTER トリガーに変換します。<br /><br />INSTEAD OF トリガーは、INSTEAD of トリガーに変換されます。 同じ操作で定義された複数の INSTEAD OF トリガーは、1 つのトリガーに結合されます。<br /><br />カーソルを使用して行レベルのトリガーがエミュレートされます。<br /><br />トリガーの連鎖は、複数の個々 のトリガーに変換されます。|  
|シノニム|**シノニムは、次のオブジェクトの種類に対して作成されます。**<br /><br />テーブルとオブジェクト テーブル<br /><br />ビューとオブジェクトのビュー<br /><br />ストアド プロシージャ<br /><br />関数<br /><br />**次のオブジェクトのシノニムは解決されており、直接オブジェクト参照によって置き換えられます。**<br /><br />シーケンス<br /><br />パッケージ<br /><br />Java クラス スキーマ オブジェクト<br /><br />ユーザー定義オブジェクトの種類<br /><br />別のシノニムのシノニムでは、移行できないし、エラーとしてマークされます。<br /><br />シノニムは、Materialized ビューは作成されません。|  
|ユーザー定義型|**SSMA では、ユーザー定義型の変換のサポートは提供されません。PL/SQL プログラムでその使用法を含むユーザー定義型は、次の規則によって実行される特別な変換のエラーでマークされます。**<br /><br />ユーザー定義型のテーブルの列は、varchar (8000) に変換されます。<br /><br />ユーザーの引数は、ストアド プロシージャに型を定義または関数は varchar (8000) に変換されます。<br /><br />PL/SQL ブロック内のユーザー定義型の変数は、varchar (8000) に変換されます。<br /><br />オブジェクト テーブルは、標準のテーブルに変換されます。<br /><br />オブジェクトのビューは、標準的なビューに変換されます。|  
  
## <a name="converting-oracle-database-objects"></a>Oracle データベースのオブジェクトの変換  
Oracle データベースのオブジェクトを変換する、変換するオブジェクトを選択し、SSMA 変換を実行します。 変換中に出力メッセージを表示する、**ビュー**メニューの **出力**します。  
  
**Oracle オブジェクトを SQL Server の構文に変換するには**  
  
1.  Oracle メタデータ エクスプ ローラーで、Oracle サーバーを展開し、展開**スキーマ**します。  
  
2.  変換するオブジェクトを選択します。  
  
    -   すべてのスキーマを変換する場合は、横にチェック ボックスを選択します**スキーマ**します。  
  
    -   変換または省略データベース、スキーマ名の横にあるチェック ボックスを選択します。  
  
    -   変換またはオブジェクトのカテゴリの省略は、スキーマを展開し、オンまたはカテゴリの横にあるチェック ボックスをオフにします。  
  
    -   変換または個々 のオブジェクトの省略は、カテゴリ フォルダーを展開し、オンまたはオブジェクトの横にチェック ボックスをオフにします。  
  
3.  右クリックし、選択したすべてのオブジェクトを変換する**スキーマ**選択**スキーマの変換**します。  
  
    オブジェクトまたはその親フォルダーを右クリックして選択し、個々 のオブジェクトまたはオブジェクトのカテゴリを変換することも**スキーマの変換**します。  
  
## <a name="viewing-conversion-problems"></a>変換の問題を表示します。  
いくつかの Oracle オブジェクトを変換しない可能性があります。 変換の概要レポートを表示することによってコンバージョンの成功率を指定できます。  
  
**概要レポートを表示するには**  
  
1.  Oracle メタデータ エクスプ ローラーで選択**スキーマ**します。  
  
2.  右側のウィンドウで、選択、**レポート**タブ。  
  
    このレポートには、変換または評価されているすべてのデータベース オブジェクトの評価の概要レポートが表示されます。 個々 のオブジェクトの概要レポートを表示することもできます。  
  
    -   個々 のスキーマのレポートを表示するには、Oracle メタデータ エクスプ ローラーでスキーマを選択します。  
  
    -   個々 のオブジェクトのレポートを表示するには、Oracle メタデータ エクスプ ローラーで、オブジェクトを選択します。 変換の問題のあるオブジェクトは赤いエラー アイコンがあります。  
  
オブジェクトの変換に失敗した場合は、変換エラーを発生させた構文を表示することができます。  
  
**個々 の変換の問題を表示するには**  
  
1.  Oracle メタデータ エクスプ ローラーで、**スキーマ**します。  
  
2.  赤いエラー アイコンが表示されるスキーマを展開します。  
  
3.  スキーマの下に赤いエラー アイコンが付いているフォルダーを展開します。  
  
4.  赤いエラー アイコンを含むオブジェクトを選択します。  
  
5.  右側のウィンドウでをクリックして、**レポート**タブ。  
  
6.  上部にある、**レポート** タブは、ドロップダウン リスト。 一覧表示されている場合**統計**、選択範囲を変更**ソース**します。  
  
    SSMA は、ソース コードとコードのすぐ上のいくつかのボタンに表示されます。  
  
7.  をクリックして、**次の問題**ボタンをクリックします。 これは、右向き矢印の付いた赤いエラー アイコンです。  
  
    SSMA は、現在のオブジェクトで見つかった最初の問題のあるソース コードを強調表示されます。  
  
変換できなかった項目ごとにそのオブジェクトを決定する必要があります。  
  
-   プロシージャのソース コードを変更することができます、 **SQL**タブ。  
  
-   削除または問題のあるコードを変更するには、Oracle データベースでオブジェクトを変更することができます。 SSMA に更新されたコードを読み込むには、メタデータを更新する必要があります。 詳細については、次を参照してください。 [Oracle データベースに接続する&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)します。  
  
-   オブジェクトは、移行から除外できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーと Oracle メタデータ エクスプ ローラーにオブジェクトを読み込む前に、項目の横にあるチェック ボックスをオフに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と Oracle からデータを移行します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順が、 [SQL Server に変換されたオブジェクトを読み込む](loading-converted-database-objects-into-sql-server-oracletosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server にデータベースを移行する Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
