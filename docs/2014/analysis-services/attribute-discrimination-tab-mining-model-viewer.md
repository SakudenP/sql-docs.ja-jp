---
title: '[属性の識別] タブ (マイニングモデルビューアー) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.discrimination.f1
ms.assetid: 68323f23-121e-44fc-be85-6f9915d6d3c7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 69a03f1580b525707ccadbd018d9d270b0cc7740
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527913"
---
# <a name="attribute-discrimination-tab-mining-model-viewer"></a>[属性の識別] タブ (マイニング モデル ビューアー)
  入力属性の状態を比較して、それが結果属性とどのように関連しているかを確認するには、 **[属性の識別]** タブを使用します。 2 つの選択された予測可能属性の間で最も違いの大きい属性値が、一覧の先頭に表示されます。  
  
 **詳細:** [Microsoft Naive Bayes アルゴリズム](data-mining/microsoft-naive-bayes-algorithm.md)、 [Microsoft Naive Bayes ビューアーを使用したモデルの参照](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>オプション  
 **[ビューアーのコンテンツを最新状態に更新]**  
 ビューアーにマイニング モデルを再読み込みします。  
  
 **[マイニング モデル]**  
 現在のマイニング構造に含まれているマイニング モデルから選択します。 マイニング モデルは、自動的に適切なカスタム ビューアーに表示されます。  
  
 **Viewer**  
 選択したマイニング モデルを調べるために使用するビューアーを選択します。 モデルごとに、カスタム ビューアーまたは [!INCLUDE[msCoName](../includes/msconame-md.md)] マイニング コンテンツ ビューアーのいずれかを選択できます。 利用可能な場合プラグイン ビューアーを使用することもできます。  
  
 **属性**  
 予測可能な属性を選択します。  
  
 **値1**  
 **[値 2]** に指定された状態と比較する予測可能な属性の状態を選択します。  
  
 **値2**  
 **[値 1]** に指定された状態と比較する予測可能な属性の状態を選択します。 [**その他のすべての状態**] を選択して、**値 1**の値とその補数 (値1以外のすべての値) を比較することもできます。  
  
 **との識別スコア \<Value 1>\<Value 2>**  
 グラフには、対象となる属性が入力属性の特定の状態とどのように関係するかを記述する次の列が含まれます。  
  
|値|説明|  
|-----------|-----------------|  
|**属性**|マイニング モデルの入力属性です。|  
|**値**|**[属性]** に表示される属性の状態です。|  
|**ライター\<Value 1>**|バーは、現在の属性と値が、**[値 1]** で選択した対象となる結果を優先するかどうかを示します。|  
|**ライター\<Value 2>**|バーは、現在の属性と値が、**[値 2]** で選択した対象となる結果を優先するかどうかを示します。|  
  
## <a name="see-also"></a>参照  
 [データマイニングアルゴリズム &#40;Analysis Services-データマイニング&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [データマイニングモデルデザイナー &#40;のマイニングモデルビューアー&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [データ マイニング モデル ビューアー](data-mining/data-mining-model-viewers.md)  
  
  
