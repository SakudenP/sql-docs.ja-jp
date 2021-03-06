---
title: SQL Server レプリケーション [ディストリビューター情報] ダイアログボックス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.Distributor.Publications.f1
- sql12.rep.monitor.Distributor.commonjobs..f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.merge.f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.snapshot.f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.tran.f1
ms.assetid: 1f499277-7f12-42ba-8cf4-52b683434944
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ca0717a63c9660c225ec238e1e4d2423f7d01ba
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010791"
---
# <a name="distributor-information-dialog-box"></a>[ディストリビューター情報] ダイアログボックス 
このトピックでは、[**ディストリビューター** ] ダイアログボックスについて説明します。 

## <a name="publications"></a>パブリケーション

  **[パブリケーション]** タブを使用すると、左ペインで選択したディストリビューターにおけるすべてのパブリケーションに関する要約情報を取得できます。  
  
### <a name="options"></a>オプション  
 ディストリビューターによりサポートされるパブリケーションについて表示される情報には、パブリッシャーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを含む列などがあります。 それ以外は、レプリケーション モニターのパブリッシャー ビューに表示されるものと同じパブリケーション情報です。 **[パブリケーション]** タブ内の列の詳細については、「 [Publisher Information, Publications](publisher-information-publications.md)」を参照してください。  

## <a name="subscription-watch-list"></a>サブスクリプション ウォッチ リスト

