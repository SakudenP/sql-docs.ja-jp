---
title: sysmail_event_log (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e80d631e4470e04d0ab5ab7edf6883350335586e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724642"
---
# <a name="sysmail_event_log-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  データベース メール システムから返される、Windows または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のメッセージごとに 1 行のデータを格納します。 (このコンテキスト内のメッセージは、電子メールメッセージではなく、エラーメッセージなどのメッセージを参照します)。データベースメール構成ウィザードの [**システムパラメーターの構成**] ダイアログボックスまたは[sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)ストアドプロシージャを使用して、**ログレベル**のパラメーターを構成し、返されるメッセージを決定します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|ログ内のアイテムの識別子。|  
|**event_type**|**varchar (11)**|ログに挿入された通知の種類。 指定できる値は、エラー、警告、情報メッセージ、成功メッセージ、および追加の内部メッセージです。|  
|**log_date**|**datetime**|ログ エントリが作成された日時。|  
|**description**|**nvarchar(max)**|記録されているメッセージのテキスト。|  
|**process_id**|**int**|データベースメール外部プログラムのプロセス id。 通常、データベース メール外部プログラムが起動するたびに変更されます。|  
|**mailitem_id**|**int**|メールキュー内のメールアイテムの識別子。 メッセージが特定の電子メール アイテムに関係していない場合は NULL になります。|  
|**account_id**|**int**|イベントに関連付けられているアカウントの**account_id** 。 メッセージが特定のアカウントに関連付けられていない場合は NULL です。|  
|**last_mod_date**|**datetime**|行が最後に変更された日付と時刻。|  
|**last_mod_user**|**sysname**|行を最後に変更したユーザー。 電子メールの場合は、メールを送信したユーザーです。 データベースメール外部プログラムによって生成されるメッセージの場合、これはプログラムのユーザーコンテキストです。|  
  
## <a name="remarks"></a>Remarks  
 データベースメールのトラブルシューティングを行う場合は、 **sysmail_event_log**ビューで、電子メールの失敗に関連するイベントを検索します。 データベースメール外部プログラムの失敗などの一部のメッセージは、特定の電子メールに関連付けられていません。 特定の電子メールに関連するエラーを検索するには、 **sysmail_faileditems**ビューで失敗した電子メールの**mailitem_id**を参照し、その**mailitem_id**に関連するメッセージを**sysmail_event_log**で検索します。 **Sp_send_dbmail**からエラーが返された場合、電子メールはデータベースメールシステムに送信されず、この表示にはエラーが表示されません。  
  
 個々のアカウントで配信試行が失敗した場合は、再試行の間、メール アイテムの配信が成功または失敗するまで、データベース メールでエラー メッセージが保持されます。 究極の成功の場合、すべての累積エラーは、 **account_id**を含む個別の警告としてログに記録されます。 これにより、電子メールが送信された場合でも警告が表示されることがあります。 最終的な配信エラーが発生した場合、すべてのアカウントで障害が発生したため、以前のすべての警告は、 **account_id**なしで1つのエラーメッセージとしてログに記録されます。  
  
## <a name="permissions"></a>アクセス許可  
 このビューにアクセスするには、 **sysadmin**固定サーバーロールまたは**databasemailuserrole**データベースロールのメンバーである必要があります。 **Sysadmin**ロールのメンバーではない**databasemailuserrole**のメンバーは、自分が送信した電子メールのイベントのみを表示できます。  
  
## <a name="see-also"></a>関連項目  
 [sysmail_faileditems &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [データベース メール外部プログラム](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
