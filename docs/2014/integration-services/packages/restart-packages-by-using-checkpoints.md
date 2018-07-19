---
title: チェックポイントを使用してパッケージを再開する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 48f2fbb7-8964-484a-8311-5126cf594bfb
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 02aa88c80200ece060204fc339e84560a069cc17
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260988"
---
# <a name="restart-packages-by-using-checkpoints"></a>チェックポイントを使用してパッケージを再開する
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、失敗したパッケージ全体を再実行する代わりに、失敗した時点から再開することができます。 パッケージがチェックポイントを使用するように設定されている場合、パッケージの実行に関する情報がチェックポイント ファイルに書き込まれます。 失敗したパッケージを再実行する場合、チェックポイント ファイルを使用して、失敗した時点からパッケージを再開します。 パッケージの実行が成功するとチェックポイント ファイルは削除され、次にパッケージが実行されるときに再度作成されます。  
  
 パッケージでチェックポイントを使用すると、次の利点があります。  
  
-   大きなファイルのダウンロードおよびアップロードの繰り返しを防止します。 たとえば、FTP タスクを使用して複数の大きなファイルをダウンロードするパッケージで 1 つのファイルのダウンロードが失敗した場合、パッケージを再開して、そのファイルのみをダウンロードすることができます。  
  
-   大量データ読み込みの繰り返しを防止します。 たとえば、ディメンションごとに別々の一括挿入タスクを使用してデータ ウェアハウスのディメンション テーブルに一括挿入を行うパッケージで 1 つのディメンション テーブルに対する挿入が失敗した場合、パッケージを再開して、そのディメンションのみを再読み込みすることができます。  
  
-   値の集計の繰り返しを防止します。 たとえば、平均や合計など多くの集計値の計算を集計ごとに別々のデータ フロー タスクを使用して実行するパッケージで 1 つの集計値の計算が失敗した場合、パッケージを再開して、その集計のみを再実行することができます。  
  
 パッケージがチェックポイントを使用するように設定されている場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] はチェックポイント ファイルから再開ポイントを取得します。 失敗したコンテナーの種類や、トランザクションなどの実装機能によって、チェックポイント ファイルに記録される再開ポイントは影響を受けます。 変数の現在の値も、チェックポイント ファイルにキャプチャされます。 ただし、変数の値がある、`Object`データ型はチェックポイント ファイルに保存されません。  
  
## <a name="defining-restart-points"></a>再開ポイントの定義  
 単一のタスクがカプセル化されているタスク ホスト コンテナーが、再開可能な最小のアトミック作業単位です。 Foreach ループ コンテナーおよびトランザクション化されたコンテナーも、アトミックな作業単位です。  
  
 トランザクション化されたコンテナーの実行中にパッケージが停止した場合、トランザクションが終了し、コンテナーによって実行された作業がすべてロールバックされます。 パッケージが再開されると、失敗したコンテナーが再実行されます。 トランザクション化されたコンテナーのいずれかの子コンテナーが完了しても、チェックポイント ファイルには記録されません。 このため、パッケージが再開されると、トランザクション化されたコンテナーと子コンテナーが再実行されます。  
  
