---
title: MSpeer_conflictdetectionconfigrequest (T-sql)
description: ピアツーピアパブリケーションのトポロジ全体の構成要求を追跡するために使用される MSPeer_conflictdetectionconfigurerequest ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 17872cfae8da4d8f28b6031be168aa60a063d54b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730804"
---
# <a name="mspeer_conflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  ピア ツー ピア レプリケーションで、パブリケーションに対するトポロジ全体の構成要求を追跡するために使用されます。 このテーブルは、パブリケーションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**int**|競合構成要求を識別します。 [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md)の request_id 列には、この値が使用されます。|  
|パブリケーション (publication)|**sysname**|競合構成要求が発行されたパブリケーションの名前です。|  
|sent_date|**datetime**|競合構成要求が開始された日付と時刻。|  
|timeout|**int**|すべてのピアから競合情報が返されるのをプロシージャが待機する時間です。|  
|modified_date|**datetime**|フェーズが完了した日付と時刻。|  
|progress_phase|**nvarchar(32)**|次のいずれかの値を使用して、処理の現在のフェーズを識別します。<br /><br /> Started<br /><br /> トポロジの探索<br /><br /> 収集 (ステータスを)<br /><br /> 収集された状態|  
|phase_timed_out|**bit**|現在のフェーズがタイムアウトしたかどうかを示します。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
