---
title: テーブルの別名の作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
author: stevestein
ms.author: sstein
ms.openlocfilehash: a2b43873acb67cb4ca9aae80ab267f3d01522114
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040792"
---
# <a name="create-table-aliases-visual-database-tools"></a>テーブルの別名の作成 (Visual Database Tools)
  別名を使用すると、テーブル名を使った操作が容易になります。 別名は、次の場合に使用すると便利です。  
  
-   [SQL ペイン](visual-database-tools.md) のステートメントを短くして、読みやすくする場合。  
  
-   クエリでテーブル名を列名の修飾などに頻繁に参照する場合で、クエリの文字数を一定文字数にする場合。 一部のデータベースでは、クエリの最大文字数が決まっています。  
  
-   自己結合などで同一テーブルの複数のインスタンスを使用し、いずれかのインスタンスを参照する方法が必要な場合。  
  
 たとえば、テーブル名 `"e"` _ `employee`に対して別名`information`を作成すると、クエリの残りの部分でテーブルを `"e"` として参照できます。  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>テーブルまたはテーブル値オブジェクトの別名を作成するには  
  
1.  クエリにテーブルまたはテーブル値オブジェクトを追加します。  
  
2.  **ダイアグラム ペイン**で、別名を作成するオブジェクトを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。  
  
3.  **[プロパティ]** ウィンドウの **[エイリアス]** フィールドに別名を入力します。  
  
## <a name="see-also"></a>参照  
 [Visual Database Tools &#40;クエリにテーブルを追加する&#41;](add-tables-to-queries-visual-database-tools.md)   
 [クエリ結果の並べ替えとグループ化 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Visual Database Tools &#40;クエリ結果の概要&#41;](summarize-query-results-visual-database-tools.md)   
 [クエリに関する基本操作の実行 (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
