---
title: Size プロパティ (ADO Parameter) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 58f989ab60099673f95debbe4eb5f8217beb0ccd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759888"
---
# <a name="size-property-ado-parameter"></a>Size プロパティ (ADO Parameter)
[パラメーター](../../../ado/reference/ado-api/parameter-object.md)オブジェクトの最大サイズをバイト数または文字数で示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **パラメーター**オブジェクトの値の最大サイズをバイトまたは文字単位で示す**Long 型**の値を設定または返します。  
  
## <a name="remarks"></a>解説  
 **Size**プロパティを使用して、**パラメーター**オブジェクトの[Value](../../../ado/reference/ado-api/value-property-ado.md)プロパティに対して書き込みまたは読み取りを行う値の最大サイズを決定します。  
  
 **パラメーター**オブジェクトに可変長データ型 (たとえば、 **adVarChar**などの任意の**文字列**型) を指定する場合は、[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクションに追加する前に、オブジェクトの**Size**プロパティを設定する必要があります。それ以外の場合は、エラーが発生します。  
  
 **Parameter**オブジェクトを[Command](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトの**Parameters**コレクションに既に追加していて、その型を可変長データ型に変更した場合は、 **command**オブジェクトを実行する前に、**パラメーター**オブジェクトの**Size**プロパティを設定する必要があります。それ以外の場合は、エラーが発生します。  
  
 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)メソッドを使用してプロバイダーからパラメーター情報を取得し、1つまたは複数の可変長データ型**パラメーター**オブジェクトを返す場合、ADO では、可能な最大サイズに基づいてパラメーターにメモリが割り当てられるため、実行中にエラーが発生する可能性があります。 エラーを回避するには、コマンドを実行する前に、これらのパラメーターの**Size**プロパティを明示的に設定する必要があります。  
  
 **Size**プロパティは読み取り/書き込み可能です。  
  
## <a name="applies-to"></a>適用対象  
 [Parameter オブジェクト](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>参照  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size プロパティ (ADO Stream)](../../../ado/reference/ado-api/size-property-ado-stream.md)
