---
title: dm_audit_class_type_map (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_audit_class_type_map
- sys.dm_audit_class_type_map_TSQL
- dm_audit_class_type_map
- dm_audit_class_type_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_audit_class_type_map dynamic management view
ms.assetid: e10b5431-1bb0-47ca-8fd0-c04bd73a4410
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7ed2102562b16be51f70abf22d7a18aeba010806
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830936"
---
# <a name="sysdm_audit_class_type_map-transact-sql"></a>sys.dm_audit_class_type_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  監査ログ内の class_type フィールドを、sys.dm_audit_actions 内の class_desc フィールドにマップするテーブルを返します。 監査の詳細につい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ては、「 [SQL Server audit &#40;データベースエンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**class_type**|**char(2)**|監査されたエンティティのクラス型。 監査ログに書き込まれ、 **get_audit_file ()** 関数によって返される class_type に割り当てられます。 NULL 値は許可されません。|  
|**class_type_desc**|**nvarchar(120)**|監査可能なエンティティの名前。 NULL 値は許可されません。|  
|**securable_class_desc**|**nvarchar(120)**|監査対象の class_type にマップされるセキュリティ保護可能なオブジェクト。 class_type がセキュリティ保護可能なオブジェクトにマップされない場合は NULL です。 sys.dm_audit_actions の class_desc に関連付けることができます。|  
  
## <a name="permissions"></a>アクセス許可  
 プリンシパルには**SELECT**権限が必要です。 既定では、これは Public に与えられます。  
  
## <a name="see-also"></a>参照  
 [CREATE SERVER AUDIT &#40;Transact-sql&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-sql&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-sql&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [Transact-sql&#41;&#40;のサーバー監査の仕様の作成](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-sql&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-sql&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [Transact-sql&#41;&#40;データベース監査の仕様の作成](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [Transact-sql&#41;&#40;データベース監査の仕様の変更](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [Transact-sql&#41;&#40;データベース監査の仕様を削除します。](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-sql&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [fn_get_audit_file &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [server_audits &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [server_file_audits &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [server_audit_specifications &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [server_audit_specification_details &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [database_audit_specifications &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [database_audit_specification_details &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [dm_server_audit_status &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [dm_audit_class_type_map](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
