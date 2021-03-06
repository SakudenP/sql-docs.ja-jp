---
title: Windows 認証を使用したデータベースミラーリングの設定の例 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- Windows authentication [SQL Server]
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: 35800769-aede-4aac-b077-0e0e487e302f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 95df855e8e41c5937aae02884c71792537eb2bfc
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934193"
---
# <a name="example-setting-up-database-mirroring-using-windows-authentication-transact-sql"></a>Windows 認証を使用したデータベース ミラーリングの設定の例 (Transact-SQL)
  この例では、Windows 認証を使用してミラーリング監視サーバーを利用するデータベース ミラーリング セッションを作成する場合に必要なすべての段階を示しています。 このトピックの例では、 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用する代わりに、データベース ミラーリング セキュリティ構成ウィザードを使用してデータベース ミラーリングを設定することもできます。 詳細については、このトピックの後半の「 [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)」を参照してください。  
  
## <a name="prerequisite"></a>前提条件  
 この例では、既定により単純復旧モデルを使用する **AdventureWorks** サンプル データベースを使用します。 このデータベースでデータベース ミラーリングを使用するには、完全復旧モデルを使用するように変更する必要があります。 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用してこの変更を行うには、次のように ALTER DATABASE ステートメントを使用します。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks   
SET RECOVERY FULL;  
GO  
```  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の復旧モデルを変更する方法については、「[データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)」をご覧ください。  
  
### <a name="permissions"></a>アクセス許可  
 データベースにおける ALTER 権限、および CREATE ENDPOINT 権限、または **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="example"></a>例  
 この例では、2 つのパートナーとミラーリング監視サーバーが、3 つのコンピューター システムの既定のサーバー インスタンスです。 3 つのサーバー インスタンスは同じ Windows ドメインで実行されますが、ミラーリング監視サーバー インスタンスはユーザー アカウント (スタートアップ サービス アカウントとして使用されます) が異なります。  
  
 次の表は、この例で使用する値をまとめたものです。  
  
|初期ミラー化ロール|ホスト システム|ドメイン ユーザー アカウント|  
|----------------------------|-----------------|-------------------------|  
|プリンシパル|PARTNERHOST1|*\<Mydomain>\\<dbousername\>*|  
|ミラー|PARTNERHOST5|*\<Mydomain>\\<dbousername\>*|  
|ミラーリング監視サーバー|WITNESSHOST4|*\<Somedomain>\\<witnessuser\>*|  
  
1.  プリンシパル サーバー インスタンス (PARTNERHOST1 の既定のインスタンス) でエンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=PARTNER)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    -- Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
2.  ミラー サーバー インスタンス (PARTNERHOST5 の既定のインスタンス) でエンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
3.  ミラーリング監視サーバー インスタンス (WITNESSHOST4 の既定のインスタンス) でエンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=WITNESS)  
    GO  
    --Create a login for the partner server instances,  
    --which are both running as Mydomain\dbousername:  
    USE master ;  
    GO  
    CREATE LOGIN [Mydomain\dbousername] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
4.  ミラー データベースを作成します。 詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)を使用します。  
  
5.  PARTNERHOST5 のミラー サーバー インスタンスで、PARTNERHOST1 のサーバー インスタンスをパートナーとして設定します (初期プリンシパル サーバー インスタンスにします)。  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER =   
        'TCP://PARTNERHOST1.COM:7022'  
    GO  
    ```  
  
6.  PARTNERHOST1 のプリンシパル サーバー インスタンスで、PARTNERHOST5 のサーバー インスタンスをパートナーとして設定します (初期ミラー サーバー インスタンスにします)。  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://PARTNERHOST5.COM:7022'  
    GO  
    ```  
  
7.  プリンシパル サーバーで、ミラーリング監視サーバー (WITNESSHOST4) を設定します。  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET WITNESS =   
        'TCP://WITNESSHOST4.COM:7022'  
    GO  
    ```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
  
-   [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
-   [TRUSTWORTHY プロパティを使用するようにミラー データベースを設定する方法 &#40;Transact-SQL&#41;](set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
-   [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [証明書を使用したデータベース ミラーリングの設定の例 &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [データベースミラーリングエンドポイント &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [データベースミラーリングと AlwaysOn 可用性グループ &#40;SQL Server のトランスポートセキュリティ&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
