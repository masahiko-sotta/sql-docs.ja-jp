---
title: 新しいスケジュール:スケジュールの編集 ページ (レポート マネージャー) |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 52a4d250-e185-4116-a29c-d809940a00fb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea1eed70c3eac8bac1c4141628e72ce0af8099c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108150"
---
# <a name="new-schedule-edit-schedule-page-report-manager"></a>新しいスケジュール:編集のスケジュール ページ (レポート マネージャー)
  [新しいスケジュール] ページまたは [スケジュールの編集] ページを使用すると、レポートのスケジュールを作成できます。 スケジュールはサブスクリプションで使用されます。その用途は、キャッシュされたレポートを更新、スナップショットをスタンドアロン アイテムとして作成、スナップショットをレポート履歴で作成することです。  
  
> [!NOTE]  
>  この機能は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
 自動的に実行されるレポートに対してのみ、スケジュールを作成できます。 レポートを自動的に実行するには、レポート サーバー データベースにレポート データ ソース資格情報を保存しておく必要があります。 詳細については、次を参照してください。[データ ソース プロパティ ページ&#40;レポート マネージャー&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md)します。  
  
 1 つのスケジュールの中で、複数の頻度を組み合わせて使用することができない場合があります。 たとえば、毎週金曜日の正午と 午後 4 時 00 分まで レポートを実行する場合、実行日を金曜日に指定した日単位のスケジュールを 2 つ作成し、1 つは開始時刻を正午に、 もう 1 つは開始時刻を午後 4 時に設定する必要があります。  
  
 スケジュールは、そのスケジュールをホストおよび処理するレポート サーバーのローカル時間に基づいて処理されます。  
  
## <a name="navigation"></a>ナビゲーション  
 ユーザー インターフェイス (UI) のこの場所に移動するには、次の手順に従います。  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-execution-properties-page-of-a-report"></a>レポートの [実行] プロパティ ページから [新しいスケジュール] ページまたは [スケジュールの編集] ページを開くには  
  
1.  レポート マネージャーを開き、スケジュールを構成するレポートを探します。  
  
2.  レポートの上にマウス ポインターを移動し、下矢印をクリックします。  
  
3.  ドロップダウン メニューの **[管理]** をクリックします。 この操作により、モデルの [全般] プロパティ ページが開きます。  
  
4.  **[実行]** タブをクリックします。  
  
5.  **[このレポートをレポート実行スナップショットから表示する]** をクリックします。 次に、 **[次のスケジュールを使用して、スナップショットをレポート履歴に追加する]** チェック ボックスをオンにし、 **[レポート固有のスケジュール]** をクリックします。 **[構成]** をクリックします。  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-history-properties-page-of-a-report"></a>レポートの [履歴] プロパティ ページから [新しいスケジュール] ページまたは [スケジュールの編集] ページを開くには  
  
1.  レポート マネージャーを開き、スケジュールを構成するレポートを探します。  
  
2.  レポートの上にマウス ポインターを移動し、下矢印をクリックします。  
  
3.  ドロップダウン メニューの **[管理]** をクリックします。 この操作により、モデルの [全般] プロパティ ページが開きます。  
  
4.  **[履歴]** タブをクリックします。  
  
5.  **[次のスケジュールを使用して、スナップショットをレポート履歴に追加する]** チェック ボックスをオンにし、 **[レポート固有のスケジュール]** をクリックします。 **[構成]** をクリックします。  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-subscriptions-page"></a>[サブスクリプション] ページから [新しいスケジュール] ページまたは [スケジュールの編集] ページを開くには  
  
1.  レポート マネージャーを開き、スケジュールを構成するレポートを探します。  
  
2.  レポートの上にマウス ポインターを移動し、下矢印をクリックします。  
  
3.  ドロップダウン メニューで、次のどちらかの操作を行います。  
  
    -   **[管理]** をクリックします。 この操作により、レポートの [全般] プロパティ ページが開きます。 **[サブスクリプション]** タブをクリックします。  
  
    -   **[サブスクライブ]** をクリックします。 この操作により、レポートの **[サブスクリプション]** プロパティ ページが開きます。  
  
4.  ツール バーで、 **[新しいサブスクリプション]** をクリックするか、編集する既存のサブスクリプションを選択します。  
  
5.  **[サブスクリプション処理のオプション]** で、 **[新しいスケジュール]** をクリックします。  
  
## <a name="options"></a>および  
 **スケジュールの詳細**  
 レポートを実行する日時と頻度を決定するオプションを選択します。 頻度を表すオプションは、階層化されています。 最初のオプション群で、頻度のカテゴリ (時間単位、日単位、週単位など) を指定します。 2 番目のオプション群は、最初の選択に基づいて表示されます。  
  
-   **[時間]** では、1 時間ごとに実行されるスケジュールを定義します。 **[開始日および終了日]** セクションを使用して、スケジュールを実行する日を指定します。  
  
-   **[日]** では、選択した日の指定した時刻に実行されるスケジュールを定義します。 次の方法では、日を指定できます。すべて\<*日*>、すべての平日、毎回\<*数*> 日。 いずれかのオプションを選択すると、それ以外のオプションは表示されていても無効になります。  
  
-   **[週]** では、1 週間ごとの指定した時刻に実行されるスケジュールを定義します。 実行間隔は、2 週間ごとのようにちょうど 1 週間を単位としているものでも、週の複数の曜日を指定するものでもかまいません。  
  
-   **[月]** では、1 か月ごとに実行されるスケジュールを定義します。 1 か月の中で、あるパターンを基にした日 (毎月最終日曜日など) か、特定の日付 (たとえば、1 と 15 を指定して毎月 1 日と 15 日) を選択できます。 コンマおよびハイフンを使用して、複数の日や期間を指定できます (たとえば、1, 5, 7-12, 21)。  
  
-   **[一度だけ]** は、一度だけ実行されるスケジュールを定義します。 **[開始日および終了日]** セクションを使用して、スケジュールを実行する日を指定します。 このスケジュールは、処理が終了すると失効します。  
  
 **開始と終了日**  
 スケジュール タスクが発効する日を確定する開始日、およびスケジュールが失効する日を確定する終了日を指定します。  
  
 スケジュールは予告なく失効します。 終了日を過ぎると、スケジュールは実行されません。 期限切れのスケジュールは削除されません。 スケジュールの削除は、手動によってのみ可能です。 したがって、スケジュールを続行することにした場合、終了日を延長できます。  
  
## <a name="see-also"></a>参照  
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Create, Modify, and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md)   
 [レポート マネージャー F1 ヘルプ](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
