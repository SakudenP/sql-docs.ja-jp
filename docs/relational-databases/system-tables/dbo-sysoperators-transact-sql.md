---
title: dbo.sys演算子 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysoperators
- dbo.sysoperators
- dbo.sysoperators_TSQL
- sysoperators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoperators system table
ms.assetid: c2afa20c-b15f-46ca-ae74-2eb65909409e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6f56da445992067e31f2088dc3d35f109fb02c2f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750311"
---
# <a name="dbosysoperators-transact-sql"></a>dbo.sysoperators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのオペレーターごとに 1 行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|オペレーターの ID。|  
|**name**|**sysname**|演算子の名前。|  
|**enabled**|**tinyint**|アラート通知の状態 (ブール値)。 **1**の場合、このオペレーターは警告が発生したときに通知を受け取ることができます。|  
|**email_address**|**nvarchar (100)**|このオペレーターの電子メールアドレス。|  
|**last_email_date**|**int**|このオペレーターが最後に電子メール通知を受信した日付。|  
|**last_email_time**|**int**|このオペレーターが最後に電子メール通知を受信した時刻。|  
|**pager_address**|**nvarchar (100)**|このオペレーターのポケットベルアドレス。|  
|**last_pager_date**|**int**|オペレーターが前回ポケットベルによる警告通知を受信した日付。|  
|**last_pager_time**|**int**|このオペレーターが最後にポケットベルによる警告通知を受信した時刻。|  
|**weekday_pager_start_time**|**int**|このオペレーターがポケットベルによる警告通知を受け取ることができるようになる曜日 (月曜から金曜) の時刻。|  
|**weekday_pager_end_time**|**int**|平日 (月曜から金曜まで)、オペレーターのポケットベルによる警告通知が受信不能になる時刻。|  
|**saturday_pager_start_time**|**int**|土曜日にこのオペレーターがポケットベルによる警告通知を受信できるようになる時刻。|  
|**saturday_pager_end_time**|**int**|土曜日にこのオペレーターがポケットベルによる警告通知を受信できない時間。|  
|**sunday_pager_start_time**|**int**|日曜日にこのオペレーターがポケットベルによる警告通知を受信できるようになる時刻。|  
|**sunday_pager_end_time**|**int**|日曜日にこのオペレーターがポケットベルによる警告通知を受信できない時間。|  
|**pager_days**|**tinyint**|このオペレーターがポケットベルによる警告通知を受け取ることができる曜日を表すビットマスク。|  
|**netsend_address**|**nvarchar (100)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**last_netsend_date**|**int**|指定したオペレーター ID に最新のネットワークメッセージが最後に送信された日付。|  
|**last_netsend_time**|**int**|指定したオペレーター ID に最新のネットワークメッセージが最後に送信された時刻。|  
|**category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェントテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
