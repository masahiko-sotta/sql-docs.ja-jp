---
title: ローカル パッケージの出力の読み込み | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow [Integration Services], loading results
- loading data flow results
ms.assetid: aba8ecb7-0dcf-40d0-a2a8-64da0da94b93
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c7b0056def4b62d7305fe5ac78db93ba15fb22a8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254634"
---
# <a name="loading-the-output-of-a-local-package"></a>ローカル パッケージの出力の読み込み
  クライアント アプリケーションは、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先に出力が保存された場合、または **System.IO** 名前空間のクラスを使用してフラット ファイル変換先に出力が保存された場合に、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの出力を読み取ることができます。 ただし、メモリから直接、パッケージの出力を読み取ることもできます。その際、データを保持するための中間手段を必要としません。 このソリューションにキーが、`Microsoft.SqlServer.Dts.DtsClient`の特殊な実装を含む名前空間、 `IDbConnection`、 `IDbCommand`、および**IDbDataParameter**からインターフェイス、 **System.Data**名前空間。 既定では、アセンブリ Microsoft.SqlServer.Dts.DtsClient.dll は、**%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn** にインストールされています。  
  
> [!NOTE]  
>  このトピックで説明されている手順では、データ フロー タスクおよび親オブジェクトの DelayValidation プロパティが既定値の **False** に設定されている必要があります。  
  
## <a name="description"></a>説明  
 この手順では、マネージド コードを使用して、DataReader 変換先でパッケージの出力をメモリから直接読み込むクライアント アプリケーションを開発する方法を示します。 ここにまとめた手順は、後のコード例で示します。  
  
#### <a name="to-load-data-package-output-into-a-client-application"></a>クライアント アプリケーションにパッケージ出力を読み込むには  
  
1.  パッケージで、クライアント アプリケーションに読み込む出力を受信するように DataReader 変換先を構成します。 DataReader 変換先にはわかりやすい名前を付けます。この名前は後からクライアント アプリケーションで使用します。 DataReader 変換先の名前はメモしておきます。  
  
2.  開発プロジェクトで参照を設定、`Microsoft.SqlServer.Dts.DtsClient`名前空間、アセンブリを配置することにより**Microsoft.SqlServer.Dts.DtsClient.dll**します。 既定では、このアセンブリは **C:\Program Files\Microsoft SQL Server\100\DTS\Binn** にインストールされます。 C# の `Using` ステートメント、または [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] の `Imports` ステートメントを使用し、作成するコードにこの名前空間をインポートします。  
  
3.  型のオブジェクトを作成、コードに`DtsClient.DtsConnection`に必要なコマンド ライン パラメーターを含む接続文字列で**dtexec.exe**パッケージを実行します。 詳しくは、「 [dtexec Utility](../packages/dtexec-utility.md)」をご覧ください。 次に、この接続文字列を使用して接続を開きます。 **dtexecui** ユーティリティを使用して、必要な接続文字列を視覚的に作成することもできます。  
  
    > [!NOTE]  
    >  このサンプル コードは、`/FILE <path and filename>` 構文を使用してファイル システムからパッケージを読み込む方法を示していますが、 `/SQL <package name>` 構文を使用して MSDB データベースからパッケージを読み込んだり、`/DTS \<folder name>\<package name>` 構文を使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ ストアからパッケージを読み込むこともできます。  
  
4.  前に作成した `DtsClient.DtsCommand` を使用する `DtsConnection` という種類のオブジェクトを作成し、その `CommandText` プロパティに、パッケージ内の DataReader 変換先の名前を設定します。 次に、コマンド オブジェクトの `ExecuteReader` メソッドを呼び出して、パッケージの結果を新しい DataReader に読み込みます。  
  
5.  必要に応じて、`DtsDataParameter` オブジェクトで `DtsCommand` オブジェクトのコレクションを使用して、パッケージに定義された変数に値を渡すことによって、パッケージの出力を間接的にパラメーター化できます。 パッケージ内では、これらの変数をクエリ パラメーターとして、または式で使用して、DataReader 変換先に返される結果に影響を与えることができます。 パッケージにこれらの変数を定義する必要があります、 **DtsClient**名前空間を使用する前に、`DtsDataParameter`クライアント アプリケーションからのオブジェクト。 (**[名前空間]** 列を表示するには、**[変数]** ウィンドウの **[変数列の選択]** ツール バー ボタンをクリックする必要がある場合があります)。クライアント コードで、`DtsDataParameter` を `Parameters` の `DtsCommand` コレクションに追加する場合、変数名からの DtsClient 名前空間参照を省略してください。 以下に例を示します。  
  
    ```  
    command.Parameters.Add(new DtsDataParameter("MyVariable", 1));  
    ```  
  
