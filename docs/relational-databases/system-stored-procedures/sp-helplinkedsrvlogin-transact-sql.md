---
title: sp_helplinkedsrvlogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplinkedsrvlogin_TSQL
- sp_helplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplinkedsrvlogin
ms.assetid: a2b1eba0-bf71-47e7-a4c7-9f55feec82a3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 70c189733cdc45c8d496f2842486dbec433c32db
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733165"
---
# <a name="sp_helplinkedsrvlogin-transact-sql"></a>sp_helplinkedsrvlogin (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  分散クエリおよびリモートストアドプロシージャに使用される特定のリンクサーバーに対して定義されたログインマッピングに関する情報を提供します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helplinkedsrvlogin [ [ @rmtsrvname = ] 'rmtsrvname' ]   
     [ , [ @locallogin = ] 'locallogin' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @rmtsrvname = ] 'rmtsrvname'`ログインマッピングが適用されるリンクサーバーの名前を指定します。 *rmtsrvname*は**sysname**,、既定値は NULL です。 NULL の場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行中のローカル コンピューターで定義されているすべてのリンク サーバーに対して定義された、すべてのログインのマッピングが返されます。  
  
`[ @locallogin = ] 'locallogin'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]リンクサーバー *rmtsrvname*へのマッピングを持つローカルサーバー上のログインを指定します。 *locallogin*は**sysname**,、既定値は NULL です。 NULL を指定すると、 *rmtsrvname*に定義されているすべてのログインマッピングが返されます。 NULL でない場合は、 *locallogin*から*rmtsrvname*へのマッピングが既に存在している必要があります。 *locallogin*には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインまたは Windows ユーザーを指定できます。 Windows ユーザーに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、直接またはアクセス権が付与されている windows グループのメンバーシップを使用して、へのアクセスが許可されている必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**リンク サーバー**|**sysname**|リンク サーバー名。|  
|**ローカルログイン**|**sysname**|マッピングが適用されるローカルログイン。|  
|**Is Self Mapping**|**smallint**|0 =**ローカルログイン**は、**リンクサーバー**に接続するときに**リモートログイン**にマップされます。<br /><br /> 1 =**ローカルログイン**は、**リンクサーバー**に接続するときに同じログインとパスワードにマップされます。|  
|**Remote Login**|**sysname**|**Isselfmapping**が0の場合、 **locallogin**にマップされている**LinkedServer**のログイン名。 **Isselfmapping**が1の場合、 **REMOTELOGIN**は NULL になります。|  
  
## <a name="remarks"></a>Remarks  
 ログインマッピングを削除する前に、 **sp_helplinkedsrvlogin**を使用して、関連するリンクサーバーを特定します。  
  
## <a name="permissions"></a>アクセス許可  
 アクセス許可はチェックされません。  
  
## <a name="examples"></a>例  
  
### <a name="a-displaying-all-login-mappings-for-all-linked-servers"></a>A. すべてのリンクサーバーのすべてのログインマッピングを表示する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行中のローカル コンピューターで定義されているすべてのリンク サーバーの、すべてのログインのマッピングを表示します。  
  
```  
EXEC sp_helplinkedsrvlogin;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Accounts         NULL          1               NULL  
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
Marketing        NULL          1               NULL  
  
(4 row(s) affected)  
```  
  
### <a name="b-displaying-all-login-mappings-for-a-linked-server"></a>B: リンクサーバーのすべてのログインマッピングを表示する  
 次の例では、リンクサーバーに対してローカルに定義されているすべてのログインマッピングを表示し `Sales` ます。  
  
```  
EXEC sp_helplinkedsrvlogin 'Sales';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
### <a name="c-displaying-all-login-mappings-for-a-local-login"></a>C: ローカルログインのすべてのログインマッピングを表示する  
 次の例では、ログインに対してローカルに定義されているすべてのログインマッピングを表示し `Mary` ます。  
  
```  
EXEC sp_helplinkedsrvlogin NULL, 'Mary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
