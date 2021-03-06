---
title: 拡張イベント セッションの変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: rothja
ms.author: jroth
ms.openlocfilehash: 14be41e48262bc7ebc8aeeaf55185f5e35d0c72e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050930"
---
# <a name="alter-an-extended-events-session"></a>拡張イベント セッションの変更
  拡張イベント セッションを作成したら、 **SQL Server 拡張イベント ウィザード**を使用して、必要に応じて拡張イベント セッションを変更できます。  
  
## <a name="before-you-begin"></a>開始する前に  
 アクティブなセッションおよび非アクティブなセッションのターゲットを変更することはできません。また、アクティブなセッションの詳細プロパティの構成を変更することはできません。  
  
 アクティブなイベント セッションと非アクティブなイベント セッションの両方に対して、次の変更を実行できます。  
  
-   セッションのイベントの追加または削除、および、イベントの構成 (イベントのフィールド、フィルター、アクションなど) の変更。  
  
-   イベント セッションのターゲットの追加または削除。  
  
-   **[サーバーの起動時にイベント セッションを開始する]** オプションの有効化。  
  
 非アクティブなイベント セッションに対しては、次の変更も実行できます。  
  
-   **[イベント間のリレーションシップの追跡]** オプションの有効化。  
  
-   詳細プロパティの構成の変更。  
  
> [!NOTE]  
>  **SQL Server 拡張イベント ウィザード** では、イベント セッションの変更はサポートされていません。  
  
## <a name="how-to-alter-an-extended-events-session-using-the-sql-server-extended-events-wizard"></a>SQL Server 拡張イベント ウィザードを使用して拡張イベント セッションを変更する方法  
  
-   オブジェクト エクスプローラーで **[管理]** を展開し、 **[拡張イベント]** を展開して、 **[セッション]** を展開します。  
  
-   変更するセッションを右クリックし、 **[プロパティ]** をクリックします。  
  
-   **[プロパティ]** ダイアログ ボックスで、必要な変更を行い、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のイベントセッションの変更](/sql/t-sql/statements/alter-event-session-transact-sql)   
 [クエリ エディターを使用した拡張イベント セッションの作成](../../database-engine/create-an-extended-events-session-using-query-editor.md)  
  
  
