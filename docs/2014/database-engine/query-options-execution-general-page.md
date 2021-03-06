---
title: '[クエリオプション] の [実行] ([全般] ページ)Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.general.f1
ms.assetid: 858a0263-2f04-4692-b8bf-63e93c998ead
author: rothja
ms.author: jroth
ms.openlocfilehash: a7d317e3fd4b225236064d02157aff37f3529f83
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929613"
---
# <a name="query-options-execution-general-page"></a>[クエリ オプション] の [実行] ([全般] ページ)
  このページを使用して、クエリを実行するためのオプションを指定し [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ます。 このダイアログ ボックスにアクセスするには、クエリ エディター ウィンドウ内で右クリックし、 **[クエリ オプション]** をクリックします。  
  
## <a name="ui-element-list"></a>UI 要素の一覧  
 **SET ROWCOUNT**  
 既定値の 0 は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] がすべての結果を受け取るまで待機することを意味します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が指定された行数を取得した後にクエリを停止するように設定するには、0 より大きい値を指定します。 このオプションをオフにして、すべての行が返されるようにするには、SET ROWCOUNT 0 を指定してください。  
  
 **SET TEXTSIZE**  
 既定値の 2,147,483,647 バイトは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が `text`、`ntext`、`nvarchar(max)`、および `varchar(max)` の各データ フィールドの上限まで、完全なデータ フィールドを提供することを示します。 XML データ型は影響を受けません。 大きな値の場合に結果を制限するには、これより小さなサイズを指定します。 指定されたサイズよりも大きい列は切り捨てられます。  
  
 **[実行タイムアウト]**  
 クエリを取り消すまで待機する秒数を示します。 値 0 は、待ち時間が無限 (タイムアウトなし) であることを示します。  
  
 **[バッチ区切り記号]**  
 Transact-SQL ステートメントをバッチに分けるために使用する単語を入力します。 既定値は GO です。  
  
 **[既定で、新しいクエリを SQLCMD モードで開始する]**  
 新しいクエリを SQLCMD モードで開始するには、このチェック ボックスをオンにします。 このチェック ボックスは、 **[ツール]** メニューからダイアログ ボックスを開いたときだけ表示されます。  
  
 このオプションを選択する場合は、次の制限事項に注意してください。  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)] クエリ エディターの IntelliSense が無効になります。  
  
-   クエリ エディターはコマンド ラインから実行できないため、変数などのコマンド ライン パラメーターを渡すことができません。  
  
-   クエリ エディターはオペレーティング システムのプロンプトに応答できないため、対話型のステートメントを実行しないように注意する必要があります。  
  
 **既定値にリセット**  
 このページ上のすべての値を元の既定値にリセットします。  
  
  
