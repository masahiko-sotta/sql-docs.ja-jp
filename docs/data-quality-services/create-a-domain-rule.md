---
title: ドメイン ルールの作成
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.testdomainrule.f1
- sql13.dqs.dm.rules.f1
ms.assetid: 339fa10d-e22c-4468-b366-080c33f1a23f
author: swinarko
ms.author: sawinark
ms.openlocfilehash: c6a73d3f0dca65d0feb74cf572754351ccf86c7a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245479"
---
# <a name="create-a-domain-rule"></a>ドメイン ルールの作成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でドメイン ルールを作成する方法について説明します。 ドメイン ルールとは、ドメイン値の検証、修正、および標準化のために使用される条件です。 ドメイン値が正確で、ビジネス要件に準拠していると見なされるためには、ドメイン ルールがドメイン全体に当てはまる必要があります。 ドメイン ルールには検証規則を含めることができます。検証規則は、データ品質プロジェクトでドメイン値の検証に使用され、データの修正には使用されません。 また、標準化規則を含めることもできます。標準化規則は、有効なデータに対して適用され、データ修正で使用されます。  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Prerequisites"></a>応募  
 ドメイン ルールを作成するには、ドメイン管理アクティビティでナレッジ ベースとドメインを開いておく必要があります。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 ドメイン ルールを作成するには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="Build"></a>ドメインルールの作成  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、ナレッジ ベースを開くか作成します。 アクティビティとして **[ドメイン管理]** を選択した後に、 **[開く]** または **[作成]** をクリックします。 詳細については、「 [ナレッジ ベースの作成](../data-quality-services/create-a-knowledge-base.md) 」または「 [ナレッジ ベースを開く](../data-quality-services/open-a-knowledge-base.md)」を参照してください。  
  
    > [!NOTE]  
    >  Data Quality Service クライアントのドメイン管理用のページには、それぞれ異なるドメイン管理操作に対応する 5 つのタブが含まれています。 ウィザード ベースのプロセスではないため、任意の管理操作を個別に実行することができます。  
  
3.  
  **[ドメイン管理]** ページの **[ドメイン リスト]** から、ドメイン ルールを作成するドメインを選択するか、新しいドメインを作成します。 新しいドメインを作成する必要がある場合は、「 [ドメインの作成](../data-quality-services/create-a-domain.md)」を参照してください。  
  
4.  
  **[ドメイン ルール]** タブをクリックします。  
  
5.  
  **[新しいドメイン ルールの追加]** をクリックし、ナレッジ ベース内で一意の名前とルールの説明を入力します。  
  
6.  ルールが実行されるようにする場合は、 **[アクティブ]** を選択します (既定値)。実行されないようにする場合は選択を解除します。  
  
7.  
  **[ルールの作成]** ペインで、ルールの句のボックスのドロップダウン リストから条件を選択します。  
  
8.  条件に値が必要な場合は、対応するテキスト ボックスに値を入力します。  
  
9. 別の句が必要な場合は、 **[選択した句に新しい条件を追加]** アイコンをクリックします。  
  
10. 演算子として、 **[AND]** または **[OR]** を選択します。  
  
11. ドロップダウン リストから条件を選択し、必要に応じてオペランドの値を入力します。  
  
12. 一覧の句の順序を変更するには、句を選択して上下の矢印をクリックします。 句が実行される順序が変わるため、結果に影響する可能性があります。  
  
13. 必要に応じてさらに句を追加します。 句を削除する場合は、削除する句を選択し、 **[選択した句の削除]** をクリックします。  
  
14. 必要に応じて、上の手順を繰り返して新しいルールを追加します。  
  
15. 検証規則を実装した場合の値への影響を確認するには、 **[ドメインの値に対するドメイン ルールの影響を分析します]** アイコンをクリックします。  
  
16. 以下のテストの手順に進みます。  
  
##  <a name="Test"></a>ドメインルールのテスト  
  
1.  ルールを 1 つ選択した状態で、 **[テスト データについて選択したドメイン ルールを実行します]** アイコンをクリックします。  
  
2.  [ドメイン ルールのテスト] ダイアログ ボックスで、 **[ドメイン ルールの新しいテスト用語を追加]** アイコンをクリックします。 テストする値を入力し、 必要に応じてその他の値を入力します。 値を削除する場合は、削除する値を選択し、 **[選択したテスト用語を削除]** アイコンをクリックします。  
  
3.  
  **[すべての用語でドメイン ルールをテスト]** アイコンをクリックします。  
  
4.  各用語の妥当性を確認します。 チェック マークは "適切"、十字型は "エラー"、三角形は "無効" を表します。  
  
5.  完了したら、テスト ダイアログ ボックスの **[閉じる]** をクリックします。  
  
6.  必要に応じて、他のルールに対して上の手順を繰り返します。  
  
7.  以下の適用の手順に進みます。  
  
##  <a name="Apply"></a>ドメインルールの適用  
  
