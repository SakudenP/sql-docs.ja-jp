---
title: sp_denylogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_denylogin_TSQL
- sp_denylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_denylogin
ms.assetid: db80f152-e8af-4303-95b6-3a3a7b664374
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4a902cc7ad691da5159dc3308aa69045fdc2f169
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85692690"
---
# <a name="sp_denylogin-transact-sql"></a>sp_denylogin (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Windows ユーザーまたは Windows グループが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続できないようにします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]代わりに[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_denylogin [ @loginame = ] 'login'   
```  
  
## <a name="arguments"></a>引数  
`[ @loginame = ] 'login_ '`Windows ユーザーまたはグループの名前を指定します。 *login*は**sysname**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 指定した Windows ユーザーまたは Windows グループにマップされているサーバーレベルのプリンシパルに対する CONNECT SQL 権限を拒否**sp_denylogin**ます。 サーバープリンシパルが存在しない場合は、作成されます。 新しいプリンシパルは、 [server_principals &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)カタログビューに表示されます。  
  
 **sp_denylogin**は、ユーザー定義のトランザクション内では実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、 **sp_denylogin**を使用して、Windows ユーザーがサーバーに接続できないようにする方法を示し `CORPORATE\GeorgeV` ます。  
  
```  
EXEC sp_denylogin 'CORPORATE\GeorgeV';  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-sql&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
