---
title: 照合ポリシーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.kbmatchingresults.f1
- sql12.dqs.kb.kbmatchingmap.f1
- sql12.dqs.kb.kbmatchingpolicy.f1
ms.assetid: cce77a06-ca31-47b6-8146-22edf001d605
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f2f6a9b3b8e5e1f63a2c539c710b03375b7061fd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937883"
---
# <a name="create-a-matching-policy"></a>照合ポリシーの作成
  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でナレッジ ベースの照合ポリシーを作成する方法について説明します。 サンプル データに対して照合ポリシー アクティビティを実行して、DQS の照合プロセスの準備を行います。 このアクティビティでは、まず、ポリシーの照合ルールを 1 つ以上作成してテストします。次に、ナレッジ ベースを発行して、それらの照合ルールを使用できるように公開します。 ナレッジ ベースで作成できる照合ポリシーは 1 つだけですが、そのポリシーに複数の照合ルールを含めることができます。  
  
 照合ポリシーを作成する手順は、データ ソースを特定してドメインを列にマップするマップ プロセス、1 つ以上の照合ルールを作成してそれぞれを個別にテストする照合ポリシー プロセス、およびすべての照合ルールをまとめて実行し、問題がなければポリシーをナレッジ ベースに追加する照合結果プロセスの 3 つのステージで構成されます。 照合ポリシー アクティビティのウィザードでは、これらの各プロセスをそれぞれ異なるページで実行します。前後の各ページに移動したり、プロセスを再実行したり、特定の照合ポリシー プロセスを完了した後にそのプロセスの同じステージに戻ることも可能です。 すべてのルールをまとめてテストした後、必要に応じて **[照合ポリシー]** ページに戻り、個々のルールを調整して再び個別にテストすることもできます。その後、 **[照合結果]** ページに戻り、もう一度すべてのルールをまとめて実行します。 DQS から提供されるソース データ、照合ルール、および照合結果に関する統計情報に基づいて照合ポリシーに関する決定を行い、照合ポリシーを調整することができます。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 ソース データが Excel ファイルに含まれている場合は、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] コンピューターに Microsoft Excel がインストールされている必要があります。 Excel がインストールされていないと、マップ ステージで Excel ファイルを選択できません。 Microsoft Excel で作成されるファイルの拡張子は、.xlsx、.xls、または .csv です。 64 ビット バージョンの Excel を使用する場合は、Excel 2003 ファイル (.xls) のみがサポートされます。Excel 2007 または 2010 ファイル (.xlsx) はサポートされません。 64 ビット バージョンの Excel 2007 または 2010 を使用している場合は、ファイルを .xls ファイルまたは .csv ファイルとして保存するか、32 ビット バージョンの Excel をインストールしてください。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 照合ポリシーを作成するには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="how-to-set-matching-rule-parameters"></a><a name="MatchingRules"></a>照合ルールのパラメーターを設定する方法  
 照合ルールを作成する際には、2 つのレコードが一致しているかどうかの確認に使用される要素を反復的なプロセスで入力します。 テーブル内の任意のドメインの条件を入力できます。 DQS で 2 つのレコードが照合される際には、照合ルールに含まれているドメインにマップされているフィールドの値が比較されます。 ルールの各フィールドの値が分析され、ルールで各ドメインに対して入力した要素を使用して最終的な照合スコアが計算されます。 比較された 2 つのレコードの照合スコアが最小照合スコアより大きい場合、その 2 つのフィールドは一致と見なされます。  
  
 照合ルールで入力する要素を以下に示します。  
  
-   重み: ルールに含まれている各ドメインの重みを表す数値を入力します。これにより、ルールに含まれている各ドメインの照合分析の相対的な重要度が決まります。 重みは、そのフィールドのスコアが 2 つのレコードの照合スコア全体に与える影響を示します。 各ソース フィールドに割り当てられた計算済みのスコアが集計されて、2 つのレコードの複合的な照合スコアが特定されます。 前提条件ではない各フィールド (類似性が "完全一致" または "部分一致" のフィールド) に対して、10 ～ 100 の重みを設定します。 前提条件ではないドメインの重みの合計が 100 になるようにする必要があります。 値が前提条件である場合、重みは 0 に設定され、変更できません。  
  
