---
title: IHpublishercolumnconstraints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnconstraints
- IHpublishercolumnconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnconstraints system table
ms.assetid: d7a41da6-e067-430a-8da2-3f6745b8a4f3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9e31b1b7e595926948072317d2d3cb71137f5f91
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750182"
---
# <a name="ihpublishercolumnconstraints-transact-sql"></a>IHpublishercolumnconstraints (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **IHpublishercolumnconstraints**システムテーブルは、 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)システムテーブル内の非 SQL Server パブリケーションの列を[IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md)システムテーブルの制約にマップします。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|制約が関連付けられている[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)から列を識別します。|  
|**publisherconstraint_id**|**int**|列に関連付けられている[IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md)から制約を識別します。|  
|**indid**|**int**|パブリッシュされたテーブル内の列の位置を示します。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベースレプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