### <a name="transactional-replication"></a>トランザクション レプリケーション 
  トランザクション サブスクリプションの情報にはパブリッシャーの名前が含まれます。 それ以外は、このダイアログ ボックスで提供される機能と情報はパブリッシャーのビューと同様です。 このダイアログ ボックスに関する情報については、「[Publisher Information, Subscription Watch List &#40;Transactional Publication, SQL Server 2005 and Later&#41;](publisher-information-subscription-watch-list-transactional.md)」 (パブリッシャー情報、サブスクリプション ウォッチ リスト スナップショット (トランザクション パブリケーション、SQL Server 2005 以降)) を参照してください。  

### <a name="merge-replication"></a>マージ レプリケーション
  マージ パブリケーションのサブスクリプションの情報にはパブリッシャーの名前が含まれます。 それ以外は、このダイアログ ボックスで提供される機能と情報はパブリッシャーのビューと同様です。 このダイアログ ボックスに関する情報については、「[Publisher Information, Subscription Watch List &#40;Merge Publication, SQL Server 2005 and Later&#41;](publisher-information-subscription-watch-list-merge-publication.md)」 (パブリッシャー情報、サブスクリプション ウォッチ リスト スナップショット (マージ パブリケーション、SQL Server 2005 以降)) を参照してください。 

### <a name="snapshot-replication"></a>スナップショット レプリケーション
  スナップショット パブリケーションのサブスクリプションの情報にはパブリッシャーの名前が含まれます。 それ以外は、このダイアログ ボックスで提供される機能と情報はパブリッシャーのビューと同様です。 このダイアログ ボックスに関する情報については、「[Publisher Information, Subscription Watch List &#40;Snapshot Publication, SQL Server 2005 and Later&#41;](publisher-information-subscription-watch-list-snapshot.md)」 (パブリッシャー情報、サブスクリプション ウォッチ リスト スナップショット (スナップショット パブリケーション、SQL Server 2005 以降)) を参照してください。  

## <a name="agents"></a>エージェント
  **[エージェント]** タブには、パブリッシャーおよびサブスクライバーに関連するエージェントおよびメンテナンス ジョブに関する詳細情報が表示されます。  
  
 ディストリビューター ビューのディストリビューターの **[エージェント]** タブで利用可能なエージェントには、パブリッシャーの **[エージェント]** タブで利用可能なすべてのエージェントが含まれています。 ただし、ディストリビューター ビューのディストリビューターの **[エージェント]** タブには、ディストリビューター エージェントおよびマージ エージェントも含まれています。  
  
 スナップショット エージェント、ログ リーダー エージェント、キュー リーダー エージェント、およびメンテナンス ジョブの詳細については、「 [Publisher Information, Agents](publisher-information-agents.md)」を参照してください。 ディストリビューターの **[エージェント]** タブでエージェント情報を表示する場合は、スナップショット エージェントおよびログ リーダー エージェントのパブリッシャー情報があることに注意してください ただし、ディストリビューター ビューのディストリビューターの **[エージェント]** タブでは、 **[ディストリビューター エージェント]** および **[マージ エージェント]** も選択できます。  
  
### <a name="options"></a>オプション  
 この後のセクションでは、このタブで表示されるディストリビューター エージェントおよびマージ エージェントのデータについて説明します。  
  
### <a name="distributor-agent"></a>[ディストリビューター エージェント]  
 **状態**  
 エージェントの状態です。 表示される状態の種類を、次に示します。  
  
-   エラー    
-   [再試行]    
-   実行中    
-   停止中    
-   [一度も開始していない]  
  
 **発行元**  
 パブリッシャーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスです。  
  
 **パブリケーション**  
 エージェントが関連付けられているパブリケーションの名前です。  
  
 **サブスクリプション**  
 [*SubscriberName*].[*Database*] という形式のサブスクリプションの名前です。  
  
 **Type**  
 レプリケーションの種類 (プッシュ、プル、または匿名) です。  
  
 **前回の開始時刻**  
 前回のエージェントの開始時刻です。  
  
 **期間**  
 エージェントが実行された時間の長さです。 この時間は、エージェントが現在実行中の場合は経過時間、エージェントが以前に実行されている場合は合計時間を表します。  
  
 **[最後のアクション]**  
 エージェントが最後に実行されたときに最後に実行されたアクションです。  
  
 **[配信率]**  
 エージェントが最後に実行されたときにディストリビューション データベースで初期化コマンドがコミットされた頻度 (1 秒あたりのコマンド数) です。  
  
 **待機時間**  
 パブリケーション データベースで最新の変更がコミットされてから、ディストリビューション データベースで対応するコマンドがコミットされるまでに経過した時間 (秒単位) です。  
  
 **[#Trans]**  
 エージェントが最後に実行されたときにディストリビューション データベースでコミットされたトランザクションの数です。  
  
 **[#Cmds]**  
 エージェントが最後に実行されたときにディストリビューション データベースでコミットされたコマンドの数です。 更新などのデータ変更がコマンドに相当します。  
  
 **[Avg. #Cmds]**  
 エージェントが最後に実行されたときの 1 トランザクションあたりの平均コマンド数です。  
  
### <a name="merge-agent"></a>[マージ エージェント]  
 **状態**  
 エージェントの状態です。 表示される状態の種類を、次に示します。  
  
-   エラー    
-   [再試行]    
-   実行中    
-   停止中    
-   [一度も開始していない]  
  
 **発行元**  
 パブリッシャーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスです。  
  
 **パブリケーション**  
 エージェントが関連付けられているパブリケーションの名前です。  
  
 **サブスクリプション**  
 [*SubscriberName*].[*Database*] という形式のサブスクリプションの名前です。  
  
 **Type**  
 レプリケーションの種類 (プッシュ、プル、または匿名) です。  
  
 **前回の開始時刻**  
 前回のエージェントの開始時刻です。  
  
 **期間**  
 エージェントが実行された時間の長さです。 この時間は、エージェントが現在実行中の場合は経過時間、エージェントが以前に実行されている場合は合計時間を表します。  
  
 **[最後のアクション]**  
 エージェントが最後に実行されたときに最後に実行されたアクションです。  
  
 **[配信率]**  
 ディストリビューション データベースで変更がコミットされた頻度 (1 秒あたりのコマンド数) です。  
  
 **[パブリッシャーの挿入]**  
 パブリッシャー側で適用される INSERT コマンドの数です。  
  
 **[パブリッシャーの更新]**  
 パブリッシャー側で適用される UPDATE コマンドの数です。  
  
 **[パブリッシャーの削除]**  
 パブリッシャー側で適用される DELETE コマンドの数です。  
  
 **[パブリッシャーの競合]**  
 マージ プロセス中にパブリッシャー側で発生した競合の数です。  
  
 **[サブスクライバーの挿入]**  
 サブスクライバー側で適用される INSERT コマンドの数です。  
  
 **[サブスクライバーの更新]**  
 サブスクライバー側で適用される UPDATE コマンドの数です。  
  
 **[サブスクライバーの削除]**  
 サブスクライバー側で適用される DELETE コマンドの数です。  
  
 **[サブスクライバーの競合]**  
 マージ プロセス中にサブスクライバー側で発生した競合の数です。  
  
 
## <a name="see-also"></a>参照  
 [レプリケーションモニターを開始する](monitor/start-the-replication-monitor.md)   
 [レプリケーションの監視](monitoring-replication.md)  
  
  
