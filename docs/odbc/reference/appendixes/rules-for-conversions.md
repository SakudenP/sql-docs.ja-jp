---
title: 変換の規則 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c49177d62fffc3b3b5c47a25bf3fb421d7564245
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305088"
---
# <a name="rules-for-conversions"></a>変換規則
このセクションの規則は、数値リテラルを含む変換に適用されます。 これらの規則のために、次の用語が定義されています。  
  
-   *ストアの割り当て:* データベースのテーブル列にデータを送信する場合。 これは、 **Sqlexecute**、 **SQLExecDirect**、および**SQLSetPos**の呼び出し中に発生します。 ストアの割り当て時に、"ターゲット" はデータベース列を参照し、"ソース" はアプリケーションバッファー内のデータを参照します。  
  
-   *取得の割り当て:* データベースからアプリケーションバッファーにデータを取得する場合。 これは、 **Sqlfetch**、 **SQLGetData**、 **sqlfetchscroll**、 **SQLSetPos**の呼び出し中に発生します。 取得の割り当て中、"ターゲット" はアプリケーションバッファーを指し、"ソース" はデータベース列を参照します。  
  
-   *CS:* 文字ソースの値。  
  
-   *NT:* 数値ターゲットの値。  
  
-   *NS:* 数値ソースの値。  
  
-   *CT:* 文字ターゲットの値。  
  
-   正確な数値リテラルの有効桁数: 含まれる桁数。  
  
-   正確な数値リテラルの小数点以下桁数。表現された期間の右側の桁数。  
  
-   概数型の有効桁数。仮数部の有効桁数。  
  
## <a name="character-source-to-numeric-target"></a>数値ターゲットへの文字ソース  
 文字ソース (CS) から数値ターゲット (NT) に変換するための規則を次に示します。  
  
1.  Cs は、cs の先頭または末尾のスペースを削除することによって取得した値に置き換えます。 CS が有効な*数値リテラル*でない場合、SQLSTATE 22018 (キャストの指定に無効な文字値) が返されます。  
  
2.  CS を、小数点の前の先頭のゼロ、小数点の後のゼロ、またはその両方を削除して取得した値に置き換えます。  
  
3.  CS を NT に変換します。 変換によって有効桁数が失われた場合、SQLSTATE 22003 (数値の範囲外) が返されます。 変換によって非有意数字が失われた場合、SQLSTATE 01S07 (小数部の切り捨て) が返されます。  
  
## <a name="numeric-source-to-character-target"></a>数値ソースから文字ターゲットへ  
 数値ソース (NS) から文字ターゲット (CT) に変換するための規則を次に示します。  
  
1.  CT の長さを文字数で指定します。 取得の割り当ての場合、LT は、文字のバッファーの長さから、この文字セットの null 終端文字のバイト数を引いた値と等しくなります。  
  
2.  場合  
  
    -   NS が正確な数値型である場合は、yp の小数点以下桁数が NS の小数点以下桁数と同じになるように、*完全な数値リテラル*の定義に準拠する最短の文字列を yp として指定します。また、yp の解釈された値は、ns の絶対値です。  
  
    -   NS が概数型である場合は、次のように、YP を文字列にします。  
  
         大文字と小文字の区別:  
  
         NS が0の場合、YP は0になります。  
  
         実際の*数値リテラル*の定義に準拠し、解釈された値が NS の絶対値である最短文字列を ysn にします。 YSN の長さが、NS のデータ型の (*precision* + 1) よりも小さい場合は、YP を ysn にします。  
  
         それ以外の場合、YP は、*概数リテラル*の定義に準拠した最短の文字列です。解釈された値は、NS の絶対値で、*仮数*は ' 0 ' 以外の 1*桁*で構成され、その後に*ピリオド*と*符号なし整数*が続きます。  
  
3.  大文字と小文字の区別:  
  
    -   NS が0未満の場合、Y は次の結果になります。  
  
         '-'  &#124;&#124; YP  
  
         ここで、' &#124;&#124; ' は文字列連結演算子です。  
  
         それ以外の場合は、Y は YP と等しくなります。  
  
4.  長さは、Y の文字数で指定します。  
  
5.  大文字と小文字の区別:  
  
    -   が LT に等しい場合、CT は Y に設定されます。  
  
    -   値が LT より小さい場合、CT は適切なスペース数で右側に [Y 拡張] に設定されます。  
  
         それ以外の場合 (非常に > LT)、Y の最初の LT 文字を CT にコピーします。  
  
         大文字と小文字の区別:  
  
         これがストアの割り当ての場合は、エラー SQLSTATE 22001 (文字列データ、右の切り捨て) を返します。  
  
         取得の割り当てである場合は、警告 SQLSTATE 01004 (文字列データ、右の切り捨て) を返します。 コピーによって小数部の桁が失われた場合 (後続のゼロを除く)、次のいずれかが発生した場合にドライバーによって定義されます。  
  
         (1) ドライバーは、Y 内の文字列を適切な小数点以下桁数に切り捨て、結果を CT に書き込みます。  
  
         (2) ドライバーは、Y の文字列を適切な小数点以下桁数に丸め、結果を CT に書き込みます。  
  
         (3) ドライバーは、切り捨てもラウンドも行いませんが、Y の最初の LT 文字を CT にコピーするだけです。