6.  出力データの行をループするのに必要なだけ、DataReader の `Read` メソッドを繰り返し呼び出します。 クライアント アプリケーションで、データを使用するか、または後で使用するために保存します。  
  
    > [!IMPORTANT]  
    >  DataReader のこの実装の `Read` メソッドは、データの最後の行が読み取られた後にもう一度 `true` を返します。 このため、`Read` が `true` を返している間、DataReader をループする通常のコードを使用することが難しくなります。 予定した行数を読み取った後に `Read` メソッドの追加の最終呼び出しがないと、コードで DataReader または接続を閉じようとした場合に、ハンドルされていない例外が発生します。 しかし、コードがこのループの最後の反復でデータを読み取ろうとした場合、`Read` がまだ `true` を返しているのに最後の行に到達すると、ハンドルされていない `ApplicationException` が発生し、"SSIS IDataReader は結果セットの末尾に到達しました。" というメッセージが表示されます。 この動作は、その他の DataReader 実装の動作とは異なります。 したがって、`Read` が `true` を返している間にループを使用して DataReader 内の行を最後まで読み取るようにするには、最後の `ApplicationException` メソッドの正常な呼び出しで予想されるこの `Read` をキャッチ、テスト、および破棄するコードを記述する必要があります。 あるいは、予定の行数があらかじめわかっている場合は、行を処理してから、DataReader および接続を閉じる前にもう一度 `Read` メソッドを呼び出します。  
  
7.  `Dispose` オブジェクトの `DtsCommand` メソッドを呼び出します。 `DtsDataParameter` オブジェクトを使用している場合、これは特に重要です。  
  
8.  DataReader と接続オブジェクトを閉じます。  
  
## <a name="example"></a>例  
 次の例では、1 つの集計値を計算してその値を DataReader 変換先に保存するパッケージを実行します。次に、この値を DataReader から読み取って、Windows フォーム上のテキスト ボックスに表示します。  
  
 パッケージの出力をクライアント アプリケーションに読み込む場合は、パラメーターを使用する必要はありません。 パラメーターを使用しない場合は、内の変数の使用を省略できます、 **DtsClient**名前空間を使用するコードを省略して、`DtsDataParameter`オブジェクト。  
  
#### <a name="to-create-the-test-package"></a>テスト パッケージを作成するには  
  