-   "完全一致" の類似性: 2 つの異なるレコードの同じフィールドの値が一致と見なされるためには値が同一でなければならない場合は、 **[完全一致]** を選択します。 値が同一である場合は、そのドメインの照合スコアが "100" に設定され、そのスコアとルール内の他のドメインのスコアを使用して合計照合スコアが特定されます。 値が同一でない場合は、そのドメインの照合スコアが "0" に設定され、ルールの次の条件が処理されます。 数値ドメインの照合ルールを設定し、 **[部分一致]** を選択した場合は、パーセンテージまたは整数の許容範囲を入力できます。 日付型のドメインで **[部分一致]** を選択した場合は、日、月、または年 (整数) の許容範囲を入力できます。日付ドメインにはパーセンテージの許容範囲はありません。 このオプションは、 **[完全一致]** を選択した場合には使用できません。  
  
-   "部分一致" の類似性: 2 つの異なるレコードの同じフィールドの値が同一でなくても一致と見なされうる場合は、 **[部分一致]** を選択します。 ルールが実行されると、そのドメインの照合スコアが計算され、そのスコアとルール内の他のドメインのスコアを使用して合計照合スコアが特定されます。 フィールドの値の最小類似は 60% です。 2 つのレコードのフィールドに対して計算された照合スコアが 60 未満だった場合は、類似性スコアが自動的に 0 に設定されます。 数値フィールドの照合ルールを設定し、 **[部分一致]** を選択した場合は、パーセンテージまたは整数の許容範囲を入力できます。 日付フィールドの照合ルールを設定し、 **[部分一致]** を選択した場合は、数値の許容範囲を入力できます。  
  
