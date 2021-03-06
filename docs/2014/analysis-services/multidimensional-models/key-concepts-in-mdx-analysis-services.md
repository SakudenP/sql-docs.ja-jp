---
title: MDX の主な概念 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], about MDX
- dimensional modeling [MDX]
- MDX [Analysis Services], about MDX
- Multidimensional Expressions [Analysis Services], dimensional modeling
- MDX [Analysis Services], dimensional modeling
ms.assetid: 4797ddc8-6423-497a-9a43-81a1af7eb36c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1e6907913bd5e068f30cea2e652ccdad5247d965
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546614"
---
# <a name="key-concepts-in-mdx-analysis-services"></a>MDX の主な概念 (Analysis Services)
  多次元式 (MDX) を使用して多次元データを照会したり、キューブ内で MDX 式を作成したりするには、多次元の概念と用語を理解しておく必要があります。  
  
 既にご存じのデータ要約の例を足掛かりにして、それと MDX の関連性を確認することをお勧めします。 ここでは、Excel で作成された、Analysis Services のサンプルキューブのデータを含む PivotTable を作成します。  
  
 ![メジャーとディメンションが呼び出されたピボットテーブル](../media/ssas-keyconcepts-pivot1-measures-dimensions.png "メジャーとディメンションが呼び出されたピボットテーブル")  
  
## <a name="measures-and-dimensions"></a>メジャーとディメンション  
 Analysis Services キューブは、ピボットテーブルの例で示したメジャー、ディメンション、およびディメンション属性で構成されます。  
  
 **メジャー** は、合計、カウント、パーセンテージ、最小、最大、または平均として集計されるセル内の数値データ値です。 メジャー値は、動的で、ユーザーのナビゲーションやピボットテーブルとのやり取りに反応して、リアルタイムに計算されます。 この例では、各セルが軸の展開と折りたたみに基づいて増減する Reseller Sales Amounts を表しています。 Date (年、四半期、月、または日付) と Sales Territory (国のグループ、国、地域) の任意の組み合わせに対して、その特定のコンテキストで集計された Reseller Sales Amount を取得できます。 メジャーの同義語である他の用語としては、ファクト (データ ウェアハウス内) と計算フィールド (テーブルと Excel データ モデル内) があります。  
  
 **ディメンション** は、ピボットテーブルの列軸と行軸上に表示され、メジャーの背後にある意味を表します。 ディメンションは、リレーショナル データ モデル内のテーブルに似ています。 ディメンションの一般的な例として、Time、Geography、Products、Customers、Employees などが挙げられます。 この例は、各行の Sales Territory と最上部の Date の 2 つのディメンションで構成されていますが、Promotions や Products などの Reseller Sales に関連付けられた他のディメンションをドラッグ アンド ドロップして、簡単に、それらのディメンションに沿った販売実績を表示することができます。 データを効率的に探索できるかどうかは、作成するディメンションと、それがデータ ソース内のファクト テーブルと関連性があるかどうかに応じて異なります。  
  
 **ディメンション属性** は、テーブル内の列と同様の、ディメンション内の名前付きアイテムです。 この例では、Sales Territory ディメンション属性が、Country Group (Europe、North America、Pacific)、Country (Canada、United States)、および Region (Central、Northeast、Northwest、Southeast、Southwest) で構成されています。  
  
 各属性には、データ値のコレクション、または、それに関連付けられたメンバーが含まれています。 この例では、Country Group 属性のメンバーは、Europe、North America、および Pacific です。 **メンバー** は、属性に属している実際のデータ値を表します。  
  
> [!NOTE]  
>  データ モデリングの 1 つの側面は、データ自体に内在するパターンとリレーションシップを形式化することです。 国/地域/都市のような自然階層に分類されるデータを操作する場合は、 **属性リレーションシップ**を作成することによって、そのリレーションシップを形式化することができます。 属性リレーションシップは、属性間の一対多リレーションシップです。たとえば、州と都市の間のリレーションシップには多くの都市がありますが、都市は1つの州にのみ属します。 モデル内で属性リレーションシップを作成すると、クエリのパフォーマンスが向上します。そのため、データでサポートされている場合は、作成することをお勧めします。 属性リレーションシップは、SQL Server Data Tools 内のディメンション デザイナーで作成できます。 「 [Define Attribute Relationships](attribute-relationships-define.md)」を参照してください。  
  
 Excel 内部のピボットテーブル フィールド リストにモデル メタデータが表示されます。  上のピボットテーブルと下のフィールド リストを比較します。 フィールド リストには Sales Territory、Group、Country、Region (メタデータ) が含まれているのに対して、ピボットテーブルにはメンバー (データ値) しか含まれていないことに注意してください。 アイコンの外観を識別することによって、多次元モデルの部品を容易に Excel 内のピボットテーブルに関連付けることができます。  
  
 ![ピボットテーブルのフィールドリスト](../media/ssas-keyconcepts-ptfieldlist.png "ピボットテーブルのフィールド リスト")  
  
