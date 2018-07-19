---
title: ブレークポイントの位置の編集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.breakpt.location.file
helpviewer_keywords:
- Transact-SQL debugger, breakpoint location
ms.assetid: 5c28e411-0377-4210-a7ce-2a5c13dcdf74
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93b4127793631aa9ea393bfa420ac82390023910
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37186129"
---
# <a name="edit-a-breakpoint-location"></a>ブレークポイントの位置の編集
  ブレークポイントの位置では、ブレークポイントを設定する [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイル内の行や文字を指定します。 ブレークポイントの位置を編集して、ブレークポイントを別の位置や別のスクリプトに移動できます。  
  
## <a name="editing-a-location"></a>位置の編集  
 ブレークポイントの位置を編集すると、ブレークポイントはヒット カウント、条件などの既存のすべてのプロパティと共に新しい位置に移動します。  
  
#### <a name="to-edit-a-breakpoint-location"></a>ブレークポイントの位置を編集するには  
  
1.  エディター ウィンドウで、ブレークポイント グリフを右クリックし、ショートカット メニューの **[場所]** をクリックします。  
  
     - または -  
  
     **[ブレークポイント]** ウィンドウで、ブレークポイント グリフを右クリックし、ショートカット メニューの **[場所]** をクリックします。  
  
2.  **[ファイルのブレークポイント]** ダイアログ ボックスで、新しいファイルを指定するには **[ファイル]** 、新しい行を指定するには **[行]** 、行内の新しい場所を指定するには **[文字]** の各項目を編集します。 指定した新しいファイルがクエリ エディター ウィンドウで既に開いている場合は、ブレークポイントがそのエディター ウィンドウに移動します。 ファイルが開いていない場合は、新しいクエリ エディター ウィンドウが開き、そのファイルが読み込まれ、ブレークポイントが新しい位置に移動します。  
  
     **をデバッグする場合、** [元のバージョンと異なるソース コードを許可する] [!INCLUDE[tsql](../../includes/tsql-md.md)]オプションは無効です。  
  
## <a name="see-also"></a>参照  
 [ヒット カウントの指定](specify-a-hit-count.md)   
 [ブレークポイント アクションの指定](specify-a-breakpoint-action.md)   
 [ブレークポイント条件の指定](specify-a-breakpoint-condition.md)   
 [ブレークポイント フィルターの指定](specify-a-breakpoint-filter.md)  
  
  