---
title: マークされたトランザクションへのデータベースの復元 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6cc4515806fc43aa06cb53b340c38081479ada3e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84957156"
---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>マークされたトランザクションへのデータベースの復元 (SQL Server Management Studio)
  データベースが復元中の状態である場合、 **[トランザクション ログの復元]** ダイアログ ボックスを使用して、使用可能なログ バックアップのマークされたトランザクションにデータベースを復元できます。  
  
> [!NOTE]  
>  詳細については、「[マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル#41;](use-marked-transactions-to-recover-related-databases-consistently.md)」および「[マークされたトランザクションを含む関連データベースの復旧](recovery-of-related-databases-that-contain-marked-transaction.md)」を参照してください。  
  
### <a name="to-restore-a-marked-transaction"></a>マークされたトランザクションを復元するには  
  
1.  オブジェクト エクスプローラーで適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。さらに、そのデータベースに応じて、ユーザー データベースを選択するか、または **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[復元]** をクリックします。  
  
4.  **[トランザクション ログ]** をクリックして **[トランザクション ログの復元]** ダイアログ ボックスを開きます。  
  
5.  **[全般]** ページの **[復元先]** で、 **[マークされたトランザクション]** をクリックします。 **[マークされたトランザクションの選択]** ダイアログ ボックスが開きます。 このダイアログ ボックスには、選択したトランザクション ログ バックアップで使用できるマークされたトランザクションを一覧表示するグリッドが表示されます。  
  
     既定では、マークされたトランザクションの前まで復元され、マークされたトランザクションは復元されません。 マークされたトランザクションも復元するには、 **[マークされたトランザクションを含める]** チェック ボックスをオンにします。  
  
     次の表は、グリッドの列ヘッダーとその値を示しています。  
  
    |ヘッダー|値|  
    |------------|-----------|  
    |\<blank>|マークを選択するためのチェック ボックスを表示します。|  
    |**トランザクション マーク**|トランザクションがコミットされたときにユーザーによって指定された、マークされたトランザクションの名前。|  
    |**Date**|トランザクションがコミットされた日時。 トランザクションの日付と時刻は、クライアント コンピューターの日付と時刻ではなく、 **msdbgmarkhistory** テーブルに記録されたとおりに表示されます。|  
    |**説明**|トランザクションがコミットされたときにユーザーが指定したマークされたトランザクションの説明 (該当する場合)。|  
    |**LSN (LSN)**|マークされたトランザクションのログ シーケンス番号。|  
    |**[データベース]**|マークされたトランザクションがコミットされたデータベースの名前。|  
    |**ユーザー名**|マークされたトランザクションをコミットしたデータベース ユーザーの名前。|  
  
## <a name="see-also"></a>参照  
 [データベースバックアップを復元する &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
  
