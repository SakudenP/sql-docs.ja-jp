---
title: 予測クエリの入力データの選択およびマップ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tables [Analysis Services], prediction queries
- Mining Model Prediction [Analysis Services], input tables
ms.assetid: 00d330a0-879d-4da0-9f29-53c288116f4d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 20a10c066fc77e8d760bde456be54b366def8f59
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524889"
---
# <a name="choose-and-map-input-data-for-a-prediction-query"></a>予測クエリの入力データの選択およびマップ
  マイニング モデルから予測を作成する場合は、一般に新しいデータをモデルに供給することでこの操作を行います (例外はタイム シリーズ モデルで、履歴データのみに基づいて予測を行うことができます)。モデルに新しいデータを提供するには、データがデータ ソース ビューの一部として使用可能であることを確認する必要があります。 予測に使用するデータがあらかじめわかっている場合は、モデルの作成に使用するデータ ソース ビューにそのデータを含めることができます。 それ以外の場合は、新しいデータ ソース ビューを作成する必要があります。 詳細については、 [「多次元モデルのデータ ソース ビュー」](../multidimensional-models/data-source-views-in-multidimensional-models.md)を参照してください。  
  
 必要なデータが一対多の結合で複数の表に含まれている場合があります。 これはデータがアソシエーション モデルまたはシーケンス クラスター モデルに使用されるケースであり、製品またはトランザクションの詳細を含む入れ子になったテーブルにリンクしているケース テーブルを使用します。 モデルでケースが入れ子になったテーブル構造を使用する場合は、予測に使用するデータにもケースが入れ子になったテーブル構造が必要です。  
  
> [!WARNING]  
>  新しい列を追加したり、別のデータ ソース ビュー内にある列をマップしたりすることはできません。 選択したデータ ソース ビューには、予測クエリに必要なすべての列が含まれている必要があります。  
  
 予測に使用するデータが格納されているテーブルを識別した後で、外部データの列をマイニング モデルの列にマップする必要があります。 たとえば、モデルで人口統計とアンケートの回答に基づいて顧客の購入行動を予測する場合、入力データには、モデル内に何があるかに通常対応する情報が含まれている必要があります。 すべての単一列に対応データが必要なわけではありませんが、対応する列が多い方が適しています。 異なるデータ型の列をマップしようとすると、エラーが発生することがあります。 その場合は、データ ソース ビューで名前付きの計算を定義して、新しい列データをモデルに必要なデータ型にキャストまたは変換できます。 詳細については、「[データソースビューでの名前付き計算の定義 &#40;Analysis Services&#41;](../multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)」を参照してください。  
  
 予測に使用するデータを選択すると、選択したデータ ソース内の一部の列は、名前の類似性および一致するデータ型に基づいてマイニング モデルの列に自動的にマップされることがあります。 **[マイニング モデル予測]** の **[マッピングの変更]** ダイアログ ボックスを使用して、マップされる列の変更、不適切なマッピングの削除、または既存の列の新規マッピングの作成を行うことができます。 **[マイニング モデル予測]** デザイン画面では、接続のドラッグ アンド ドロップ編集もサポートされます。  
  
-   新しい接続を作成するには、 **[マイニング モデル]** テーブルで単に列を選択し、 **[入力テーブルの選択]** テーブルの対応する列にドラッグします。  
  
-   接続を削除するには、接続線を選択して Del キーを押します。  
  
 次の手順では、 **[入れ子になった結合の指定]** ダイアログ ボックスを使用して、予測クエリへの入力として使用するためにケース テーブルと入れ子になったテーブルの間に作成された結合を変更する方法を説明します。  
  
### <a name="select-an-input-table"></a>入力テーブルの選択  
  
1.  **のデータ マイニング デザイナーの** [マイニング精度チャート] **タブにある** [入力テーブルの選択] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]テーブルで、 **[ケース テーブルの選択]** をクリックします。  
  
     **[テーブルの選択]** ダイアログ ボックスが表示され、クエリの基になるデータが含まれているテーブルを選択できます。  
  
2.  **[テーブルの選択]** ダイアログ ボックスで、データ ソースを **[データ ソース]** 一覧から選択します。  
  
3.  **[テーブル名またはビュー名]** で、モデルのテストに使用するデータが含まれているテーブルを選択します。  
  
4.  **[OK]** をクリックします。  
  
     マイニング構造の列が、入力テーブル内の同じ名前を持つ列に自動的にマップされます。  
  
