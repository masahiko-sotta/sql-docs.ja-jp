---
title: SQLFetchScroll |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fa4b974c834581158c6bf60e4abecfb51b9e8c7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410041"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
  **SQLFetchScroll**アプリケーションへのデータの 1 つの行セットを返します。 使用して、行セットのサイズを設定[SQLSetStmtAttr](sqlsetstmtattr.md)します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、次の制限事項にすべての定義済みフェッチ命令 (SQL_FETCH_RELATIVE など) をサポートしています。  
  
-   ステートメントに順方向専用カーソルを定義する場合は、SQL_FETCH_NEXT が必要です。他の形式でフェッチを試行すると、エラーが返されます。  
  
-   SQL_FETCH_BOOKMARK がサポートされるのは、静的カーソルとキーセット ドリブン カーソルに対してのみです。  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>SQLFetchScroll による機能強化された日付と時刻のサポート  
 説明されているように、日付/時刻型の結果列の値が変換されます[SQL から C への変換](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)します。  
  
 詳細については、次を参照してください。[日付と時刻の強化&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)します。  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>SQLFetchScroll による大きな CLR UDT のサポート  
 **SQLFetchScroll**大きなの CLR ユーザー定義型 (Udt) をサポートしています。 詳細については、次を参照してください。 [Large CLR User-Defined 型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)します。  
  
## <a name="see-also"></a>参照  
 [SQLFetchScroll 関数](http://go.microsoft.com/fwlink/?LinkId=59343)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)  
  
  