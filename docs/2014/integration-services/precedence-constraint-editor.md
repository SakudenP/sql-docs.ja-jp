---
title: 優先順位制約エディター |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.precedenceconstraint.f1
helpviewer_keywords:
- Precedence Constraint Editor dialog box
ms.assetid: b10d4330-6e35-4037-b309-ef56efcd60c5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 02cd814a3b4e52c8685d0df654c6e74071db9907
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964652"
---
# <a name="precedence-constraint-editor"></a>優先順位制約エディター
  **[優先順位制約エディター]** ダイアログ ボックスを使用すると、優先順位制約を構成できます。  
  
## <a name="options"></a>オプション  
 **[評価操作]**  
 優先順位制約で使用する評価操作を指定します。 操作として、 **[制約]**、 **[式]**、 **[式と制約]**、および **[式または制約]** を指定できます。  
  
 **Value**  
 制約値として、 **[成功]**、 **[失敗]**、または **[完了]** を指定します。  
  
> [!NOTE]  
>   優先順位制約を表す線は、 **[成功]** の場合は緑色、 **[失敗]** の場合は強調表示、 **[完了]** の場合は青色です。  
  
 **条件**  
 操作として **[式]**、 **[式と制約]**、または **[式または制約]** を使用する場合は、式を入力するか、式ビルダーを起動して式を作成します。 式はブール値に評価される必要があります。  
  
 **テスト**  
 式を検証します。  
  
 **論理 AND**  
 同一の実行可能ファイルに対して、複数の優先順位制約を同時に評価することを指定する場合に選択します。 すべての制約が `True` に評価される必要があります。  
  
> [!NOTE]  
>  この種類の優先順位制約は、緑色、強調表示、または青色の実線で示されます。  
  
 **論理和**  
 同一の実行可能ファイルに対して、複数の優先順位制約を同時に評価することを指定する場合に選択します。 少なくとも 1 つの制約が `True` に評価される必要があります。  
  
> [!NOTE]  
>  この種類の優先順位制約は、緑色、強調表示、または青色の点線で示されます。  
  
## <a name="see-also"></a>参照  
 [優先順位制約](control-flow/precedence-constraints.md)   
 [Integration Services タスク](control-flow/integration-services-tasks.md)   
 [Integration Services コンテナー](control-flow/integration-services-containers.md)   
 [Integration Services &#40;SSIS&#41; 式](expressions/integration-services-ssis-expressions.md)  
  
  
