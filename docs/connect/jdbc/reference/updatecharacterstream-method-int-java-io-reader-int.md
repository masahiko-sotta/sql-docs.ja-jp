---
title: updateCharacterStream (java.io.Reader, int) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateCharacterStream (int, java.io.Reader, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b692c372-f6d7-4528-9c5d-cd8421bdb12e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da62f9647b6d9aeff40e43c80a59213d5e8cd239
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996863"
---
# <a name="updatecharacterstream-method-int-javaioreader-int"></a>updateCharacterStream (int, java.io.Reader, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列を文字ストリームの値で更新します。文字ストリームの値は、指定された文字数を持ちます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader readerValue,  
                                  int length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
 *readerValue*  
  
 リーダーオブジェクト。  
  
 *length*  
  
 ストリームの長さを示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この updateCharacterStream メソッドは、java.sql.ResultSet インターフェイスの updateCharacterStream メソッドで規定されています。  
  
 このメソッドは、Unicode 文字を Reader オブジェクトから選択したテキストおよびバイナリ列に渡します。 これには、すべてのテキスト列と **binary**、**varbinary**、**varbinary(max)** 、**image**、**xml** の各列が含まれますが、**udt** 列は含まれません。  
  
 ストリームの長さが、*length* パラメーターで指定された長さと異なる場合は、行の更新または挿入時に JDBC ドライバーが例外をスローします。  
  
 ストリームの長さが不明である場合、*length* パラメーターを -1 に設定して、ドライバーが長さに関係なくストリームを受け入れるように指定できます。 sqljdbc4.jar を使用する場合、アプリケーションで長さが不明なストリームを使用して列を更新するときには、JDBC 4.0 メソッドの [updateCharacterStream メソッド &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-int-java-io-reader.md) を使用することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [updateCharacterStream メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
