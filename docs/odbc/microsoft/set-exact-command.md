---
title: SET EXACT Command |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e754fff35b6b948ac63d19361067b2d65a07fdd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300872"
---
# <a name="set-exact-command"></a>SET EXACT コマンド
長さが異なる2つの文字列を比較するための規則を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 式が文字の文字と一致する必要があることを指定します。 比較では、式の後続の空白は無視されます。 比較のために、2つの式の短い方が右側に空白が埋め込まれ、長い式の長さと一致します。  
  
 OFF  
 (既定値)。等しいと見なされるように、右辺の式の終わりに達するまで、式が文字の文字と一致する必要があることを指定します。  
  
## <a name="remarks"></a>Remarks  
 両方の文字列が同じ長さである場合、[正確に設定] 設定は無効です。  
  
## <a name="string-comparisons"></a>文字列比較  
 Visual FoxPro には、等しいかどうかをテストする2つの関係演算子があります。  
  
 = 演算子は、同じ型の2つの値の比較を実行します。 この演算子は、文字、数値、日付、および論理データを比較する場合に適しています。  
  
 ただし、文字式を = 演算子と比較すると、結果が期待どおりではない可能性があります。 文字式は、左から右への文字の文字が比較されます。この場合、式の1つがもう一方の式と等しくならないようになります。これは、= 演算子の右側にある式の末尾に到達するか (正確に OFF に設定)、両方の式の末尾に到達するまで (が完全に設定されます  
  
 文字データを正確に比較する必要がある場合は、= = 演算子を使用できます。 2つの文字式が = = 演算子と比較される場合、= = 演算子の両側の式は、等しいと見なされるように、空白を含む同じ文字を正確に含む必要があります。 厳密な設定は、= = を使用して文字列を比較する場合には無視されます。  
  
 次の表は、[演算子の選択] と [設定の正確な設定] が比較にどのように影響するかを示しています。 (アンダースコアは空白文字を表します)。  
  
|比較|= 完全にオフ|= 完全一致|= = 完全にオンまたはオフ|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|照合|照合|照合|  
|"ab" = "abc"|一致なし。|一致なし。|一致なし。|  
|"abc" = "ab"|照合|一致なし。|一致なし。|  
|"abc" = "ab_"|一致なし。|一致なし。|一致なし。|  
|"ab" = "ab_"|一致なし。|照合|一致なし。|  
|"ab_" = "ab"|照合|照合|一致なし。|  
|"" = "ab"|一致なし。|一致なし。|一致なし。|  
|"ab" = ""|照合|一致なし。|一致なし。|  
|"__" = ""|照合|照合|一致なし。|  
|"" = "___"|一致なし。|照合|一致なし。|  
|TRIM ("__ _") = ""|照合|照合|照合|  
|"" = TRIM ("__ _")|照合|照合|照合|  
  
## <a name="see-also"></a>参照  
 [SET ANSI コマンド](../../odbc/microsoft/set-ansi-command.md)
