---
title: 結果セットの情報の取得 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5500a8a0575e04df01989b2a8ab8b81d67468f32
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724996"
---
# <a name="processing-results---retrieve-result-set-information"></a>結果の処理 - 結果セットの情報の取得
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

    
### <a name="to-get-information-about-a-result-set"></a>結果セットに関する情報を取得するには  
  
1.  [Sqlnumresultcols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)を呼び出して、結果セット内の列の数を取得します。  
  
2.  結果セット内の各列に対して次の操作を行います。  
  
    -   [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)を呼び出して、結果列に関する情報を取得します。  
  
     または  
  
    -   [Sqlcolattribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)を呼び出して、結果列に関する特定の記述子情報を取得します。  
  
## <a name="see-also"></a>関連項目  
[ODBC&#41;&#40;の結果の処理](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[ODBC&#41;&#40;結果セットの特性の決定](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
