---
title: sp_mergesubscription_cleanup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergesubscription_cleanup
- sp_mergesubscription_cleanup_TSQL
helpviewer_keywords:
- sp_mergesubscription_cleanup
ms.assetid: bfad414f-2bda-4bf5-9507-56a1e743dfc4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 73af981371ecbadf92936016316222c061a14b8b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85640066"
---
# <a name="sp_mergesubscription_cleanup-transact-sql"></a>sp_mergesubscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  指定されたマージプッシュサブスクリプションがパブリッシャーで削除された後に、 **sysmergesubscriptions**および**sysmergearticles**内のトリガーやエントリなどのメタデータを削除します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
> [!NOTE]  
>  プルサブスクリプションの場合、 [transact-sql&#41;&#40;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)実行され sp_dropmergepullsubscription と、メタデータが削除されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_mergesubscription_cleanup [ @publisher =] 'publisher'  
        , [ @publisher_db =] 'publisher_db'  
        , [ @publication =] 'publication'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *publisher*は**sysname**で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシャーデータベースの名前を指定します。 *publisher_db*は**sysname**であり、既定値はありません。  
  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *publication*は**sysname**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_mergesubscription_cleanup**は、マージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_mergesubscription_cleanup**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [プッシュサブスクリプションを削除する](../../relational-databases/replication/delete-a-push-subscription.md)   
 [sp_expired_subscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-expired-subscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
