---
title: プル サブスクリプションのプロパティの表示または変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying subscriptions
- viewing replication properties
- modifying replication properties, pull subscriptions
- pull subscriptions [SQL Server replication], modifying
- subscriptions [SQL Server replication], pull
- pull subscriptions [SQL Server replication], properties
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b847a22d31bbf3ea7540c55339fe27531134125
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063718"
---
# <a name="view-and-modify-pull-subscription-properties"></a>プル サブスクリプションのプロパティの表示または変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、プル サブスクリプションのプロパティを表示および変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **プル サブスクリプションのプロパティを表示および変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリッシャーまたはサブスクライバーからのプルサブスクリプションのプロパティを表示するには、の [**サブスクリプションのプロパティ- \<Publisher> \<PublicationDatabase> :** ] ダイアログボックスを使用します。このダイアログボックスは、から入手でき [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。 その他のプロパティはサブスクライバーから表示でき、サブスクライバーで変更できます。 パブリッシャーからも、レプリケーション モニターの **[すべてのサブスクリプション]** タブでプロパティを表示できます。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-management-studio"></a>Management Studio でパブリッシャーからのプル サブスクリプション プロパティを表示するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  適切なパブリケーションを展開し、サブスクリプションを右クリックして、 **[プロパティ]** をクリックします。  
  
4.  プロパティを表示して **[OK]** をクリックします。  
  
#### <a name="to-view-and-modify-pull-subscription-properties-from-the-subscriber-in-management-studio"></a>Management Studio でサブスクライバーからのプル サブスクリプション プロパティを表示および変更するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル サブスクリプション]** フォルダーを展開します。  
  
3.  サブスクリプションを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-replication-monitor"></a>レプリケーション モニターでパブリッシャーからのプル サブスクリプション プロパティを表示するには  
  
1.  レプリケーション モニターの左ペインのパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[すべてのサブスクリプション]** タブをクリックします。  
  
3.  サブスクリプションを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  プロパティを表示して **[OK]** をクリックします。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
 レプリケーション ストアド プロシージャを使用して、プル サブスクリプションを変更し、そのプロパティにプログラムからアクセスできます。 使用するストアド プロシージャは、サブスクリプションが属するパブリケーションの種類によって異なります。  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプル サブスクリプションのプロパティを表示するには  
  
1.  サブスクライバーで、 [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql)を実行します。 **@publisher**、、およびを指定し **@publisher_db** **@publication** ます。 これにより、サブスクライバーのシステム テーブルに格納されている、サブスクリプションに関する情報が返されます。  
  
2.  サブスクライバーで、 [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)を実行します。 **@publisher**、、 **@publisher_db** **@publication** 、およびに対して次のいずれかの値を指定し **@publication_type** ます。  
  
    -   **0** - サブスクリプションがトランザクション パブリケーションに属します。  
  
    -   **1** - サブスクリプションがスナップショット パブリケーションに属します。  
  
3.  パブリッシャーで、 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)を実行します。 およびを指定し **@publication** **@subscriber** ます。  
  
4.  パブリッシャーで、 [@subscriber](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)を指定して **@subscriber**から表示できます。 これにより、サブスクライバーに関する情報が表示されます。  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプル サブスクリプションのプロパティを変更するには  
  
1.  サブスクライバーで、、、を指定して[sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql)を実行します。この場合、 **@publisher** には **@publisher_db** **@publication** **0** (トランザクション) または**1** (snapshot) の値を、には変更するサブスクリプションプロパティを、には新しい値を指定し **@publication_type** **@property** **@value** ます。  
  
2.  (省略可) サブスクライバー側のサブスクリプション データベースに対して、 [sp_changesubscriptiondtsinfo](/sql/relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql)を実行します。 にディストリビューションエージェントジョブの ID を指定 **@jobid** し、次のデータ変換サービス (DTS) パッケージのプロパティを指定します。  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     これにより、サブスクリプションの DTS パッケージ プロパティが変更されます。  
  
    > [!NOTE]  
    >  ジョブ ID は、 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)を実行することで取得できます。  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションのプロパティを表示するには  
  
1.  サブスクライバーで、 [sp_helpmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql)を実行します。 **@publisher**、、およびを指定し **@publisher_db** **@publication** ます。  
  
2.  サブスクライバーで、 [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)を実行します。 **@publisher**、、 **@publisher_db** **@publication** 、およびの値を2に指定し **@publication_type** ます。  
  
3.  パブリッシャーで [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql) を実行し、サブスクリプション情報を表示します。 特定のサブスクリプションに関する情報を返すには **@publication** 、、 **@subscriber** 、およびに**pull**の値を指定する必要があり **@subscription_type** ます。  
  
4.  パブリッシャーで、 [@subscriber](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)を指定して **@subscriber**から表示できます。 これにより、サブスクライバーに関する情報が表示されます。  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションのプロパティを変更するには  
  
1.  サブスクライバーで、 [sp_changemergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql)を実行します。 **@publication**、、 **@publisher** **@publisher_db** 、変更するサブスクリプションプロパティを、 **@property** および新しい値として指定し **@value** ます。  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 プル サブスクリプションのプロパティを表示または変更する際に使用する RMO のクラスは、プル サブスクリプションがサブスクライブされるパブリケーションの種類によって異なります。  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのプル サブスクリプションのプロパティを表示または変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> の各プロパティを設定します。  
  
4.  手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから `false` が返された場合、手順 3. で指定したサブスクリプションのプロパティが正しく定義されていないか、サブスクリプションがサーバー上に存在していません。  
  
6.  (省略可) プロパティを変更するには、 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> の設定可能なプロパティに新しい値を設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出します。  
  
7.  (省略可) 新しい設定を表示するには、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> メソッドを呼び出して、アーティクルのプロパティを再読み込みします。  
  
8.  すべての接続を閉じます。  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションのプル サブスクリプションのプロパティを表示または変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> の各プロパティを設定します。  
  
4.  手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから `false` が返された場合、手順 3. で指定したサブスクリプションのプロパティが正しく定義されていないか、サブスクリプションがサーバー上に存在していません。  
  
6.  (省略可) プロパティを変更するには、 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> の設定可能なプロパティに新しい値を設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出します。  
  
7.  (省略可) 新しい設定を表示するには、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> メソッドを呼び出して、アーティクルのプロパティを再読み込みします。  
  
8.  すべての接続を閉じます。  
  
## <a name="see-also"></a>参照  
 [レプリケーションモニターを使用して情報を表示し、タスクを実行する](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [パブリケーションのサブスクライブ](subscribe-to-publications.md)  
  
  
