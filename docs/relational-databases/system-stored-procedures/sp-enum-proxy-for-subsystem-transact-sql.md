---
title: sp_enum_proxy_for_subsystem (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 93a55b28325bd9b04af569120ad34baeb689e8f9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "68124659"
---
# <a name="sp_enum_proxy_for_subsystem-transact-sql"></a>sp_enum_proxy_for_subsystem (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシがサブシステムにアクセスするための権限を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_enum_proxy_for_subsystem  
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @proxy_id = ] proxy_id`情報を一覧表示するプロキシの識別番号を指定します。 *Proxy_id*は**int**,、既定値は NULL です。 *Id*または*proxy_name*を指定できます。  
  
`[ @proxy_name = ] 'proxy_name'`情報を一覧表示するプロキシの名前。 *Proxy_name*は**sysname**で、既定値は NULL です。 *Id*または*proxy_name*を指定できます。  
  
`[ @subsystem_id = ] subsystem_id`情報を一覧表示するサブシステムの識別番号を指定します。 *Subsystem_id*は**int**,、既定値は NULL です。 *Subsystem_id*または*subsystem_name*のいずれかを指定できます。  
  
`[ @subsystem_name = ] 'subsystem_name'`情報を一覧表示するサブシステムの名前。 *Subsystem_name*は**sysname**で、既定値は NULL です。 *Subsystem_id*または*subsystem_name*のいずれかを指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|サブシステムの識別番号。|  
|**subsystem_name**|**sysname**|サブシステムの名前。|  
|**proxy_id**|**int**|プロキシの識別番号。|  
|**proxy_name**|**sysname**|プロキシの名前。|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>Remarks  
 パラメーターが指定されていない場合、 **sp_enum_proxy_for_subsystem**は、すべてのサブシステムについて、インスタンス内のすべてのプロキシに関する情報を一覧表示します。  
  
 プロキシ id またはプロキシ名を指定すると、 **sp_enum_proxy_for_subsystem**はプロキシがアクセスできるサブシステムの一覧を表示します。 サブシステム id またはサブシステムの名前を指定すると、 **sp_enum_proxy_for_subsystem**そのサブシステムへのアクセス権を持つプロキシが一覧表示されます。  
  
 プロキシ情報とサブシステム情報の両方を指定すると、指定したプロキシが指定したサブシステムにアクセスできる場合は、結果セットから行が返されます。  
  
 このストアドプロシージャは**msdb**にあります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では**sysadmin**固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-all-associations"></a>A. すべての関連付けを一覧表示する  
 次の例では、現在のインスタンスに対し、プロキシとサブシステムの間に確立されているすべての権限を一覧表示します。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>B. プロキシが特定のサブシステムにアクセスできるかどうかを判断する  
 次の例では、プロキシ`Catalog application proxy`が`ActiveScripting`サブシステムにアクセスできる場合に行を返します。 それ以外の場合、この例では空の結果セットが返されます。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_grant_proxy_to_subsystem &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
