---
title: 依存関係ネットワークダイアグラムのチュートリアル (データマイニングアドイン) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, dependency network
- shapes, data mining
- shapes, network
- dependencies
- diagram, dependency network
- data mining layout toolbar
- dependency network
ms.assetid: aac732a8-5262-4649-b7d7-3ccf6f9cfa8b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8138cef980e7b040a99a6e1db21f1b67fd84aeb5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528778"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>依存関係ネットワーク ダイアグラムのチュートリアル (データ マイニング アドイン)
  データ マイニング モデルのいくつかの種類では、データのリレーションシップを調査する方法としてネットワーク グラフを使用します。 これらのモデルを Visio に**依存関係ネットワーク**図形を使用してインポートした後、レイアウトのカスタマイズと拡張を続けることができます。 **Visio のデータマイニング図形**には、依存関係ネットワーク図を操作するための次のカスタムコントロールが含まれています。  
  
-   ネットワーク グラフの描画コントロール  
  
     これは、Visio ワークスペースに図形をドロップすると起動されるウィザードの一部です。  
  
-   **データマイニングレイアウト**ツールバー  
  
     これは、依存関係ネットワーク グラフの操作に役立つように Visio ワークスペースに追加されます。  
  
## <a name="build-a-dependency-network-graph"></a>依存関係ネットワーク グラフの作成  
 Visio のページに図形をドロップして、 **Visio 依存関係ネットワーク図形ウィザード**を起動し、ダイアグラムのオプションを設定します。  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>Visio 依存関係ネットワーク図形ウィザードの使用  
  
1.  [**図形**] ボックスの一覧に [ **Microsoft データマイニング図形**] が表示されない場合は、[**その他の図形**] をクリックし、[**ステンシルを開く**] を選択して、既定のインストール場所からテンプレートを開きます。  
  
     \<drive>: \Microsoft files (x85) SQL Server 2012 DM アドイン  
  
2.  ページに [**依存関係ネットワーク**] 図形をドラッグして、ウィザードを開始します。 **[次へ]** をクリックします。  
  
3.  **Visio 依存関係ネットワーク図形ウィザード**の [ようこそ] ページで、[**次へ**] をクリックします。  
  
4.  **Visio 依存関係ネットワーク図形ウィザード**の [**データソースの選択**] ページで、視覚化する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] モデルがあるサーバーへの接続を選択します。  
  
5.  適切なマイニングモデルを選択し、[**次へ**] をクリックします。  
  
     適切なモデルを選択するには、[**プロパティ**] ペインでデータの名前、説明、列、および種類を確認します。  
  
     この図形は以下の方法で作成されたモデルをサポートしています。  
  
    -   Naïve Bayes  
  
    -   デシジョン ツリー  
  
    -   アソシエーションルール  
  
6.  ページで、**表示するノードを選択**し、グラフのサイズをカスタマイズします。必要に応じて、特定のノードのみが含まれるようにフィルター処理します。  
  
     大規模なデータセットの場合、依存関係グラフは大きくなる可能性があり、*ノード*として表される多くの関連オブジェクトが含まれています。 このダイアログ ボックスを使うと、興味のあるノードだけを含むカスタム ネットワーク グラフを作成できます。  
  
     [アートプレースホルダー]  
  
     **[フェッチするノード数]**  
     モデルに含まれているノードの数が指定したノードの数より少ない場合、この設定は機能しません。 モデルに含まれているノードの数が指定したノードの数より多い場合は、関連性の強いノードだけが表示されます。  
  
     **[名前に含まれる文字列]**  
     このボックスを空白のままにして緑色の矢印をクリックすると、モデル内のすべてのノードが取得されます。  
  
     文字列を入力して、緑色の矢印をクリックすると、指定した文字列を含むノードだけが返されます。  
  
     サンプル データから作成できるモデルの大半は大きくありません。そのため、この例の場合、ノード数を 10 に増やして緑色の矢印をクリックすると、クエリが実行されて、すべてのノードの一覧が取得されます。  
  
7.  [**詳細**設定] をクリックして、グラフの網掛けおよび形状のオプションを設定します。  
  
8.  [**閉じる**] をクリックして [**詳細**オプション] ダイアログボックスを閉じ、[**完了**] をクリックしてグラフを作成します。  
  
## <a name="explore-and-modify-the-finished-diagram"></a>完成したダイアグラムの調査と変更  
 ネットワークの依存グラフが作成された後も、Visio の機能を使用して引き続きグラフを変更し強化することができます。  
  
 次の図は、依存関係ネットワーク グラフの既定のレイアウトを示しています。  
  
 [アートプレースホルダー]  
  
1.  Visio**ビュー**リボンの [**タスクペイン**] 領域にある [**パンとズーム**] コントロールを使用して、グラフのセクションにフォーカスを移動し、ダイアグラム内を移動します。  
  
2.  Visio の [**ページの再レイアウト**] オプションで提供されるさまざまなグラフレイアウトを試してみてください。  
  
3.  [**アドイン**] リボンをクリックし、データマイニングダイアグラムを操作するために使用するカスタムツールバーの1つを表示します。  
  
     **レイアウト**  
     ページ上のノードのレイアウトを最適化し、すべてのノードが表示されるように表示を変更します。  
  
     **[ページのサイズ変更]**  
     すべてのノードが表示されるように、ページのサイズを変更します。  
  
     **[枠の太さ]**  
     グラフ全体の枠の太さの表示を切り替えます。 枠とは、ノード間の接続です。 スライダー コントロールを使用すると、強度が低い接続をフィルターで除外できます。  
  
     **Slider**  
     **スライダー**を使用すると、依存関係ネットワークダイアグラムに表示されるリレーションシップの強度を制御できます。  
  
     グラフ内の各ノードは状態を表します。 矢印は、2 つの状態間の遷移とその遷移に関連付けられた確率を表します。 グラフに表示されるノードの数を減らすには、スライダー バーを上方向に動かします。  
  
     グラフに表示されるノードの数を増やすには、スライダー バーを下方向に動かします。  
  
     **項目の追加**  
     [**表示するノードの選択**] ダイアログボックスを開きます。これにより、グラフに追加する新しいノードを選択できます。  
  
4.  モデルに接続した状態のまま、好みに応じてグラフを単純または詳細にし、注釈を追加することができます。  
  
     [図のプレースホルダー]  
  
> [!WARNING]  
>  アドインの以前のバージョンで使用できた依存ノードの強調表示などのショートカット メニュー オプションは、Office 2013 では機能しません。  
  
## <a name="see-also"></a>参照  
 [データマイニングアドインの &#40;SQL Server Visio データマイニングダイアグラムのトラブルシューティング&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
