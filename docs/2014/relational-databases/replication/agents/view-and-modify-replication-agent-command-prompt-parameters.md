---
title: レプリケーションエージェントコマンドプロンプトパラメーターの表示および変更 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e64551075920f2f08bf84fe22086c06387b4439a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068745"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters-sql-server-management-studio"></a>レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する (SQL Server Management Studio)
  レプリケーション エージェントは、コマンド ライン パラメーターを使用できる実行可能ファイルです。 既定では、エージェントは [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントのジョブステップで実行されるため、これらのパラメーターは [**ジョブの \<Job> プロパティ-** ] ダイアログボックスを使用して表示および変更できます。 このダイアログ ボックスは、 **の** [ジョブ] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] フォルダーおよびレプリケーション モニター内の **[エージェント]** タブからアクセスできます。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
> [!NOTE]  
>  エージェント パラメーターの変更は、エージェントの次回起動時に反映されます。 エージェントを継続して実行している場合は、そのエージェントを停止して再起動する必要があります。  
  
 パラメーターは直接変更することもできますが、エージェント プロファイルを使用して変更する方が一般的です。 詳しくは、「 [レプリケーション エージェント プロファイル](replication-agent-profiles.md)」をご覧ください。  
  
 **[ジョブ]** フォルダーからエージェント ジョブにアクセスする場合は、次の表を使用して、各エージェントで使用できるエージェント ジョブ名とパラメーターを決定してください。  
  
|エージェント|ジョブ名|パラメーターの一覧の参照先|  
|-----------|--------------|------------------------------------|  
|スナップショット エージェント|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|マージ パブリケーション パーティションに対するスナップショット エージェント|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|ログ リーダー エージェント (Log Reader Agent)|**\<Publisher>-\<PublicationDatabase>-\<integer>**|[レプリケーション ログ リーダー エージェント](replication-log-reader-agent.md)|  
|プル サブスクリプションに対するマージ エージェント|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|[Replication Merge Agent](replication-merge-agent.md)|  
|プッシュ サブスクリプションに対するマージ エージェント|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Merge Agent](replication-merge-agent.md)|  
|プッシュ サブスクリプションに対するディストリビューション エージェント|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**<sup>1</sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|プル サブスクリプションに対するディストリビューション エージェント|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>**<sup>2</sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|SQL Server 以外のサブスクライバーへのプッシュ サブスクリプションに対するディストリビューション エージェント|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Distribution Agent](replication-distribution-agent.md)|  
|キュー リーダー エージェント (Queue Reader Agent)|**[\<Distributor>].\<integer>**|[レプリケーション キュー リーダー エージェント](replication-queue-reader-agent.md)|  
  
 <sup>1</sup> Oracle パブリケーションに対するプッシュサブスクリプションの場合は、* * \<Publisher> - \<Publisher**> ではなく * ***\<Publisher>-\<PublicationDatabase>**  
  
 <sup>2</sup> Oracle パブリケーションに対するプルサブスクリプションの場合、これは * * \<Publisher> - \<DistributionDatabase**> ではなく * * になります。**\<Publisher>-\<PublicationDatabase>**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Management Studio からレプリケーション エージェント コマンド ライン パラメーターを表示または変更するには  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]で適切なコンピューターに接続して、サーバー ノードを展開します。  
  
    -   プル サブスクリプションに対するディストリビューション エージェントとマージ エージェントの場合は、サブスクライバーに接続します。  
  
    -   その他のエージェントの場合は、ディストリビューターに接続します。  
  
2.  **[SQL Server エージェント]** フォルダーを展開して、 **[ジョブ]** フォルダーを展開します。  
  
3.  ジョブを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  [**ジョブのプロパティ \<Job> -** ] ダイアログボックスの [**ステップ**] ページで、[**エージェントの実行**] ステップを選択し、[**編集**] をクリックします。  
  
5.  **[ジョブ ステップのプロパティ - エージェントを実行します]** ダイアログ ボックスで、 **[コマンド]** フィールドを編集します。  
  
6.  両方のダイアログ ボックスで **[OK]** をクリックします。  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>レプリケーション モニターからディストリビューション エージェントとマージ エージェントのコマンド ライン パラメーターを表示および変更するには  
  
1.  レプリケーション モニターの左ペインのパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[すべてのサブスクリプション]** タブをクリックします。  
  
3.  サブスクリプションを右クリックし、 **[詳細表示]** をクリックします。  
  
4.  [**サブスクリプション \< SubscriptionName> ** ] ウィンドウで、[**アクション**] をクリックし、[ ** \<AgentName> ジョブのプロパティ**] をクリックします。  
  
5.  [**ジョブのプロパティ \<Job> -** ] ダイアログボックスの [**ステップ**] ページで、[**エージェントの実行**] ステップを選択し、[**編集**] をクリックします。  
  
6.  **[ジョブ ステップのプロパティ - エージェントを実行します]** ダイアログ ボックスで、 **[コマンド]** フィールドを編集します。  
  
7.  両方のダイアログ ボックスで **[OK]** をクリックします。  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>レプリケーション モニターからスナップショット エージェント、ログ リーダー エージェント、およびキュー リーダー エージェントのコマンド ライン パラメーターを表示および変更するには  
  
1.  レプリケーション モニターの左ペインのパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[エージェント]** タブをクリックします。  
  
3.  グリッド内のエージェントを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  [**ジョブのプロパティ \<Job> -** ] ダイアログボックスの [**ステップ**] ページで、[**エージェントの実行**] ステップを選択し、[**編集**] をクリックします。  
  
5.  **[ジョブ ステップのプロパティ - エージェントを実行します]** ダイアログ ボックスで、 **[コマンド]** フィールドを編集します。  
  
6.  両方のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レプリケーションエージェントの管理](replication-agent-administration.md)   
 [レプリケーションエージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)   
 [レプリケーション エージェントの概要](replication-agents-overview.md)  
  
  
