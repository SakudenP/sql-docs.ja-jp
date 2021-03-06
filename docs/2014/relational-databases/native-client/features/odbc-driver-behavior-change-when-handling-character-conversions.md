---
title: 文字変換を処理するときの ODBC ドライバーの動作の変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 682a232a-bf89-4849-88a1-95b2fbac1467
author: rothja
ms.author: jroth
ms.openlocfilehash: 5f4ec8a9538cead097402c046e2f9f91c95faa01
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047932"
---
# <a name="odbc-driver-behavior-change-when-handling-character-conversions"></a>文字変換処理での ODBC ドライバーの動作の変更
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]Native CLIENT ODBC ドライバー (SQLNCLI11.dll) では、SQL_WCHAR * (NCHAR/nvarchar/nvarchar (max)) と SQL_CHAR \* (CHAR/VARCHAR/NARCHAR (max)) 変換の動作が変更されました。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client ODBC ドライバーを使用する場合、SQLGetData、SQLBindCol、SQLBindParameter などの ODBC 関数では長さまたはインジケーターのパラメーターとして (-4) SQL_NO_TOTAL が返されます。 以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは長さの値が返されましたが、これは誤りである可能性があります。  
  
## <a name="sqlgetdata-behavior"></a>SQLGetData の動作  
 多くの Windows 関数ではバッファー サイズに 0 を指定できます。返される長さは、返されるデータのサイズです。 以下は、Windows プログラミングで一般的なパターンです。  
  
```  
int iSize = 0;  
BYTE * pBuffer = NULL;  
GetMyFavoriteAPI(pBuffer, &iSize);   // Returns needed size in iSize  
pBuffer = new BYTE[iSize];   // Allocate buffer   
GetMyFavoriteAPI(pBuffer, &iSize);   // Retrieve actual data  
```  
  
 ただし、このシナリオでは**SQLGetData**を使用しないでください。 次のパターンは使用できません。  
  
```  
// bad  
int iSize = 0;  
WCHAR * pBuffer = NULL;  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)0x1, 0, &iSize);   // Get storage size needed  
pBuffer = new WCHAR[(iSize/sizeof(WCHAR)) + 1];   // Allocate buffer  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)pBuffer, iSize, &iSize);   // Retrieve data  
```  
  
 **SQLGetData**は、実際のデータのチャンクを取得するためにのみ呼び出すことができます。 **SQLGetData**を使用してデータのサイズを取得することはサポートされていません。  
  
 次に、不適切なパターンを使用した場合のドライバーの変更による影響を示します。 このアプリケーションでは `varchar` 列およびバインドを Unicode (SQL_UNICODE/SQL_WCHAR) としてクエリを実行します。  
  
 照会`select convert(varchar(36), '123')`  
  
```  
SQLGetData(hstmt, SQL_WCHAR, ....., (SQLPOINTER*) 0x1, 0 , &iSize);   // Attempting to determine storage size needed  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのバージョン|長さまたはインジケーターの結果|説明|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 以前|6|ドライバーには、CHAR から WCHAR への変換が長さ * 2 として実行できるという誤った想定がありました。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (Version 11.0.2100.60) 以降|-4 (SQL_NO_TOTAL)|ドライバーは、CHAR から WCHAR または WCHAR から CHAR への変換が、(乗算) \* 2 または (除算)/2 アクションであると想定しなくなりました。<br /><br /> **SQLGetData**を呼び出すと、予期される変換の長さが返されなくなりました。 ドライバーでは CHAR と WCHAR との間の変換が検出され、誤りの可能性のある *2 または /2 の動作の代わりに (-4) SQL_NO_TOTAL が返されます。|  
  
 **SQLGetData**を使用して、データのチャンクを取得します。 (擬似コードを示します)。  
  
```  
while( (SQL_SUCCESS or SQL_SUCCESS_WITH_INFO) == SQLFetch(...) ) {  
   SQLNumCols(...iTotalCols...)  
   for(int iCol = 1; iCol < iTotalCols; iCol++) {  
      WCHAR* pBufOrig, pBuffer = new WCHAR[100];  
      SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get original chunk  
      while(NOT ALL DATA RETREIVED (SQL_NO_TOTAL, ...) ) {  
         pBuffer += 50;   // Advance buffer for data retrieved  
         // May need to realloc the buffer when you reach current size  
         SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get next chunk  
      }  
   }  
}  
```  
  
## <a name="sqlbindcol-behavior"></a>SQLBindCol の動作  
 照会`select convert(varchar(36), '1234567890')`  
  
```  
SQLBindCol(... SQL_W_CHAR, ...)   // Only bound a buffer of WCHAR[4] - Expecting String Data Right Truncation behavior  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのバージョン|長さまたはインジケーターの結果|説明|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 以前|20|-   **Sqlfetch**は、データの右側に切り捨てがあることを報告します。<br />-Length は、返されるデータの長さであり、格納されたデータではありません (グリフに対して正しくない場合がある * 2 CHAR から WCHAR への変換が想定されます)。<br />-バッファーに格納されているデータは 123 \ 0 です。 バッファーは NULL 終端であることが保証されます。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (Version 11.0.2100.60) 以降|-4 (SQL_NO_TOTAL)|-   **Sqlfetch**は、データの右側に切り捨てがあることを報告します。<br />-データの残りの部分が変換されていないため、-4 (SQL_NO_TOTAL) を指定します。<br />-バッファーに格納されているデータは 123 \ 0 です。 - バッファーは NULL 終端であることが保証されます。|  
  
## <a name="sqlbindparameter-output-parameter-behavior"></a>SQLBindParameter (出力パラメーターの動作)  
 照会`create procedure spTest @p1 varchar(max) OUTPUT`  
  
 `select @p1 = replicate('B', 1234)`  
  
```  
SQLBindParameter(... SQL_W_CHAR, ...)   // Only bind up to first 64 characters  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのバージョン|長さまたはインジケーターの結果|説明|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 以前|2468|-   **Sqlfetch**は、使用可能なデータがないことを返します。<br />-   **Sqlmoreresults**は、これ以上使用できるデータを返しません。<br />-Length は、サーバーから返されるデータのサイズを示します。バッファーに格納されません。<br />-元のバッファーには、63バイトと NULL 終端文字が含まれています。 バッファーは NULL 終端であることが保証されます。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (Version 11.0.2100.60) 以降|-4 (SQL_NO_TOTAL)|-   **Sqlfetch**は、使用可能なデータがないことを返します。<br />-   **Sqlmoreresults**は、これ以上使用できるデータを返しません。<br />-データの残りの部分が変換されなかったため、が (-4) SQL_NO_TOTAL を示します。<br />-元のバッファーには、63バイトと NULL 終端文字が含まれています。 バッファーは NULL 終端であることが保証されます。|  
  
## <a name="performing-char-and-wchar-conversions"></a>CHAR と WCHAR の変換の実行  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client ODBC ドライバーには、CHAR と WCHAR の変換を実行する方法が複数用意されています。 ロジックは、blob の操作 (varchar (max)、nvarchar (max)、...) に似ています。  
  
-   **SQLBindCol**または**SQLBindParameter**にバインドする場合、データは指定されたバッファーに保存されるか、または切り捨てられます。  
  
-   バインドしない場合は、 **SQLGetData**と**sqlparamdata**を使用して、データをチャンク単位で取得できます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](sql-server-native-client-features.md)  
  
  