-   前提条件: 2 つの異なるレコードの同じフィールドの値の一致率が 100% でなければそれらのレコードを一致と見なさず、ルールの他の句を無視する場合は、 **[前提条件]** を選択します。 **[前提条件]** を選択すると、そのドメインの重みのフィールドが削除されて、そのドメインの重みを定義できなくなります。 重みの合計が 100 になるように、1 つまたは複数のドメインの重みを設定し直す必要があります。 前提条件のドメインは、レコードの照合スコアに影響しません。 レコードの照合スコアは、[類似性] が [部分一致] または [完全一致] に設定されているフィールドの値を比較することによって決定されます。 フィールドを前提条件にすると、そのドメインの [類似性] が自動的に [完全一致] に設定されます。  
  
 最小照合スコアは、値がそれ以上の場合に 2 つのレコードが一致と見なされる (レコードの状態が "一致" に設定される) しきい値です。 値を整数で入力するか ("1" 刻み)、上下の矢印をクリックして設定します ("10" ずつ増減)。 最小値は 80 です。 照合スコアが 80 未満の場合、2 つのレコードは一致と見なされません。 このページで最小照合スコアの範囲を変更することはできません。 最小照合スコアの最小値は 80 です。 ただし、管理ページで最小照合スコアの最小値を変更できます (DQS 管理者である場合)。  
  
 照合ルールの作成は、反復的なプロセスです。必要な結果を得るためには、ルールに含まれているドメインの相対的な重み、ドメインの類似性や前提条件のプロパティ、またはルールの最小照合スコアを変更しなければならなくなる場合があるためです。 複数のルールを作成し、各ルールを実行して照合スコアが作成されるようにする必要がある場合もあります。 1 つのルールでは必要な結果を得るのが難しい場合でも、 複数のルールを使用すると、必要な一致をさまざまな角度から分析できます。 複数のルールを使用すると、各ルールのドメインの数を減らして、各ドメインの重みの値を高くすることができるため、結果が改善される可能性があります。 必要な一致を見つけるために必要なルールの数は、データの精度や完全性が低いほど多くなり、 データの精度や完全性が高いほど少なくなります。  
  
 プロファイリングでは、完全性と一意性について調査できます。 完全性と一意性は、同時に検討する必要があります。 照合プロセスでフィールドに適用する重みを決定する際には、完全性と一意性のデータを使用します。 一意性が高いフィールドを照合ポリシーで使用する場合は、一致する結果が少なくなる可能性があるため、そのフィールドの重みを比較的小さな値に設定します。 一意性も完全性も低い列のドメインは含めないようにし、 一意性は低いが完全性は高い場合は含めるようにします。 性別など、一意性が必然的に低くなる列もあります。 詳細については、「 [[プロファイラー] タブと [結果] タブ](#Tabs)」をご参照ください。  
  
##  <a name="first-step-starting-a-matching-policy"></a><a name="Starting"></a> 最初の手順: 照合ポリシーの開始  
 照合ポリシー アクティビティは、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションのナレッジ ベース管理領域で実行します。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../../2014/data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  新しいナレッジ ベースの照合ポリシーを作成する場合は、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で **[新しいナレッジ ベース]** をクリックします。 ナレッジ ベースの名前を入力し、説明を入力して、必要に応じて **[次の場所からナレッジ ベースを作成]** を設定します。 アクティビティとして **[照合ポリシー]** をクリックし、 **[次へ]** をクリックします。  
  
3.  既存のナレッジ ベースの照合ポリシーを作成または変更する場合は、 **[ナレッジ ベースを開く]** をクリックします。 ナレッジ ベースを選択し、 **[照合ポリシー]** を選択して、 **[次へ]** をクリックします。 **[最近使用したナレッジ ベース]** でナレッジ ベースをクリックすることもできます。 照合ポリシー アクティビティの途中で閉じられたナレッジ ベースを開くと、閉じられたときのステージ (ナレッジ ベース テーブルのそのナレッジ ベースの **[状態]** 列または **[最近使用したナレッジ ベース]** のナレッジ ベース名に示されます) に移動します。 照合ポリシーが含まれている完了済みのナレッジ ベースを開くと、 **[照合ポリシー]** ページに移動します。 照合ポリシーが含まれていない完了済みのナレッジ ベースを開くと、 **[マッピング]** ページに移動します。  
  
##  <a name="mapping-stage"></a><a name="MatchingStage"></a> マップ ステージ  
 マップ ステージでは、照合ポリシーを作成するデータのソースを特定し、ドメインを照合ポリシー アクティビティで使用できるようにソース列をドメインにマップします。  
  
1.  データベースのポリシーを作成する場合は、 **[マップ]** ページで **[データ ソース]** を **[SQL Server]** のままにして、 **[データベース]** でポリシーを作成するデータベースを選択し、 **[テーブル/ビュー]** でテーブルまたはビューを選択します。 ソース データベースは、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]と同じ SQL Server インスタンス上に存在する必要があります。 それ以外の場合、データベースはドロップダウン リストに表示されません。  
  
2.  Excel ワークシートのデータのポリシーを作成する場合は、 **[データ ソース]** で **[Excel ファイル]** を選択し、 **[参照]** をクリックして Excel ファイルを選択します。必要に応じて、 **[先頭の行を見出しとして使用]** は選択したままにします。 **[ワークシート]** で、データのソースとなる Excel ファイルのワークシートを選択します。 Excel ファイルを選択するには、Data Quality Client コンピューターに Microsoft Excel がインストールされている必要があります。 インストールされていない場合は、[参照] ボタンを使用できません。Microsoft Excel がインストールされていないことを通知するメッセージが、このテキスト ボックスの下に表示されます。  
  
3.  **[マッピング]** の **[ソース列]** でフィールドを選択し、 **[ドメインの作成]** アイコンをクリックします。  
  
