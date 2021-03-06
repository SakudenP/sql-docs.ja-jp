---
title: 行セット内のデータの更新 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, updating data
- SQL Server Native Client OLE DB provider, data updates
- data updates [SQL Server], OLE DB
ms.assetid: 37769b1c-c480-419a-8c54-5cc420bf73db
author: rothja
ms.author: jroth
ms.openlocfilehash: 993cfb67d4e6b72eec7cc0537e9b47371e94af10
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011194"
---
# <a name="updating-data-in-rowsets"></a>行セット内のデータの更新
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンシューマーがそのデータを含む変更可能な行セットを更新するときにデータを更新します。 コンシューマーが **IRowsetChange** インターフェイスまたは **IRowsetUpdate** インターフェイスのいずれかのサポートを要求すると、変更可能な行セットが作成されます。  
  
 すべて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Native Client OLE DB プロバイダー変更可能な行セット [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、カーソルを使用して行セットをサポートします。 行セット プロパティ DBPROP_LOCKMODE は、カーソルでの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコンカレンシー制御動作を変更し、更新可能な行セット内の行をフェッチする動作や、その行セット内のデータの整合性に関するエラーを生成する動作を決定します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーでは、更新前または更新後の行の同期がサポートされます。  
  
> [!NOTE]  
>  IRowChange::SetColumns を使用して、行オブジェクトの 1 つ以上の名前付き列の値を設定できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [SQL Server カーソルでのデータ更新](updating-data-in-sql-server-cursors.md)  
  
-   [行の再同期](updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>参照  
 [行セット](rowsets.md)  
  
  
