---
title: dm_db_mirroring_auto_page_repair (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair
- dm_db_mirroring_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- automatic page repair
- database mirroring [SQL Server], automatic page repair
- sys.dm_db_mirroring_auto_page_repair dynamic management view
ms.assetid: 49f0fc2a-e25e-47e1-a135-563adb509af1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b030903602a5356d273e3bd5ce46995a83ea9bf3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720340"
---
# <a name="database-mirroring---sysdm_db_mirroring_auto_page_repair"></a>データベースミラーリング-sys. dm_db_mirroring_auto_page_repair
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  サーバー インスタンス上のミラー化されたデータベースに対して試行されたページの自動修復ごとに 1 行を返します。 このビューには、ミラー化された特定のデータベースに対して最近試行されたページの自動修復に対応する行が含まれます (データベースあたり最大 100 行)。 データベースあたりの最大行数に達すると、その後に試行されたページの自動修復の行によって、既存のエントリが置き換えられます。 次の表では、さまざまな列の意味を定義します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|この行が対応するデータベースの ID。|  
|**file_id**|**int**|ページが配置されているファイルの ID。|  
|**page_id**|**bigint**|ファイル内のページの ID です。|  
|**error_type**|**int**|エラーの種類です。 指定できる値は次のとおりです。<br /><br /> **-** 1 = すべてのハードウェア823エラー<br /><br /> 1 = 不適切なチェックサムまたは破損ページ (不適切なページ ID など) 以外のエラー824<br /><br /> 2 = 不適切なチェックサム<br /><br /> 3 = 破損ページ|  
|**page_status**|**int**|ページ修復の試行ステータスです。<br /><br /> 2 = パートナーからの要求を待機中。<br /><br /> 3 = 要求がパートナーに送信されました。<br /><br /> 4 = 自動ページ修復のためのキューに登録済み (応答をパートナーから受信)<br /><br /> 5 = ページの自動修復に成功し、ページは使用可能。<br /><br /> 6 = 修復不可能。 これは、ページの修復の試行中にエラーが発生したことを示します。たとえば、ページがパートナーでも破損している、パートナーが切断されている、ネットワークの問題が発生したなどが原因です。 この状態はターミナルではありません。ページで再び破損が発生した場合は、そのページがパートナーから再度要求されます。|  
|**modification_time**|**datetime**|ページの状態が最後に変更された時刻。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [自動ページ修復 &#40;可用性グループ: データベースミラーリング&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Transact-sql&#41;&#40;の動的管理ビューおよび関数](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [suspect_pages &#40;Transact-sql&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  


