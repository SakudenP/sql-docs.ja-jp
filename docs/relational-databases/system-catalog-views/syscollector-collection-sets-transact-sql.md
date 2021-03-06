---
title: syscollector_collection_sets (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collection_sets_TSQL
- syscollector_collection_sets
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collection_sets view
ms.assetid: db0def92-f25b-45da-9709-eab972b33800
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 62b63057e34c2d26ad9d8ee3689267c9a06c93dc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754312"
---
# <a name="syscollector_collection_sets-transact-sql"></a>syscollector_collection_sets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  スケジュール、コレクションモード、およびその状態を含む、コレクションセットに関する情報を提供します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|collection_set_id|**int**|コレクション セットのローカル識別子です。 NULL 値は許可されません。|  
|collection_set_uid|**uniqueidentifier**|コレクション セットのグローバルな一意識別子です。 NULL 値は許可されません。|  
|name|**nvarchar (4000)**|コレクションセットの名前。 NULL 値が許可されます。|  
|ターゲット (target)|**nvarchar(max)**|コレクションセットの対象を識別します。 NULL 値が許可されます。|  
|is_system|**bit**|コレクション セットがデータ コレクターに付属のものか、後から dc_admin によって追加されたものかをオン (1) またはオフ (0) で示します。 たとえば、社内またはサード パーティによって開発されたコレクション セットの場合が考えられます。 NULL 値は許可されません。|  
|is_running|**bit**|コレクションセットが実行されているかどうかを示します。 NULL 値は許可されません。|  
|collection_mode|**smallint**|コレクション セットのコレクション モードを指定します。 NULL 値は許可されません。<br /><br /> コレクション モードは、次のいずれかになります。<br /><br /> 0-キャッシュモード。 データの収集とアップロードは別々のスケジュールに基づいています。<br /><br /> 1-非キャッシュモード。 データの収集とアップロードは同じスケジュールに従います。|  
|proxy_id|**int**|コレクションセットのジョブステップを実行するために使用されるプロキシを識別します。 NULL 値が許可されます。|  
|schedule_uid|**uniqueidentifier**|コレクションセットのスケジュールへのポインターを提供します。 NULL 値が許可されます。|  
|collection_job_id|**uniqueidentifier**|コレクションジョブを識別します。 NULL 値が許可されます。|  
|upload_job_id|**uniqueidentifier**|コレクションのアップロードジョブを識別します。 NULL 値が許可されます。|  
|logging_level|**smallint**|ログ記録レベルを 0、1、または 2 から指定します。 NULL 値は許可されません。|  
|days_until_expiration|**smallint**|収集したデータを管理データウェアハウスに保存する日数。 NULL 値は許可されません。|  
|description|**nvarchar (4000)**|コレクションセットについて説明します。 NULL 値が許可されます。|  
|dump_on_any_error|**bit**|[!INCLUDE[ssIS](../../includes/ssis-md.md)]エラーが発生した場合にダンプファイルを作成するかどうかを指定するために、(1) または off (0) をオンにします。 NULL 値は許可されません。|  
|dump_on_codes|**nvarchar(max)**|ダンプ ファイルの原因となった [!INCLUDE[ssIS](../../includes/ssis-md.md)] エラー コードのリストです。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 dc_operator、dc_proxy に対する SELECT 権限が必要です。  
  
## <a name="remarks"></a>Remarks  
 データ コレクター API で変更または削除が許可されるコレクション セットは、ユーザーが作成したコレクション セットのみです。 システムが提供するコレクション セットは変更または削除できません。 ただし、システム コレクション セットを有効または無効にしたり、その構成を変更することはできます。  
  
## <a name="see-also"></a>関連項目  
 [データコレクターストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データコレクタービュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [データコレクション](../../relational-databases/data-collection/data-collection.md)  
  
  
