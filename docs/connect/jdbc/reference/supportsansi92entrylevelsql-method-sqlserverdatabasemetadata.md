---
title: supportsANSI92EntryLevelSQL メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsANSI92EntryLevelSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a3fffc08-7254-4af7-bbae-8ff591fbd5ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a67def3f71e0298f00382f13bb0c7925adf61ba6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80915548"
---
# <a name="supportsansi92entrylevelsql-method-sqlserverdatabasemetadata"></a>supportsANSI92EntryLevelSQL メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースが ANSI92 エントリ レベルの SQL 文法をサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsANSI92EntryLevelSQL()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は、**true** です。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この supportsANSI92EntryLevelSQL メソッドは、java.sql.DatabaseMetaData インターフェイスの supportsANSI92EntryLevelSQL メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
