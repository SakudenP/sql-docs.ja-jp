---
title: MSSQLSERVER_3159 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3159 (Database Engine error)
ms.assetid: c93c1003-0e3a-40aa-9873-44a0f5b8b57e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4942120db61798a9f5917e6b5402ffc095ba21c7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054037"
---
# <a name="mssqlserver_3159"></a>MSSQLSERVER_3159
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|3159|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LDDB_LOGNOTBACKEDUP|  
|メッセージ テキスト|データベース "%ls" のログの末尾がバックアップされませんでした。 この部分の作業を保存しておく場合は BACKUP LOG WITH NORECOVERY を使用してログをバックアップしてください。 ログのコンテンツを上書きするだけの場合は、RESTORE ステートメントで WITH REPLACE 句または WITH STOPAT 句を使用してください。|  
  
## <a name="explanation"></a>説明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で完全復旧モデルまたは一括ログ復旧モデルを使用するほとんどの場合は、まだバックアップされていないログ レコードをキャプチャするため、ログの末尾をバックアップする必要があります。 復元操作直前のログの末尾から取ったログ バックアップをログ末尾のバックアップといいます。  
  
 データベースを障害発生時点に復旧するとき、ログ末尾のバックアップは復旧計画の対象になる最後のバックアップです。 ログの末尾をバックアップできない場合、障害の前に作成した最後のバックアップの末尾までしかデータベースを復旧できません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では通常、データベースの復元を開始する前に、ログ末尾のバックアップを取る必要があります。 ログ末尾のバックアップを取ることで、作業の損失を防ぎ、ログ チェーンを完全な状態で保持することができます。 ただし、ログ末尾のバックアップは、すべての復元シナリオで必要となるわけではありません。 復元ポイントが以前のログ バックアップに含まれている場合、またはデータベースを移動するか置き換えて (上書きして) いる場合、ログ末尾のバックアップは不要であり、最新のバックアップ以降の特定の時点に復元する必要もありません。 また、ログ ファイルが破損し、ログ末尾のバックアップを作成できない場合、ログ末尾のバックアップを使用することなくデータベースを復元する必要があります。 最新のログ バックアップの後にコミットされたトランザクションは失われます。 詳細については、後の「ログ末尾のバックアップを使用しない復元」を参照してください。  
  
> [!CAUTION]  
>  REPLACE は頻繁に使用するのではなく、十分に検討した後で必要と判断される場合にのみ使用してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 ログ末尾のバックアップを行い、復元操作を再試行します。  
  
 ログ末尾をバックアップできない場合は、RESTORE ステートメントで WITH STOPAT または WITH REPLACE を使用します。  
  
## <a name="see-also"></a>参照  
 [SQL Server データベースを特定の時点に復元する方法 &#40;完全復旧モデル&#41;](../backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [データベースが破損したときにトランザクションログをバックアップ &#40;SQL Server&#41;](../backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)   
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)   
 [ログ末尾のバックアップ &#40;SQL Server&#41;](../backup-restore/tail-log-backups-sql-server.md)  
  
  
