---
title: レポートへの HTML の追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e309710e72ec344a9e54255483893800b6a4018f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37288248"
---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>レポートへの HTML の追加 (レポート ビルダーおよび SSRS)
  レポートでプレースホルダーを使用すると、データセットのフィールドから HTML をインポートできます。 既定のプレースホルダーはプレーン テキストを表すため、プレースホルダーのマークアップ タイプを HTML に変更する必要があります。 詳細については、[「レポートへの HTML のインポート &#40;レポート ビルダーおよび SSRS&#41;](importing-html-into-a-report-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>データセットのフィールドからテキスト ボックスに HTML を追加するには  
  
1.  **[挿入]** タブの **[一覧]** をクリックします。 デザイン画面をクリックし、次にマウスをドラッグして、必要なサイズのボックスを作成します。  
  
     **[データセットのプロパティ]** ダイアログ ボックスが表示されます。 共有データセットまたはレポートに埋め込まれたデータセットを使用できます。 詳細については、「[[クエリ] ([データセットのプロパティ] ダイアログ ボックス) &#40;レポート ビルダー&#41;](../report-data/dataset-properties-dialog-box-query-report-builder.md)」または「[[クエリ] ([データセットのプロパティ] ダイアログ ボックス)](../dataset-properties-dialog-box-query.md)」を参照してください。  
  
2.  **[挿入]** タブの **[テキスト ボックス]** をクリックします。 一覧内をクリックし、次にマウスをドラッグして、必要なサイズのボックスを作成します。  
  
3.  データセットからテキスト ボックスに HTML フィールドをドラッグします。 フィールドに対してプレースホルダーが作成されます。  
  
4.  プレースホルダーを右クリックし、 **[プレースホルダーのプロパティ]** をクリックします。  
  
5.  **[全般]** タブの **[値]** ボックスに、手順 3 でドロップしたフィールドを評価する式が入力されていることを確認します。  
  
6.  **[HTML - HTML タグをスタイルとして解釈]** をクリックします。 これで、フィールドが HTML として評価されます。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [数値と日付の書式設定&#40;レポート ビルダーおよび SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [線、色、および画像の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](images-report-builder-and-ssrs.md)   
 [[全般] ([プレースホルダーのプロパティ] ダイアログ ボックス) &#40;レポート ビルダーおよび SSRS&#41;](../placeholder-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  