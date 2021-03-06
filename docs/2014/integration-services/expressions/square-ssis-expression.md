---
title: SQUARE (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: cecf1bb2-3d55-40a6-9688-ed67bcc150b4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ea619cb05064788869e211b6cb5ef96cb4f7188d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428136"
---
# <a name="square-ssis-expression"></a>SQUARE (SSIS 式)
  数値式の 2 乗値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SQUARE(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 任意の数値データ型の数値式です。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 DT_R8  
  
## <a name="remarks"></a>解説  
 引数が NULL の場合、SQUARE は NULL を返します。  
  
 2 乗演算の前に、引数は DT_R8 データ型にキャストされます。  
  
## <a name="expression-examples"></a>式の例  
 この例では、12 の 2 乗が返されます。 返される結果は 144 です。  
  
```  
SQUARE(12)  
```  
  
 この例では、2 つの列の値を減算した結果の 2 乗が返されます。 **Value1** が 12 で **Value2** が 4 の場合、SQUARE 関数は 64 を返します。  
  
```  
SQUARE(Value1 - Value2)  
```  
  
 この例では、SQUARE 関数を 2 つの変数に適用して、その合計の平方根を計算することにより、直角三角形の 3 番目の辺の長さが返されます。 **Side1** の値が 3、 **Side2** の値が 4 の場合、SQRT 関数は 5 を返します。  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  式に含まれる変数名には、常にプレフィックス \@ を付けます。  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