1.  
  **[すべてのルールを適用する]** をクリックして、ドメインの値にルールを適用します。 
  **[すべてのルールを適用する]** をクリックすると、ルールの影響を受ける各状態の値の数がポップアップ画面に表示されます。 そのままルールを適用する場合は **[はい]** を、ルールの適用を中止する場合は **[いいえ]** をクリックします。 
  **[はい]** をクリックした場合は、 **[OK]** をクリックして結果のポップアップ画面を閉じます。  
  
    > [!NOTE]  
    >  ルールを作成または変更するときには、変更を保存する必要はありませんが、 変更を有効にするにはルールを適用する必要があります。  
  
2.  ドメイン ルールに加えた変更を削除して、以前に適用したルールに戻すには、 **[すべての変更の破棄]** をクリックします。これにより、前回ルールを適用した後に加えた変更は適用されなくなります。 ドメインの値の妥当性は、破棄された変更ではなく、以前に適用したルールに従って更新されます。  
  
3.  
  **[完了]** をクリックし、「 [ドメイン管理アクティビティの終了](https://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)」の説明に従ってドメイン管理アクティビティを完了します。  
  
##  <a name="FollowUp"></a>補足情報: ドメインルールを作成した後  
 ドメイン ルールを作成した後、ドメインで他のドメイン管理タスクを実行したり、ナレッジ検出を実行してナレッジをドメインに追加したり、照合ポリシーをドメインに追加することができます。 詳しくは、「[ナレッジ検出の実行](../data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」、または「[照合ポリシーの作成](../data-quality-services/create-a-matching-policy.md)」をご覧ください。  
  
##  <a name="Conditions"></a>ドメインルールの条件  
 次の表は、ドメイン ルールで適用できる条件と、適用の例を示しています。  
  
 ドメイン ルールを適用すると、そのルールが失敗したドメイン値が "無効" に指定されます。 "無効" に指定された値は、無効になった原因のルールが削除されるか、非アクティブ化されるか、失敗しないように変更された場合、"適切" に変更されます。 手動で "無効" に指定した値は (ドメイン管理アクティビティの [ドメイン値] タブを使用)、失敗したルールが削除、非アクティブ化、または変更されても "無効" (手動で指定した状態) のままです。  
  
 ドメイン ルールに明確な条件が含まれている場合、その条件では、特定の値だけでなくその値のシノニムにもルールのロジックが適用されます。 明確な条件とは、"値が次の値と等しい"、"値が次の値と等しくない"、"値が次の中に存在する"、または "値が次の中に存在しない" です。 たとえば、"For 'City', Value is equal to 'Los Angeles'" というドメイン ルールでは、 'Los Angeles' と 'LA' がシノニムであれば、どちらも正しい値です。 一方、"For City, Value ends with 's'" など、明確な条件を含まないルールでは、"Los Angeles" は正しくなりますが、そのシノニムの "LA" はエラーになります。  
  
 ドメイン ルールを作成するときには、いくつかの選択肢があります。 たとえば、値が A、B、C のいずれかの文字で始まるかどうかを検証するには、複雑な条件を含む単純なルール (パイプ文字を含む正規表現など) を作成することも、複数の単純な条件を含む複雑なルールを作成することもできます。 たとえば、前者の例は "Value contains regular expression (^A|^B|^C)" です。 後者の例は、"'Value begins with A' OR 'Value begins with B' OR 'Value begins with C'" です。  
  
|条件|説明|例|  
|---------------|-----------------|-------------|  
|長さが次の値と等しい|オペランドで指定された文字数の文字で構成される値のみが有効になります。|オペランドの例: 3<br /><br /> 有効な値: BB1<br /><br /> 無効な値: AA|  
|長さが次の値以上|オペランドで指定された文字数以上の文字で構成される値のみが有効になります。|オペランドの例: 3<br /><br /> 有効な値: BB1、BBAA<br /><br /> 無効な値: AA|  
|長さが次の値以下|オペランドで指定された文字数以下の文字で構成される値のみが有効になります。|オペランドの例: 3<br /><br /> 有効な値: BB1、AA<br /><br /> 無効な値: BBAA|  
|値が次の値と等しい|オペランドと同じ値のみが有効になります。|オペランドの例: BB1<br /><br /> 有効な値: BB1<br /><br /> 無効な値: BB、BB1#|  
|値が次の値と等しくない|オペランドと同じではない値のみが有効になります。|オペランドの例: BB1<br /><br /> 有効な値: BB、BB1#<br /><br /> 無効な値: BB1|  
|値が次の値を含む|すべての文字が任意の順序でオペランドに含まれる値のみが有効になります。|オペランドの例: A1<br /><br /> 有効な値: A1、AA1<br /><br /> 無効な値: 1A、AA|  
|値が次の値を含まない|オペランドに含まれていない値のみが有効になります。|オペランドの例: A1<br /><br /> 有効な値: 1A、AA<br /><br /> 無効な値: A1、AA1|  
|値が次の値で始まる|オペランド内の文字で始まる値のみが有効になります。|オペランドの例: AA<br /><br /> 有効な値: AA1<br /><br /> 無効な値: 1AAB|  
|値が次の値で終わる|オペランド内の文字で終わる値のみが有効になります。|オペランドの例: AA<br /><br /> 有効な値: 1AA<br /><br /> 無効な値: 1AAB|  
|値が数値である|SQL Server の数値データ型を持つ値のみが有効になります。 これには、int、decimal、float などが含まれます。|オペランドの例: N/A<br /><br /> 有効な値: 1、25、345.1234<br /><br /> 無効な値: 2b、bcdef|  
|値が日付または時刻である|SQL Server の日付/時刻データ型を持つ値のみが有効になります。 これには、datetime、time、date などが含まれます。|オペランドの例: N/A<br /><br /> 有効な値: 1916-06-04、1916-06-04 18:24:24、March 21, 2001、5/18/2011、18:24:24<br /><br /> 無効な値: March 213, 2006|  
|値が次の中に存在する|オペランドのセットの中に存在する値のみが有効になります。<br /><br /> セット内の値を入力するには、まず、オペランドのテキスト ボックスをクリックします。次に、1 つ目の値を入力し、Enter キーを押して、2 つ目の値を入力します。この操作を、セットに必要な値の数だけ繰り返します。最後にもう一度、オペランドのテキスト ボックスをクリックします。 セット内の値の間に自動的にコンマが追加されます。 値の間で Enter キーを押す代わりにコンマを入力して 1 つの文字列を入力した場合 ("A1, B1" など)、その文字列は、セット内の 1 つの値と見なされます。|オペランドの例: [A1, B1]<br /><br /> 有効な値: A1、B1<br /><br /> 無効な値: AA、11|  
|値が次の中に存在しない|オペランドのセットの中に存在しない値のみが有効になります。|オペランドの例: [A1, B1]<br /><br /> 有効な値: AA、11<br /><br /> 無効な値: A1、B1|  
|値が次のパターンと一致する|オペランド内の文字、数字、または特殊文字のパターンと一致する値のみが有効になります。<br /><br /> 任意の文字 (A ～ Z) を任意の文字のパターンとして使用できます (大文字と小文字は区別されません)。 任意の数字 (0 ～ 9) を任意の数字のパターンとして使用できます。 文字および数字を除く任意の特殊文字をその特殊文字のパターンとして使用できます。 角かっこ ([]) は、省略可能な一致を定義する場合に使用します。|オペランドの例: AA:000 ( *任意* の 2 文字の後にコロン (:) が続き、その後に *任意* の 3 桁の数字が続くパターン)。<br /><br /> 有効な値: AB:012、df:257<br /><br /> 無効な値: abc:123、FJ-369<br /><br /> DQS でのパターンのルールの詳細および例については、「 [DQS ドメイン ルールでのパターン検索](https://blogs.msdn.com/b/dqs/archive/2012/10/08/pattern-matching-in-dqs-domain-rules.aspx)」を参照してください。|  
|値が次のパターンと一致しない|オペランド内の文字、数字、または特殊文字のパターンと一致しない値のみが有効になります。|オペランドの例: A1 ( *任意* の 1 文字とその後に *任意* の 1 桁の数字が続くパターンに一致しない値)。<br /><br /> 有効な値: AB1、A、A:5<br /><br /> 無効な値: B7、c9|  
|値が次のパターンを含む|オペランド内の文字、数字、または特殊文字のパターンを含む値のみが有効になります。|オペランドの例: AA-12 ( *任意* の 2 文字の後にハイフン (-) が続き、その後に *任意* の 2 桁の数字が続くパターンを含む値)。<br /><br /> 有効な値: AAA-01、ab-975<br /><br /> 無効な値: A7、AA-6、C-45、aa;98|  
|値が次のパターンを含まない|オペランド内の文字パターンを含まない値のみが有効になります。|オペランドの例: AB-12 ( *任意* の 2 文字の後にハイフン (-) が続き、その後に *任意* の 2 桁の数字が続くパターンを含まない値)。<br /><br /> 有効な値: A7、AA-6、C-45、aa;98<br /><br /> 無効な値: AAA-01、ab-975|  
|値が正規表現と一致する|オペランド内の正規表現と一致する値のみが有効と見なされます。<br /><br /> "^"、"$" などのアンカーを正規表現に含めないでください。これらのアンカーは、この条件を含む句に自動的に追加されます。 (または、"^" アンカーと "$" アンカーを含む正規表現をかっこで囲むこともできます)。正規表現の詳細については、「[正規表現言語要素](https://go.microsoft.com/fwlink/?LinkId=225561)」を参照してください。|オペランドの例: [1-5]+ (1 ～ 5 の数字の 1 回以上の繰り返し)<br /><br /> 有効な値: 123、12345、14352<br /><br /> 無効な値: 456、ABC|  
|値が正規表現と一致しない|オペランド内の正規表現と一致しない値のみが有効と見なされます。|オペランドの例: [1-5]+ (1 ～ 5 の数字のみで構成されていない文字列)<br /><br /> 有効な値: 456、ABC<br /><br /> 無効な値: 123、123456、14352|  
  
  
