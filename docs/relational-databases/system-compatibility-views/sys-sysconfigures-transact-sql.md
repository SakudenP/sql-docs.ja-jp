---
title: sys.sysの構成 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysconfigures
- sysconfigures
- sys.sysconfigures_TSQL
- sysconfigures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconfigures compatibility view
- sysconfigures system table
ms.assetid: 146bf10a-c898-4676-a2a1-673fb1cee7a2
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e0e65f06ccecd01ae9396b2c64962040a446aeb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85663347"
---
# <a name="syssysconfigures-transact-sql"></a>sys.sysconfigures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  ユーザーによって設定された構成オプションごとに1行の値を格納します。 **sysconfigures**には、の最後の起動前に定義されている構成オプションに加え、その後に設定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 動的な構成オプションが含まれます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**value**|**int**|ユーザーが変更可能な変数の値。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]再構成が実行されている場合にのみ、によって使用されます。|  
|**config**|**int**|構成変数番号。|  
|**comment**|**nvarchar(255)**|構成オプションの説明。|  
|**status**|**smallint**|オプションの状態を示すビットマップ。 次の値があります。<br /><br /> 0 = 静的。 設定は、サーバーの再起動時に有効になります。<br /><br /> 1 = 動的。 変数は、再構成ステートメントが実行されたときに有効になります。<br /><br /> 2 = 詳細。 変数は、 **[詳細の表示] オプション**が設定されている場合にのみ表示されます。 設定は、サーバーの再起動時に有効になります。<br /><br /> 3 = 動的および詳細。|  
  
## <a name="see-also"></a>関連項目  
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
