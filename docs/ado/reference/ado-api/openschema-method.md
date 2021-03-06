---
title: OpenSchema メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
author: rothja
ms.author: jroth
ms.openlocfilehash: 716eec332690d1a6e9df1f16d67d82afc1a30985
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762103"
---
# <a name="openschema-method"></a>OpenSchema メソッド
プロバイダーからデータベーススキーマ情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>戻り値  
 スキーマ情報を含む[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトを返します。 **レコードセット**は、読み取り専用の静的カーソルとして開かれます。 *QueryType*は、**レコードセット**に表示される列を決定します。  
  
#### <a name="parameters"></a>パラメーター  
 *QueryType*  
 実行するスキーマクエリの種類を表す[Schemaenum](../../../ado/reference/ado-api/schemaenum.md)値。  
  
 *条件*  
 任意。 [Schemaenum](../../../ado/reference/ado-api/schemaenum.md)に記載されているように、各*QueryType*オプションのクエリ制約の配列。  
  
 *SchemaID*  
 OLE DB 仕様で定義されていないプロバイダースキーマクエリの GUID。 *QueryType*が**Adschemaproviderspecific**に設定されている場合、このパラメーターは必須です。それ以外の場合は使用されません。  
  
## <a name="remarks"></a>解説  
 **OpenSchema**メソッドは、データソース内のテーブル、テーブル内の列、サポートされるデータ型など、データソースに関する自己記述的な情報を返します。  
  
 *QueryType*引数は、返される列 (スキーマ) を示す GUID です。 OLE DB 仕様には、スキーマの完全な一覧が含まれています。  
  
 *Criteria*引数は、スキーマクエリの結果を制限します。 *条件*には、結果として得られる**レコードセット**内の、対応する列のサブセット (制約列) に出現する必要がある値の配列を指定します。  
  
 プロバイダーが、前に示した以外の非標準のスキーマクエリを定義している場合は、 *QueryType*引数に定数**Adschemaproviderspecific**が使用されます。 この定数を使用する場合は、実行するスキーマクエリの GUID を渡すために*Schemaid*引数が必要です。 *QueryType*が**Adschemaproviderspecific**に設定されていても、 *schemaid*が指定されていない場合、エラーが発生します。  
  
 プロバイダーは、すべての OLE DB 標準スキーマクエリをサポートする必要はありません。 具体的には、OLE DB の仕様で**adSchemaColumns**は、 **adschematables**、 **adschematables**だけが必要です。 ただし、これらのスキーマクエリに対して前述した*条件*制約をサポートするために、プロバイダーは必要ありません。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況****OpenSchema**メソッドは、クライアント側の[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトでは使用できません。  
  
> [!NOTE]
>  Visual Basic、**接続**オブジェクトの**OpenSchema**メソッドから返された**レコードセット**内の4バイト符号なし整数 (DBTYPE UI4) を持つ列を他の変数と比較することはできません。 OLE DB データ型の詳細については、「 [OLE DB のデータ型」 (OLE DB)](https://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a)および「[付録 a:](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6) Microsoft OLE DB プログラマーリファレンス」の「データ型」を参照してください。  
  
> [!NOTE]
>  **Visual C/c + + ユーザー**クライアント側カーソルを使用していない場合は、ADO の列スキーマの "ORDINAL_POSITION" を取得すると、mdac 2.7、MDAC 2.8、および Windows Data Access Components (Windows DAC) 6.0 の VT_R8 型のバリアントが返されますが、MDAC 2.6 で使用されていた型は VT_I4 ます。 MDAC 2.6 用に記述されたプログラムでは、VT_I4 型で返される variant のみを検索する場合、MDAC 2.7、MDAC 2.8、および Windows DAC 6.0 で変更を行わずに実行すると、すべての序数に対して0が返されます。 この変更は、OLE DB が返すデータ型が DBTYPE_UI4 であり、符号付き VT_I4 型には、切り捨てが発生してデータが失われる可能性がないため、すべての可能な値を格納するのに十分な領域がないためです。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [OpenSchema メソッドの例 (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema メソッドの例 (VC + +)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open メソッド (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open メソッド (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open メソッド (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
