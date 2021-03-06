---
title: SSVARIANT 構造体 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55f91748efb8ad5b46abf8c36f407bf4a52b2a52
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724973"
---
# <a name="ssvariant-structure"></a>SSVARIANT 構造体
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Sqlncli で定義されている**Ssvariant**構造体は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLEDB プロバイダーの DBTYPE_SQLVARIANT 値に対応しています。  
  
 **SSVARIANT** は、識別共用体です。 vt メンバーの値に応じて、コンシューマーは読み取るメンバーを決めることができます。 vt 値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型に対応します。 したがって、**SSVARIANT** 構造体には、任意の SQL Server 型を格納できます。 標準の OLE DB 型のデータ構造体の詳細については、「[型インジケーター](https://go.microsoft.com/fwlink/?LinkId=122171)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 DataTypeCompat==80 の場合、いくつかの **SSVARIANT** サブタイプが文字列になります。 たとえば、次の vt 値は **SSVARIANT** では VT_SS_WVARSTRING として表されます。  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 DateTypeCompat == 0 の場合、これらの型はネイティブ形式で表されます。  
  
 SSPROP_INIT_DATATYPECOMPATIBILITY の詳細については、「 [SQL Server Native Client での接続文字列キーワードの使用](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 Sqlncli ファイルには、 **ssvariant**構造体内のメンバー型の逆参照を簡略化するバリアントアクセスマクロが含まれています。 たとえば、V_SS_DATETIMEOFFSET を次のように使用できます。  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 **Ssvariant**構造体の各メンバーの access マクロの完全なセットについては、sqlncli ファイルを参照してください。  
  
 次の表で、**SSVARIANT** 構造体のメンバーについて説明します。  
  
|メンバー|OLE DB 型インジケーター|OLE DB C データ型|vt の値|説明|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||**SSVARIANT** 構造体に格納される値の型を指定します。|  
|bTinyIntVal|DBTYPE_UI1|**バイト**|**VT_SS_UI1**|**Tinyint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|sShortIntVal|DBTYPE_I2|**短い**|**VT_SS_I2**|では、 **smallint**データ型がサポートされてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|**Int** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|では、 **bigint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|では、 **real** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|**Float** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|**money** と **smallmoney**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型がサポートされています。|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|では、 **bit** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|では、 **uniqueidentifier** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|**数値** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|**日付** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|**smalldatetime**、**datetime**、**datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型がサポートされています。|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|では、 **time** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**BYTE**) *tTime2Val* 値の小数点以下桁数を指定します。|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|では、 **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**BYTE**) *tsDataTimeVal* 値の小数点以下桁数を指定します。|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|では、 **datetimeoffset**データ型がサポートされてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。<br /><br /> 次のメンバーを含みます。<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**BYTE**) *tsoDateTimeOffsetVal* 値の小数点以下桁数を指定します。|  
|NCharVal|対応する OLE DB 型インジケーターはありません。|**struct _NCharVal**|**VT_SS_WVARSTRING、**<br /><br /> **VT_SS_WSTRING**|**nchar** と **nvarchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *sActualLength* (**SHORT**) *pwchNCharVal* がポイントする文字列の実際の長さを指定します。 末尾の 0 は含まれません。<br /><br /> *sMaxLength* (**SHORT**) *pwchNCharVal* がポイントする文字列の最大長を指定します。<br /><br /> *pwchNCharVal* (**WCHAR** \*) 文字列へのポインター。<br /><br /> 使用されていないメンバー: *rgbReserved*、*dwReserved*、および *pwchReserved*。|  
|CharVal|対応する OLE DB 型インジケーターはありません。|**struct _CharVal**|**VT_SS_STRING、**<br /><br /> **VT_SS_VARSTRING**|**char** と **varchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *sActualLength* (**SHORT**) *pchCharVal* がポイントする文字列の実際の長さを指定します。 末尾の 0 は含まれません。<br /><br /> *sMaxLength* (**SHORT**) *pchCharVal* がポイントする文字列の最大長を指定します。<br /><br /> *pchCharVal* (**CHAR** \*) 文字列へのポインター。<br /><br /> 使用されないメンバー : <br /><br /> *rgbReserved*、*dwReserved*、および *pwchReserved*。|  
|BinaryVal|対応する OLE DB 型インジケーターはありません。|**struct _BinaryVal**|**VT_SS_VARBINARY、**<br /><br /> **VT_SS_BINARY**|**binary** と **varbinary**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *sActualLength* (**SHORT**) *prgbBinaryVal* がポイントするデータの実際の長さを指定します。<br /><br /> *sMaxLength* (**SHORT**) *prgbBinaryVal* がポイントするデータの最大長を指定します。<br /><br /> *prgbBinaryVal* (**BYTE** \*) バイナリ データへのポインター。<br /><br /> 使用されていないメンバー: *dwReserved*。|  
|UnknownType|未使用|未使用|未使用|未使用|  
|BLOBType|未使用|未使用|未使用|未使用|  
  
## <a name="see-also"></a>関連項目  
 [データ型 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
