---
title: AlwaysOn 可用性グループの構成のトラブルシューティング (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [SQL Server], deploying
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], configuring
ms.assetid: 8c222f98-7392-4faf-b7ad-5fb60ffa237e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 165036ba539c3392b1944282bd9d6126eb471a97
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936353"
---
# <a name="troubleshoot-alwayson-availability-groups-configuration-sql-server"></a>AlwaysOn 可用性グループの構成のトラブルシューティング (SQL Server)
  このトピックでは、サーバー インスタンスでの [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。 構成に関する一般的な問題には、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] が無効になっている、アカウントが適切に構成されていない、データベース ミラーリング エンドポイントが存在しない、エンドポイントにアクセスできない (SQL Server エラー 1418)、ネットワーク アクセスが存在しない、データベース参加コマンドが失敗する (SQL Server エラー 35250) などがあります。

> [!NOTE]
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の前提条件を満たしていることを確認してください。 詳細については、「[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。

 **このトピックの内容**

|Section|説明|
|-------------|-----------------|
|[AlwaysOn 可用性グループが有効になっていない](#IsHadrEnabled)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスで [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]が有効になっていない場合、そのインスタンスでは可用性グループの作成がサポートされず、可用性レプリカをホストできません。|
|[Accounts](#Accounts)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているアカウントを適切に構成するための要件について説明します。|
|[EndPoints](#Endpoints)|サーバー インスタンスのデータベース ミラーリング エンドポイントに関する問題の診断方法について説明します。|
|[システム名](#SystemName)|エンドポイントの URL でサーバー インスタンスのシステム名を指定するためのその他の方法について概要を説明します。|
|[ネットワーク アクセス](#NetworkAccess)|可用性レプリカをホストしている各サーバー インスタンスが TCP で他の各サーバー インスタンスのポートにアクセスできる必要があるという要件について説明します。|
|[エンドポイント アクセス (SQLServer エラー 1418)](#Msg1418)|この [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エラー メッセージに関する情報が含まれます。|
|[データベースへの参加に失敗しました (SQL Server エラー 35250)](#JoinDbFails)|プライマリ レプリカへの接続がアクティブでないためにセカンダリ データベースを可用性グループに参加させることができない問題について、考え得る原因と解決策について説明します。|
|[読み取り専用ルーティングが正常に動作しない](#ROR)||
|[関連タスク](#RelatedTasks)|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] オンライン ブックの中の、可用性グループ構成のトラブルシューティングに特に関連するタスク指向のトピックの一覧が含まれます。|
|[関連コンテンツ](#RelatedContent)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの外部にある関連したリソースの一覧が含まれます。|

##  <a name="alwayson-availability-groups-is-not-enabled"></a><a name="IsHadrEnabled"></a>AlwaysOn 可用性グループが有効になっていません
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 機能は、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]の各インスタンスで有効になっている必要があります。 詳細については、「[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)」を参照してください。

##  <a name="accounts"></a><a name="Accounts"></a>企業
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の実行に使用するアカウントは、正しく構成されている必要があります。

1.  アカウントに適切な権限が与えられていることを確認します。

    1.  パートナーを同じドメイン ユーザー アカウントで実行している場合は、両方の **master** データベースに正しいユーザー ログインが自動的に存在します。 この場合は、データベースのセキュリティ構成が単純になるため、望ましいといえます。

    2.  2 つのサーバー インスタンスが別々のアカウントで実行されている場合、リモート サーバー インスタンスの **master** にそれぞれのアカウントのログインを作成する必要があります。また、そのログインには、対応するサーバー インスタンスのデータベース ミラーリング エンドポイントに接続するための CONNECT 権限を付与する必要があります。 詳細については、「[データベースミラーリングのログインアカウントの設定」または「AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)」を参照してください。

2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がビルトイン アカウント (Local System、Local Service、Network Service など) で実行されている場合または非ドメイン アカウントで実行されている場合は、エンドポイント認証に証明書を使用する必要があります。 サービス アカウントで同じドメインのドメイン アカウントを使用している場合は、すべてのレプリカの場所の各サービス アカウントに対して CONNECT アクセスを付与するか、証明書を使用できます。 詳細については、「[データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)」を参照してください。

##  <a name="endpoints"></a><a name="Endpoints"></a> エンドポイント
 エンドポイントが正しく構成されている必要があります。

1.  可用性レプリカ (各 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリカの場所 *) をホストする*の各インスタンスにデータベース ミラーリング エンドポイントがあることを確認します。 データベース ミラーリング エンドポイントが特定のサーバー インスタンスに存在するかどうかを確認するには、[sys.database_mirroring_endpoints](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql) カタログ ビューを使用します。 詳細については、「[Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)」または「[データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)」を参照してください。

2.  ポート番号が適切であることを確認します。

     サーバー インスタンスのデータベース ミラーリング エンドポイントに現在関連付けられているポートを識別するには、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。

    ```
    SELECT type_desc, port FROM sys.tcp_endpoints;
    GO
    ```

3.  説明が困難な [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のセットアップに関する問題については、各サーバー インスタンスを調査して、それぞれが正しいポートでリッスンしているかどうかを確認することをお勧めします。 ポートの可用性の検証については、「 [MSSQLSERVER_1418](../../../relational-databases/errors-events/mssqlserver-1418-database-engine-error.md)」を参照してください。

4.  エンドポイントが開始されていること (STATE = STARTED) を確認します。 各サーバー インスタンスで、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。

    ```
    SELECT state_desc FROM sys.database_mirroring_endpoints
    ```

     **state_desc** 列の詳細については、「[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)」を参照してください。

     エンドポイントを開始するには、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。

    ```
    ALTER ENDPOINT Endpoint_Mirroring 
    STATE = STARTED 
    AS TCP (LISTENER_PORT = <port_number>)
    FOR database_mirroring (ROLE = ALL);
    GO
    ```

     詳細については、「 [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)」を参照してください。

5.  他のサーバーからのログインに、CONNECT 権限があることを確認します。 あるエンドポイントに対して CONNECT 権限のあるユーザーを確認するには、各サーバー インスタンスで、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。

    ```
    SELECT 'Metadata Check';
    SELECT EP.name, SP.STATE, 
       CONVERT(nvarchar(38), suser_name(SP.grantor_principal_id)) 
          AS GRANTOR, 
       SP.TYPE AS PERMISSION,
       CONVERT(nvarchar(46),suser_name(SP.grantee_principal_id)) 
          AS GRANTEE 
       FROM sys.server_permissions SP , sys.endpoints EP
       WHERE SP.major_id = EP.endpoint_id
       ORDER BY Permission,grantor, grantee; 
    GO

    ```

##  <a name="system-name"></a><a name="SystemName"></a> System Name
 エンドポイントの URL におけるサーバー インスタンスのシステム名には、システムを明確に識別できる任意の名前を使用できます。 サーバー アドレスには、システム名 (システムが同じドメインに存在する場合)、完全修飾ドメイン名、または IP アドレス (可能であれば静的 IP アドレス) を使用できます。 完全修飾ドメイン名を使用すると動作が保証されます。 詳細については、「 [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)の構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。

##  <a name="network-access"></a><a name="NetworkAccess"></a> Network Access
 可用性レプリカをホストしている各サーバー インスタンスは、TCP で他の各サーバー インスタンスのポートにアクセスできる必要があります。 これは、サーバー インスタンスが相互に信頼関係を持たない別のドメイン (信頼されていないドメイン) に存在する場合に特に重要になります。

##  <a name="endpoint-access-sql-server-error-1418"></a><a name="Msg1418"></a> エンドポイント アクセス (SQLServer エラー 1418)
 この [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] メッセージは、エンドポイントの URL で指定されたサーバー ネットワーク アドレスに到達できないか、そのアドレスが存在しないことを意味し、ネットワーク アドレス名を確認してコマンドを再実行するように示しています。 詳細については、「 [MSSQLSERVER_1418](../../../relational-databases/errors-events/mssqlserver-1418-database-engine-error.md)」を参照してください。

##  <a name="join-database-fails-sql-server-error-35250"></a><a name="JoinDbFails"></a> データベースの参加の失敗 (SQL Server エラー 35250)
 ここでは、プライマリ レプリカへの接続がアクティブでないためにセカンダリ データベースを可用性グループに参加させることができない問題について、考え得る原因と解決策について説明します。

 **解決策:**

1.  ファイアウォールの設定を調べて、プライマリ レプリカをホストするサーバー インスタンスとセカンダリ レプリカをホストするサーバー インスタンス (既定ではポート 5022) の間でエンドポイント ポート通信が許可されているかどうかを確認します。

2.  ネットワーク サービス アカウントにエンドポイントへの接続権限があるかどうかを確認します。

##  <a name="read-only-routing-is-not-working-correctly"></a><a name="ROR"></a>読み取り専用ルーティングが正しく機能していません
 次の構成値の設定を確認し、必要に応じて修正します。

||対象|アクション|コメント|Link|
|------|---------|------------|--------------|----------|
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|現在のプライマリ レプリカ|可用性グループ リスナーがオンラインであることを確認します。|**リスナーがオンラインになっているかどうかを確認するには:**<br /><br /> `SELECT * FROM sys.dm_tcp_listener_states;`<br /><br /> **オフラインのリスナーを再起動するには:**<br /><br /> `ALTER AVAILABILITY GROUP myAG RESTART LISTENER 'myAG_Listener';`|[sys.dm_tcp_listener_states &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)|
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|現在のプライマリ レプリカ|READ_ONLY_ROUTING_LIST に、読み取り可能なセカンダリ レプリカをホストしているサーバー インスタンスだけが含まれていることを確認します。|**読み取り可能なセカンダリ レプリカを識別するには:** sys.availability_replicas  (**secondary_role_allow_connections_desc** 列)<br /><br /> **読み取り専用ルーティング リストを表示するには:** sys.availability_read_only_routing_lists<br /><br /> **読み取り専用ルーティング リストを変更するには:** ALTER AVAILABILITY GROUP|[sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)<br /><br /> [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)|
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|read_only_routing_list にあるすべてのレプリカ|READ_ONLY_ROUTING_URL ポートが Windows ファイアウォールでブロックされていないことを確認します。|-|[データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|read_only_routing_list にあるすべてのレプリカ|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーで次のことを確認します:<br /><br /> SQL Server のリモート接続が有効になっている。<br /><br /> TCP/IP が有効になっている。<br /><br /> IP アドレスが正しく構成されている。|-|[サーバー プロパティの表示または変更 &#40;SQL Server&#41;](../../configure-windows/view-or-change-server-properties-sql-server.md)<br /><br /> [特定の TCP ポートで受信待ちするようにサーバーを構成する方法 &#40;SQL Server 構成マネージャー&#41;](../../configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)|
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|read_only_routing_list にあるすべてのレプリカ|READ_ONLY_ROUTING_URL (TCP<strong>:// *`system-address`* :</strong>*ポート*) に正しい完全修飾ドメイン名 (FQDN) とポート番号が含まれていることを確認します。|-|[AlwaysOn の read_only_routing_url の計算](https://docs.microsoft.com/archive/blogs/mattn/calculating-read_only_routing_url-for-alwayson)<br /><br /> [sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)|
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|クライアント システム|クライアント ドライバーが読み取り専用のルーティングをサポートしていることを確認します。|-|[AlwaysOn クライアント接続 (SQL Server)](always-on-client-connectivity-sql-server.md)|

##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク

-   [可用性グループの作成と構成 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)

-   [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)

-   [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)

-   [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)

-   [失敗したファイルの追加操作のトラブルシューティング &#40;AlwaysOn 可用性グループ&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)

-   [可用性グループのデータベースのためのログインとジョブの管理 &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)

-   [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)

##  <a name="related-content"></a><a name="RelatedContent"></a> 関連コンテンツ

-   [フェールオーバー クラスターのイベントおよびログを表示する](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)

-   [Get-ClusterLog フェールオーバー クラスター コマンドレット](https://technet.microsoft.com/library/ee461045.aspx)

-   [SQL Server AlwaysOn チームのブログ: AlwaysOn チームの公式 SQL Server のブログ](https://blogs.msdn.com/b/sqlalwayson/)

## <a name="see-also"></a>参照
 [データベースミラーリングのトランスポートセキュリティと AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md) [クライアントのネットワーク構成](../../configure-windows/client-network-configuration.md)の[前提条件、制限](prereqs-restrictions-recommendations-always-on-availability.md)事項、AlwaysOn 可用性グループ &#40;SQL Server に関する推奨事項&#41;


