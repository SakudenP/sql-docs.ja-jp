---
title: getClientInfoProperties メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a84002f7b44644ee5ba86ee277925e5f482b412
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926000"
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>getClientInfoProperties メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  ドライバーがサポートしているクライアント情報のプロパティの一覧を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>戻り値  
 ResultSet オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getClientInfoProperties メソッドは、java.sql.DatabaseMetaData インターフェイスの getClientInfoProperties メソッドによって指定されます。  
  
> [!NOTE]  
>  このメソッドでは、空の結果セットが返されます。 ドライバーは **applicationName**の設定のみをサポートし、**applicationName**は接続時にのみ設定されます。 SQL Server では、接続が確立された後のクライアント アプリケーション情報の更新はサポートされていません。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
