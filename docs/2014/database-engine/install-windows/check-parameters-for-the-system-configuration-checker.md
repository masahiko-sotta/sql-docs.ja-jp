---
title: システム構成チェッカーの検査パラメーター | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, system configuration checks
- failed system configuration checks [SQL Server]
- verifying configuration before installation
- SCC [SQL Server]
- system configuration checker
- scanning computer before installation [SQL Server]
- checking configuration before installation
- status information [SQL Server], system configuration checker
- parameters [SQL Server], system configuration checker
- configuration checkers [SQL Server]
- Setup [SQL Server], system configuration checker
ms.assetid: 8e712c15-6bfa-4d71-b303-9526101e5594
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f3846ae220bc1e0e412185daca57f576a7a2e030
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197802"
---
# <a name="check-parameters-for-the-system-configuration-checker"></a>システム構成チェッカーの検査パラメーター
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップの実行中、システム構成チェッカー (SCC) は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール先コンピューターをスキャンします。 SCC は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールの成功を妨げる条件がないかどうかを調べます。 セットアップで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードが起動する前に、SCC は各項目の状態を取得します。 次に、必要な条件と取得した結果を比較し、ブロックの問題解決に関するガイダンスを提供します。  
  
 システム構成チェッカーは、実行された各ルールの簡単な記述と、実行ステータスを含むレポートを生成します。 システム構成チェッカーのレポートは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\します。  
  
## <a name="see-also"></a>参照  
 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [サポートされているバージョンとエディションのアップグレード](supported-version-and-edition-upgrades.md)  
  
  