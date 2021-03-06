---
title: デシジョンツリーモデルの参照 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- tree viewer
- mining model, decision tree
- decision tree [data mining]
- dependency network
ms.assetid: 6b3dd1ae-caff-41c3-817b-802dc020ff88
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4a4f41e548746d443ff9cbed5eca17e557127240
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527748"
---
# <a name="browsing-a-decision-trees-model"></a>デシジョン ツリー モデルの参照
  [**参照**] を使用して分類モデルを開くと、のデシジョンツリービューアーと同様に、モデルが対話型のデシジョンツリービューアーに表示され [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。 ビューアーは、あるデータ グループを別のデータ グループから区別する条件を強調するグラフとして分類結果を表示します。 ツリーの個々のサブセットにドリルダウンして、基になるデータを取得することもできます。  
  
##  <a name="explore-the-model"></a><a name="bkmk_Top"></a>モデルの調査  
 デシジョン ツリー アルゴリズムに基づくモデルは、興味深い情報を多数持っています。 [**参照**] ウィンドウには、次のタブとペインがあり、グラフを使用してパターンを学習し、結果を予測するのに役立ちます。  
  
-   [デシジョン ツリー](#BKMK_DecisionTree)  
  
-   [依存関係ネットワーク](#BKMK_DNetwork)  
  
 デシジョン ツリー モデルをテストするには、サンプル データ ブックの [トレーニング データ] (または [ソース データ]) タブにあるサンプル データを使用して、Bike Buyer を予測可能な属性としてデシジョン ツリー モデルを構築します。  
  
###  <a name="decision-tree"></a><a name="BKMK_DecisionTree"></a>デシジョンツリー  
 このビューの目的は、結果につながる要因の理解と調査に役立てることです。  
  
 デシジョン ツリー グラフは、左から右に次のように読むことができます。  
  
-   *ノード*と呼ばれる四角形は、データのサブセットを含みます。 ノードのラベルはそのサブセットの定義特性を示します。  
  
-   左端のノード (**すべて**) は、完全なデータセットを表します。 後続のすべてのノードは、データのサブセットを表します。  
  
-   デシジョンツリーには、多くの分割が含まれています。また、属性に基づいてデータが複数のセットに*分割*される場所もあります。  
  
     たとえば、サンプル モデルの最初の分割は、データセットを年齢別に 3 つのグループに分割します。  
  
-   [**すべて**のノードの直後に分割することは、このデータセットを分割するプライマリ条件を示すため、最も重要です。  
  
     その他の分割は右側に表示されます。 こうして、ツリーのさまざまなセグメントを分析することで、どの属性が購入行動に最も大きな影響を及ぼすかを知ることができます。  
  
 ![アソシエーション モデルの依存関係ネットワーク グラフ](media/dm13-dec-tree-split-definition.gif "アソシエーション モデルの依存関係ネットワーク グラフ")  
  
 この情報を使用すると、購入を勧めるだけで実際に購入する可能性が高い顧客に対して重点的にマーケティング キャンペーンを実施することができます。  
  
##### <a name="explore-the-decision-tree"></a>デシジョン ツリーの調査  
  
1.  [**すべて**] ノードをクリックし、[**マイニング凡例**] を確認します。  
  
     トレーニング データ セット内のケースの正確な数と、結果の内訳が表示されます。  
  
     ノードの上にマウス カーソルを置くと、ツールヒントにも同じ情報が表示されます。  
  
2.  各ノードの横にあるプラス記号とマイナス記号をクリックして、ツリーを展開し折りたたみます。  
  
     [**レベルの表示]** スライダーを使用して、ツリーを展開または縮小することもできます。  
  
3.  ノードには濃淡の差があります。  
  
     既定では、**母集団**はシェーディング変数として使用されます。つまり、色の輝度によって、どのノードで最もサポートされているかがわかります。  
  
     したがって、データセット全体を含む一番左端のノードの色が最も濃くなります。  
  
4.  [**背景**] の値を [**すべてのケース**] から **[はい]** に変更します。  
  
     ![購入者を強調表示するようにデシジョン ツリー グラフを変更](media/dm13-dectreeshadedbuyer.gif "購入者を強調表示するようにデシジョン ツリー グラフを変更")  
  
5.  これで、色の濃さによって各ノードの顧客が自転車を購入した人数が示されるようになります。それが興味の対象となっている購入行動です。  
  
     各ノードには色分けされたバーがあります。 これは、このデータのサブセット内で結果の分布を示すヒストグラムです。 たとえば、サンプルの自転車購入者デシジョンツリーでは、色分けされたバーに自転車 (Yes 値) を購入した顧客の割合と、(値のない) ユーザーの比率が示されます。 正確な値を取得するには、ノードをクリックして [**マイニング凡例**] を表示します。  
  
6.  グラフを調べると、データの各サブセットがより小さなグループにさらに分解されていて、どの属性が結果の予測に最も役立つかどうかを確認できます。  
  
     網掛けの濃さを見るだけで、いくつかのグループに注目して、その詳細データを比較することができます。 たとえば、次のようなグループは自転車を購入する確率がかなり高くなっています。  
  
    -   Age >= 32、 \< 53 and Yearly Income > = 26000、および Children = 0  
  
         ケースの合計: 1150  
  
         自転車購入者の確率: 18%  
  
    -   Age >= 32、 \< 53 and Yearly Income > = 26000、子 not = 0 および配偶の状態 = ' Single '  
  
         ケースの合計: 402  
  
         自転車購入確率: 16%  
  
7.  [**背景**] の値を **[はい] から [** **いいえ**] に変更し、グラフがどのように変化するかを確認します。  
  
     ![アソシエーション モデルの依存関係ネットワーク グラフ](media/dm13-dec-tree-background-no.gif "アソシエーション モデルの依存関係ネットワーク グラフ")  
  
 **ヒント**  
  
-   データを複数のシリーズに分割できる場合、モデル化するデータ セットごとに異なるモデルが構築されます。  
  
-   サンプルデータモデルには、予測可能な結果が1つだけ含まれています。ただし、顧客がサービスプランを購入したかどうかや、それを予測する必要があるかどうかに関する情報があるとします。 その場合、そのデータを別の列に保持して、モデルに 2 つの予測可能な属性を含めます。  
  
     [デシジョンツリー] ペインの左上隅にある [**ヒストグラム**] オプションをクリックして、ツリーのヒストグラムに表示できる状態の最大数を変更します。 これは、予測可能な属性に多数の状態が含まれている場合に便利です。 ヒストグラムには、状態がポピュラリティ順に左から右に表示されます。  
  
-   [**デシジョンツリー** ] タブのオプションを使用して、ツリーの表示方法に影響を与えることもできます。これには、ウィンドウを拡大または縮小したり、グラフのサイズを変更したりすることができます。  
  
-   モデル内のすべてのツリーに表示される既定のレベル数を設定するには、 **[既定の展開]** を使用します。  
  
-   [**長い名前を表示**する] を選択すると、データソースを含む属性の完全な名前が表示されます。 各ケースの属性と異なるデータ ソースからケースが取得されている場合を除いて、短い名前と長い名前は同じになります。  
  
 [トップに戻る](#bkmk_Top)  
  
###  <a name="dependency-network"></a><a name="BKMK_DNetwork"></a>依存関係ネットワーク  
 [**依存関係ネットワーク**] ビューには、モデル内の入力属性と予測可能属性の間の接続が表示されます。  
  
1.  ビューアーの左側にあるスライダーをクリックしてドラッグします。  
  
     一番上の位置では、すべての接続が表示されます。 スライダーをドラッグして下げると、最も強いリンクだけが表示されます。  
  
2.  ここで [Bike Buyer] (自転車購入者) ノードをクリックします。  
  
     ![デシジョン ツリーの依存関係ネットワーク ビュー](media/dm13-dectree-depnet.gif "デシジョン ツリーの依存関係ネットワーク ビュー")  
  
     ノードを選択すると、そのノードに固有の依存関係が強調表示されます。 この場合、ビューアーでは、結果の予測に役立つ各ノードが強調表示されます。  
  
3.  ビューアーに多数のノードが含まれている場合は、[ノードの**検索**] ボタンを使用して特定のノードを検索できます。 **[ノードの検索]** をクリックすると、 **[ノードの検索]** ダイアログ ボックスが開き、フィルターを使用して特定のノードを検索して選択できます。  
  
4.  ビューアーの下部にある凡例は、グラフ内の依存関係の種類に色を関連付けています。 たとえば、予測可能なノードを選択すると、予測可能なノードが水色で網掛けされ、選択したノードを予測するノードがオレンジ色で網掛けされます。  
  
 [トップに戻る](#bkmk_Top)  
  
### <a name="drill-through-to-underlying-data"></a>基になるデータへのドリルスルー  
 いくつかの種類のモデルでは、モデルから基になるケースデータにドリルスルーする機能がサポートされ*て*います。 これは、特定のセグメントの顧客にコンタクトする場合や、データを取り出してさらに分析を実行する場合に、非常に便利な機能です。  
  
##### <a name="get-case-data"></a>ケース データの取得  
  
1.  目的のデータを含むノードを右クリックし、以下のいずれかのオプションを選択します。  
  
    -   **モデルのドリル**スルー。 このオプションは、選択したノードに属するケースを取得して、Excel のテーブルに保存します。 モデルの構築に実際に使用されたデータ列のみが取り出されます。  
  
    -   **構造列をドリル**スルーします。 このオプションは、選択したノードに属するケースを取得して、Excel のテーブルに保存します。 モデルで使用されていない列でも、基になるデータで使用できるすべての情報を取得できます。 たとえば、分析には役立たないため顧客の住所と郵便番号をモデルから除外して、構造には残していた場合です。  
  
     Excel に戻ってデータを表示します。 参照ビューアーを使って、クエリを実行し、新しいワークシートのテーブルにデータを保存し、結果にラベルを付けます。  
  
     ![ドリルスルーの結果を Excel に保存](media/dm13-dectree-drillthroughresults.gif "ドリルスルーの結果を Excel に保存")  
  
## <a name="see-also"></a>参照  
 [Excel &#40;SQL Server データマイニングアドインのモデルの参照&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
