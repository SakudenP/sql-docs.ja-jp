---
title: '[トレーステンプレートのプロパティ] ([イベントの選択] タブ) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracetemplateproperties.eventsselection.f1
helpviewer_keywords:
- Trace Template Properties dialog box
ms.assetid: 5b202457-ab42-4902-8012-7f3f40aa09f5
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: f70460e68d1161fa8aa718a5e5264a8e6f0782df
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928168"
---
# <a name="trace-template-properties-events-selection-tab"></a>[トレース テンプレートのプロパティ] ([イベントの選択] タブ)
  **[トレース テンプレートのプロパティ]** ダイアログ ボックスの **[イベントの選択]** タブを使用すると、 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] トレース テンプレートに含めるイベント クラスとデータ列の表示、編集、指定ができます。  
  
## <a name="options"></a>オプション  
 **[イベント]** 列  
 イベント列のチェック ボックスをオンまたはオフにして、トレースするイベントを指定します。 イベントは、イベント カテゴリ別に分類されます。  
  
 **[全般]** タブの **[既存のテンプレートを基に新しいテンプレートを作成する]** を選択した場合、指定したテンプレートに応じてイベントが自動的に選択されます。 イベント クラスの詳細については、「 [SQL Server イベント クラスの参照](../relational-databases/event-classes/sql-server-event-class-reference.md)」を参照してください。  
  
 データ列  
 トレースするデータ列を指定するには、必要なイベント列とデータ列に対応するチェック ボックスをオンにします。 トレースに含まれる各イベントに対応するチェック ボックスがオンになっている場合、そのイベントのイベント列は既定ですべてオンになります。 **[全般]** タブの **[既存のテンプレートを基に新しいテンプレートを作成する]** をオンにした場合、指定したテンプレートに応じてデータ列とフィルターが自動的に選択されます。  
  
 フィルターを指定するには、データ列のヘッダーをクリックし、フィルター基準を入力します。 フィルター選択されるデータ列については、 **[フィルターの編集]** ダイアログ ボックスの列ラベルの左側にフィルターのアイコンが表示されます。  
  
 **[すべてのイベントを表示する]**  
 表示できるイベントをすべて表示します。 既存のテンプレートを基にしていない新しいテンプレートを作成する場合、このオプションは既定でオンになります。 オフにすると、 **[イベントの選択]** グリッドで選択されていないイベントがすべて非表示になります。  
  
 **[すべての列を表示]**  
 表示できるデータ列をすべて表示します。 既存のテンプレートを基にしていない新しいテンプレートを作成する場合、このオプションは既定でオンになります。 オフにすると、 **[イベントの選択]** グリッドで選択されていないデータ列がすべて非表示になります。  
  
 **列フィルター**  
 **[フィルターの編集]** ダイアログ ボックスを開きます。ここでは、データ列のラベルの左側にフィルターのアイコンが表示されます。 **[フィルターの編集]** ダイアログ ボックスを使用して、データ列のフィルターを編集します。  
  
 **[列の構成]**  
 トレースとグループ化の結果で、1 つ以上の列を使用して列の順序を変更します。  
  
## <a name="see-also"></a>参照  
 [トレースファイルのイベントとデータ列を指定する &#40;SQL Server プロファイラー&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [トレース &#40;SQL Server プロファイラーに表示される列の構成&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [トレース &#40;SQL Server プロファイラーのイベントをフィルター処理し&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [フィルター情報の表示 &#40;SQL Server プロファイラー&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [フィルター &#40;SQL Server プロファイラーの変更&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server プロファイラーのテンプレートと権限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
