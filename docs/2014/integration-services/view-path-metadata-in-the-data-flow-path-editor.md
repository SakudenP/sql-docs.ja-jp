---
title: データフローパスエディターでパスのメタデータを表示する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- metadata [Integration Services]
- paths [Integration Services], metadata
ms.assetid: 25cf8bdd-8691-4caa-96b6-3081b2f37dea
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 16a86fa9098efcd6f4d8d46917df175667414dd9
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972492"
---
# <a name="view-path-metadata-in-the-data-flow-path-editor"></a>データ フロー パス エディターでパスのメタデータを表示する
  パスは、2 つのデータ フロー コンポーネントを連結します。 パスのメタデータを表示する場合、データ フローには、2 つ以上の連結されたデータ フロー コンポーネントをあらかじめ含めておく必要があります。 詳細については、「 [データ フローでコンポーネントを追加または削除する](data-flow/add-or-delete-a-component-in-a-data-flow.md) 」と「 [データ フロー内でコンポーネントを連結する](data-flow/connect-components-in-a-data-flow.md)」を参照してください。  
  
### <a name="to-view-path-metadata"></a>パスのメタデータを表示するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、パスをダブルクリックします。  
  
4.  **[データ フロー パス エディター]** ダイアログ ボックスで、 **[メタデータ]** をクリックします。  
  
5.  パスのメタデータが表示されます。メタデータには、各列の列名、データ型、有効桁数、小数点以下桁数、データ長、コード ページ、および基になるコンポーネントの名前が含まれます。  
  
6.  メタデータをコピーするには、 **[クリップボードにコピー]** をクリックします。  
  
7.  **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services パス](data-flow/integration-services-paths.md)   
 [データ フロー](data-flow/data-flow.md)  
  
  
