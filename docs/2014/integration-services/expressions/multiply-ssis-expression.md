---
title: '* (乗算) (SSIS 式) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4597c528f10e5461a7f11916fb173f16ff87b354
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969202"
---
# <a name="-multiply-ssis-expression"></a>* (乗算) (SSIS 式)
  2 つの数値式を乗算します。  
  
## <a name="syntax"></a>構文  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression1、numeric_expression2*  
 数値データ型の有効な式です。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 2 つの引数のデータ型によって決まります。 詳しくは、「 [式における Integration Services データ型](integration-services-data-types-in-expressions.md)」をご覧ください。  
  
## <a name="remarks"></a>解説  
 オペランドのいずれかが NULL の場合、結果は NULL になります。  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値リテラルを乗算します。  
  
```  
5 * 6.09  
```  
  
 この例では、 **ListPrice** 列の値に 10% を乗算します。  
  
```  
ListPrice * .10  
```  
  
 この例では、 **ListPrice** 列から式の結果を減算します。 変数 **Discount%** は、名前に % 文字が含まれているため、角かっこで囲む必要があります。 詳しくは、「[識別子 &#40;SSIS&#41;](identifiers-ssis.md)」をご覧ください。  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>参照  
 [演算子の優先順位と結合規則](operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](operators-ssis-expression.md)  
  
  
