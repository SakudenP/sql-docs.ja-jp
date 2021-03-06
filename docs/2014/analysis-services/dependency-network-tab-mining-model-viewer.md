---
title: '[依存関係ネットワーク] タブ (マイニングモデルビューアー) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.dependencynetwork.f1
ms.assetid: e58ce1b7-20d6-42cb-ade5-916da8471e09
author: minewiskan
ms.author: owend
ms.openlocfilehash: dde94a8d08bba3ea529c9edf3fde12ee0260a3f0
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528738"
---
# <a name="dependency-network-tab-mining-model-viewer"></a>[依存関係ネットワーク] タブ (マイニング モデル ビューアー)
  **[依存関係ネットワーク]** タブでは、マイニング モデルに含まれるすべての属性のグラフィカル ビューが表示され、属性がどのように関連しているかが示されます。  
  
 **[依存関係ネットワーク]**  タブは、Naïve Bayes モデル、デシジョン ツリー モデル、アソシエーション モデルなどのさまざまな種類のマイニング モデルで使用されます。 これらのモデルのコンテキストにおける **[依存関係ネットワーク]**  タブの内容の解釈方法については、次のリンクを参照してください。  
  
 [Microsoft ツリー ビューアーを使用したモデルの参照](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
 [Microsoft Naive Bayes ビューアーを使用したモデルの参照](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
 [Microsoft アソシエーション ルール ビューアーを使用したモデルの参照](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>オプション  
 **[ビューアーのコンテンツを最新状態に更新]**  
 ビューアーにマイニング モデルを再読み込みします。  
  
 **[マイニング モデル]**  
 現在のマイニング構造に含まれているマイニング モデルから、表示するものを選択します。 マイニング モデルがカスタム ビューに表示されます。 各モデルで使用されるカスタム ビューアーの種類は、モデルの作成時に使用したアルゴリズムによって決まります。  
  
 **Viewer**  
 選択したマイニング モデルを調べるために使用するビューアーを選択します。 モデルごとに、各マイニング モデル用に用意されているカスタム ビューアー、または [!INCLUDE[msCoName](../includes/msconame-md.md)] マイニング コンテンツ ビューアーを使用できます。 利用可能な場合プラグイン ビューアーを使用することもできます。 Microsoft コンテンツ ツリー ビューアーはすべてのモデルで使用でき、モデルの内容を HTML テーブルで表現します。  
  
 **拡大**  
 属性の詳細を見ることができるように、図を拡大します。  
  
 **縮小**  
 多くの属性とリンクが表示されるように、図を拡大します。  
  
 **[グラフ ビューのコピー]**  
 ダイアグラムで表示されている部分をクリップボードにコピーします。  
  
 **[グラフ全体のコピー]**  
 ダイアグラム全体をクリップボードにコピーします。  
  
 **リンク**  
 属性の右側のスライダーを調整することにより、ビューアーに表示するリンク (エッジ) とノードの数を調整します。 スライダーを下方にドラッグするとしきい値が大きくなり、最も強いリンクだけが表示されます。 モデルの種類ごとに、グラフのリンクを表すために使用される値は多少異なります。  
  
-   **デシジョン ツリー** モデルでは、エッジは接続の予測強度を表します。その一部は分割スコアによって決定されます。  
  
-   **Naïve Bayes** モデルでは、2 つのノード間のリンクは双方向です。つまり、ノード A がノード B を予測でき、逆も可能です。 エッジに関連付けられているスコアは、接続の予測強度を表します。  
  
-   **アソシエーション モデル**では、ノード間のエッジは、2 つのアイテムセットを接続するルールの重要度スコアを表します。  
  
 すべてのモデルに適用される一般的なルールとして、リンクが強ければ強いほど、2 つの属性間の予測関係も強くなります。  
  
## <a name="see-also"></a>参照  
 [データマイニングアルゴリズム &#40;Analysis Services-データマイニング&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [データマイニングモデルデザイナー &#40;のマイニングモデルビューアー&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [データ マイニング モデル ビューアー](data-mining/data-mining-model-viewers.md)  
  
  
