---
title: SQL Server:Locks オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Locks object
- SQLServer:Locks
ms.assetid: ace04f0d-3993-4444-8317-ca39d7087e49
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3a9d3a934e7b08e863c4ca5241c6bfc20600a539
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047882"
---
# <a name="sql-server-locks-object"></a>SQL Server:Locks オブジェクト
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **SQLServer:Locks** オブジェクトでは、各リソースの種類の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロックに関する情報を提供します。 ロックは、複数のトランザクションで同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースが同時に使用されるのを防ぐために、トランザクション中に読み取られたり変更されたりする行などにかけられます。 たとえば、あるトランザクションによってテーブルの行に排他 (X) ロックがかけられると、他のトランザクションはロックが解除されるまでその行を変更できません。 ロックを最小限にとどめるとコンカレンシーが向上し、パフォーマンスが向上します。 異なる種類のリソースのロックを表す複数の **Locks** オブジェクトのインスタンスを同時に監視することができます。  
  
 次の表では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** カウンターについて説明します。  
  
|SQL Server:Locks カウンター|説明|  
|-------------------------------|-----------------|  
|**Average Wait Time (ms)**|待つ必要がある各ロック要求の平均待ち時間 (ミリ秒)。|  
|**Lock Requests/sec**|ロック マネージャーから 1 秒あたりに要求された新しいロックと、ロック変換の数。|  
|**Lock Timeouts (timeout > 0)/sec**|NOWAIT ロックの要求を除く、1 秒あたりにタイムアウトしたロック要求の数。|  
|**Lock Timeouts/sec**|NOWAIT ロックの要求を含めた、1 秒あたりにタイムアウトしたロック要求の数。|  
|**Lock Wait Time (ms)**|最後の 1 秒間のロックの総待機時間 (ミリ秒)。|  
|**ロック待機数/秒**|呼び出し元が待つ必要のあった 1 秒あたりのロック要求の数。|  
|**デッドロック数/秒**|デッドロックが発生した 1 秒あたりのロック要求の数。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、以下のリソースをロックできます。  
  
|Item|説明|  
|----------|-----------------|  
|**_Total**|すべてのロックに関する情報。|  
|**AllocUnit**|アロケーション ユニットのロック。|  
|**アプリケーション**。|アプリケーションで指定されているリソースのロック。|  
|**[データベース]**|データベース内のすべてのオブジェクトを含むデータベースのロック。|  
|**エクステント**|連続した 8 ページのグループのロック。|  
|**[最近使ったファイル]**|データベース ファイルのロック。|  
|**Heap/BTree**|ヒープまたは BTree (HOBT)。 データ ページのヒープまたはインデックスの BTree 構造のロック。|  
|**キー**|インデックスの行のロック。|  
|**Metadata**|カタログ情報 (メタデータ) のロック。|  
|**オブジェクト**|すべてのデータとインデックスを含む、テーブル、ストアド プロシージャ、ビューなどのロック。 このオブジェクトには、 **sys.all_objects**内のエントリを持つ任意のアイテムが含まれます。|  
|**ページ**|データベース内の 8 KB のページのロック。|  
|**RID**|行 ID。 ヒープ内の単一行のロック。|  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
