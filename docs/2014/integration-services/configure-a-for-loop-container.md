---
title: For ループコンテナーを構成する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: b9cd7ea7-b198-4a35-8b16-6acf09611ca5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 24e2fe71b958395a5be35afad32804d2a748348d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921983"
---
# <a name="configure-a-for-loop-container"></a>For ループ コンテナーを構成する
  この手順では、 **[For ループ エディター]** ダイアログ ボックスを使用して、For ループ コンテナーを構成する方法について説明します。  
  
### <a name="to-configure-the-for-loop-container"></a>For ループ コンテナーを構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、For ループ コンテナーをダブルクリックして **[For ループ エディター]** を開きます。  
  
2.  必要に応じて、For ループ コンテナーの名前と説明を変更します。  
  
3.  必要に応じて、 **[InitExpression]** テキスト ボックスに初期化式を入力します。  
  
4.  **[EvalExpression]** テキスト ボックスに、評価式を入力します。  
  
    > [!NOTE]  
    >  式はブール値に評価される必要があります。 式が `false` に評価されると、ループは実行を停止します。  
  
5.  必要に応じて、 **[AssignExpression]** テキスト ボックスに代入式を入力します。  
  
6.  必要に応じて、 **[式]** をクリックし、 **[式]** ページで For ループ コンテナーのプロパティ用のプロパティ式を作成します。 詳細については、「 [プロパティ式を追加または変更する](expressions/add-or-change-a-property-expression.md)」を参照してください。  
  
7.  **[OK]** をクリックし、 **[For ループ エディター]** を閉じます。  
  
## <a name="see-also"></a>参照  
 [For ループコンテナー](control-flow/for-loop-container.md)   
 [SSIS&#41; 式の Integration Services &#40;](expressions/integration-services-ssis-expressions.md)   
 [パッケージでプロパティ式を使用する](expressions/use-property-expressions-in-packages.md)  
  
  
