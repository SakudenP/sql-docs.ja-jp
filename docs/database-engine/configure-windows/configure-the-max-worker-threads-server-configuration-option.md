---
title: max worker threads サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 04/14/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d573bc4c8fc628bf4f1cc1fa36e50bc0e69c3202
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488331"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>max worker threads サーバー構成オプションの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 **または** を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] max worker threads [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **max worker threads** オプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで利用できるワーカー スレッド数を構成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、オペレーティング システムのネイティブ スレッド サービスを使用しているため、1 つ以上のスレッドが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で同時にサポートされている各ネットワークをサポートし、他のスレッドがデータベース チェックポイントを処理し、スレッド プールがすべてのユーザーを処理します。 **max worker threads** の既定値は 0 です。 この場合、ワーカー スレッドの数が、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって起動時に自動で構成されます。 既定の設定は、ほとんどのシステムで最適な設定です。 ただし、システム構成によっては、 **max worker threads** を特定の値に設定するとパフォーマンスが向上することがあります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用して max worker threads オプションを構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [max worker threads オプションを構成した後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   実際のクエリ要求数が **max worker threads**に設定した値を下回る場合、1 つのスレッドで 1 つのクエリ要求が処理されます。 一方、実際のクエリ要求数が **max worker threads** に設定されている値を超えた場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってワーカー スレッドがプールされ、次に使用可能なワーカー スレッドで要求を処理できるようになります。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロフェッショナルだけが変更するようにしてください。 パフォーマンスの問題が疑われる場合、それはおそらくワーカー スレッドの問題ではありません。 I/O などがワーカー スレッドを待機させている可能性が高いです。 ワーカー スレッドの最大数設定を変更する前に、パフォーマンス問題の根本原因を見つけることが推奨されます。  
  
-   スレッド プールは、多数のクライアントがサーバーに接続されている場合のパフォーマンスの最適化に役立ちます。 通常、クエリ要求ごとに個別のオペレーティング システム スレッドが作成されます。 ただし、サーバーへの接続が数百にもなる場合、クエリ要求ごとに 1 つのスレッドを使用すると大量のシステム リソースが消費されることがあります。 **max worker threads** オプションを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってワーカー スレッド プールが作成され多数のクエリ要求を処理できるようになります。その結果、パフォーマンスが向上します。  
  
-   次の表では、CPU、コンピューターのアーキテクチャ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンのさまざまな組み合わせに対して、自動的に構成されるワーカー スレッドの最大数を示します。"* **既定の最大ワーカー数* + ((* 論理 CPU 数* - 4) **CPU あたりのワーカー数*)**" という式が使用されています。  
  
    |CPU の数|32 ビット コンピューター ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以前)|64 ビット コンピューター ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以前)|64 ビット コンピューター ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降)|   
    |------------|------------|------------|------------|  
    |\<= 4|256|512|512|   
    |8|288|576|576|   
    |16|352|704|704|   
    |32|480|960|960|   
    |64|736|1472|2432|   
    |128|1248|2496|4480|   
    |256|2272|4544|8576|   
    
    [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以前の "*CPU あたりのワーカー数*" は、アーキテクチャ (32 ビットまたは 64 ビット) にのみ依存します。
    
    |CPU の数|32 ビット コンピューター <sup>1</sup>|64 ビット コンピューター|   
    |------------|------------|------------|   
    |\<= 4|256|512|   
    |\> 4|256 + ((論理 CPU - 4) * 8)|512 <sup>2</sup> + ((論理 CPU 数 - 4) * 16)|   
    
    [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降の "*CPU あたりのワーカー数*" は、アーキテクチャとプロセッサの数 (4 から 64 の間か、64 を超えるか) に依存します。
    
    |CPU の数|32 ビット コンピューター <sup>1</sup>|64 ビット コンピューター|   
    |------------|------------|------------|   
    |\<= 4|256|512|   
    |\> 4 かつ \<= 64|256 + ((論理 CPU - 4) * 8)|512 <sup>2</sup> + ((論理 CPU 数 - 4) * 16)|   
    |\> 64|256 + ((論理 CPU - 4) * 32)|512 <sup>2</sup> + ((論理 CPU 数 - 4) * 32)|   
  
    <sup>1</sup> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、32 ビットのオペレーティング システムにインストールすることはできません。 32 ビット コンピューターの値は、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以前のバージョンを実行しているお客様への参考として一覧表示されています。 32 ビット コンピューター上で動作する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの場合、ワーカー スレッドの最大数として 1,024 をお勧めします。
    
    <sup>2</sup> [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]以降の "*既定の最大ワーカー数*" の値は、メモリが 2 GB 未満のコンピューターの場合は 2 で除算されます。
  
    > [!TIP]  
    > 64 個を超える CPU を使用する場合の推奨事項については、「 [64 個を超える CPU を搭載したコンピューター上で SQL Server を実行する場合のベスト プラクティス](../../relational-databases/thread-and-task-architecture-guide.md#best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus)」を参照してください。  
  
-   クエリの実行が長時間にわたり、すべてのスレッドがアクティブになっている場合、いずれかのワーカー スレッドが処理を完了し使用できるようになるまで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が応答していないように見えることがあります。 これは欠陥ではありませんが、望ましくない場合があります。 プロセスが応答せず新しいクエリを処理できない場合は、専用管理者接続 (DAC) を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、プロセスを終了します。 このような状態を回避するには、ワーカー スレッド数を増やします。  
  
 **max worker threads** サーバー構成オプションでは、システム内に生成できる全スレッドに制限はありません。 可用性グループ、Service Broker、ロック マネージャーなどのタスクに必要なスレッドは、この制限の外部で生成されます。 構成されたスレッドの数を超えている場合は、次のクエリによって、追加のスレッドを生成したシステム タスクに関する情報が取得されます。  
  
 ```sql  
 SELECT  s.session_id, r.command, r.status,  
    r.wait_type, r.scheduler_id, w.worker_address,  
    w.is_preemptive, w.state, t.task_state,  
    t.session_id, t.exec_context_id, t.request_id  
 FROM sys.dm_exec_sessions AS s  
 INNER JOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
 INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
 INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
 WHERE s.is_user_process = 0;  
 ```  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり `RECONFIGURE` ステートメントを実行したりするには、`ALTER SETTINGS` サーバーレベル権限がユーザーに付与されている必要があります。 `ALTER SETTINGS` 権限は、**sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="using-ssmanstudiofull"></a><a name="SSMSProcedure"></a> 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>max worker threads オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[プロセッサ]** ノードをクリックします。  
  
3.  **[ワーカー スレッド最大数]** ボックスに、128 ～ 32,767 の値を入力するか、または選択します。  
  
> [!TIP]
> **[ワーカー スレッド最大数]** オプションを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで利用できるワーカー スレッド数を設定できます。 ほとんどのシステムの場合、 **[ワーカー スレッド最大数]** の既定値を使用するのが最適です。 ただし、システム構成によっては、 **max worker threads** の値を小さくするとパフォーマンスが向上することがあります。
> 詳細については、このページの「[推奨事項](#Recommendations)」を参照してください。
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>max worker threads オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用して、 `max worker threads` オプションを `900`に設定する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'max worker threads', 900 ;  
GO  
RECONFIGURE;  
GO  
```  
  
##  <a name="follow-up-after-you-configure-the-max-worker-threads-option"></a><a name="FollowUp"></a>補足情報: max worker threads オプションを構成した後  
 [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) の実行後、[!INCLUDE[ssDE](../../includes/ssde-md.md)] を再起動しなくても、変更は直ちに有効になります。  
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [データベース管理者用の診断接続](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  