## <a name="attribute-hierarchies"></a>属性階層  
 深く考えなくても、各軸に沿ってレベルを展開したり、折りたたんだりするだけで、ピボットテーブル内の値が増減することがわかっていますが、どうしてこんなことができるのでしょうか。 答えは属性階層にあります。  
  
 すべてのレベルを折りたたむと、各 Country Group と Calendar Year の総合計が表示されます。 この値は、階層内の **(すべての) メンバー** と呼ばれるものから抽出されます。 (すべての) メンバーは、属性階層内のすべてのメンバーの値を計算したものです。  
  
-   すべての Country Groups と Dates の (すべての) メンバーを集計すると、$80,450,596.98 になります。  
  
-   CY2008 の (すべての) メンバーは $16,038,062.60 です。  
  
-   Pacific の (すべての) メンバーは $1,594,335.38 です。  
  
 このような集計は、事前に計算され、保存されます。これが、Analysis Services のクエリ パフォーマンスが優れている秘密の一部です。  
  
 ![すべてのメンバーが呼び出されたピボットテーブル](../media/ssas-keyconcepts-pivot2-allmember.png "すべてのメンバーが呼び出されたピボットテーブル")  
  
 階層を展開すると、最終的に、最下位レベルに到達します。 これは **リーフ メンバー**と呼ばれます。 リーフ メンバーは、子が存在しない階層のメンバーです。 この例では、Australia がリーフ メンバーです。  
  
 ![リーフ メンバーが呼び出されたピボットテーブル](../media/ssas-keyconcepts-pivot3-leafparent.PNG "リーフ メンバーが呼び出されたピボットテーブル")  
  
 上位にあるものは **親メンバー**と呼ばれます。 Pacific は Australia の親です。  
  
 **属性階層の構成要素**  
  
 総じて、これらの概念のすべてが **属性階層**という概念を作り上げています。 属性階層は、さまざまな属性メンバーからなる 1 つのツリー構造であり、それには以下のレベルが含まれています。  
  
-   リーフ レベル。個別の属性メンバーが含まれています。リーフ レベルの各メンバーを **リーフ メンバー**ともいいます。  
  
-   属性階層が親子階層の場合の中間レベル (詳細は後述)。  
  
-   すべての子属性の集計値を含む (すべての) メンバー。 必要に応じて、データが意味を持たない場合に、(All) レベルを非表示にしたり、無効にしたりすることができます。 たとえば、製品コードは数値ですが、合計または平均を意味したり、すべての製品コードを集計したりすることは意味がありません。  
  
> [!NOTE]  
>  BI 開発者の多くは、クライアント アプリケーションで特定の動作を実現するためや特定のパフォーマンス メリットを得るために、属性階層のプロパティを設定します。 たとえば、(All) メンバーが意味を持たない属性に対しては、AttributeHierarchyEnabled = False を設定します。 または、(すべての) メンバーを非表示にするだけなら、AttributeHierarchyVisible=False を設定することができます。 プロパティの詳細については、「 [Dimension Attribute Properties Reference](dimension-attribute-properties-reference.md) 」を参照してください。  
  
## <a name="navigation-hierarchies"></a>ナビゲーション階層  
 ピボットテーブル (少なくともこの例の) では、行軸と列軸を展開すると、下位レベルの属性が表示されます。 拡張可能なツリーは、モデル内に作成されたナビゲーション階層を通して実現されます。  AdventureWorks サンプル モデルでは、Sales Territory ディメンションに Country Group、Country、および Region の順で複数レベル階層が含まれています。  
  
 ご存じのように、階層はピボットテーブルまたはその他のデータ要約オブジェクト内のナビゲーション パスを提供するために使用されます。 これには均衡と不均衡という 2 つの基本的な種類があります。  
  
 **均衡階層**  
  
