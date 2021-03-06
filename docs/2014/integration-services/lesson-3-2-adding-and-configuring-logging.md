---
title: 手順 2:ログ機能の追加と設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 23738ca4258bf61ff95087b1b6e2aeaffa97cafa
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440489"
---
# <a name="step-2-adding-and-configuring-logging"></a>手順 2:ログ機能の追加と設定
  ここでは、Lesson 3.dtsx パッケージのデータ フローのログを有効にします。 次に、PipelineExecutionPlan イベントと PipelineExecuteTrees イベントを記録するテキスト ファイル ログ プロバイダーを構成します。 テキスト ファイル ログ プロバイダーは、表示や移行が容易なログを作成します。 パッケージの基本テスト段階では、この簡潔なログ ファイルは特に便利です。 ログ エントリは、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの [ログ イベント] ウィンドウでも確認できます。  
  
### <a name="to-add-logging-to-the-package"></a>パッケージにログ機能を追加するには  
  
1.  次に、 **[SSIS]** メニューの **[ログ記録]** をクリックします。  
  
2.  **[SSIS ログの構成]** ダイアログ ボックスの **[コンテナー]** ペインで、一番上のパッケージ オブジェクト (Lesson 3) が選択されていることを確認します。  
  
3.  **[プロバイダーとログ]** タブで、 **[プロバイダーの種類]** ボックスの一覧から **[テキスト ファイルの SSIS ログ プロバイダー]** を選択し、 **[追加]** をクリックします。  
  
     新しいテキストファイルログプロバイダーをパッケージに追加します。既定の名前は、[**テキストファイルの SSIS ログプロバイダー**] です。 Integration Services 次に、この新しいログ プロバイダーを構成します。  
  
4.  [**名前**] 列に「」と入力 `Lesson 3 Log File` します。  
  
5.  必要に応じて、 **[説明]** の内容を修正します。  
  
6.  **[構成]** 列で **\<New Connection>** をクリックし、ログ情報を書き込む場所を指定します。  
  
     **[ファイル接続マネージャー エディター]** ダイアログ ボックスで、 **[使用法の種類]** ボックスの一覧から **[ファイルの作成]** を選択し、 **[参照]** をクリックします。 既定では、 **[ファイルの選択]** ダイアログ ボックスにこのプロジェクトのフォルダーが表示されますが、ログ情報を別の場所に保存することもできます。  
  
7.  [**ファイルの選択**] ダイアログボックスの [**ファイル名**] ボックスに、「」と入力し、 `TutorialLog.log` [**開く**] をクリックします。  
  
8.  **[OK]** をクリックして、 **[ファイル接続マネージャー エディター]** ダイアログ ボックスを閉じます。  
  
9. **[コンテナー]** ペインで、パッケージ コンテナー階層のすべてのノードを展開します。次に、 **[Extract Sample Currency Data]** チェック ボックスも含めすべてのチェック ボックスをオフにします。 次に、このノードのイベントのみを取得するため、 **[Extract Sample Currency Data]** チェック ボックスをオンにします。  
  
    > [!IMPORTANT]  
    >  **[Extract Sample Currency Data]** チェック ボックスがオフの状態で淡色表示になっている場合は、親コンテナーのログ設定が使用され、この作業用にログ イベントを有効にすることはできません。  
  
10. **[詳細]** タブの **[イベント]** 列で、 **[PipelineExecutionPlan]** イベントと **[PipelineExecutionTrees]** イベントのチェック ボックスをオンにします。  
  
11. **[詳細設定]** をクリックし、各イベントについて書き込まれるログ情報の詳細を確認します。 既定では、指定したイベントについて、すべての情報カテゴリが自動的に選択されます。  
  
12. **[標準]** をクリックして、情報カテゴリを非表示にします。  
  
13. [**プロバイダーとログ**] タブの [**名前**] 列で、[] を選択し `Lesson 3 Log File` ます。 目的のパッケージのログ プロバイダーを作成したら、必要に応じてログの記録を一時的にオフにすることができます。ログ プロバイダーを削除したり、再作成する必要はありません。  
  
14. **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 [手順 3:レッスン 3 のチュートリアル パッケージのテスト](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
  