4.  **[マッピング]** の **[ソース列]** でデータ ソースのフィールドを選択し、対応するドメインを選択します。 照合プロセスで使用するすべてのドメインについて繰り返します。 必要に応じて、 **[ドメインの作成]** または **[複合ドメインの作成]** をクリックしてドメインを作成します。  
  
    > [!NOTE]  
    >  照合ポリシーの作成時にソース データを DQS ドメインにマッピングできるのは、ソースのデータ型が DQS でサポートされていて、なおかつ DQS ドメインのデータ型と一致する場合だけです。 DQS でサポートされるデータ型の詳細については、「 [DQS ドメインに対してサポートされる SQL Server のデータ型と SSIS のデータ型](../../2014/data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md)」を参照してください。  
  
5.  マッピング テーブルに行を追加するには、**プラス記号 (+)** コントロールをクリックします。行を削除するには、**マイナス記号 (-)** コントロールをクリックします。  
  
6.  選択した SQL Server のテーブルやビューのデータ、または選択した Excel ワークシートのデータを表示するには、 **[データ ソースのプレビュー]** をクリックします。  
  
7.  ナレッジ ベースで使用できる複合ドメインの一覧を表示し、必要に応じてマップするものを選択するには、 **[複合ドメインの表示と選択]** をクリックします。  
  
8.  **[次へ]** をクリックして照合ポリシー ステージに進みます。  
  
    > [!NOTE]  
    >  **[閉じる]** をクリックすると、照合プロジェクトのステージが保存され、DQS ホーム ページに戻ります。 次回このプロジェクトを開いたとき、プロジェクトは同じステージから開始されます。 **[キャンセル]** をクリックすると、照合アクティビティが終了して作業内容が破棄され、DQS ホーム ページに戻ります。  
  
