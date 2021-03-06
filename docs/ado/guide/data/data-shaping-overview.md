---
title: データ シェイプの概要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3bce50892520dbc889a62960065ce3d8e423a81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925620"
---
# <a name="data-shaping-overview"></a>データ シェイプの概要
*データ シェイプ*クエリ内の 2 つ以上の論理エンティティ間の階層リレーションシップを構築することを意味します。 1 つのレコード間の親子関係に階層を表示できます[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)、および別の 1 つまたは複数のレコード (章とも呼ばれます)**レコード セット**します。 親子リレーションシップで親**レコード セット**子を含む**レコード セット**します。 このような階層関係の例は、顧客と注文です。 データベース内のすべての顧客の 0 個以上の注文があります。 階層関係を再帰的孫のレコードが子レコード内に入れ子にするとできます。 原則として、階層のレコードを任意の深さに入れ子にできます。 実際には、ADO は最大 512 個、再帰を制限**Recordset**秒。  
  
 [全般]、列、形状の**レコード セット**Microsoft® SQL Server の間の参照など、データ プロバイダーからデータを含めることができます**レコード セット**、の単一行での計算から派生した値**レコード セット**、全体の列に対する操作から派生した値または**Recordset**します。 作成されると空の列が新しくこともできます。  
  
 別の参照を含んでいる列の値を取得する場合**レコード セット**、ADO に自動的に返す実際**レコード セット**参照によって表されます。 参照を**レコード セット**と呼ばれる、子のサブセットへの参照を実際には、*章*します。 1 つの親は 1 つ以上の子を参照できる**Recordset**します。  
  
 データ シェイプの ADO サポート、データ ソースのクエリを返すことができます、 **Recordset** (親) のレコードが (子) を表します**Recordset**します。 顧客と注文のシナリオでデータを 1 つのクエリでは、各顧客の注文と顧客の情報を取得するシェイプを使用できます。 結果として得られる**Recordset**の整形とも呼ばれます**レコード セット**します。  
  
 さらに、データ シェイプの ado を使用すると、新規作成**Recordset**オブジェクトを使用して基になるデータ ソースを使用せず、**新規**親と子のフィールドを説明するキーワード**レコード セット**します。 新しい**Recordset**オブジェクトするデータを設定し、永続的に保存します。 開発者には、さまざまな計算や集計もを実行できます (たとえば、**合計**、 **AVG**と**最大**) 子フィールドにします。 データ シェイプ作成することも、親**レコード セット**子から**レコード セット**子のレコードをグループ化して、親、子グループごとに 1 つの行を配置することです。  
  
 通常の SQL を使用してデータを取得できます。**参加**構文が、このことは非効率的扱いにくくなるため、冗長な親データが指定された親/子リレーションシップに対して返されるレコードごとに繰り返されます。 親の 1 つの親レコードを関連付けることができるデータの整形**レコード セット**子内の複数の子レコードを**レコード セット**の冗長性を回避、**参加**。 ほとんどの人が親と子を見つける複数**Recordset**より自然で 1 つより操作しやすいプログラミング モデル**レコード セットに参加**モデル。
