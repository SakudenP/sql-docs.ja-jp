---
title: ODBC 入力先を使用したデータ読み込み | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 339ec0a8-922e-48c0-97b3-fc5ee34f95e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c6f96f65d6c223ebf08e30d854aff58dcd1047f6
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437719"
---
# <a name="load-data-by-using-the-odbc-destination"></a>ODBC 入力先を使用したデータ読み込み
  次の手順では、ODBC 入力先を使用してデータを読み込む方法を示します。 ODBC 入力先を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 1 つの入力元があらかじめ含まれている必要があります。  
  
### <a name="to-load-data-using-an-odbc-destination"></a>ODBC 入力先を使用してデータを読み込むには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、使用する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、ODBC 入力先をデザイン画面にドラッグします。  
  
3.  利用可能なデータ フロー コンポーネントの出力を ODBC 入力先の入力にドラッグします。  
  
4.  ODBC 入力先をダブルクリックします。  
  
5.  **[ODBC 入力先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで、既存の ODBC 接続マネージャーを選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。  
  
6.  データのアクセス方法を選択します。  
  
    -   **[テーブル名 - バッチ]** バッチモードで動作する ODBC 入力先を構成するには、このオプションを選択します。 このオプションを選択すると、 **[バッチ サイズ]** を設定できます。  
  
    -   **[テーブル名 - 行ごと]** : 一度に 1 行ずつ、入力先に各行を挿入する ODBC 入力先を構成するには、このオプションを選択します。 このオプションを選択すると、データは一度に 1 行ずつ、テーブルに読み込まれます。  
  
7.  **[テーブル名またはビュー名]** フィールドで、使用できるテーブルまたはビューを一覧のデータベースから選択するか、正規表現を入力してテーブルを指定します。この一覧には、最初の 1,000 テーブルのみが表示されます。 データベースに 1,000 を超えるテーブルがある場合、テーブル名の最初の文字を入力するか、名前の一部の入力にワイルドカード (*) を使用すると、目的のテーブルが表示されます。  
  
8.  **[プレビュー]** をクリックすると、ODBC 入力先で選択されるテーブルのデータを最大 200 行表示することができます。  
  
9. **[マッピング]** をクリックし、 **[使用できる入力列]** 一覧にある列を、 **[使用できる変換先列]** 一覧の列にドラッグして、列をマップします。  
  
10. エラー出力を構成するには、 **[エラー出力]** をクリックします。  
  
11. **[OK]** をクリックします。  
  
12. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [ODBC 変換先エディター &#40;[接続マネージャー] ページ&#41;](../odbc-destination-editor-connection-manager-page.md)   
 [[ODBC 変換先エディター] &#40;[マッピング] ページ&#41;](../odbc-destination-editor-mappings-page.md)   
 [[ODBC ソース エディター] &#40;[エラー出力] ページ&#41;](../odbc-source-editor-error-output-page.md)  
  
  
