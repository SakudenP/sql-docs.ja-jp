---
title: 'SQL Server: General Statistics オブジェクト | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:General Statistics
- General Statistics object
ms.assetid: c738e549-d7e7-4211-9ec3-064ac140af7c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9eb59f03b1526153bec88039a0d619bac8ad6368
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066981"
---
# <a name="sql-server-general-statistics-object"></a>SQL Server: General Statistics オブジェクト
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **SQLServer:General Statistics** オブジェクトには、現在の接続数や、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを実行しているコンピューターとの間で接続または切断を行っている 1 秒あたりのユーザー数など、一般的なサーバー全体の利用状況を監視するためのカウンターがあります。 これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスとの間で接続と切断を行うクライアントの数が多い、大規模オンライン トランザクション処理 (OLTP) で作業している場合に便利です。  
  
 次の表では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **General Statistics** カウンターについて説明します。  
  
|SQL Server General Statistics カウンター|説明|  
|--------------------------------------------|-----------------|  
|**Active Temp Tables**|使用中の一時テーブル/テーブル変数の数。|  
|**Connection resets/sec**|接続プールから開始されたログインの総数。|  
|**Event Notifications Delayed Drop**|システム スレッドによって削除されるのを待機しているイベント通知の数。|  
|**HTTP Authenticated Requests**|秒単位で開始された認証済み HTTP 要求の数。|  
|**Logical Connections**|システムへの論理接続の数。<br /><br /> 論理接続の主な目的は、複数のアクティブな結果セット (MARS) の要求を処理することです。 MARS 要求の場合、アプリケーションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続するたびに、1 つの物理接続に複数の論理接続が対応します。<br /><br /> MARS を使用しない場合、物理接続と論理接続の比率は 1:1 です。 したがって、アプリケーションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続するたびに、論理接続は 1 つずつ増えます。|  
|**Logins/sec**|開始されるログインの秒単位の総数。 これには、プールされた接続は含まれません。|  
|**Logouts/sec**|開始されるログアウトの秒単位の総数。|  
|**Mars Deadlocks**|検出された Mars Deadlock の数。|  
|**Non-atomic yield rate**|1 秒間に非アトミックなトランザクションが発生した回数。|  
|**Processes blocked**|現在ブロックされているプロセスの数。|  
|**SOAP Empty Requests**|秒単位で開始された空の SOAP 要求の数。|  
|**SOAP Method Invocations**|1 秒間に開始された SOAP メソッドの呼び出し数。|  
|**SOAP Session Initiate Requests**|1 秒間に開始された SOAP セッション開始要求の数。|  
|**SOAP Session Terminate Requests**|1 秒間に開始された SOAP セッション終了要求の数。|  
|**SOAP SQL Requests**|1 秒間に開始された SOAP SQL 要求の数。|  
|**SOAP WSDL Requests**|1 秒間に開始された SOAP Web サービス記述言語の要求の数。|  
|**Temp Tables Creation Rate**|1 秒間に作成された一時テーブル/テーブル変数の数。|  
|**Temp Tables For Destruction**|クリーンアップ システム スレッドによって破棄されるのを待機している一時テーブル/テーブル変数の数。|  
|**Trace Event Notifications Queue**|Service Broker によって送信されるのを内部キューで待機しているトレース イベント通知インスタンスの数。|  
|**トランザクション**|参加中のトランザクションの数 (ローカル、DTC、およびバインド済みのすべてのトランザクション)。|  
|**ユーザー接続**|SQL Server に現在接続しているユーザー数。|  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
