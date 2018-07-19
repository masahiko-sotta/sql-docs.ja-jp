---
title: スキーマ比較を使用して各種のデータベース定義を比較する方法 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.data.tools.schemacompare.SchemaCompareOptionsDialog
- sql.data.tools.schemacompare.watermark.f1
- sql.data.tools.schemacompare.f1
- sql.data.tools.schemacompare.connectiondialog.f1
- sql.data.tools.schemacompare.connectiondialog.error.f1
ms.assetid: 7f0905a4-081c-46e2-bd7d-325b63e5c675
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b3b52f87fe2c144a71d5826cc66970c0f18e5d1
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094753"
---
# <a name="how-to-use-schema-compare-to-compare-different-database-definitions"></a>スキーマ比較を使用して各種のデータベース定義を比較する方法
SQL Server Data Tools (SSDT) に付属しているスキーマ比較ユーティリティを使用して、2 つのデータベース定義を比較できます。  比較のソースとターゲットには、接続されているデータベース、SQL Server データベース プロジェクトまたはスナップショット、または .dacpac ファイルを指定できます。  比較結果は、ターゲットをソースと同じにするためにターゲットに実行する必要があるアクションのセットとして表示されます。  比較が完了したら、ターゲットを直接更新するか (ターゲットがプロジェクトまたはデータベースの場合)、同じ効果がある更新スクリプトを生成することができます。  
  
ソースとターゲットとの相違点はグリッドに表示されるので、簡単に確認できます。  それぞれの相違点を結果グリッドまたはスクリプト形式でドリル インして確認できます。  確認後、特定の相違点を選択的に除外できます。  
  
SQL Server データベース プロジェクトの一部またはスタンドアロン ファイルとして、比較を保存できます。  比較の範囲および更新の特性を制御するオプションを設定することもできます。  さらに、比較を保存できるので、同じ比較を後で簡単に繰り返したり、新しい比較の起点として使用したりすることができます。  
  
次の手順では、データベース プロジェクトのスキーマを、接続されているデータベースと比較します。  
  
> [!WARNING]  
> 比較のターゲットとしてプロジェクトを指定した場合、プロジェクトのパスとしてサポートされる長さ (ドライブ文字、コロン、および先頭のバックスラッシュを除く) は、最大 256 文字です。 プロジェクトのパスが 256 文字を超えていても、スキーマをデータベースまたは別のプロジェクトと比較することはできます。 ただし、スキーマを更新することはできません。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」および「[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)」に示されているこれまでの手順で作成したエンティティを使用します。  
  
### <a name="to-compare-database-definitions"></a>データベース定義を比較するには  
  
1.  **[SQL]** メニューの **[スキーマ比較]** をポイントし、**[新しいスキーマ比較]** をクリックします。  
  
    または、**ソリューション エクスプローラー**で **TradeDev** プロジェクトを右クリックし、**[スキーマ比較]** をクリックします。  
  
    **[スキーマ比較]** ウィンドウが開き、`SqlSchemaCompare1` などの名前が Visual Studio によって自動的に割り当てられます。  
  
    **[スキーマの比較]** ウィンドウのツール バーのすぐ下に、2 つのドロップダウン メニューとその間に緑の矢印が表示されます。 これらのメニューを使用して、比較のソースおよびターゲットとなるデータベース定義を選択できます。  
  
2.  **[ソースの選択]** ボックスの一覧の **[ソースの選択]** をクリックし、**[ソース スキーマの選択]** ダイアログ ボックスを開きます。  
  
    プロジェクト名を右クリックして **[スキーマ比較]** ウィンドウを開いた場合は、ソース スキーマが既に設定されているので、手順 4 に進むことができます。  
  
3.  **[プロジェクト]** オプション ボタンをクリックし、前の手順で作成した **TradeDev** データベース プロジェクトを選択します。  
  
4.  **[スキーマ比較]** ウィンドウで **[ターゲットの選択]** ボックスの一覧の **[ターゲットの選択]** をクリックし、**[ターゲット スキーマの選択]** ダイアログ ボックスを開きます。 **[スキーマ]** セクションの **[データベース]** オプション ボタンをクリックし、**[新しい接続]** をクリックします。  
  
5.  **[接続のプロパティ]** ダイアログ ボックスで、`TradeDev` データベースがあるサーバーの名前を入力し、認証に使用する正しい資格情報が指定されていることを確認します。 **[データベースへの接続]** で **TradeDev** をクリックし、**[OK]** をクリックします。  
  
    **[スキーマ比較]** ウィンドウのツール バーにある **[オプション]** をクリックして、比較対象のオブジェクトや無視する相違の種類などの設定を指定することもできます。  
  
6.  **[スキーマ比較]** ウィンドウのツール バーにある **[比較]** をクリックして、比較プロセスを開始します。  
  
    比較が完了すると、プロジェクトとデータベースの間の構造上の相違点がウィンドウ上部の**結果**ペインに表示されます。 既定では、比較結果のすべての相違点はアクション (削除、変更、追加など) 別にグループ化されます。 **結果**ペインには、データベース定義間で異なっているデータベース オブジェクトが 1 行に 1 つ表示されます。 ソース スキーマまたはターゲット スキーマ (あるいはその両方) のオブジェクトと、ターゲット オブジェクトをソース オブジェクトと同じにするためにターゲット スキーマに対して実行されるアクションが、各行に示されます。  オブジェクトがリファクタリングされ、名前が変更されたか新しいスキーマに移動された場合は、ソース名とターゲット名が異なり、不一致を強調するためにソース名が太字フォントで表示されます。  
  
    既定では、両方のスキーマで同じオブジェクトまたは更新の対象としてサポートされていないオブジェクト (たとえばビルトイン オブジェクト) は、結果リストで非表示になります。  ツール バーの適切なフィルター ボタンをクリックして、非表示のオブジェクトを表示できます。  
  
    グループ化の設定を変更するには、ツール バーにある **[結果のグループ化]** ボックスの一覧をクリックします。  結果をオブジェクトの種類別にグループ化するには (テーブル別、ビュー別、ストアド プロシージャ別など)、**[種類]** をクリックします。  
  
