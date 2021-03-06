---
title: 対数スケールの指定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f3092c1c-b128-433d-9a95-983508b2a8d4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0910888603528d899f0180bf96c66cfbea045aa4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104936"
---
# <a name="specify-a-logarithmic-scale-report-builder-and-ssrs"></a>対数スケールの指定 (レポート ビルダーおよび SSRS)
  対数比例するデータがある場合は、グラフ上での対数スケールの使用を検討します。 これにより、データの管理が容易になり、グラフの外観が向上します。 ほとんどの対数スケールでは、底に 10 を使用します。  
  
 この機能は値軸でのみ使用できます。 通常、値軸は縦軸 (Y 軸) です。 ただし、横棒グラフの値軸は横軸 (X 軸) です。  
  
 軸が対数の場合、その軸に関連するその他すべてのプロパティは、対数スケールで示されます。 たとえば、10 を底とする対数スケールを軸で指定した場合、軸の間隔を 2 に設定すると、10 の 2 乗 (つまり 100) の増分率で間隔が生成されます。 つまり、軸の値は既定の 1、10、100、1000、10000 ではなく、1、100、10000 という値を取ります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-a-logarithmic-scale"></a>対数スケールを指定するには  
  
1.  グラフの Y 軸を右クリックし、 **[縦軸のプロパティ]** をクリックします。 **[縦軸のプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[軸のオプション]** で、 **[対数スケールを使用する]** を選択します。  
  
3.  **[対数の底]** ボックスに、対数の底を正の値で入力します。 値を指定しなかった場合、対数の底は既定値の 10 に設定されます。  
  
## <a name="see-also"></a>関連項目  
 [グラフの軸ラベルの書式設定 (レポート ビルダーおよび SSRS)](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [グラフの書式設定 (レポート ビルダーおよび SSRS)](formatting-a-chart-report-builder-and-ssrs.md)   
 [日付または通貨として軸ラベルを書式設定する &#40;レポート ビルダーおよび SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
