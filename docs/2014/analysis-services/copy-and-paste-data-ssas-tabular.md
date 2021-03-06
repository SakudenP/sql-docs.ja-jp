---
title: データのコピーと貼り付け (SSAS テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.pastepreviewdb.f1
ms.assetid: 2f8d8b3d-810b-4c31-98f2-341015e13da8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 30d7e6aafe613e5ca43307aa75540d8fb1cea3ec
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526838"
---
# <a name="copy-and-paste-data-ssas-tabular"></a>データのコピーと貼り付け (SSAS テーブル)
  テーブルのデータを外部アプリケーションからコピーし、モデル デザイナーの新規または既存のテーブルに貼り付けることができます。 Excel や Word からコピーされたデータなど、クリップボードから貼り付けるデータは HTML 形式である必要があります。 モデル デザイナーは自動的にデータ型を検出し、貼り付けられたデータにその型を適用します。 手動でデータ型を変更することも、列の書式を表示することもできます。  
  
 データ ソースが接続されたテーブルとは異なり、貼り付けたテーブルには、接続名またはソース データ プロパティがあります。 貼り付けられたデータは、Model.bim ファイルに保存されます。 プロジェクトまたは Model.bim ファイルを保存すると、貼り付けられたデータも保存されます。  
  
 モデルを配置すると、配置によってモデルが処理されるかどうかに関係なく、貼り付けられたデータも一緒に配置されます。  
  
 このトピックのセクション:  
  
-   [前提条件](#bkmk_prerequisites)  
  
-   [データの貼り付け](#bkmk_paste_data)  
  
-   [[貼り付けプレビュー] ダイアログ ボックス](#bkmk_paste_preview)  
  
##  <a name="prerequisites"></a><a name="bkmk_prerequisites"></a> 前提条件  
 データを貼り付けるときには、次のような制限事項があります。  
  
-   貼り付けたテーブルは 10, 000 より多い行を持つことはできません。  
  
-   貼り付けたテーブルをパーティション分割することはできません。  
  
-   貼り付けられたテーブルは、DirectQuery モードではサポートされていません。  
  
-   **[貼り付け追加]** と **[貼り付け置換]** は、クリップボードからのデータの貼り付けによって作成されたテーブルで作業する場合にのみ使用できます。 **[貼り付け追加]** または **[貼り付け置換]** を使用して、別の種類のデータ ソースからインポートされたデータのテーブルにデータを追加することはできません。  
  
-   **[貼り付け追加]** または **[貼り付け置換]** を使用する場合、新しいデータには元のデータと同じ数の列が必要です。 さらに、貼り付けまたは追加するデータの列は、貼り付け先または追加先のテーブルの列のデータ型と同じか互換性のあるデータ型である必要があります。 異なるデータ型を使用できる場合もありますが、 **型の不一致** エラーが表示されることもあります。  
  
##  <a name="paste-data"></a><a name="bkmk_paste_data"></a>データの貼り付け  
  
#### <a name="to-paste-data-into-the-designer"></a>デザイナーにデータを貼り付けるには  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]の **[編集]** メニューをクリックし、次のいずれかをクリックします。  
  
    -   クリップボードの内容を新しいテーブルに貼り付けるには、 **[貼り付け]** をクリックします。  
  
    -   クリップボードの内容を選択したテーブルに追加の行として貼り付けるには、 **[貼り付け追加]** をクリックします。 新しい行がテーブルの末尾に追加されます。  
  
    -   選択したテーブルをクリップボードの内容に置き換えるには、 **[貼り付け置換]** をクリックします。 既存のすべての列ヘッダー名はテーブルに残り、リレーションシップは保持されます。  
  
##  <a name="paste-preview-dialog-box"></a><a name="bkmk_paste_preview"></a>[貼り付けプレビュー] ダイアログボックス  
 **[貼り付けプレビュー]** ダイアログ ボックスを使用すると、デザイナー ウィンドウにコピーされたデータのプレビューを表示して、データが正しくコピーされたことを確認することができます。 このダイアログ ボックスにアクセスするには、テーブル ベースのデータを HTML 形式でクリップボードにコピーし、デザイナーで **[編集]** メニューをクリックして、 **[貼り付け]**、 **[貼り付け追加]**、または **[貼り付け置換]** をクリックします。 **[貼り付け追加]** オプションと **[貼り付け置換]** オプションは、クリップボードからコピーして貼り付けることで作成されたテーブル内のデータを追加または置換する場合にのみ使用できます。 **[貼り付け追加]** または **[貼り付け置換]** を使用して、インポートされたデータのテーブルにデータを追加することはできません。  
  
 このダイアログ ボックスのオプションは、まったく新しいテーブルにデータを貼り付けるか、既存のテーブルにデータを貼り付けて既存のデータを新しいデータで置き換えるか、既存のテーブルにデータを追加するかによって異なります。  
  
### <a name="paste-to-new-table"></a>[新規テーブル]  
 **テーブル名**  
 デザイナーで作成するテーブルの名前を指定します。  
  
 **[貼り付けるデータ]**  
 貼り付け先テーブルに追加されるクリップボードの内容のサンプルが表示されます。  
  
### <a name="paste-append"></a>[貼り付け追加]  
 **[テーブル内の既存のデータ]**  
 列やデータ型を確認できるように、テーブル内の既存のデータのサンプルが表示されます。  
  
 **[貼り付けるデータ]**  
 クリップボードの内容のサンプルが表示されます。 既存のデータに、このデータが追加されます。  
  
### <a name="paste-replace"></a>[貼り付け置換]  
 **[テーブル内の既存のデータ]**  
 列やデータ型を確認できるように、テーブル内の既存のデータのサンプルが表示されます。  
  
 **[貼り付けるデータ]**  
 クリップボードの内容のサンプルが表示されます。 貼り付け先のテーブル内の既存のデータは削除され、テーブルに新しい行が挿入されます。  
  
## <a name="see-also"></a>参照  
 [SSAS 表形式&#41;&#40;データをインポートする](import-data-ssas-tabular.md)   
 [SSAS 表形式&#41;&#40;サポートされるデータソース](tabular-models/data-sources-supported-ssas-tabular.md)   
 [列のデータ型の設定 &#40;SSAS テーブル&#41;](tabular-models/set-the-data-type-of-a-column-ssas-tabular.md)  
  
  
