---
title: オプション (テキストエディター、Transact-sql-IntelliSense) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Advanced
- VS.ToolsOptionsPages.Text_Editor.SQL_Server_Tools.Advanced
dev_langs:
- TSQL
ms.assetid: 1855d916-5bf9-4d94-b0fb-9f9bb05ff950
author: rothja
ms.author: jroth
ms.openlocfilehash: b130152a8817550b32eb3c923c24feaea96bf5b0
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929753"
---
# <a name="options-text-editor-transact-sql-intellisense"></a>オプション (テキストエディター、Transact-sql-IntelliSense)
  **[オプション]** ダイアログ ボックスを使用すると、[!INCLUDE[ssDE](../includes/ssde-md.md)] クエリ エディターの IntelliSense の設定を変更できます。 この設定を変更するには、**[ツール]** メニューの **[オプション]** をクリックし、**[テキスト エディター]** フォルダー、**[Transact-SQL]** フォルダーの順に展開し、**[詳細設定]** をクリックします。  
  
## <a name="transact-sql-intellisense-settings"></a>[Transact-SQL IntelliSense の設定]  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] クエリ エディターの IntelliSense のオプションを指定します。  
  
### <a name="enable-intellisense"></a>[IntelliSense を有効にする]  
 IntelliSense 機能を有効にします。 このボックスをオフにすると、特定の IntelliSense オプションを使用できなくなります。 既定では、このチェック ボックスはオンになっています。  
  
 **[エラーに下線を引く]**  
 クエリ ウィンドウで [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの構文エラーとセマンティック エラーを識別します。 すべてのエラーと警告が赤で表示されます。 エラーと警告は、IntelliSense が実装されている [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントについてのみサポートされます。 既定では、このチェック ボックスはオンになっています。  
  
 **[ステートメントのアウトラインを表示する]**  
 ファイルが開いているときにアウトライン機能を有効にします。 これにより、[!INCLUDE[tsql](../includes/tsql-md.md)] コードの折りたたみ可能なブロックが作成されます。 既定では、このチェック ボックスはオンになっています。  
  
 **[スクリプトの最大サイズ]**  
 IntelliSense 機能が無効になるサイズを指定します。 スクリプトが指定したサイズを超えると、警告メッセージが出され、 そのエディター ウィンドウでコードの色分けを除くすべての IntelliSense 機能が無効になります。 十分な量のテキストが削除されて制限内までスクリプトのサイズが縮小されると、IntelliSense が再度有効になります。 サイズの大きいスクリプトに対して IntelliSense を有効にすると、速度の遅いコンピューターではパフォーマンスが低下することがあります。 指定できるサイズは、100 KB、500 KB、1 MB、2 MB、および無制限です。 既定値は 1 MB です。  
  
 **[組み込み関数名の文字種]**  
 入力候補一覧に含まれている組み込み [!INCLUDE[tsql](../includes/tsql-md.md)] 関数の名前に大文字 (DATEADD など) と小文字 (dateadd など) のどちらを使用するかを指定します。 使用中の [!INCLUDE[tsql](../includes/tsql-md.md)] コーディング規則に最適なオプションを選択してください。  
  
## <a name="see-also"></a>参照  
 [IntelliSense のトラブルシューティング &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/troubleshooting-intellisense.md)  
  
  
