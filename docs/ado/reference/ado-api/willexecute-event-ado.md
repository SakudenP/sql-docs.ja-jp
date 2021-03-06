---
title: イベント実行 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: rothja
ms.author: jroth
ms.openlocfilehash: ef47b4bac626d82754ce01685504b4a48303a4b4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764453"
---
# <a name="willexecute-event-ado"></a>WillExecute イベント (ADO)
この**イベントは、接続**で保留中のコマンドが実行される直前に呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ソース*  
 SQL コマンドまたはストアドプロシージャ名を含む**文字列**。  
  
 *CursorType*  
 開かれる**レコードセット**のカーソルの種類が格納されている[cursor typeenum](../../../ado/reference/ado-api/cursortypeenum.md) 。 このパラメーターを使用すると、**レコードセット**の[OPEN メソッド (ADO recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)操作中に、カーソルを任意の型に変更できます。 *CursorType*は、他の操作では無視されます。  
  
 *LockType*  
 開かれる**レコードセット**のロックの種類を格納する[locktypeenum](../../../ado/reference/ado-api/locktypeenum.md) 。 このパラメーターを使用すると、 **RecordsetOpen**操作中に任意の型にロックを変更できます。 他の操作では、 *LockType*は無視されます。  
  
 *[オプション]*  
 コマンドを実行したり、**レコードセット**を開いたりするために使用できるオプションを示す**Long 型**の値です。  
  
 *adStatus*  
 このイベントが呼び出されたときに**Adstatuscantdeny**または**Adstatusok**となる[eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md)ステータス値。 **Adstatuscantdeny**の場合、このイベントは保留中の操作の取り消しを要求しない可能性があります。  
  
 *pCommand*  
 このイベント通知を適用する対象の[コマンドオブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト。  
  
 *pRecordset*  
 このイベント通知を適用する[ADO (Recordset オブジェクト](../../../ado/reference/ado-api/recordset-object-ado.md)) オブジェクト。  
  
 *pConnection*  
 このイベント通知を適用する[接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
## <a name="remarks"></a>Remarks  
 接続によっ**てイベントが発生する可能性**があります。  [Execute メソッド (Ado Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)、 [EXECUTE メソッド (ado Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)、または[Open method (Ado Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッド。 *Pconnection*パラメーターには、常に**接続**オブジェクトへの有効な参照を含める必要があります。 イベントが接続によって発生した場合、 *Precordset*および*Precordset*パラメーターは**Nothing**に設定され**ます**。 イベントが**レコードセット**によって発生した場合、 *Precordset*パラメーターは**レコードセット**オブジェクトを参照し、 *precordset*パラメーターは**Nothing**に設定されます。 イベントが**コマンドの実行**によって発生した場合、 *Pcommand*パラメーターは**コマンド**オブジェクトを参照し、 *pcommand*パラメーターは**Nothing**に設定されます。  
  
 を**実行**すると、保留中の実行パラメーターを確認および変更できます。 このイベントは、保留中のコマンドがキャンセルされたことを示す要求を返す場合があります。  
  
> [!NOTE]
>  **コマンド**の元のソースが[COMMANDSTREAM プロパティ (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)プロパティによって指定されたストリームである場合は、新しい文字列をに渡し**て、****コマンド**_のソースを_変更します。 **Commandstream**プロパティがクリアされ、 [COMMANDTEXT プロパティ (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)プロパティが新しいソースで更新されます。 **Commandstream**によって指定された元のストリームは解放され、アクセスできなくなります。  
  
 新しいソース文字列の言語が、 [Dialect プロパティ](../../../ado/reference/ado-api/dialect-property.md)プロパティ ( **commandstream**にこれ) の元の設定と異なる場合は、 *pcommand*によって参照されるコマンドオブジェクトの**dialect**プロパティを設定して、正しい言語を指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベントハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
