---
title: setCharacterStream (java.lang.String, java.io.Reader, long) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 54fb2f13-f8d8-47b5-bec1-4a5af3e86a84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 304797651e93ea39269b9a68f810a3e98290eac8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80929055"
---
# <a name="setcharacterstream-method-javalangstring-javaioreader-long"></a>setCharacterStream (java.lang.String, java.io.Reader, long) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、指定された文字数である指定された java.io.Reader オブジェクトに設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setCharacterStream(java.lang.String parameterName  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterName*  
  
 パラメーターの名前を含む**文字列**です。  
  
 *reader*  
  
 Unicode データを含む Reader オブジェクトです。  
  
 *length*  
  
 ストリームの文字数を示す **long** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setCharacterStream メソッドは、java.sql.CallableStatement インターフェイスの setCharacterStream メソッドで規定されています。  
  
 ストリームの長さが、*length* パラメーターで指定された長さと異なる場合は、行の更新または挿入時に JDBC ドライバーが例外をスローします。  
  
 ストリームの長さが不明である場合、*length* パラメーターを -1 に設定して、ドライバーが長さに関係なくストリームを受け入れるように指定できます。 sqljdbc4.jar を使用する場合、アプリケーションで長さが不明なストリームを使用して列を更新するときには、JDBC 4.0 メソッドの [setCharacterStream (java.lang.String, java.io.Reader)](../../../connect/jdbc/reference/setcharacterstream-method-java-lang-string-java-io-reader.md) メソッドを使用することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [setCharacterStream メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