> [!NOTE]  
>  同じパッケージでチェックポイントとトランザクションを使用すると、予期しない結果が生じる可能性があります。 たとえば、パッケージが失敗してチェックポイントから再開した場合、既に正常にコミットされているトランザクションがパッケージで繰り返し実行される可能性があります。  
  
 チェックポイント データは、For ループ コンテナーおよび Foreach ループ コンテナーには保存されません。 パッケージが再開されると、For ループ コンテナーおよび Foreach ループ コンテナーと、子コンテナーが再実行されます。 ループ内の子コンテナーの実行が成功してもチェックポイント ファイルには記録されないため、子コンテナーは再実行されます。 詳細情報および回避策については、「 [SSIS チェックポイントが For ループ コンテナーまたは Foreach ループ コンテナーの項目に格納されない](http://go.microsoft.com/fwlink/?LinkId=241633)」を参照してください。  
  
 パッケージの再開時にはパッケージの構成が再読み込みされず、チェックポイント ファイルに書き込まれた構成情報が代わりに使用されます。 これによって、確実に、パッケージが失敗した時点と同じ構成を使用してパッケージが再実行されます。  
  
 パッケージは、制御フロー レベルでのみ再開できます。 データ フローの途中からパッケージを再開することはできません。 データ フロー全体の再実行を防止するには、パッケージを複数のデータ フローで設計して、各データ フローで別々のデータ フロー タスクを使用するようにします。 これによりパッケージを再開すると、1 つのデータ フロー タスクだけを再実行できます。  
  
## <a name="configuring-a-package-to-restart"></a>パッケージを再開する設定  
 チェックポイント ファイルには、完了したすべてのコンテナーの実行結果、システム変数およびユーザー定義変数の現在の値、およびパッケージの構成情報が記録されています。 また、パッケージ固有の識別子も記録されています。 パッケージを正常に再開するには、チェックポイント ファイルに記録されたパッケージの識別子とパッケージが一致しなければなりません。一致しない場合、再開は失敗します。 これにより、パッケージの別のバージョンで作成されたチェックポイント ファイルの使用を防止します。 パッケージの再開後に実行が成功すると、チェックポイント ファイルは削除されます。  
  
 次の表に、チェックポイントの実装時に設定するパッケージのプロパティの一覧を示します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|CheckpointFileName|チェックポイント ファイルの名前を指定します。|  
|CheckpointUsage|チェックポイントを使用するかどうかを指定します。|  
|SaveCheckpoints|パッケージでチェックポイントを保存するかどうかを示します。 失敗した時点からパッケージを再開するには、このプロパティを True に設定する必要があります。|  
  
 さらに、FailPackageOnFailure プロパティ設定する必要があります`true`を識別するパッケージ内のすべてのコンテナーの再開ポイントとして。  
  
 ForceExecutionResult プロパティを使用して、パッケージのチェックポイントの使用をテストできます。 タスクまたはコンテナーの ForceExecutionResult を Failure に設定すると、実行時の障害を擬似的に実現できます。 パッケージを再実行すると、失敗したタスクとコンテナーが再実行されます。  
  
### <a name="checkpoint-usage"></a>チェックポイントの使用法  
 CheckpointUsage プロパティは次の値に設定できます。  
  
|値|説明|  
|-----------|-----------------|  
|`Never`|チェックポイント ファイルを使用せず、パッケージのワークフローの最初からパッケージを実行することを指定します。|  
|`Always`|チェックポイント ファイルを常に使用し、前の実行で失敗した時点からパッケージを再開することを指定します。 チェックポイント ファイルが見つからない場合、パッケージは失敗します。|  
|`IfExists`|チェックポイント ファイルが存在する場合、チェックポイント ファイルを使用することを指定します。 チェックポイント ファイルが存在する場合、パッケージは前の実行で失敗した時点から再開されます。存在しない場合、パッケージのワークフローの最初から実行されます。|  
  
> [!NOTE]  
>  **で/CheckPointing** dtexec のオプションは設定に相当、`SaveCheckpoints`するパッケージのプロパティ`True`、および`CheckpointUsage`プロパティを always にします。 詳しくは、「 [dtexec Utility](dtexec-utility.md)」をご覧ください。  
  
## <a name="securing-checkpoint-files"></a>チェックポイント ファイルのセキュリティ保護  
 パッケージ レベルの保護にはチェックポイント ファイルの保護が含まれないため、チェックポイント ファイルは個別にセキュリティ保護する必要があります。 チェックポイントのデータはファイル システムにしか格納できないので、オペレーティング システムのアクセス制御リスト (ACL) を使用して、ファイルの格納先またはフォルダーのセキュリティを保護する必要があります。 チェックポイント ファイルには、現在の変数値などパッケージの状態に関する情報が含まれているため、セキュリティで保護することが重要です。 たとえば変数には、電話番号などの個人データを含む多数の行で構成されるレコードセットが格納されている場合があります。 詳細については、「 [パッケージで使用されるファイルへのアクセス](../access-to-files-used-by-packages.md)」を参照してください。  
  
### <a name="to-configure-the-checkpoint-properties"></a>チェックポイント プロパティを設定するには  
  
-   [失敗したパッケージを再開するためのチェックポイントを構成する](../configure-checkpoints-for-restarting-a-failed-package.md)  
  
## <a name="external-resources"></a>外部リソース  
  
-   social.technet.microsoft.com の技術資料「 [フェールオーバーまたはエラー後の SSIS パッケージの自動再起動](http://go.microsoft.com/fwlink/?LinkId=200407)」  
  
-   support.microsoft.com のサポート技術情報の記事「 [SSIS チェックポイントが For ループ コンテナーまたは Foreach ループ コンテナーの項目に格納されない](http://go.microsoft.com/fwlink/?LinkId=241633)」  
  
## <a name="see-also"></a>参照  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  