##  <a name="matching-policy-stage"></a><a name="MatchingPolicyStage"></a> 照合ポリシー ステージ  
 [照合ポリシー] ページで、照合ルールを作成して個別にテストします。 **[照合ポリシー]** ページで照合ルールをテストすると、選択したルールに対して特定されたクラスターが照合結果のテーブルに表示されます。 このテーブルには、クラスターの各レコードが、マップされるドメイン値および照合スコアと共に表示されるほか、クラスターの最初のピボット レコードも表示されます。 照合プロセス全体のプロファイル データ、各照合ルールの条件、および各照合ルールの個別の結果に関する統計情報を表示することもできます。 マスター ルール データにフィルターを適用することもできます。  
  
 照合ルールの動作の詳細については、「 [照合ルールのパラメーターを設定する方法](#MatchingRules)」をご参照ください。  
  
1.  **[照合ポリシー]** ページで、 **[照合ルールを作成します]** アイコンをクリックします。  
  
2.  ルールの名前と説明を入力します。  
  
3.  照合要件を厳しくする場合は、 **[最小の照合スコア]** の値を大きくします。 最小照合スコアの詳細については、「 [照合ルールのパラメーターを設定する方法](#MatchingRules)」をご参照ください。  
  
4.  **[新しいドメイン要素を追加します]** アイコンをクリックします。  
  
5.  ルールの値を入力するドメインまたは複合ドメインを選択します。  
  
    > [!NOTE]  
    >  複合ドメインは、その複合ドメイン内の各単一ドメインがソース列にマップされている場合にのみ選択できます。  
  
6.  **[類似性]** で、2 つの異なるレコードの同じフィールドの値が同一でなくても一致と見なされうる場合は **[部分一致]** を選択し、 2 つの異なるレコードの同じフィールドの値が一致と見なされるためには値が同一でなければならない場合は **[完全一致]** を選択します 詳細については、「 [照合ルールのパラメーターを設定する方法](#MatchingRules)」をご覧ください。  
  
7.  **[重み]** で、ドメインの照合スコアが 2 つのレコードの照合スコア全体に与える影響を決定する値を入力します。  
  
    > [!NOTE]  
    >  複合ドメインの重みを定義するときには、複合ドメイン内の各単一ドメインの重みを個別に入力することも (この場合、複合ドメインの重みは指定しません)、複合ドメインに対して単一の重みを入力することもできます (この場合、複合ドメイン内の単一ドメインの重みは指定しません)。  
  
8.  2 つのレコードのフィールドの値の一致率が 100% でなければそれらのレコードを一致と見なさず、ルールの他の句を無視する場合は、 **[前提条件]** を選択します。 **[類似性]** が **[部分一致]** になっている場合は **[完全一致]** に変更され、重みが削除されます (一致率が 100% でなければならないため)。  
  
9. 照合ルールに含める他のすべてのドメインに対して、手順 4. ～ 8. を繰り返します。 ルールに含まれているすべてのドメインの重みの合計が 100 になるようにします。  
  
10. 照合の実行時に、クラスターのグループに共通のレコードがあるかどうかに関係なく、すべてのクラスターのピボット レコードとそれに従ったレコードを表示する場合は、ドロップダウン リストから **[重複するクラスター]** を選択します。 **[重複しないクラスター]** を選択すると、照合の実行時に、共通のレコードを持つクラスターが 1 つのクラスターとして表示されます。  
  
11. 照合ポリシーの実行時に、データ ソースからステージング テーブルにデータをコピーしてインデックスを再作成する場合は、 **[ソースからデータを再読み込み]** をクリックします。 ステージング テーブルへのデータのコピーとインデックスの再作成を行わずに照合ポリシーを実行する場合は、 **[以前のデータで実行]** をクリックします。 **[以前のデータで実行]** は、照合ポリシーの初回実行時は無効になります。また、 **[マップ]** ページでマッピングを変更した後に、ポップアップ画面で **[はい]** をクリックした場合も無効になります。 この場合はどちらも、インデックスを再作成する必要があります。 照合ポリシーに変更がなければ、インデックスを再作成する必要はありません。 以前のデータで実行するとパフォーマンスの向上に役立ちます。  
  
12. 選択したルールの照合プロセスを実行するには、 **[開始]** をクリックします。 プロセスが完了すると、クラスター内の各レコードのレコード ID、クラスター番号、およびデータ列 (照合ルールに含まれていない列を含む) がテーブルに表示されます。 クラスター内のピボット行は、重複除去プロセスで保持される最有力候補と見なされます。 クラスター内のその他の各行は重複と見なされ、照合スコア (ピボット レコードとの比較) が結果テーブルに表示されます。 クラスター番号は、クラスター内のピボット レコードのレコード ID と同じになります。  
  
13. **"照合結果"** テーブルのデータは、次のように操作することができます。  
  
    -   **[フィルター]** で **[一致]** を選択すると、一致しているすべての行とそのスコアが表示されます。 一致と見なされない行 (照合スコアが最小照合スコアを下回る行) は表示されません。 **[不一致]** を選択すると、一致している行ではなく、一致していないすべての行が表示されます。  
  
    -   **[パーセント]** ボックスの一覧で、パーセンテージ ("5" 刻み) を選択します。 選択したパーセンテージ以上の照合スコアを持つすべての行が照合結果テーブルに表示されます。  
  
    -   照合結果テーブルのレコードをダブルクリックすると、 **[照合スコアの詳細]** ポップアップが表示され、ピボット レコードとソース レコード (およびそれらのフィールドの値)、それらのレコード間のスコア、およびレコード照合のドリルダウンが表示されます。 ドリルダウンでは、ピボット レコードとソース レコードの各フィールドの値が表示されるため、それらを比較することができます。2 つのレコードの照合スコア全体に占める各フィールドの照合スコアも確認できます。  
  
14. **[プロファイラー]** タブと **[照合結果]** タブで統計情報を表示して、必要な結果が得られたことを確認します。 詳細については、「 [[プロファイラー] タブと [結果] タブ](#Tabs)」をご参照ください。  
  
15. ルールを変更する必要がある場合は、ルール エディターで変更して、 **[再起動]** をクリックします。  
  
    > [!NOTE]  
    >  初回の分析が完了すると、 **[開始]** ボタンが **[再起動]** ボタンに変わります。 前回の分析の結果がまだ保存されていない場合は、 **[再起動]** をクリックすると前のデータが失われます。 分析の実行中にページを移動しないでください。ページを移動すると、分析プロセスが終了します。  
  
16. **[照合結果]** タブには、ルールの過去 2 回の実行の統計情報が表示されます。 照合ルールを異なる設定で複数回実行すると、現在のルールと以前のルールの統計情報を比較することができます。 以前のルールの方が結果が良かった場合は、 **[以前のルールを復元]** をクリックして以前のルールの条件を復元し、ルールを編集前の状態に戻します。 現在のルールの条件は失われます。 これにより、過去 2 回の照合結果に基づいてポリシーを調整できるため、照合ポリシーの調整に費やされる時間を短縮できます。  
  
17. 照合ポリシーに別のルールを追加する場合は、この手順を手順 1. から繰り返します。  
  
18. **[次へ]** をクリックして照合結果ステージに進みます。  
  
##  <a name="matching-results-stage"></a><a name="MatchingResultsStage"></a> 照合結果ステージ  
 **[照合結果]** ページでは、すべての照合ルールを一度にテストします。 ルールのテストを実行する前に、重複するクラスターと重複しないクラスターのどちらを特定するかを指定できます。 ルールを複数回実行する場合は、ソースから再読み込みされたデータに対して実行するか、以前のデータに対して実行するかも指定できます。  
  
 **[照合結果]** ページで照合ルールをテストすると、すべてのルールに対して特定されたクラスターが照合結果のテーブルに表示されます。 このテーブルには、クラスターの各レコードが、マップされるドメイン値および照合スコアと共に表示されるほか、クラスターの最初のピボット レコードも表示されます。 照合ルール全体のプロファイル データ、各照合ルールの条件、およびすべての照合ルールの結果に関する統計情報を表示することもできます。  
  
1.  **[照合結果]** ページで、ドロップダウン リストから **[重複するクラスター]** を選択すると、照合の実行時に、クラスターのグループに共通のレコードがあるかどうかに関係なく、すべてのクラスターのピボット レコードとそれに従ったレコードが表示されます。 **[重複しないクラスター]** を選択すると、照合の実行時に、共通のレコードを持つクラスターが 1 つのクラスターとして表示されます。  
  
2.  照合ポリシーの実行時に、データ ソースからステージング テーブルにデータをコピーしてインデックスを再作成する場合は、 **[ソースからデータを再読み込み]** をクリックします。 ステージング テーブルへのデータのコピーとインデックスの再作成を行わずに照合ポリシーを実行する場合は、 **[以前のデータで実行]** をクリックします。 **[以前のデータで実行]** は、照合ポリシーの初回実行時は無効になります。また、 **[マップ]** ページでマッピングを変更した後に、ポップアップ画面で **[はい]** をクリックした場合も無効になります。 この場合はどちらも、インデックスを再作成する必要があります。 照合ポリシーに変更がなければ、インデックスを再作成する必要はありません。 以前のデータで実行するとパフォーマンスの向上に役立ちます。  
  
3.  定義したすべてのルールの照合プロセスを実行するには、 **[開始]** をクリックします。 クラスター内の各レコードのレコード ID、クラスター番号、およびデータ列 (照合ルールに含まれていない列を含む) が **"照合結果"** テーブルに表示されます。 クラスターの先頭レコードはランダムに選択されます (残りのレコードを確認するには、照合プロジェクトの実行時に [**エクスポート**] ページで [サバイバーシップ] 規則を選択します)。クラスター内のその他の各行は重複していると見なされます。結果テーブルには、照合スコア (ピボットレコードと比較) が表示されます。  
  
4.  **"照合結果"** テーブルのデータは、次のように操作することができます。  
  
    -   **[フィルター]** で **[一致]** を選択すると、一致しているすべての行とそのスコアが表示されます。 一致と見なされない行 (照合スコアが最小照合スコアを下回る行) は表示されません。 **[不一致]** を選択すると、一致している行ではなく、一致していないすべての行が表示されます。  
  
    -   **[パーセント]** ボックスの一覧で、パーセンテージ ("5" 刻み) を選択します。 選択したパーセンテージ以上の照合スコアを持つすべての行が照合結果テーブルに表示されます。  
  
    -   照合結果テーブルのレコードをダブルクリックすると、 **[照合スコアの詳細]** ポップアップが表示され、ピボット レコードとソース レコード (およびそれらのフィールドの値)、それらのレコード間のスコア、およびレコード照合のドリルダウンが表示されます。 ドリルダウンでは、ピボット レコードとソース レコードの各フィールドの値が表示されるため、それらを比較することができます。2 つのレコードの照合スコア全体に占める各フィールドの照合スコアも確認できます。  
  
5.  **[プロファイラー]** タブと **[照合結果]** タブで統計情報を表示して、必要な結果が得られたことを確認します。 各ルールのドメインの設定を確認するには、 **[照合ルール]** タブをクリックします。 詳細については、「 [[プロファイラー] タブと [結果] タブ](#Tabs)」をご参照ください。  
  
6.  すべてのルールの結果に満足できない場合は、 **[戻る]** をクリックして **[照合ポリシー]** ページに戻り、必要に応じてルールを変更します。その後、 **[照合結果]** ページに戻って **[再起動]** をクリックします。  
  
    > [!NOTE]  
    >  分析が完了すると、 **[開始]** ボタンが **[再起動]** ボタンに変わります。 前回の分析の結果がまだ保存されていない場合は、 **[再起動]** をクリックすると前のデータが失われます。  
  
7.  すべてのルールの結果に問題がなければ、 **[完了]** をクリックして照合ポリシー プロセスを完了し、次のいずれかをクリックします。  
  
    -   **[はい - ナレッジ ベースを発行して終了]**: 現在のユーザーまたは他のユーザーに対してナレッジ ベースが発行されます。 ナレッジ ベースはロックされず、(ナレッジ ベース テーブルの) ナレッジ ベースの状態が空白に設定されます。ドメイン管理アクティビティとナレッジ検出アクティビティの両方を使用できるようになります。 [ナレッジ ベースを開く] 画面に戻ります。  
  
    -   **[いいえ - 作業内容をナレッジ ベースに保存して終了]**: 作業内容が保存され、ナレッジ ベースはロックされたままになります。ナレッジ ベースの状態は **[作業中]** に設定されます。 ドメイン管理アクティビティとナレッジ検出アクティビティの両方を使用できるようになります。 ホーム ページに戻ります。  
  
    -   **[キャンセル]-現在の画面に表示**されます。ポップアップは閉じられ、[ドメイン管理] 画面に戻ります。  
  
8.  作業内容を保存して DQS ホーム ページに戻るには、 **[閉じる]** をクリックします。 ナレッジ ベースの状態として、"ポリシーの照合 - " という文字列と現在の状態が表示されます。 **[照合結果]** 画面で **[閉じる]** をクリックした場合は、"ポリシーの照合 - 結果" と表示されます。 **[照合ポリシー]** 画面で [閉じる] をクリックした場合は、"ポリシーの照合 - ポリシーの照合" と表示されます。 **[閉じる]** をクリックした後で **[ナレッジ検出]** アクティビティを実行するには、 **[照合ポリシー]** アクティビティに戻り、 **[完了]** をクリックします。次に、ナレッジ ベースを発行する場合は **[はい]** を、作業内容をナレッジ ベースに保存して終了する場合は **[いいえ]** をクリックします。  
  
    > [!NOTE]  
    >  照合プロセスの実行中に **[閉じる]** をクリックした場合は、 **[閉じる]** をクリックしても照合プロセスは終了しません。 再びナレッジ ベースを開くと、プロセスがまだ実行されているかどうかを確認できます。プロセスが完了している場合は結果が表示されます。 プロセスが完了していない場合は進行状況が表示されます。  
  
9. 照合ポリシー アクティビティを終了し、作業内容を破棄して DQS ホーム ページに戻るには、 **[キャンセル]** をクリックします。  
  
##  <a name="follow-up-after-creating-a-matching-policy"></a><a name="FollowUp"></a> 補足情報: 照合ポリシーの作成後  
 照合ポリシーを作成したら、その照合ポリシーを含むナレッジ ベースに基づいて照合プロジェクトを実行できます。 詳細については、「 [照合プロジェクトの実行](../../2014/data-quality-services/run-a-matching-project.md)」をご参照ください。  
  
##  <a name="profiler-and-results-tabs"></a><a name="Tabs"></a> [プロファイラー] タブと [結果] タブ  
 [プロファイラー] タブと [結果] タブには、[照合ポリシー] と [照合結果] の両方のページの統計情報が含まれています。  
  
###  <a name="profiler-tab"></a><a name="Profiler"></a> [プロファイラー] タブ  
 **[プロファイラー]** タブをクリックすると、ソース データベースの統計情報とポリシーのルールに含まれる各フィールドの統計情報が表示されます。 これらの統計情報は、ポリシーのルールを実行すると更新されます。  
  
 以下の統計情報の解釈に関する詳細については、「 [照合ルールのパラメーターを設定する方法](#MatchingRules)」を参照してください。  
  
 ソース データベースの統計情報には、次の情報が含まれます。  
  
-   **レコード**: ソース データベース内のレコードの総数  
  
-   **合計値**: データ ソースのフィールドの値の総数  
  
-   **新しい値**: 前回の実行以降の新しい値の総数と、全体に占める割合  
  
-   **一意の値**: フィールドの一意の値の総数と、全体に占める割合  
  
-   **新しい一意の値**: フィールドの新しい一意の値の総数と、全体に占める割合  
  
 フィールドの統計情報には、次の情報が含まれます。  
  
-   **フィールド名**  
  
-   **ドメイン名**  
  
-   **新規**: 新しい値の数と、ドメインの既存の値に対する割合  
  
-   **一意**: フィールドの一意のレコードの数と、全体に占める割合  
  
-   **完全**: 照合のテストのためにマップされた各ソース フィールドの完全性  
  
###  <a name="matching-policy-notifications"></a><a name="Notifications"></a> 照合ポリシーの通知  
 照合ポリシー アクティビティでは、以下の状況で通知が生成されます。  
  
-   フィールドがすべてのレコードで空の場合。そのフィールドをマッピングから除去することをお勧めします。  
  
-   フィールドの完全性スコアが非常に低い場合。そのフィールドをマッピングから除去できます。  
  
-   フィールド内のすべての値が無効である場合。マッピングと、ドメイン ルールとフィールドの内容の関連を確認する必要があります。  
  
-   フィールド内の有効な値が少ない場合。マッピングと、ドメイン ルールとフィールドの内容の関連を確認する必要があります。  
  
-   フィールドの一意性が高い場合。 照合ポリシーでこのフィールドを使用すると、照合結果の数を減らすことができます。  
  
###  <a name="matching-results-tab"></a><a name="ResultsTab"></a> [照合結果] タブ  
 **[照合結果]** タブをクリックすると、照合ポリシーのルールの実行に関する統計情報と、前回のルールの実行に関する統計情報が表示されます。 同じルールを別のパラメーターで複数回実行した場合は、照合結果テーブルに両方の実行の統計情報が表示されるため、それらを比較することができます。 必要に応じて以前のルールを復元することもできます。  
  
 この統計情報には、次の情報が含まれます。  
  
-   データベース内のレコードの総数  
  
-   データベース内の一致レコードの総数  
  
-   データベース内の重複と見なされないレコードの数  
  
-   検出されたクラスターの数  
  
-   クラスターの平均サイズ (重複レコードの数をクラスターの数で割った値)  
  
-   クラスター内の重複の最小数  
  
-   クラスター内の重複の最大数  
  
  
