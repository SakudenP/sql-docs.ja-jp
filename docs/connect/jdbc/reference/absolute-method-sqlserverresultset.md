---
title: absolute メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.absolute
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638e8148-8ca0-4e1f-9ec2-04a11bc9809b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 06a6a95838ef4ee1c605fa54fce9ef2d81f4573e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923730"
---
# <a name="absolute-method-sqlserverresultset"></a>absolute メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの指定された行にカーソルを移動します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean absolute(int row)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *row*  
  
 移動先の行番号を示す **int** です。 正の値、負の値、または 0 を指定できます。  
  
## <a name="return-value"></a>戻り値  
 カーソルが指定された位置に移動した場合は **true** です。 これが最初の行より前または最後の行より後にある場合は **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この absolute メソッドは、java.sql.ResultSet インターフェイスの absolute メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
