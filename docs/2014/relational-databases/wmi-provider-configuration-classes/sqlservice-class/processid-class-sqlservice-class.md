---
title: ProcessId クラス (SqlService クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProcessId Class (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f64a81709e63510af507996cc2d2968a765e0fad
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002134"
---
# <a name="processid-class-sqlservice-class"></a>ProcessId クラス (SqlService クラス)
  サービスを一意に識別するシステム プロセス ID を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object  
.ProcessId [= value]  
```  
  
## <a name="parts"></a>指定項目  
 *object*  
 サービスを表す [SqlService クラス](sqlservice-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 プロセスを一意に識別する ID を指定する `uint32` 値。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="example"></a>例  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>参照  
 [サービスの開始および停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
