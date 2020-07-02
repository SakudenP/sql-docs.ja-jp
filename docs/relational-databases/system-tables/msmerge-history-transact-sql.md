---
title: MSmerge_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9ca908d080a77eb580f945856c3bc2a28a066f4a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85736720"
---
# <a name="msmerge_history-transact-sql"></a>MSmerge_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_history**テーブルには、過去のマージエージェントジョブセッションの結果に関する詳細な説明を含む履歴行が含まれています。 このテーブルには、エージェントの出力行ごとに1つの行が含まれています。 このテーブルは、ディストリビューション データベースと各サブスクリプション データベースで使用されます。 ディストリビューションデータベースには、ディストリビューターを使用するすべてのマージパブリケーションおよびサブスクリプションの履歴が含まれています。 各サブスクリプションデータベースには、サブスクライバーがサブスクライブされているパブリケーションの履歴が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|マージエージェントジョブの ID。|  
|**agent_id**|**int**|マージエージェントの ID。|  
|**コメント**|**nvarchar(255)**|メッセージ テキストです。|  
|**error_id**|**int**|[MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)システムテーブル内のエラーの ID。|  
|**timestamp**|**timestamp**|このテーブルのタイムスタンプ列です。|  
|**updatable_row**|**bit**|履歴行を上書きできる場合は、 **1**に設定します。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
