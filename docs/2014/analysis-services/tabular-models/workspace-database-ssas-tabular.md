---
title: ワークスペースデータベース (SSAS テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
author: minewiskan
ms.author: owend
ms.openlocfilehash: cd6d0a53894bb930c549df7b0e36dab83ed5d63e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938513"
---
# <a name="workspace-database-ssas-tabular"></a>ワークスペース データベース (SSAS テーブル)
  モデルの作成時に使用されるテーブル モデル ワークスペース データベースは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で新しいテーブル モデル プロジェクトを作成したときに作成されます。 ワークスペース データベースはテーブル モードで実行されている [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのメモリ内に存在します。通常は、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] と同じコンピューター上です。  
  
 このトピックのセクションは次のとおりです。  
  
-   [ワークスペース データベースの概要](#bkmk_overview)  
  
-   [ワークスペース データベースのプロパティ](#bkmk_ws_prop)  
  
-   [SSMS を使用したワークスペースデータベースの管理](#bkmk_use_ssms)  
  
-   [関連タスク](#bkmk_related_tasks)  
  
##  <a name="workspace-database-overview"></a><a name="bkmk_overview"></a>ワークスペースデータベースの概要  
 ワークスペース データベースは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のいずれかのテーブル モデル プロジェクト テンプレートを使用して新しい Business Intelligence プロジェクトを作成するときに、ワークスペース サーバーで指定された [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]インスタンスに作成されます。 各テーブル モデル プロジェクトには独自のワークスペース データベースがあります。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でワークスペース データベースを表示できます。 ワークスペース データベースの名前には、プロジェクト名、アンダースコア、ユーザー名、アンダースコア、GUID がこの順序で含まれています。  
  
 ワークスペース データベースは、テーブル モデル プロジェクトを [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で開いているときにメモリ内に存在します。 プロジェクトを閉じると、ワークスペース データベースは、メモリ内に保持されディスクに格納されてメモリから削除される (既定) か、ワークスペースの保有期間のプロパティで決められているとおりにメモリから削除されてディスクに格納されません。 ワークスペースの保有期間のプロパティの詳細については、このトピックの「 [ワークスペース データベースのプロパティ](#bkmk_ws_prop) 」を参照してください。  
  
 テーブルのインポート ウィザードを使用するか、コピー/貼り付けを行って、モデル プロジェクトにデータを追加後、モデル デザイナーでテーブル、列、およびデータを表示すると、ワークスペース データベースが表示されます。 追加のテーブル、列、リレーションシップなどを追加すると、ワークスペース データベースも変更されます。  
  
> [!IMPORTANT]  
>  膨大な数の行を格納するテーブルがモデルに存在する場合、モデルの作成中はデータの一部だけをインポートするようにお勧めします。 データの一部のみをインポートすることによって、処理時間を短縮し、ワークスペース データベースのサーバー リソースの消費を抑えることができます。  
  
> [!NOTE]  
>  テーブルのインポート ウィザード、[テーブルのプロパティの編集] ダイアログ ボックス、および [パーティション マネージャー] ダイアログ ボックスの [テーブルとビューの選択] ページのプレビュー ウィンドウには、データ ソースのテーブル、列、および行が表示されますが、ワークスペース データベースと同じテーブル、列、および行が表示されない場合があります。  
  
 テーブル モデル プロジェクトを配置すると、基本的にワークスペース データベースのコピーである配置済みのモデル データベースが、配置サーバー プロパティに指定された Analysis Services サーバー インスタンスに作成されます。 配置サーバー プロパティの詳細については、「[プロジェクトのプロパティ (SSAS テーブル)](properties-ssas-tabular.md)」を参照してください。  
  
 通常、モデル ワークスペース データベースは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーの localhost またはローカルの名前付きインスタンスに存在します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のリモート インスタンスを使用してワークスペース データベースをホストできますが、データのクエリ中の待機時間とその他の制約のため、この構成はお勧めしません。 最適に、ワークスペース データベースをホストする [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスが [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]と同じコンピューター上にあります。 ワークスペース データベースをホストする [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスと同じコンピューター上にモデル プロジェクトを作成すると、パフォーマンスが向上します。  
  
 リモートのワークスペース データベースには、次の制約があります。  
  
-   クエリ中に待機時間が発生する可能性があります。  
  
-   データ バックアップ プロパティを **[ディスクにバックアップする]** に設定できません。  
  
-   PowerPivot からのインポート プロジェクト テンプレートを使用して新しいテーブル モデル プロジェクトを作成するときに、PowerPivot ブックからデータをインポートすることはできません。  
  
##  <a name="workspace-database-properties"></a><a name="bkmk_ws_prop"></a>ワークスペースデータベースのプロパティ  
 ワークスペース データベースのプロパティは、モデルのプロパティに含まれます。 モデルのプロパティを表示するには、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]の **ソリューション エクスプローラー**で **Model.bim** ファイルをクリックします。 モデルのプロパティは **[プロパティ]** ウィンドウを使用して構成できます。 ワークスペース データベース固有のプロパティには、次のものが含まれます。  
  
> [!NOTE]  
>  **[ワークスペース サーバー]**、 **[ワークスペースの保有期間]**、および **[データ バックアップ]** の各プロパティには、新しいモデル プロジェクトを作成するときに既定の設定が適用されます。 [ツール] メニューから開く [オプション] ダイアログ ボックスで、 **[分析サーバー]** 設定の **[データ モデリング]** ページを使用して、新しいモデル プロジェクトの既定の設定を変更できます。 他のプロパティと同様に、これらのプロパティは **[プロパティ]** ウィンドウでモデル プロジェクトごとに設定することもできます。 既定の設定の変更は、作成済みのモデル プロジェクトには適用されません。 詳細については、「 [既定のデータ モデルと配置プロパティの構成 &#40;SSAS テーブル&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)」を参照してください。  
  
|プロパティ|既定の設定|説明|  
|--------------|---------------------|-----------------|  
|**ワークスペースデータベース**|プロジェクト名、アンダースコア、ユーザー名、アンダースコア、GUID がこの順序で含まれています。|インメモリ モデル プロジェクトを格納および編集する際に使用されるワークスペース データベースの名前です。 テーブル モデル プロジェクトの作成後、このデータベースは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [ワークスペース サーバー] **プロパティに指定された** インスタンスに表示されます。 このプロパティを [プロパティ] ウィンドウで設定することはできません。|  
|**ワークスペースの保有期間**|メモリ内でアンロード|モデル プロジェクトが閉じられた後でワークスペース データベースを保持する方法を指定します。 ワークスペース データベースには、モデル メタデータとインポートされたデータが含まれています。 場合によっては、ワークスペース データベースは非常に大きくなり、大量のメモリを消費することがあります。 既定では、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]でモデル プロジェクトを閉じると、ワークスペース データベースはメモリからアンロードされます。 この設定を変更するときには、使用可能なメモリ リソースと、モデル プロジェクトに対する作業を行う頻度を考慮することが重要です。 このプロパティの設定には、以下のオプションがあります。<br /><br /> **メモリに保持** - モデル プロジェクトを閉じた後もワークスペース データベースをメモリ内に保持するように指定します。 このオプションはより多くのメモリを消費しますが、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]でモデル プロジェクトを開くときのリソース消費が少なくて済み、ワークスペース データベースの読み込みも高速になります。<br /><br /> **メモリからアンロード** - モデル プロジェクトを閉じた後、ワークスペース データベースをディスク上に保持し、メモリには残さないように指定します。 このオプションはメモリの消費量は比較的少なくて済みますが、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]でモデル プロジェクトを開くときにワークスペース データベースを再度接続する必要があるため、リソース消費が増え、ワークスペース データベースをメモリ内に保持した場合と比べて、モデル プロジェクトの読み込みにも時間がかかるようになります。 メモリ内のリソースが制限されている場合、またはリモートのワークスペース データベースで作業する場合に、このオプションを使用します。<br /><br /> **ワークスペースの削除** - モデル プロジェクトを閉じた後、メモリからワークスペース データベースを削除し、ディスク上にもワークスペース データベースを保持しないように指定します。 このオプションはメモリとストレージ領域の消費量が比較的少なくて済みますが、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]でモデル プロジェクトを開くときのリソース消費が増え、ワークスペース データベースをメモリ内やディスク上に保持した場合と比べて、モデル プロジェクトの読み込みにも時間がかかるようになります。 このオプションは、モデル プロジェクトの使用時、必要な場合にのみ使用してください。<br /><br /> <br /><br /> このプロパティの既定の設定は、[ツール] メニューから開く [オプション] ダイアログボックスの**分析サーバー**設定の [**データモデリング**] ページで変更できます。|  
|**ワークスペース サーバー**|localhost|このプロパティは、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]でモデル プロジェクトが作成されるときにワークスペース データベースをホストするのに使用される既定のサーバーを指定します。 ローカル コンピューターで実行されている [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の使用可能なすべてのインスタンスが、このボックスの一覧に表示されます。<br /><br /> テーブル モードで実行されている別の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーを指定するには、サーバー名を入力します。 ログオンするユーザーは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーの管理者である必要があります。<br /><br /> ローカル [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーをワークスペースサーバーとして指定することをお勧めします。 リモート サーバー上のワークスペース データベースでは、PowerPivot からのインポートはサポートされておらず、データはローカルにバックアップされず、クエリ中にユーザー インターフェイスで遅延が発生する場合があります。<br /><br /> また、このプロパティの既定の設定は、[ツール] メニューから開く [オプション] ダイアログボックスの [設定] の [データモデリング] ページでも変更でき [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ます。|  
  
##  <a name="using-ssms-to-manage-the-workspace-database"></a><a name="bkmk_use_ssms"></a> SSMS を使用したワークスペース データベースの管理  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) を使用して、ワークスペース データベースをホストする [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーに接続できます。 通常、ワークスペース データベースは必ずしも管理されません。例外は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から実行する必要のあるワークスペース データベースのデタッチまたは削除です。  
  
> [!WARNING]  
>  モデル デザイナーでプロジェクトを開いているときに、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してワークスペース データベースを管理しないでください。 このような操作により、データが失われることがあります。  
  
##  <a name="related-tasks"></a><a name="bkmk_related_tasks"></a> 関連タスク  
  
|トピック|説明|  
|-----------|-----------------|  
|[モデルのプロパティ (SSAS テーブル)](model-properties-ssas-tabular.md)|モデルのワークスペースデータベースのプロパティの説明と構成手順について説明します。|  
  
## <a name="see-also"></a>参照  
 [SSAS 表形式&#41;&#40;既定のデータモデルと配置プロパティの構成](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [プロジェクトのプロパティ (SSAS テーブル)](properties-ssas-tabular.md)  
  
  
