---
title: sp_certify_removable (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_certify_removable_TSQL
- sp_certify_removable
dev_langs:
- TSQL
helpviewer_keywords:
- sp_certify_removable
ms.assetid: ca12767f-0ae5-4652-b523-c23473f100a1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b873931c5d09f3c54f61e872f8ea6646408c1a04
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715962"
---
# <a name="sp_certify_removable-transact-sql"></a>sp_certify_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  リムーバブル メディア上でデータベースが配布用に正しく構成されているかどうか確認し、問題があればユーザーにレポートします。  
  
> **重要!!** [!代わりに[ssNoteDepFutureAvoid](../../t-sql/statements/create-database-sql-server-transact-sql.md)を含めてください。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'dbname'`確認するデータベースを指定します。 *dbname*は**sysname**です。  
  
`[ @autofix = ] 'auto'`データベースとすべてのデータベースオブジェクトの所有権をシステム管理者に付与し、ユーザーが作成したデータベースユーザーと既定以外の権限を削除します。 *auto*は**nvarchar (4)**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 データベースが正しく構成されている場合、 **sp_certify_removable**は次の処理を実行します。  
  
-   ファイルをコピーできるように、データベースをオフラインに設定します。  
  
-   すべてのテーブルに関する統計を更新し、所有権やユーザーに関する問題をレポートする。  
  
-   データ ファイル グループを読み取り専用としてマークし、ファイルを読み取り専用メディアにコピーできるようにする。  
  
 システム管理者は、データベースとすべてのデータベース オブジェクトの所有者であることが必要です。 システム管理者は、を実行しているすべてのサーバー上に存在する既知のユーザーであり、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースが後で配布およびインストールされるときに存在することが予想されます。  
  
 **Auto**値を指定せずに**sp_certify_removable**を実行すると、次のいずれかの条件に関する情報が返されます。  
  
-   システム管理者は、データベースの所有者ではありません。  
  
-   ユーザーが作成したユーザーが存在します。  
  
-   システム管理者は、データベース内のすべてのオブジェクトを所有しているわけではありません。  
  
-   既定値以外の権限が与えられている。  
  
 これらの条件は、次の方法で修正できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ツールと手順を使用し、 **sp_certify_removable**を再実行します。  
  
-   **Auto**値を指定して**sp_certify_removable**を実行するだけです。  
  
 このストアドプロシージャでは、ユーザーとユーザーの権限のみがチェックされることに注意してください。 データベースにはグループを追加でき、そのグループに権限を与えることができます。 詳細については、「 [GRANT &#40;transact-sql&#41;](../../t-sql/statements/grant-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、 **sysadmin**固定サーバーロールのメンバーに制限されています。  
  
## <a name="examples"></a>使用例  
 次の例では、`inventory` データベースを削除できるかどうかを確認します。  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_create_removable &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
