---
title: sp_cycle_agent_errorlog (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b51893b5676222a713b81409e3778904e4fc9580
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733301"
---
# <a name="sp_cycle_agent_errorlog-transact-sql"></a>sp_cycle_agent_errorlog (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  サーバーを再起動するときと同様に、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログ ファイルを閉じ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログの拡張番号を使い回します。 新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログには、新しいログが作成されたことを示す行が含まれます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cycle_agent_errorlog  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントが起動されるたびに、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントエラーログの名前が SQLAgent に変更され**ます。 1**;**Sqlagent**は sqlagent になります。 **2**、 **sqlagent. 2**が**sqlagent. 3**になります。 **sp_cycle_agent_errorlog**を使用すると、サーバーを停止して起動しなくてもエラーログファイルを循環することができます。  
  
 このストアドプロシージャは、 **msdb**データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_cycle_agent_errorlog**の実行権限は、 **sysadmin**固定サーバーロールのメンバーに制限されています。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログを使い回します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_cycle_errorlog &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
