---
title: '[オプション] ([クエリ結果]-[SQL Server]-[結果をグリッドに表示] ページ) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToGrid
ms.assetid: f88a0f5c-e800-473b-ae23-c3943de5ed63
author: rothja
ms.author: jroth
ms.openlocfilehash: 5678c146dfffc4cf907e0050b2017208a0c7f141
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930053"
---
# <a name="options-query-results-sql-server-results-to-grid-page"></a>[オプション] ([クエリ結果]-[SQL Server-グリッドへの結果] ページ)
  このページを使用すると、クエリ結果セットをグリッド形式で表示するためのオプションを指定できます。 このオプションに加えた変更は、新規の [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリにのみ適用されます。 現在のクエリのオプションを変更するには、[**クエリ**] メニューの [**クエリオプション**] をクリックするか、クエリウィンドウを右クリック [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] して [**クエリオプション**] を選択します。 **[クエリ オプション]** ダイアログ ボックスの左ペインで、**[結果]** の **[グリッド]** をクリックします。  
  
## <a name="ui-element-list"></a>UI 要素の一覧  
 **[結果セットにクエリを含める]**  
 クエリのテキストをクエリ出力の一部として返します。  
  
 **[結果のコピーまたは保存時に列のヘッダーを含める]**  
 結果をクリップボードにコピーしたりファイルに保存したりするときに列のヘッダーを含めるには、このチェック ボックスをオンにします。 保存またはコピーする結果データに列のヘッダーを含めずにデータだけを含めるには、このチェック ボックスをオフにします。  
  
 **[実行後に結果を破棄する]**  
 クエリの結果が変更履歴ウィンドウに表示されないようにします。 結果は実行後すぐに破棄されます。 このオプションを指定すると、メモリを節約できます。  
  
 **[結果を別のタブに表示する]**  
 クエリ ドキュメント ウィンドウの下部ではなく、新しいタブに結果セットを表示するには、このチェック ボックスをオンにします。  
  
 **[クエリ実行後に [結果] タブに切り替える]**  
 クエリの実行時に画面フォーカスを結果ペインに自動的に設定するには、これをクリックします。  
  
 **[取得される最大文字数]**  
 **XML 以外のデータ**:  
  
 1 ～ 65,535 の値を入力して、各セルに表示される最大文字数を指定します。  
  
> [!NOTE]  
>  大きな文字数を指定すると、結果セット内のデータが切り捨てられたように見える場合があります。 各セルに表示される最大文字数は、フォントのサイズに依存します。 大きな結果セットが返された場合、このボックスに大きな値を指定していると、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のメモリ上での実行速度が低下したり、システムのパフォーマンスに悪影響が及んだりすることがあります。  
  
 **XML データ**:  
  
 **[1 MB]**、 **[2 MB]**、または **[5 MB]** を選択します。 すべての文字を取得する場合は、 **[無制限]** を選択します。  
  
 **既定値にリセット**  
 このページ上のすべての値を元の既定値にリセットします。  
  
  
