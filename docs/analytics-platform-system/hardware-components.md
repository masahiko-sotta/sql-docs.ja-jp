---
title: ハードウェア コンポーネント
description: Analytics Platform System (APS) は、ビジネス要件に応じて適切な量の処理とストレージを購入できるように、スケーラブルなコンポーネントを使用します。 APS を注文する場合は、これらのコアハードウェアコンポーネントの組み合わせが必要になります。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: db9966315d60fd4de1de7ae6805620d3f2144e6f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401147"
---
# <a name="hardware-components-for-analytics-platform-system"></a>分析プラットフォームシステムのハードウェアコンポーネント

Analytics Platform System (APS) は、ビジネス要件に応じて適切な量の処理とストレージを購入できるように、スケーラブルなコンポーネントを使用します。 APS を注文する場合は、これらのコアハードウェアコンポーネントの組み合わせが必要になります。 ハードウェアベンダーによっては、名前付け規則が異なる場合や、追加のコンポーネントを使用する場合があります。  
 
  
## <a name="rackandnetwork"></a>ラックとネットワーク 
 
APS コンポーネントはすべて、データセンターに収められている1つ以上のラックに格納されます。 各ラックには、配電ユニット (Pdu)、2つの InfiniBand スイッチ、2つのイーサネットスイッチが付属しています。  
  
![ラックとネットワーク](media/rack-and-network.png "APS ラックとネットワーク")  
  
## <a name="datascaleunit"></a>データスケールユニット
 
データスケールユニットには、ユーザーデータを処理および格納するためのデータホストと直接接続ストレージ (DAS) が含まれています。 容量を追加するには、ハードウェアベンダーによってサポートされている構成に従って、データスケールユニットを追加します。 データスケールユニットの数が増えるにつれて、より多くの電力、ネットワーク、およびラックのインフラストラクチャを提供するために、必要に応じてラック & ネットワークコンポーネントを追加する必要があります。  
  
### <a name="data-host"></a>データホスト  

データホストは、ユーザーデータを処理する専用のサーバーです。 並列データウェアハウス (PDW) は、各データホストで1つのコンピューティングノードを実行します。 HPE アプライアンスの場合、データスケールユニットには2つのデータホストがあります。 Dell およびクォンタムアプライアンスの場合、データスケールユニットには3つのデータホストがあります。  
  
### <a name="direct-attached-storage"></a>直接接続ストレージ
 
直接接続ストレージ (DAS) は、データホストに接続されているディスクのプールです。 すべてのデータホストは、どのディスクにもアクセスできます。 共有 nothing アーキテクチャの一部として、データホスト上で実行されているコンピューティングノードは個々のディスクを共有しません。 ただし、高可用性を実現するために、ストレージアクセスは共有され、各データホストはどのディスクにもアクセスできます。  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>データスケールユニットのアーキテクチャ-DELL およびクォンタム
  
![スケーラビリティユニット](media/scalability-unit-dell.png "Dell のスケーラビリティユニット")  
  
### <a name="data-scale-unit-architecture---hpe"></a>データスケールユニットのアーキテクチャ-HPE 
 
![HPE スケーラビリティユニット](media/scalability-unit-hpe.png "HPE スケーラビリティユニット")  
  
### <a name="data-scale-unit-description"></a>データスケールユニットの説明

データスケールユニットには、コンピューティングノードごとに1つのサーバー (ホスト) と、シリアル接続 SCSI (SAS) に接続されている直接接続ディスクアレイが1つあります。 ストレージキャビネット内では、ディスクアレイは2つの半分に分割され、それぞれに冗長な電源があります。 Windows Server 記憶域スペースでは、RAID 1 でミラー化されたディスクペア間でデータを複製することで、ユーザーデータを管理します。 各ディスクペアのディスクは、ディスクアレイの別の部分に格納されます。  
  
ディスクアレイには、ホットスペアディスクとシステムディスクも含まれています。 ディスクに障害が発生した場合、記憶域スペースは、機能しているディスク上のデータの適切なコピーを使用して、ホットスペア上のデータの複製コピーを再構築します。 これは、データの損失を防ぐのに役立つ、重要な自己復旧機能です。  
  
計算ノードのディスクの合計数:  
  
-   DELL は 96 disks = (3 台のサーバー) * (サーバー \*あたり16台のディスク) (冗長ディスクの場合は2個) です。  
  
-   HPE には64ディスク = (2 台のサーバー) * (サーバーあたり\* 16 台のディスク) があります (冗長ディスクの場合は 2)。  
  
-   さらに、各ディスクアレイにはホットスペアディスクとシステムディスクがあります。  
  
**高可用性の**場合、コンピューティングノードのフェールオーバー時には、データスケールユニット内の他のホストを経由して機能し、ユーザーデータにアクセスできます。 直接接続されている物理ホストの少なくとも1つが機能しているか、記憶域へのデータアクセスが失われています。  
  
**ディスクサイズの**場合、直接接続された記憶域は、1、2、または 3 tb のディスクドライブを持つことができます。 すべてのデータスケールユニットには、同じサイズのディスクが必要です。  
  
## <a name="basescaleunit"></a>基本スケールユニット 
 
基本スケールユニットには、アプライアンスに必要な、ブレイン電源ホスト、データホスト、および直接接続ストレージの最小数が含まれています。 これには、次のコンポーネントが含まれます。 
  
### <a name="orchestration-host"></a>オーケストレーションホスト  
このサーバーは PDW の頭脳を実行します。
  
### <a name="passive-host"></a>パッシブホスト  
このサーバーは高可用性を提供します。 オーケストレーションまたはデータホストで障害が発生した場合に備えて、オンラインで、ジョブを実行する準備ができています。 オーケストレーションホスト、パッシブホスト、およびデータスケールユニットサーバーは、Windows フェールオーバークラスターとして構成されます。 アプライアンスの各ラックには、1つのパッシブホストが必要です。  
  
### <a name="optional-passive-host"></a>オプションのパッシブホスト  
冗長性をさらに高めるには、基本スケールユニットに2番目のパッシブホストを追加するオプションがあります。  
  
### <a name="data-scale-unit"></a>データスケールユニット  
基本スケールユニットには、ラックの下部に配置されるデータスケールユニットが1つ含まれています。  
  
この図は、基本スケールユニットとラックおよびネットワークを示しています。 これは、Analytics Platform System アプライアンスの最小構成です。  
  
![基本スケールユニット](media/base-scale-unit.png "基本スケールユニット")  
 
