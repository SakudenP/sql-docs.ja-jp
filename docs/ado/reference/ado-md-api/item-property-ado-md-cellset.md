---
title: Item プロパティ (ADO MD セルセット) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
author: rothja
ms.author: jroth
ms.openlocfilehash: e35cf86a91be42a2a39a38642e34e747d7d13fe7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2020
ms.locfileid: "82753914"
---
# <a name="item-property-ado-md-cellset"></a>Item プロパティ (ADO MD セルセット)
セルの座標を使用して、セル[セット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)からセルを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>パラメーター  
 *Positions*  
 セルを一意に指定する値の**VariantArray** 。 *位置*は、次のいずれかになります。  
  
-   位置番号の配列  
  
-   メンバー名の配列  
  
-   序数の位置  
  
## <a name="remarks"></a>解説  
 **アイテム**プロパティを使用して、[セル](../../../ado/reference/ado-md-api/cell-object-ado-md.md)[セット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)オブジェクト内の Cell オブジェクトを返します。 **Item**プロパティが*位置*引数に対応するセルを見つけることができない場合は、エラーが発生します。  
  
 **アイテム**プロパティは、**セルセット**オブジェクトの既定のプロパティです。 次の構文形式は置き換えることができます。  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>解説  
 *位置*引数は、返すセルを指定します。 セルは、序数位置または各軸に沿った位置によって指定できます。 各軸に沿って位置によってセルを指定する場合は、位置の数値または各位置のメンバーの名前を指定できます。  
  
 序数位置は、セル**セット**内の1つのセルを一意に識別する数値です。 概念的には、セルセット内のセルには、セル**セット**が*p*次元配列であるか**のように番号が付けら**れます。ここで、 *p*は軸の数です。 セルは、行優先順で指定されます。 セルの序数を計算するための式を次に示します。  
  
 メンバー名が文字列として**Item**に渡される場合、メンバーは数値軸識別子の昇順に表示される必要があります。 軸内では、メンバーはディメンションの入れ子の昇順に表示される必要があります。つまり、最も外側のディメンションのメンバーが最初になり、その後に内側のディメンションのメンバーが続きます。 各次元は個別の文字列で表す必要があり、メンバー文字列のリストはコンマで区切る必要があります。  
  
> [!NOTE]
>  メンバー名でセルを取得することは、データプロバイダーでサポートされていない可能性があります。 詳細については、プロバイダーのドキュメントを参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [CellSet オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [Cell オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [CellSet オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
