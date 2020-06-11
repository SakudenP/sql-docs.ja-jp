---
title: 名前空間-QName からの uri (XQuery) |Microsoft Docs
description: 名前空間 uri from QName 関数を使用して、QName の名前空間 URI を取得する方法について説明します。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: a0967e9dfd9392513da3925725930111a97da0c9
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689543"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>QNames に関係する関数 - namespace-uri-from-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  *$Arg*によって指定された QName の名前空間 uri を表す文字列を返します。 *$Arg*が空のシーケンスの場合、結果は空のシーケンスになります。  
  
## <a name="syntax"></a>構文  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 は、名前空間 URI が返される QName です。  
  
## <a name="examples"></a>例  
 このトピックでは、AdventureWorks データベースのさまざまな**xml**型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. QName から名前空間 URI を取得する  
 実際のサンプルについては、「[ローカル名-QName からの &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md)」を参照してください。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **名前空間 uri From QName ()** 関数は、Xs: anyURI ではなく xs: string のインスタンスを返します。  
  
## <a name="see-also"></a>参照  
 [QNames &#40;XQuery&#41;に関連する関数](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
