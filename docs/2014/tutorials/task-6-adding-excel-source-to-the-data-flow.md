---
title: 'タスク 6: Excel ソースをデータフローに追加する |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0bbb134106fde9607bd51bc84bcd49969aec19ef
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064726"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>タスク 6: Excel ソースをデータ フローに追加する
  ここでは、Excel ソースをデータ フローに追加してソース Excel ファイルから仕入先データを読み取ります。 Excel ソースは、Microsoft Excel ブック内のワークシートまたは範囲からデータを抽出します。 詳細については、「 [Excel ソース](../integration-services/data-flow/excel-source.md)」を参照してください。

1.  [ **SSIS ツールボックス**] の [**その他のソース**] から [ **Excel ソース**] を [**データフロー** ] タブにドラッグアンドドロップします。

2.  [**データフロー** ] タブで [ **Excel ソース**] を右クリックし、[**名前の変更**] をクリックします。

3.  「 **Excel ファイルから Supplier データを読み取る**」と入力し、 **enter**キーを押します。

4.  [Excel**ファイルから Supplier データを読み取る**] をダブルクリックして、[ **excel ソースエディター** ] ダイアログボックスを開きます。

5.  [ **Excel ソースエディター** ] ダイアログボックスで、[**新規**] をクリックして excel 接続を作成します。

6.  [ **Excel 接続マネージャー** ] ダイアログボックスで、 **[参照**] をクリックし、 **EIM チュートリアル**フォルダー内の**Suppliers.xls**ファイルを選択します。 [ **Excel バージョン**] ボックスで [ **Microsoft excel 97-2003** ] が選択されていることを確認し、[ **OK**] をクリックします。

     ![[Excel 接続マネージャー] ダイアログ ボックス](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "[Excel 接続マネージャー] ダイアログ ボックス")

7.  [ **Excel ソースエディター** ] ダイアログボックスで、[ **Excel シートの名前**] ボックスの一覧の [ **IncomingSuppliers $** ] を選択します。

     ![Excel シートの名前 - 今後の仕入先$](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "Excel シートの名前 - 今後の仕入先$")

8.  Excel ファイルでデータをプレビューするには、[**プレビュー** ] をクリックします。

9. **[OK]** をクリックしてダイアログ ボックスを閉じます。

10. [ **SSIS ツールボックス**] の**他の変換**で**DQS クレンジング**変換を [**データフロー** ] タブにドラッグアンドドロップします。 [ **Excel ファイルから Supplier データを読み取る**] の下にあります。 DQS クレンジング変換では、Data Quality Services (DQS) を使用し、ナレッジ ベースの承認済みのルールを適用することで、データを修正します。 この変換は、実行時に、DQS サーバー上に DQS クレンジング プロジェクトを作成します。 詳細については、「 [DQS クレンジング変換](https://msdn.microsoft.com/library/ee677619.aspx)」を参照してください。

## <a name="next-step"></a>次の手順

[タスク 7: DQS クレンジング変換をデータ フローに追加する](task-7-adding-dqs-cleansing-transform-to-the-data-flow.md)

### <a name="see-also"></a>参照

[データ フロー](../integration-services/data-flow/data-flow.md)
