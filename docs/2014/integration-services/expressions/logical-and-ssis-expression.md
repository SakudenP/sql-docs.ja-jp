---
title: '&amp;&amp; (論理 AND) (SSIS 式) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2dd2456bfada856e9f9e78e95a7d7561a2413dc2
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428359"
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp; (論理 AND) (SSIS 式)
  論理 AND 演算を実行します。 両方の条件が TRUE の場合、式は TRUE に評価されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## <a name="arguments"></a>引数  
 *boolean _expression1, boolean_expression2*  
 TRUE、FALSE、または NULL に評価される、任意の有効な式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_BOOL  
  
## <a name="remarks"></a>解説  
 次の表は、&& 演算子の結果を示します。  
  
|結果|式|式|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## <a name="expression-examples"></a>式の例  
 この例では、 **StandardCost** 列と **ListPrice** 列を使用しています。 **StandardCost** 列の値が 300 より小さく、かつ **ListPrice** 列の値が 500 より大きい場合、式は TRUE に評価されます。  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 この例では、リテラルの代わりに変数 **SPrice** と **LPrice** を使用しています。  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>参照  
 [& (ビット演算子 AND) (SSIS 式)](bitwise-and-ssis-expression.md)   
 [演算子の優先順位と結合規則](operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](operators-ssis-expression.md)  
  
  
