---
title: sys. triggers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- triggers
- triggers_TSQL
- sys.triggers
- sys.triggers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.triggers catalog view
ms.assetid: cefa4fc4-b8b9-4cd7-b124-eed5283acbfc
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8bcf1832c8f25da9ac10274c3dac2f6d120c98ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733415"
---
# <a name="systriggers-transact-sql"></a>sys.triggers (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  TR トリガーまたは TA トリガーであるオブジェクトごとに、1 行のデータを格納します。 DML トリガー名はスキーマスコープであるため、 **sys. オブジェクト**に表示されます。 DDL トリガー名は親エンティティによってスコープが設定され、このビューでのみ表示されます。  
  
 **Parent_class**列と**name**列は、データベース内のトリガーを一意に識別します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|トリガー名。 DML トリガー名はスキーマ スコープです。 DDL トリガーの名前は、親エンティティに対してスコープが設定されます。|  
|**object_id**|**int**|オブジェクト ID 番号。 データベース内で一意です。|  
|**parent_class**|**tinyint**|トリガーの親のクラス。<br /><br /> 0 = DDL トリガー用のデータベース<br /><br /> 1 = DML トリガー用のオブジェクトまたは列|  
|**parent_class_desc**|**nvarchar(60)**|トリガーの親クラスの説明です。<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|トリガーの親の ID。次に例を示します。<br /><br /> 0 = データベースが親となっているトリガー<br /><br /> DML トリガーの場合、これは DML トリガーが定義されているテーブルまたはビューの**object_id**です。|  
|**type**|**char(2)**|オブジェクトの種類:<br /><br /> TA = アセンブリ (CLR) トリガー<br /><br /> TR = SQL トリガー|  
|**type_desc**|**nvarchar(60)**|オブジェクトの種類の説明。<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|トリガーが作成された日付。|  
|**modify_date**|**datetime**|オブジェクトが ALTER ステートメントを使用して最後に変更された日付です。|  
|**is_ms_shipped**|**bit**|内部コンポーネントによってユーザーの代理として作成されたトリガー [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**is_disabled**|**bit**|トリガーは無効です。|  
|**is_not_for_replication**|**bit**|トリガーは NOT FOR REPLICATION として作成されました。|  
|**is_instead_of_trigger**|**bit**|1 = INSTEAD OF トリガー<br /><br /> 0 = AFTER トリガー|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [セキュリティカタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
