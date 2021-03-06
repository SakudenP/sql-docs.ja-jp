---
title: BottomSum (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1fdb72a4067a9b48e648cffe1d12b29b23f1652a
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669843"
---
# <a name="bottomsum-dmx"></a>BottomSum (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  累積合計が指定された値以上になるテーブルの最下位行を、ランクの増加順 (昇順) に返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>適用対象  
 テーブル列参照> などのテーブルを返す式、 \< またはテーブルを返す関数。  
  
## <a name="return-type"></a>戻り値の型  
 \<テーブル式の>  
  
## <a name="remarks"></a>Remarks  
 **BottomSum**関数は、順位の昇順で一番下の行を返します。 ランクは、各行の順位式> 引数の評価値に基づいています。これは、 \< \<> 値の順位付け式の合計が、sum> 引数で指定されている指定された合計以上であることを示し \< ます。 **BottomSum**は、指定された合計値を維持しながら、可能な限り最小の要素数を返します。  
  
## <a name="examples"></a>例  
 次の例では、「[基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」を使用して作成したアソシエーションモデルに対して予測クエリを作成します。  
  
 BottomSum の動作を理解するために、入れ子になったテーブルのみを返す予測クエリを最初に実行すると便利な場合があります。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  この例では、入力として指定された値に単一引用符が含まれているため、その前に別の単一引用符を付けてエスケープする必要があります。 エスケープ文字を挿入するための構文がわからない場合は、予測クエリビルダーを使用してクエリを作成できます。 ドロップダウンリストから値を選択すると、必要なエスケープ文字が挿入されます。 詳細については、「[データマイニングデザイナーでの単一クエリの作成](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer)」を参照してください。  
  
 結果の例:  
  
|モデル|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|道路ボトルケージ|1195|0.080314537|0.077173962|  
  
 BottomSum 関数は、このクエリの結果を受け取り、指定されたカウントに合計される最小値を持つ行を返します。  
  
```  
SELECT   
BottomSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .1)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 BottomSum 関数の最初の引数は、テーブル列の名前です。 この例では、Predict 関数を呼び出し、INCLUDE_STATISTICS 引数を使用して、入れ子になったテーブルが返されます。  
  
 BottomSum 関数の2番目の引数は、結果の並べ替えに使用する入れ子になったテーブルの列です。 この例では、INCLUDE_STATISTICS オプションを使用して、列 $SUPPORT、$PROBABILTY、および $ADJUSTED 確率を返します。 この例では、$PROBABILITY を使用して、少なくとも50% の確率に合計する行を返します。  
  
 3番目の引数、BottomSum 関数は、ターゲットの合計を double として指定します。 合計が 10% の確率となる、カウントが最小の製品の行を取得するには「1」と入力します。  
  
 結果の例:  
  
|モデル|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|道路ボトルケージ|1195|0.08...|0.07...|  
|Mountain Bottle Cage|1367|0.09...|0.08...|  
  
 **メモ**この例は、BottomSum の使用方法を示すことだけを目的としています。 データセットのサイズによっては、このクエリの実行に時間がかかることがあります。  
  
## <a name="see-also"></a>参照  
 [DMX&#41;&#40;関数](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数](../dmx/general-prediction-functions-dmx.md)   
 [DMX&#41;&#40;の割合](../dmx/bottompercent-dmx.md)  
  
  