|||  
|-|-|  
|![均衡階層が呼び出されたピボットテーブル](../media/ssas-keyconcepts-pivot4-balancedhierarchy.PNG "均衡階層が呼び出されたピボットテーブル")|**均衡階層** は、最上位メンバーと任意のリーフ メンバーの間のレベル数が等しい階層です。<br /><br /> **自然階層** は基になるデータから自然に発生する階層です。 一般的な例は、それぞれの下位レベルが予想どおり親から派生する、国/地域/州や年/月/日などのカテゴリ/サブカテゴリ モデルです。<br /><br /> 多次元モデルでは、ほとんどの階層が均衡階層で、その多くが自然階層でもあります。<br /><br /> 属性階層とよく対比される、もう 1 つの関連モデリング用語として、`user-defined hierarchy`があります。 これは、属性を定義すると Analysis Services によって自動的に生成される属性階層とは対照的に、BI 開発者によって作成される階層を意味します。|  
  
 **不均衡階層**  
  
|||  
|-|-|  
|![不規則階層が呼び出されたピボットテーブル](../media/ssas-keyconcepts-pivot15-raggedhierarchy.PNG "不規則階層が呼び出されたピボットテーブル")|**不規則階層** または **不均衡階層** は、トップ レベル メンバーとリーフ メンバーの間に存在するレベルの数が一様でない階層です。 ここでも、BI 開発者によって作成される階層ですが、この場合はデータにギャップがあります。<br /><br /> AdventureWorks サンプル モデルでは、United States に他の国には存在しない追加のレベル (Regions) が含まれている Sales Territory が不規則階層を表しています。<br /><br /> 不規則階層は、クライアント アプリケーションでうまく処理されない場合、BI 開発者が対処する必要があります。 Analysis Services モデルでは、複数レベルのデータ間のリレーションシップを明示的に定義することによって、レベル間のあいまいな関係性を排除した **親子階層** を構築できます。 「 [Parent-Child Hierarchy](parent-child-dimension.md) 」をご覧ください。|  
  
## <a name="key-attributes"></a>キー属性  
 モデルは、キーとインデックスを使って関連付けを示す関連オブジェクトのコレクションです。 Analysis Services モデルについても違いはありません。 ディメンション (リレーショナル モデルのテーブルに相当することを思い出してください) ごとに、キー属性が存在します。 **キー属性** は、ファクト テーブル (メジャー グループ) に対する外部キー リレーションシップで使用されます。 ディメンション内のすべての非キー属性がキー属性に (直接的または間接的に) リンクされます。  
  
 必ずではありませんが、キー属性の多くは **粒度属性**でもあります。 粒度は、データ内の詳細または精度のレベルを表します。 この場合も、一般的な例が理解の助けになります。 日付の値を考えてみましょう。日次売上の場合は、日付の値を日に設定する必要があります。売上予算の場合は、四半期ごとで十分ですが、分析データがスポーツ イベントのレース結果で構成されている場合は、粒度をミリ秒にする必要があります。 データ値の精度のレベルが粒度です。  
  
 通貨はもう1つの例です。金融アプリケーションでは、多くの小数点以下の通貨値を追跡する場合があります。一方、地元の学校のファンド調達担当者では、最も近いドルの値のみが必要になる場合があります。 粒度の理解は、不要なデータの保存を避けるという意味でも重要です。 詳細のレベルが分析に影響しない場合は、タイムスタンプからミリ秒を切り捨てる、または、売上高から少額を切り捨てることによって、ストレージと処理時間を節約することができます。  
  
 粒度属性を設定するには、SQL Server Data Tools 内のキューブ デザイナーの [ディメンションの使用法] タブを使用します。 AdventureWorks サンプル モデルでは、Date ディメンションのキー属性は Date キーです。 Sales Orders の場合は、粒度属性がキー属性と等価です。 Sales Targets の場合は、粒度のレベルが四半期ごとであり、それに応じて、粒度属性が Calendar Quarter に設定されます。  
  
 ![粒度属性を示すモデル](../media/ssas-keyconcepts-granularityattrib.png "粒度属性を示すモデル")  
  
> [!NOTE]  
>  粒度属性とキー属性が異なる場合は、すべての非キー属性を直接的または間接的に粒度属性にリンクする必要があります。 キューブ内ではディメンションの粒度が粒度属性で定義されます。  
  
