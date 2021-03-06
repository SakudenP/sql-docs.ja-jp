---
title: 変更データキャプチャのストアドプロシージャ (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system stored procedures [SQL Server], change data capture
- change data capture [SQL Server], stored procedures
ms.assetid: 7da7068d-6388-465a-b708-a2f27ded1efe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 65cafaf2a4ea26b620bbcf5932031a8781cb9a14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85647013"
---
# <a name="change-data-capture-stored-procedures-transact-sql"></a>変更データキャプチャのストアドプロシージャ (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  変更データ キャプチャにより、有効なテーブルで実行されたデータ操作言語 (DML) 利用状況の履歴レコードを、便利なリレーショナル形式で使用できます。 次のストアドプロシージャは、変更データキャプチャの構成、変更データキャプチャエージェントジョブの管理、および現在のメタデータを変更データコンシューマーに提供するために使用されます。  
  
|||  
|-|-|  
|[sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)|[sp_cdc_generate_wrapper_function &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)|  
|[sp_cdc_change_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)|[sp_cdc_get_captured_columns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)|  
|[sp_cdc_cleanup_change_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-cleanup-change-table-transact-sql.md)|[sp_cdc_get_ddl_history &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)|  
|[sp_cdc_disable_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)|[sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)|  
|[sp_cdc_disable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)|[sp_cdc_help_jobs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)|  
|[sp_cdc_drop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)|[sp_cdc_scan &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)|  
|[sp_cdc_enable_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)|[sp_cdc_start_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)|  
|[sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)|[sp_cdc_stop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)|  
  
## <a name="see-also"></a>関連項目  
 [変更データ キャプチャのテーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)  
  
  