7.  `Products` グループの `Tables` テーブルを探します。 行をクリックすると、テーブルのソース定義とターゲット定義が**オブジェクトの定義**ペインに表示され、相違点が強調表示されます。 **結果**ペインの `Products` テーブルの行を展開し、テーブル内の相違がある特定の要素について詳細情報を確認することもできます。  
  
8.  既定では、すべての相違点が [ターゲットの更新] アクションの対象になります。 同期しない相違点は除外できます。 除外するには、各行の中央にある **[アクション]** 列をオフにします。 または、スキーマ ペイン内の行を右クリックし、**[除外]** をクリックします。 行が直ちに灰色表示されます。ターゲット データベースを更新する際に、この行は、保留中の変更であるとは見なされません。  
  
    グループ行を右クリックし、**[すべて除外]** または **[すべて追加]** をクリックする方法もあります。これは、そのグループ内のすべての相違点をオフまたはオンにするのと同じです。 この方法は、結果をスキーマ別にグループ化する場合に、特定のスキーマに対するすべての変更を対象に含めるか除外するのに便利です。  
  
    > [!WARNING]  
    > 除外する行に依存オブジェクト (**ビュー**行で参照されている**テーブル**行など) がある場合、除外した行は無効になりますが、チェック ボックスはオフになりません。 依存するすべての行がオフになったときに、無効にされた行がオフになります。 また、行がリファクタリングされる (名前が変更される、または別のスキーマに移動される) と、その行および行に依存するすべての子行のチェック ボックスが無効になります。  
    >   
    > 比較を更新すると、スキップするように指定した相違点は無視されます。  
  
ターゲットのスキーマを更新する場合は、2 つの選択肢があります。 ターゲットがデータベースまたはプロジェクトの場合は、**[スキーマ比較]** ウィンドウからターゲットを直接更新できます。ターゲットがデータベースまたはデータベース ファイルの場合は、更新スクリプトを生成することができます。  生成されたスクリプトは Transact\-SQL エディターに表示され、このエディター内からスクリプトを検査し、データベースに対して実行することができます。 次の手順では、これらのオプションについて詳しく説明します。  
  
> [!WARNING]  
> 更新は失敗します。原因は、変更の中に列を NOT NULL から NULL に変更するものがあり、その結果データ損失が発生するためです。 更新を続行するには、スキーマ比較のツール バーにある **[オプション]** (左から 5 番目のボタン) をクリックし、**[データ損失が発生する場合に増分配置をブロック]** オプションをオフにします。  
  
### <a name="to-update-directly-in-the-schema-compare-window"></a>[スキーマ比較] ウィンドウで直接更新するには  
  
1.  [スキーマ比較] ウィンドウのツール バーにある **[更新]** をクリックします。  
  
2.  生成された変更スクリプトを調べます。 [ファイル] メニューの [新規作成] を使用して、スクリプトを保存することもできます。 運用データベースを更新する権限がない場合など、このスクリプトを後で配置するように DBA に渡すことができるので便利です。  
  
3.  データベースを更新するために必要なアクセス許可がある場合は、編集ペインのツール バーにある **[クエリの実行]** をクリックしてスクリプトを実行します。  
  
### <a name="to-update-by-script"></a>スクリプトによって更新するには  
  
1.  [スキーマ比較] ウィンドウのツール バーにある **[スクリプトの生成]** (左から 4 番目のボタン) をクリックします。  
  
    生成されたスクリプトが、新しい Transact\-SQL エディター ウィンドウに表示されます  
  
    > [!WARNING]  
    > この動作は、SSDT スナップショット プロセスによって生成された .dacpac ファイルのみでサポートされます。  現時点では、SQL データ層アプリケーション (DAC) ツールまたは DAC フレームワークによって生成された .dacpac ファイルを対象にすることはできません。  
  
2.  生成された変更スクリプトを調べます。 **[ファイル]** メニューの [保存] または [名前を付けて保存] を使用して、スクリプトを保存することもできます。  
  
    保存したスクリプトは、運用データベースを更新する権限がない場合に便利です。 そのような場合は、スクリプトを DBA に渡して後で配置してもらうことができます。  
  
    または、Transact\-SQL エディターを適切なサーバーに接続し、スクリプトを直接実行できます。 この手順を実行する前に、データベースを作成または更新するために必要なアクセス許可があることを確認してください。 データベースを更新するために必要なアクセス許可がある場合は、編集ペインのツール バーにある **[クエリの実行]** をクリックしてスクリプトを実行します。  
  
3.  **[接続]** ボタンをクリックします。 この操作により、現在のサーバーに接続されるか、[サーバーに接続] ダイアログ ボックスでインスタンスの入力または選択を求められます。  データベース名はスクリプトでコマンド変数として定義されていることに注意してください。  
  
4.  スクリプトを検査し、必要に応じて、ターゲット データベース名および関連プレフィックスとファイル パスを定義するコマンド変数を変更します。  
  
5.  編集ペインのツール バーにある **[実行]** をクリックして、スクリプトを実行します。  
  