---
title: DELETE (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 600f3bc6d5ad4b9f7f67e15b894185123dccca8b
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669766"
---
# <a name="delete-dmx"></a>削除 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用するデータマイニング拡張機能 (DMX) 句に応じて、マイニングモデル、マイニング構造、またはマイニング構造とそれに関連付けられているすべてのマイニングモデルをクリアします。  
  
## <a name="syntax"></a>構文  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>引数  
 *model*  
 モデル識別子。  
  
 *データ*  
 構造体識別子。  
  
## <a name="remarks"></a>Remarks  
 **マイニングモデル**または**マイニング構造**を指定しない場合、は [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 名前に基づいてオブジェクトの種類を検索し、正しいオブジェクトを処理します。 サーバーに同じ名前のマイニング構造とマイニングモデルが含まれている場合は、エラーが返されます。  
  
 次の表は、異なる形式の構文を使用した場合の結果について示しています。  
  
|ステートメント|結果|  
|---------------|------------|  
|マイニング構造の構造から削除* \<>*<br /><br /> or<br /><br /> マイニング構造* \< 構造>* から削除します。情報|マイニング構造に対して ProcessClear を実行します。 すべてのコンテンツは、マイニング構造とそれに関連付けられているマイニングモデルから消去されます。|  
|マイニング構造* \< 構造>* から削除します。場合|マイニング構造に対してのみ Processclearstructure を実行します。 すべてのコンテンツはマイニング構造から消去され、関連付けられているマイニングモデルはそのまま残ります。 マイニング構造を消去すると、関連するマイニングモデルのドリルスルーは失敗します。|  
|マイニングモデルモデルからの削除* \<>*<br /><br /> or<br /><br /> マイニングモデル* \< モデル>* から削除します。情報|マイニングモデルに対して ProcessClear を実行しますが、状態値はそのままにします。 状態値は、列で使用できる状態です。 たとえば、性別の列の状態値は、男性と女性です。|  
  
 処理の種類の詳細については、「 [Type 要素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、NB_Sample モデルからすべてのコンテンツを削除します。  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
