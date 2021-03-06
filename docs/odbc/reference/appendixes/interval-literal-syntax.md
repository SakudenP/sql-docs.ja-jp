---
title: Interval リテラル構文 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3387b07a8e769206a6a495addff4287000691fec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290572"
---
# <a name="interval-literal-syntax"></a>Interval のリテラルの構文
ODBC の interval リテラルには、次の構文が使用されます。  
  
 *interval-リテラル:: = interval* [+*&#124;*-] *interval-文字列間隔-修飾子*  
  
 *interval-string* :: = *quote* { *year-month-リテラル*&#124; の*日付と時刻の*間の*引用符*  
  
 *年月-リテラル*:: =*年-値*&#124; [*年-値*-]*月-値*  
  
 *日時リテラル*:: =*日-時間*間隔 &#124;*時間間隔*  
  
 *日-時間-間隔*:: =*日-値*[*時間-値*[:*分-値*[:*秒-値*]]]  
  
 *時間間隔*:: =*時間-値*[:*分-値*[:*秒-値*]]  
  
 &#124;*分-値*[:*秒-値*]  
  
 &#124;*秒-値*  
  
 *years-value* :: = *datetime-値*  
  
 *month-value* :: = *datetime-value*  
  
 *日数-値*:: = *datetime-値*  
  
 *時間-値*:: = *datetime-値*  
  
 *分-値*:: = *datetime-値*  
  
 *秒-値*:: =*秒-整数-値*[. [*秒-分*]]  
  
 *秒-整数-値*:: =*符号なし整数*  
  
 *秒-分数*:: =*符号なし整数*  
  
 *datetime-value* :: = *unsigned-integer*  
  
 *interval-修飾子*:: =*開始-* フィールドから*終了*フィールド &#124; には、*単一の datetime フィールド*を指定します。  
  
 *start-field* :: = *second-datetime-field* [(*interval-先頭フィールドの有効桁数*)]  
  
 *end field* :: = *second-datetime-field* &#124; second [(*interval-秒の小数部の有効桁数*)]  
  
 *単一の datetime-field* :: = *second-datetime-field* [(*interval-先頭フィールドの有効桁数*)] &#124; second [(間隔-*先頭フィールド-* 有効桁数 [, (*間隔-秒の小数部の有効桁数*)]  
  
 *datetime-field* :: = *second-datetime-field* &#124; second  
  
 *秒以外の datetime-field* :: = YEAR &#124; MONTH &#124; DAY &#124; HOUR &#124; MINUTE  
  
 *interval-秒の小数部の有効桁数*:: =*符号なし整数*  
  
 *interval-先頭フィールド-有効桁数*:: =*符号なし整数*  
  
 *引用符*:: = '  
  
 *符号なし整数*:: = *digit...*