### <a name="change-the-way-that-input-data-is-mapped-to-the-model"></a>入力データがモデルにマップされる方法の変更  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のデータ マイニング デザイナーで、 **[マイニング モデル予測]** タブを選択します。  
  
2.  **[マイニング モデル]** メニューで **[接続の変更]** を選択します。  
  
     **[マッピングの変更]** ダイアログ ボックスが開きます。 このダイアログ ボックスの **[マイニング モデル列]** に、選択したマイニング構造の列が一覧表示されます。 **[テーブル列]** に、 **[入力テーブルの選択]** ダイアログ ボックスで選択した外部データ ソースの列が一覧表示されます。 外部データ ソースの列はマイニング モデル内の列にマップされます。  
  
3.  **[テーブル列]** で、マップ先のマイニング モデル列に対応する行を選択します。  
  
4.  外部データ ソースで使用可能な列の一覧から新しい列を選択します。 列マッピングを削除するには、一覧内の空白の項目を選択します。  
  
5.  **[OK]** をクリックします。  
  
     新しい列マッピングがデザイナーに表示されます。  
  
### <a name="remove-a-relationship-between-input-tables"></a>入力テーブル間のリレーションシップの削除  
  
1.  **のデータ マイニング デザイナーの** [マイニング モデル予測] **タブにある** [入力テーブルの選択] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]テーブルで、 **[結合の変更]** をクリックします。  
  
     **[入れ子になった結合の指定]** ダイアログ ボックスが開きます。  
  
2.  リレーションシップを選択します。  
  
3.  **[リレーションシップの削除]** をクリックします。  
  
4.  **[OK]** をクリックします。  
  
     ケース テーブルと入れ子になったテーブルの間のリレーションシップが削除されます。  
  
### <a name="create-a-new-relationship-between-input-tables"></a>入力テーブル間の新しいリレーションシップの作成  
  
1.  データ マイニング デザイナーの **[マイニング モデル予測]** タブにある **[入力テーブルの選択]** テーブルで、 **[結合の変更]** をクリックします。  
  
     **[入れ子になった結合の指定]** ダイアログ ボックスが開きます。  
  
2.  **[リレーションシップの追加]** をクリックします。  
  
     **[リレーションシップの作成]** ダイアログ ボックスが開きます。  
  
3.  入れ子になったテーブルのキーを **[基になる列]** で選択します。  
  
4.  ケース テーブルのキーを **[対象になる列]** で選択します。  
  
5.  **[リレーションシップの作成]** ダイアログ ボックスで **[OK]** をクリックします。  
  
6.  **[入れ子になった結合の指定]** ダイアログ ボックスで **[OK]** をクリックします。  
  
     ケース テーブルと入れ子になったテーブルの間に新しいリレーションシップが作成されます。  
  
### <a name="add-a-nested-table-to-the-input-tables-of-a-prediction-query"></a>入れ子になったテーブルの予測クエリの入力テーブルへの追加  
  
1.  データ マイニング デザイナーの **[マイニング モデル予測]** タブで、 **[ケース テーブルの選択]** をクリックして **[テーブルの選択]** ダイアログ ボックスを開きます。  
  
    > [!NOTE]  
    >  入れ子になったテーブルはケース テーブルを指定しないと入力に追加できません。 入れ子になったテーブルを使用するには、予測に使用するマイニング モデルでも入れ子になったテーブルを使用する必要があります。  
  
2.  **[テーブルの選択]** ダイアログ ボックスで、 **[データ ソース]** ボックスの一覧からデータ ソースを選択し、データ ソース ビュー内でケース データが含まれているテーブルを選択します。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  **[入れ子になったテーブルの選択]** をクリックして **[テーブルの選択]** ダイアログ ボックスを開きます。  
  
4.  **[テーブルの選択]** ダイアログ ボックスで、 **[データ ソース]** ボックスの一覧からデータ ソースを選択し、データ ソース ビュー内で入れ子になったデータが含まれているテーブルを選択します。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     リレーションシップが既に存在する場合は、マイニング モデルの列が、入力テーブル内の同じ名前の列に自動的にマップされます。 入れ子になったテーブルとケース テーブル間のリレーションシップは、 **[結合の変更]** をクリックし、 **[リレーションシップの作成]** ダイアログ ボックスを開いて変更できます。  
  
## <a name="see-also"></a>参照  
 [予測クエリ &#40;データ マイニング&#41;](prediction-queries-data-mining.md)  
  
  
