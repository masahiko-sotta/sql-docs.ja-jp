---
title: テキスト形式 (テキスト ファイル ドライバー) の定義 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: 3af46dad-52cc-4d5c-a27e-6315d65a74e6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 500a81146397fa5c50bd8b74c600d04887ecc99c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096353"
---
# <a name="defining-text-format-text-file-driver"></a>テキスト形式の定義 (テキスト ファイル ドライバー)
テキストのドライバーを使用すると、ときに使用できます、**テキスト形式の定義** ダイアログ ボックスで選択したファイルの列の形式を定義します。 このダイアログ ボックスでは、各データ テーブルのスキーマを指定することができます。 この情報は、データ ソース ディレクトリに Schema.ini ファイルに書き込まれます。 テキスト データのソース ディレクトリごとに個別の Schema.ini ファイルが作成されます。  
  
> [!NOTE]  
>  同じ既定のファイル形式は、すべての新しいテキスト データ テーブルに適用されます。 CREATE TABLE ステートメントによって作成されたすべてのファイルは継承これら同じ既定の形式の値でのファイル形式の値を選択して設定される、**テキスト形式の定義** ダイアログ ボックスで\<既定 >、で選択した**テーブル**一覧。 テキストのドライバーでは、このダイアログ ボックスで定義されている形式と一致する既存のテキスト ファイルの形式は変わりませんが、テキスト ファイルからデータを取得しようとする場合の形式を使用する場合にエラーが返されます。  
  
 次のオプションが表示されます、**テキスト形式の定義** ダイアログ ボックス。  
  
|OPTION|[情報]|  
|------------|-----------------|  
|**[追加]**|内の値を使用して、列を追加します**データ型**、**名前**と**幅** ダイアログ ボックスで、かどうか、該当する日付の区切り記号値 Schema.ini から。|  
|**文字**|**ANSI**または**OEM**します。 OEM では、ANSI 以外の文字セットを指定します。 項目の形式が選択されている場合に、OEM にこれが既定で、**テーブル**リストが以前によって定義されていませんこのダイアログ ボックス。|  
|**列名のヘッダー**|選択したテーブルの最初の行の列が列名として使用するかどうかを示します。 いずれか**TRUE**または**FALSE**します。 選択した項目の形式の場合は FALSE を既定値、**テーブル**リストが以前によって定義されていませんこのダイアログ ボックス。|  
|**[列]**|選択したテーブル内の各列の列名を一覧表示します。 列の順序は、テーブルの列の順序を反映します。 ファイルが選択されている場合、このリストが有効になっている、**テーブル**一覧。|  
|**[データ型]**|ビット、バイト、CHAR、通貨、日付、FLOAT、整数、LONGCHAR、短い、または 1 つを指定できます。 日付データ型は、次の形式で指定できます:「dd-mmm-年」、「月-日-年」、「mmm-日-年」、"- yyyy-mm-dd"、または"yyyy mmm--dd"。 "mm"では、数値を表しますか月間です。"mmm"か月間の文字を表します。|  
|**区切り記号**|列の区切りに使用する独自の区切り記号の文字を指定します。 有効になっているときに、**カスタム区切り**形式を選択します。 区切り記号が 1 つだけの文字の長さを指定でき、区切り記号として二重引用符 (") を使用できません。 (区切り記号は、16 進数または 10 進数形式で指定することはできません)。|  
|**形式**|区切られた、または固定の長さ。 区切り形式された場合、は、使用する区切り記号の種類を示します。 コンマ (CSV)、タブ、または特殊文字 (カスタム)。 これは、既定値は**CSV の区切り**で項目の形式が選択されている場合、**テーブル**リストが以前によって定義されていませんこのダイアログ ボックス。<br /><br /> 場合**形式**が固定長および**列名のヘッダー** true、コンマで区切られた最初の行がある必要があります。|  
|**推測**|に従って、テーブルの内容をスキャンして、選択したテーブルの列の列のデータ型、名、および幅値を自動的に生成、**形式**ボックス選択します。 表形式で区切られたときに有効になります。 以前の列が定義されている、**列**一覧がクリアされ、新しいエントリに置き換えられます。 場合**列名のヘッダー**が選択されていない場合、列名は自動的に生成"F1"、"F2"のようにします。 既定値は表示されません、**データ型**ボックス。<br /><br /> この機能は、64,513 バイト未満である列でのみ動作します。|  
|**Modify**|内の値を使用して、選択した列を変更します。**データ型**、**名前**、および**幅**します。|  
|**名前**|選択した列の名前を表示します。 既存の列または新しい列のいずれかの新しい列名を指定するために使用します。<br /><br /> 場合**列名のヘッダー** true の場合、列が表示される名前は無視されます。|  
|**[削除]**|選択した列を削除します。|  
|**スキャンする行**|列と既存のデータに基づく列のデータ型を設定するときにセットアップまたはドライバーをスキャンする行の数。<br /><br /> スキャンする行の数を 1 から 32767 まで、数を入力できます。 既定値は 25 の場合に選択した項目の形式、**テーブル**リストが以前によって定義されていませんこのダイアログ ボックス。 (上限外の数値はエラーを返します。)|  
|**テーブル**|選択されているディレクトリ内のすべてのファイルの一覧を含む、**テキスト セットアップ**指定された拡張機能の一覧に一致する ダイアログ ボックス。<br /><br /> ときに\<既定 > が選択されているテーブルの属性の値は true は、次のいずれかと、**テーブル**グループ、Schema.ini (Schema.ini の他のエントリは変更なし) に書き込まれます。<br /><br /> 指定されたディレクトリには、Schema.ini は-はありません。<br />-Schema.ini ファイルが存在するが、Schema.ini の拡張子を持つ、指定したディレクトリ内のテキスト ファイルのいずれかのセクションではありません。<br />の Schema.ini でテキスト ファイルのセクションが存在しますが、本文は空。<br /><br /> ときに\<既定 > が選択されている、**列**グループが無効になっています。|  
|**Width**|CHAR または LONGCHAR 列の列の幅を変更できます。 選択した項目の形式の 1 の場合に既定値、幅、**テーブル**リストが以前によって定義されていませんこのダイアログ ボックス。<br /><br /> 他のデータ型の幅の制御が無効になっているし、値が表示されていません。|
