---
title: MSSQL_REPL027056 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 52ba56c3b972be091995300e7b43f81ad407742e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060687"
---
# <a name="mssql_repl027056"></a>MSSQL_REPL027056
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|27056|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|マージ プロセスが、'%1' で生成履歴を変更できませんでした。 トラブルシューティングを行うには、詳細な履歴ログとの同期を再開して、書き込み先の出力ファイルを指定してください。|  
  
## <a name="explanation"></a>説明  
 通常このエラーは、極端に大きくなったマージ レプリケーション システム テーブルにおける競合の結果として発生します。 一般的にシステム テーブルは、パブリケーションの保有期間が長いと大きくなります。これは、保有期間が終了するまでメタデータを格納しておく必要があるためです。  
  
## <a name="user-action"></a>ユーザーの操作  
 **問題を解決するには、以下の操作を実行します。**  
  
1.  マージ エージェントの**DownloadGenerationsPerBatch** パラメーターと **UploadGenerationsPerBatch** パラメーターの値を小さくし、エラーの原因となっている根本的な問題に対処する間、処理を継続できるようにします。 エージェント パラメーターは、エージェント プロファイルおよびコマンド ラインで指定できます。 詳細については、次を参照してください。  
  
    -   [レプリケーション エージェント プロファイルの操作](agents/replication-agent-profiles.md)  
  
    -   [レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する &#40;SQL Server Management Studio&#41;](agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](concepts/replication-agent-executables-concepts.md)に割り当てるメモリの最大容量と最小容量を設定する。  
  
2.  パブリケーションの保有期間をできるだけ短く設定します。 詳細については、「 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)」を参照してください。  
  
3.  マージ レプリケーションのメンテナンスの一環として、マージ レプリケーションに関連付けられたシステム テーブル **MSmerge_contents**、 **MSmerge_genhistory**、 **MSmerge_tombstone**、 **MSmerge_current_partition_mappings**、および **MSmerge_past_partition_mappings**の増大を必要に応じて確認します。 定期的にこれらのテーブルのインデックスを再設定します。 詳細については、「 [インデックスの再編成と再構築](../indexes/indexes.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
