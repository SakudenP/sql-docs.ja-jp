---
title: ワークロード グループの削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], delete
- Resource Governor, workload group delete
ms.assetid: d5902c46-5c28-4ac1-8b56-cb4ca2b072d0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 801a731db6c5b31bc479d1a3f6079c45ad9a7c04
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063604"
---
# <a name="delete-a-workload-group"></a>ワークロード グループの削除
  ワークロード グループまたはリソース プールを削除にするには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または Transact-SQL を使用します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **ワークロード グループの削除に使用するもの:** [オブジェクト エクスプローラー](#DelWGObjEx)、[リソース ガバナーのプロパティ](#DelWGRGProp)、[Transact-SQL](#DelWGTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
 アクティブなセッションが含まれている場合は、ワークロード グループを削除できません。  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 ワークロード グループにアクティブなセッションが含まれている場合、そのワークロード グループの削除や別のリソース プールへの移動を行う操作は、その変更を適用するための ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを呼び出した時点で失敗します。 この問題を回避するには、次のいずれかの操作を実行します。  
  
-   そのグループからすべてのセッションが切断されるまで待ってから、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを再実行します。  
  
-   そのグループ内のセッションを KILL コマンドで明示的に停止してから、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを再実行します。 **[削除]** を使用した後アクティブなセッションを停止する前に、セッションを明示的に停止するのは不適切であると判断した場合は、元の名前でグループを再作成し、このグループを元のリソース プールに移動します。  
  
-   サーバーを再起動します。 再起動プロセスの完了後、削除したグループは作成されず、移動したグループは新しいリソース プール割り当てを使用します。  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 ワークロード グループを削除するには、CONTROL SERVER 権限が必要です。  
  
##  <a name="delete-a-workload-group-using-object-explorer"></a><a name="DelWGObjEx"></a> オブジェクト エクスプ ローラーを使用してワークロード グループを削除する  
 **オブジェクト エクスプ ローラーを使用してワークロード グループを削除するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でオブジェクト エクスプローラーを開き、 **[管理]** ノードを **[リソース プール]** ノードまで再帰的に展開します。  
  
2.  削除するワークロード グループを含むリソース プールで、 **[リソース プール]** ノードを **[ワークロード グループ]** ノードまで再帰的に展開します。  
  
3.  ワークロード グループを右クリックし、 **[削除]** をクリックします。  
  
4.  **[オブジェクトの削除]** ウィンドウの **[削除されるオブジェクト]** ボックスの一覧に、ワークロード グループが表示されます。 ワークロード グループを削除するには、 **[OK]** をクリックします。  
  
##  <a name="delete-a-workload-group-using-resource-governor-properties"></a><a name="DelWGRGProp"></a> リソース ガバナーのプロパティを使用してワークロード グループを削除する  
 **[リソース ガバナーのプロパティ] ページでワークロード グループを削除にするには**  
  
1.  オブジェクト エクスプローラーで、 **[管理]** ノードを **[リソース プール]** ノードまで展開します。  
  
2.  削除するワークロード グループを含むリソース プールを右クリックし、 **[プロパティ]** をクリックします。 **[リソース ガバナーのプロパティ]** ページが開きます。  
  
3.  **[リソース プールのワークロード グループ]** ウィンドウで、削除するワークロード グループの行をクリックし、行の左側にある右矢印を右クリックして **[削除]** をクリックします。  
  
4.  ワークロード グループを削除するには、 **[OK]** をクリックします。  
  
##  <a name="delete-a-workload-group-using-transact-sql"></a><a name="DelWGTSQL"></a> Transact-SQL を使用してワークロード グループを削除する  
 **Transact-SQL を使用してワークロード グループを削除するには**  
  
1.  削除するワークロード グループの名前を示す `DROP WORKLOAD GROUP` ステートメントを実行します。  
  
2.  `ALTER RESOURCE GOVERNOR RECONFIGURE` ステートメントを実行する前に、削除するワークロード グループにアクティブな要求がないことを確認します。 アクティブな要求があると `ALTER RESOURCE GOVERNOR` は失敗します。 この問題を回避するには、次のいずれかの操作を実行します。  
  
    -   ワークロード グループからのセッションがすべて接続解除されるまで待ちます。  
  
    -   `KILL` コマンドを使用して、ワークロード グループのセッションを明示的に停止します。  
  
    -   サーバーを再起動します。 ワークロード グループは再作成されません。  
  
    -   `DROP WORKLOAD GROUP` ステートメントを実行してから、変更適用のためにセッションを明示的に停止するのは不適切であると判断した場合、DROP ステートメントの実行前と同じ名前でグループを再作成し、このグループを元のリソース プールに移動することができます。  
  
3.  ステートメントを実行 `ALTER RESOURCE GOVERNOR RECONFIGURE` します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)  
 次の例では、 `groupAdhoc`というワークロード グループを削除します。  
  
```  
DROP WORKLOAD GROUP groupAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](resource-governor.md)   
 [リソース プールの作成](create-a-resource-pool.md)   
 [ワークロード グループの作成](create-a-workload-group.md)   
 [リソース プールの削除](delete-a-resource-pool.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-workload-group-transact-sql)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
