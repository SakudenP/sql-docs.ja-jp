---
title: 属性名とデータ型を変更する
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], changing name
ms.assetid: d348f238-f59d-41c7-ad20-3ccd55bfd9e5
author: lrtoyou1223
ms.author: lle
manager: erikre
ms.openlocfilehash: c5885c2aebb718f212ac22bee8773ceab2df2f6e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "73729680"
---
# <a name="change-an-attribute-name-and-data-type-master-data-services"></a>属性名とデータ型を変更する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、属性の名前を変更できます。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   [**システム管理**] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-change-an-attribute-name-and-type"></a>属性名と種類を変更するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  [**モデルの管理**] ページで、グリッドからモデルを選択し、[**エンティティ**] をクリックします。  
  
3.  **[エンティティの管理]** ページで、属性を作成するエンティティの行を選択します。  
  
4.  **[属性]** をクリックします。  
  
5.  **[属性の管理]** ページで、次のいずれかの操作を行います。  
  
    -   属性の対象がリーフ メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[リーフ]** を選択します。  
  
    -   属性の対象が統合メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[統合]** を選択します。  
  
    -   属性の対象がコレクションの場合、 **[メンバーの種類]** ボックスの一覧から **[コレクション]** を選択します。  
  
6.  編集する属性の行を選択し、 **[編集]** をクリックします。  
  
7.  **[名前]** ボックスに、属性の新しい名前を入力します。 属性名として使用しない単語の一覧については、「[予約語 &#40;マスターデータサービス&#41;](../master-data-services/reserved-words-master-data-services.md)」を参照してください。  
  
8.  **[属性の種類]** リストから、別の種類を選択します。  
  
9. **[Save]** (保存) をクリックします。  
  
## <a name="see-also"></a>参照  
 [テキスト属性 &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [属性 &#40;マスターデータサービスの削除&#41;](../master-data-services/delete-an-attribute-master-data-services.md)   
 [属性 (マスター データ サービス)](../master-data-services/attributes-master-data-services.md)  
  
  