## <a name="query-scope-cube-space"></a>クエリ スコープ (キューブ空間)  
 クエリのスコープは、データが選択される境界を意味します。 これは、キューブ全体 (キューブは最大のクエリ オブジェクト) からセルまでの範囲になります。  
  
 **キューブ空間** は、そのキューブのメジャーを伴った、キューブの属性階層のメンバーから構成されます。  
  
 **サブキューブ** は、キューブのフィルターを適用したビューを表す、キューブのサブセットです。 サブキューブは、MDX 計算スクリプト内の Scope ステートメントを使用して、あるいは、MDX クエリ内のサブセレクト句で、または、セッション キューブとして定義することができます。  
  
 **セル** は、メジャー ディメンション メンバーのメンバーとキューブ内の各属性階層からのメンバー間のスペースを意味します。  
  
## <a name="other-modeling-terms"></a>その他のモデリング用語  
 このセクションは、他のセクションには簡単には記載されていない概念と用語をまとめたものですが、それでも理解しておく必要があります。  
  
 **計算メンバー** は、クエリ実行時に定義と計算がなされるディメンション メンバーです。 計算されるメンバーをユーザー クエリまたは MDX 計算スクリプトで定義して、サーバーに保存しておくことができます。 計算されるメンバーは、その計算されるメンバーが定義されているディメンション内のディメンション テーブルの行と対応します。  
  
 **個別カウント** は、1 度しかカウントされないデータ項目に使用される特殊なメジャーです。 AdventureWorks サンプル モデルには、Internet Orders、Reseller Orders、および Sales Orders の個別カウント メジャーが含まれています。  
  
 **メジャー グループ** は、1 つ以上のメジャーのコレクションです。 そのほとんどは、ユーザー定義であり、関連メジャーをまとめて保持するために使用します。 個別カウント メジャーは例外です。 このメジャーは、必ず、個別メジャーのみを含む専用のメジャー グループに配置されます。 ピボットテーブルの例の図ではメジャーグループを表示できませんが、メジャーの名前付きコレクションとしてピボットテーブルのフィールドリストに表示されます。  
  
 **メジャー ディメンション** は、キューブ内のすべてのメジャーを含むディメンションです。 SQL Server Data Tools で構築する多次元モデルでは公開されませんが、まったく同じように存在します。 これにはメジャーが含まれているため、通常は、メジャー ディメンションのすべてのメンバーが集計されます (合計またはカウントによって)。  
  
 **データベース ディメンションとキューブ ディメンション**。 モデル内では、スタンドアロン ディメンションを定義して、同じモデル内の任意の数のキューブに含めることができます。 キューブにディメンションを追加すると、キューブディメンションと呼ばれます。 プロジェクト内では、オブジェクトエクスプローラーのスタンドアロンアイテムとして、データベースディメンションと呼ばれます。 どうして区別が必要なのでしょうか。 それは、それぞれに独立的にプロパティを設定できるからです。 製品ドキュメントでは、両方の用語が使用されているので、その意味を理解しておくことをお勧めします。  
  
## <a name="next-steps"></a>次の手順  
 これで、重要な概念と用語が理解できたところで、Analysis Services の基本的な概念をさらに詳しく説明している以下のトピックに進むことができます。  
  
-   [MDX の基本的なクエリ &#40;MDX&#41;](mdx/mdx-query-the-basic-query.md)  
  
-   [基本的な MDX スクリプト &#40;MDX&#41;](mdx/the-basic-mdx-script-mdx.md)  
  
-   [多次元モデリング (Adventure Works チュートリアル)](../multidimensional-modeling-adventure-works-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [キューブ空間](mdx/cube-space.md)   
 [組](mdx/tuples.md)   
 [Autoexists](mdx/autoexists.md)   
 [MDX&#41;&#40;メンバー、組、およびセットの操作](mdx/working-with-members-tuples-and-sets-mdx.md)   
 [ビジュアルの合計と非表示の合計](mdx/visual-totals-and-non-visual-totals.md)   
 [MDX クエリの基礎 &#40;Analysis Services&#41;](mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX スクリプティングの基礎 &#40;Analysis Services&#41;](mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Mdx 言語リファレンス &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [多次元式 &#40;MDX&#41; リファレンス](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
