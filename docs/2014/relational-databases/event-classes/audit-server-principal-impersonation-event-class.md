---
title: Audit Server Principal Impersonation イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Server Principal Impersonation event class
ms.assetid: 6fee1a15-325a-4f09-a95d-deecf8af1b9f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 19d7e332605f2b2f0f746d5d149451dd2646627d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85030941"
---
# <a name="audit-server-principal-impersonation-event-class"></a>Audit Server Principal Impersonation イベント クラス
  **Audit Server Principal impersonation**イベントクラスは、EXECUTE as など、サーバースコープ内で権限の借用が存在する場合に発生し \<*login*> ます。  
  
## <a name="audit-server-principal-impersonation-event-class-data-columns"></a>Audit Server Principal Impersonation イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**DatabaseName**|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|**DBUserName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー名。|40|はい|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**EventSubClass**|**int**|イベント サブクラスの種類。|21|はい|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログイン、または DOMAIN\username の形式で表された [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|**LoginSid**|**画像**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、 **sys.server_principals** カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|Windows のユーザー名。|6|はい|  
|**ObjectName**|**nvarchar**|参照されているオブジェクトの名前。|34|はい|  
|**ObjectType**|**int**|イベントに関係するオブジェクトの種類を表す値。 この値は **sys.objects** カタログ ビューの type 列に対応します。 値については、「 [ObjectType トレース イベント列](objecttype-trace-event-column.md)」を参照してください。|28|はい|  
|**アクセス許可**|**bigint**|チェックする権限の種類を表す整数値。<br /><br /> 1 = SELECT ALL<br /><br /> 2 = UPDATE ALL<br /><br /> 4 = REFERENCES ALL<br /><br /> 8 = INSERT<br /><br /> 16 = DELETE<br /><br /> 32 = EXECUTE (プロシージャのみ)|19|はい|  
|**RequestID**|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**Success**|**int**|1 = 成功。 0 = 失敗。 たとえば、値が 1 の場合は権限チェックの成功を表し、値が 0 の場合は失敗を表します。|23|はい|  
|**TextData**|**ntext**|トレースでキャプチャされたイベント クラスに依存するテキスト値。|1|はい|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|**XactSequence**|**bigint**|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
