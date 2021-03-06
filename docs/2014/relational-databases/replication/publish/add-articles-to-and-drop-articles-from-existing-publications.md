---
title: 既存のパブリケーションでのアーティクルの追加および削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- removing articles
- dropping articles
- adding articles
- administering replication, articles
- publications [SQL Server replication], adding and dropping articles
- articles [SQL Server replication], adding
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f72f15886e7105dde8d0e15dd0598a7474ed7e39
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038128"
---
# <a name="add-articles-to-and-drop-articles-from-existing-publications"></a>既存のパブリケーションでのアーティクルの追加および削除
  パブリケーションを作成したら、アーティクルを追加および削除できます。 アーティクルはいつでも追加できますが、アーティクルを削除するために必要な操作は、レプリケーションの種類と、アーティクルを削除するタイミングによって異なります。  
  
## <a name="adding-articles"></a>アーティクルの追加  
 アーティクルを追加するには、アーティクルへのパブリケーションの追加、パブリケーションの新しいスナップショットの作成、サブスクリプションの同期による新しいアーティクルのスキーマとデータの適用を行います。  
  
> [!NOTE]
>  マージパブリケーションにアーティクルを追加し、その新しいアーティクルに既存のアーティクルが依存している場合は、 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)と[sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)の** \@ processing_order**パラメーターを使用して、両方のアーティクルの処理順序を指定する必要があります。 たとえば、テーブルをパブリッシュし、テーブルが参照している関数はパブリッシュしない場合を考えます。 この関数をパブリッシュしないと、サブスクライバー側でテーブルを作成できないとします。 関数をパブリケーションに追加する場合: **sp_addmergearticle**の** \@ processing_order**パラメーターに**値 1**を指定し、 **sp_changemergearticle**の** \@ processing_order**パラメーターに値**2**を指定して、パラメーター ** \@ アーティクル**のテーブル名を指定します。 この処理順序により、サブスクライバー側で関数に依存するテーブルを作成する前に、関数の作成が求められるようになります。 各アーティクルに使用する値は、関数の値がテーブルの値より小さければ、別の値でもかまいません。  
  
1.  次のいずれかの方法を使用して、1 つ以上のアーティクルを追加します。  
  
    -   [パブリケーションでのアーティクルの追加または削除 &#40;SQL Server Management Studio&#41;](add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [アーティクルの定義](define-an-article.md)  
  
2.  パブリケーションにアーティクルを追加したら、パブリケーションの新しいスナップショット (およびパラメーター化されたフィルターを使用したマージ パブリケーションの場合は、すべてのパーティション) を作成する必要があります。 その後、ディストリビューション エージェントまたはマージ エージェントによって、新しいアーティクルのスキーマおよびデータがサブスクライバーにコピーされます (パブリケーション全体が再初期化されるわけではありません)。  
  
    -   新しいスナップショットを作成するには、「 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
    -   パラメーター化されたフィルターを使用してマージ パブリケーションに新しいスナップショットを作成するには、「[パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」 (パラメーター化されたフィルターを使用してマージ パブリケーションのスナップショットを作成する) を参照してください。  
  
3.  スナップショットを作成したら、サブスクリプションを同期し、新しいアーティクルのスキーマおよびデータをコピーします。  
  
    -   プッシュ サブスクリプションを同期するには、「[Synchronize a Push Subscription](../synchronize-a-push-subscription.md)」 (プッシュ サブスクリプションの同期) を参照してください。  
  
    -   プル サブスクリプションを同期するには、「[Synchronize a Pull Subscription](../synchronize-a-pull-subscription.md)」 (プル サブスクリプションの同期) を参照してください。  
  
## <a name="dropping-articles"></a>アーティクルのドロップ  
 アーティクルはパブリケーションからいつでも削除できます。ただし、次の動作について考慮する必要があります。  
  
-   パブリケーションからアーティクルを削除しても、パブリケーション データベースからオブジェクトが削除されたり、サブスクリプション データベースから対応するオブジェクトが削除されるわけではありません。 必要に応じて、DROP を使用して \<Object> これらのオブジェクトを削除します。 外部キー制約によってパブリッシュされた他のアーティクルに関連するアーティクルを削除する場合は、手動で、または要求時スクリプト実行を使用して、サブスクライバーでテーブルを削除することをお勧めします。適切な DROP ステートメントを含むスクリプトを指定して \<Object> ください。 詳細については、「[同期中のスクリプトの実行 (レプリケーション Transact-SQL プログラミング)](../execute-scripts-during-synchronization-replication-transact-sql-programming.md)」を参照してください。  
  
-   互換性レベル 90RTM 以上のマージ パブリケーションの場合、アーティクルはいつでも削除できますが、新しいスナップショットが必要です。 追加として:  
  
    -   アーティクルが結合フィルター リレーションシップまたは論理レコード リレーションシップの親アーティクルの場合、最初にリレーションシップの削除が必要ですが、これには再初期化が必要になります。  
  
    -   アーティクルにパブリケーションの最後のパラメーター化されたフィルターが含まれる場合、サブスクリプションを再初期化する必要があります。  
  
-   互換性レベルが 90RTM 未満のマージ パブリケーションの場合、アーティクルは特別な注意をせずに、サブスクリプションの初期同期の前に削除できます。 1 つ以上のサブスクリプションが同期された後にアーティクルが削除された場合、サブスクリプションの削除、再作成、および同期が必要です。  
  
-   スナップショット パブリケーションまたはトランザクション パブリケーションの場合、アーティクルはサブスクリプションを作成する前に、特別な事項を考慮せずに削除できます。 1 つ以上のサブスクリプションが作成された後にアーティクルが削除された場合、サブスクリプションの削除、再作成、および同期が必要です。 サブスクリプションの削除の詳細については、「[パブリケーションのサブスクライブ](../subscribe-to-publications.md)」と「[sp_dropsubscription (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql)」を参照してください。 **sp_dropsubscription** を使用すると、サブスクリプション全体ではなく、サブスクリプションの 1 つのアーティクルを削除できます。  
  
1.  パブリケーションからアーティクルを削除するには、アーティクルを削除し、パブリケーションの新しいスナップショットを作成します。 アーティクルを削除すると、現在のスナップショットは無効になります。したがって新しいスナップショットを作成する必要があります。  
  
    -   パブリケーションからアーティクルを削除するには、「[パブリケーションでのアーティクルの追加または削除 (SQL Server Management Studio)](add-articles-to-and-drop-articles-from-a-publication.md)」または「[Delete an Article](delete-an-article.md)」 (アーティクルの削除) を参照してください。  
  
2.  パブリケーションからアーティクルを削除したら、パブリケーションの新しいスナップショット (およびパラメーター化されたフィルターを使用したマージ パブリケーションの場合は、すべてのパーティション) を作成する必要があります。  
  
    -   新しいスナップショットを作成するには、「 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
    -   パラメーター化されたフィルターを使用してマージ パブリケーションに新しいスナップショットを作成するには、「[パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」 (パラメーター化されたフィルターを使用してマージ パブリケーションのスナップショットを作成する) を参照してください。  
  
 前述のように、場合によっては、アーティクルを削除するために、サブスクリプションの削除、再作成、および同期が必要になる場合があります。 詳細については、「[パブリケーションのサブスクライブ](../subscribe-to-publications.md)」と「[データの同期](../synchronize-data.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データとデータベースオブジェクトのパブリッシュ](publish-data-and-database-objects.md)   
 [サブスクリプションの再初期化](../reinitialize-subscriptions.md)   
 [パブリケーション データベースでのスキーマの変更](make-schema-changes-on-publication-databases.md)  
  
  
