---
title: SQL Server 以外のサブスクライバーの追加 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e36d048b11fcc71b27ab0ab2ee815b0284187c4d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068829"
---
# <a name="add-non-sql-server-subscriber"></a>[SQL Server 以外のサブスクライバーの追加]
  レプリケーションでは、Oracle サブスクライバーと IBM DB2 のサブスクライバーのスナップショット パブリケーションおよびトランザクション パブリケーションに対するプッシュ サブスクリプションの作成をサポートします。  
  
## <a name="options"></a>オプション  
 **[追加するサブスクライバーの種類]**  
 Oracle サブスクライバーまたは IBM DB2 サブスクライバーを選択します。 これらのサブスクライバーのサポートの詳細については、「[SQL Server 以外のサブスクライバー](non-sql/non-sql-server-subscribers.md)」を参照してください。  
  
 **[データ ソース名]**  
 ネットワーク上のデータベースを探すために使用される名前です。 レプリケーションでは、このウィザードの **[ディストリビューション エージェント セキュリティ]** ページに指定されたログイン、パスワード、および任意の接続オプションをデータ ソース名と組み合わせて、データベースの接続文字列を生成します。  
  
> [!NOTE]  
>  データ ソース名と接続文字列は、ディストリビューション エージェントがサブスクリプションの初期化を試みるまでは [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって検証されません。  
  
## <a name="see-also"></a>参照  
 [SQL Server 以外のサブスクライバーのサブスクリプションの作成](create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [パブリケーションのサブスクライブ](subscribe-to-publications.md)  
  
  