1.  新しい [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを作成します。 サンプル コードでは、パッケージの名前として "DtsClientWParamPkg.dtsx" が使用されています。  
  
2.  DtsClient 名前空間に文字列型の変数を追加します。 サンプル コードでは、変数の名前として Country が使用されています  (**[名前空間]** 列を表示するには、**[変数]** ウィンドウの **[変数列の選択]** ツール バー ボタンをクリックする必要がある場合があります)。  
  
3.  [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベースに接続する OLE DB 接続マネージャーを追加します。  
  
4.  データ フロー タスクをパッケージに追加し、[データ フロー] デザイン画面に切り替えます。  
  
5.  OLE DB ソースをデータ フローに追加し、前に作成した OLE DB 接続マネージャーを使用するように構成して、次の SQL コマンドを実行します。  
  
    ```  
    SELECT * FROM Sales.vIndividualCustomer WHERE CountryRegionName = ?  
    ```  
  
6.  クリックして`Parameters`し、**クエリ パラメーターの設定** ダイアログ ボックスで、1 つの入力パラメーター Parameter0 をクエリ内を dtsclient::country 変数にマップします。  
  
7.  データ フローに集計変換を追加し、OLE DB ソースの出力を変換に接続します。 集計変換エディターを開いて、すべての入力列 (*) で "すべてのカウント" 操作が実行され、集計された値が CustomerCount の別名で出力されるように構成します。  
  
8.  データ フローに DataReader 変換先を追加し、集計変換の出力を DataReader 変換先に接続します。 サンプル コードでは、DataReader の名前として "DataReaderDest" が使用されています。 変換先に対して使用可能な単一の入力列 CustomerCount を選択します。  
  
9. パッケージを保存します。 次に作成されたテスト アプリケーションではパッケージが実行され、その出力がメモリから直接取得されます。  
  
#### <a name="to-create-the-test-application"></a>テスト アプリケーションを作成するには  
  
1.  新しい Windows フォーム アプリケーションを作成します。  
  
2.  参照を追加、`Microsoft.SqlServer.Dts.DtsClient`名前空間内の同じ名前のアセンブリを参照して **%ProgramFiles%\Microsoft SQL server \100\dts\binn**します。  
  
3.  次のサンプル コードをコピーし、フォームのコード モジュールに貼り付けます。  
  
4.  値を変更、`dtexecArgs`必要に応じて変数格納するために必要なコマンド ライン パラメーター **dtexec.exe**パッケージを実行します。 サンプル コードは、ファイル システムからパッケージを読み込みます。  
  
5.  値を変更、`dataReaderName`必要に応じて変数格納するため、パッケージ内の DataReader 変換先の名前。  
  
6.  ボタンとテキスト ボックスをフォームに追加します。 サンプル コードを使用して`btnRun`、ボタンの名前として、`txtResults`としてテキスト ボックスの名前。  
  
7.  アプリケーションを実行し、ボタンをクリックします。 パッケージの実行中に一時停止したら、パッケージによって計算された集計値 (Canada の顧客数) が、フォーム上のテキスト ボックスに表示されます。  
  
### <a name="sample-code"></a>サンプル コード  
  
```vb  
Imports System.Data  
Imports Microsoft.SqlServer.Dts.DtsClient  
  
Public Class Form1  
  
  Private Sub btnRun_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnRun.Click  
  
    Dim dtexecArgs As String  
    Dim dataReaderName As String  
    Dim countryName As String  
  
    Dim dtsConnection As DtsConnection  
    Dim dtsCommand As DtsCommand  
    Dim dtsDataReader As IDataReader  
    Dim dtsParameter As DtsDataParameter  
  
    Windows.Forms.Cursor.Current = Cursors.WaitCursor  
  
    dtexecArgs = "/FILE ""C:\...\DtsClientWParamPkg.dtsx"""  
    dataReaderName = "DataReaderDest"  
    countryName = "Canada"  
  
    dtsConnection = New DtsConnection()  
    With dtsConnection  
      .ConnectionString = dtexecArgs  
      .Open()  
    End With  
  
    dtsCommand = New DtsCommand(dtsConnection)  
    dtsCommand.CommandText = dataReaderName  
  
    dtsParameter = New DtsDataParameter("Country", DbType.String)  
    dtsParameter.Direction = ParameterDirection.Input  
    dtsCommand.Parameters.Add(dtsParameter)  
  
    dtsParameter.Value = countryName  
  
    dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default)  
  
    With dtsDataReader  
      .Read()  
      txtResults.Text = .GetInt32(0).ToString("N0")  
    End With  
  
    'After reaching the end of data rows,  
    ' call the Read method one more time.  
    Try  
      dtsDataReader.Read()  
    Catch ex As Exception  
      MessageBox.Show("Exception on final call to Read method:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception on final call to Read method", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    ' The following method is a best practice, and is  
    '  required when using DtsDataParameter objects.  
    dtsCommand.Dispose()  
  
    Try  
      dtsDataReader.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing DataReader:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing DataReader", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Try  
      dtsConnection.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing connection:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing connection", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Windows.Forms.Cursor.Current = Cursors.Default  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Data;  
using Microsoft.SqlServer.Dts.DtsClient;  
  
namespace DtsClientWParamCS  
{  
  public partial class Form1 : Form  
  {  
    public Form1()  
    {  
      InitializeComponent();  
      this.btnRun.Click += new System.EventHandler(this.btnRun_Click);  
    }  
  
    private void btnRun_Click(object sender, EventArgs e)  
    {  
      string dtexecArgs;  
      string dataReaderName;  
      string countryName;  
  
      DtsConnection dtsConnection;  
      DtsCommand dtsCommand;  
      IDataReader dtsDataReader;  
      DtsDataParameter dtsParameter;  
  
      Cursor.Current = Cursors.WaitCursor;  
  
      dtexecArgs = @"/FILE ""C:\...\DtsClientWParamPkg.dtsx""";  
      dataReaderName = "DataReaderDest";  
      countryName = "Canada";  
  
      dtsConnection = new DtsConnection();  
      {  
        dtsConnection.ConnectionString = dtexecArgs;  
        dtsConnection.Open();  
      }  
  
      dtsCommand = new DtsCommand(dtsConnection);  
      dtsCommand.CommandText = dataReaderName;  
  
      dtsParameter = new DtsDataParameter("Country", DbType.String);  
      dtsParameter.Direction = ParameterDirection.Input;  
      dtsCommand.Parameters.Add(dtsParameter);  
  
      dtsParameter.Value = countryName;  
  
      dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default);  
  
      {  
        dtsDataReader.Read();  
        txtResults.Text = dtsDataReader.GetInt32(0).ToString("N0");  
      }  
  
      //After reaching the end of data rows,  
      // call the Read method one more time.  
      try  
      {  
        dtsDataReader.Read();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception on final call to Read method:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception on final call to Read method", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      // The following method is a best practice, and is  
      //  required when using DtsDataParameter objects.  
      dtsCommand.Dispose();  
  
      try  
      {  
        dtsDataReader.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing DataReader:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing DataReader", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      try  
      {  
        dtsConnection.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing connection:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing connection", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      Cursor.Current = Cursors.Default;  
  
    }  
  }  
}  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。** <br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [ローカル実行とリモート実行の相違点について](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [プログラムによるローカル パッケージの読み込みと実行](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [プログラムによるリモート パッケージの読み込みと実行](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
  