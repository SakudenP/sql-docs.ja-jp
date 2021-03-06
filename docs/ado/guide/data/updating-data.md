---
title: データの更新 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
author: rothja
ms.author: jroth
ms.openlocfilehash: 26f3ca9220ea41db43b9f98a12429dcb5874bba4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750223"
---
# <a name="updating-data"></a>データの更新
更新の動作と機能は、更新モード (ロックの種類)、カーソルの種類、およびカーソルの場所に大きく依存します。  
  
 **AddNew**メソッドを呼び出した後、または既存のレコードのフィールド値を変更した後に、**レコードセット**オブジェクトの現在のレコードに加えた変更を保存するには、 **Update**メソッドを使用します。 **レコードセット**オブジェクトは更新をサポートしている必要があります。  
  
 **レコードセット**オブジェクトでバッチ更新がサポートされている場合は、 **UpdateBatch**メソッドを呼び出すまで、1つ以上のレコードに対して複数の変更をローカルにキャッシュできます。 現在のレコードを編集している場合、または**UpdateBatch**メソッドを呼び出したときに新しいレコードを追加している場合、ADO は**Update**メソッドを自動的に呼び出して、保留中の変更を現在のレコードに保存してから、バッチされた変更をプロバイダーに送信します。  
  
 **Update**メソッドまたは**UpdateBatch**メソッドを呼び出した後、現在のレコードは最新のままです。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [イミディエイト モード](../../../ado/guide/data/immediate-mode.md)  
  
-   [バッチ モード](../../../ado/guide/data/batch-mode.md)  
  
-   [トランザクション処理](../../../ado/guide/data/transaction-processing.md)
