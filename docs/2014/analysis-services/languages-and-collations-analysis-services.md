---
title: 言語と照合順序 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Windows collations [Analysis Services]
- default collations
- languages [Analysis Services]
- sort orders [Analysis Services]
- language identifiers [Analysis Services]
- default languages
- collations [Analysis Services]
ms.assetid: 666cf8a7-223b-4be5-86c0-7fe2bcca0d09
author: minewiskan
ms.author: owend
ms.openlocfilehash: 641f161ede6daebdd879c3316ce73a2e446c21c1
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543664"
---
# <a name="languages-and-collations-analysis-services"></a>言語および照合順序 (Analysis Services)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows オペレーティング システムが提供する言語と照合順序をサポートします。 `Language` プロパティと `Collation` プロパティはインストール中、最初にインスタンス レベルで設定されますが、後でオブジェクト階層のさまざまなレベルで変更できます。  
  
 多次元モデル (のみ) では、これらのプロパティをデータベースまたはキューブに設定できます。また、キューブ内のオブジェクト用に作成した翻訳に設定することもできます。  
  
 `Language` と `Collation` を設定する場合、処理とクエリ実行中にデータ モデルが使用する設定値を指定するか、(多次元モデルの場合のみ) 複数の翻訳が含まれるモデルを提供し、外国語を話すユーザーが母語でモデルを操作できるようにします。 オブジェクト (データベース、モデル、キューブ) の `Language` プロパティと `Collation` プロパティの明示的な設定は、開発環境と実稼働サーバーが異なるロケールで構成され、言語と照合順序が想定しているターゲット環境に一致させる場合に適しています。  
  
 このトピックのセクションは次のとおりです。  
  
-   [言語および照合順序のプロパティをサポートするオブジェクト](#bkmk_object)  
  
-   [Analysis Services での言語サポート](#bkmk_lang)  
  
-   [Analysis Services での照合順序のサポート](#bkmk_collations)  
  
-   [インスタンスの既定の言語または照合順序を変更する](#bkmk_defaultLang)  
  
-   [キューブの言語または照合順序を変更する](#bkmk_cube)  
  
-   [XMLA を使用してデータモデル内の言語と照合順序を変更する](#bkmk_XMLA)  
  
-   [EnableFast1033Locale を通じて英語版のロケールのパフォーマンスを向上する](#bkmk_enablefast1033)  
  
-   [Analysis Services での GB18030 のサポート](#bkmk_gb18030)  
  
##  <a name="objects-that-support-language-and-collation-properties"></a><a name="bkmk_object"></a>言語および照合順序のプロパティをサポートするオブジェクト  
 `Language``Collation`プロパティとプロパティは一緒に公開されることがよくあります。を設定すると、を設定すること `Language` もでき `Collation` ます。  
  
 次のオブジェクトでは、`Language` と `Collation` を設定できます。  
  
-   **インスタンス**。 インスタンスに配置されすべてのプロジェクトは、インスタンスの言語と照合順序が未定義であると仮定した場合に、その言語と照合順序が適用されます。 既定では、多次元モデルは言語および照合順序が空のままです。 プロジェクトを配置すると、作成されるデータベースとキューブが、インスタンスの言語と照合順序を取得します。  
  
     最初に、言語および照合順序のプロパティがセットアップ中に確立されますが、管理者が Management Studio でオーバーライドできます。 詳細については、「 [インスタンスの既定の言語や照合順序を変更します。](#bkmk_defaultLang) 」をご覧ください。  
  
-   **データベース**。 継承を変更するには、にも言語および照合順序、データベースに含まれているすべてのキューブで使用されるプロジェクト レベルで、言語と照合順序を明示的に設定できます。 特に指定しない限り、データベース内のすべてのキューブはこのレベルで指定する言語と照合順序の指定を取得します。 定期的にコードを作成して別のロケールに配置する場合 (たとえば、中国語版のコンピューターでソリューションを開発して、フランス語版の関連会社が所有するサーバーに配置する場合)、データベース レベルで言語および照合順序を設定することが、ソリューションをターゲット環境で確実に機能させるために最初に実行する最も重要な手順です。 これらのプロパティを設定する最適な場所は、プロジェクト内です ( **[データベースの編集]** からプロジェクトのコマンドを使用)。  
  
-   **データベースディメンション**。 設計者はデータベース ディメンションにある `Language` プロパティと `Collation` プロパティを公開しますが、このオブジェクト上にプロパティを設定するのは便利な方法ではありません。 データベース ディメンションはスタンドアロン オブジェクトとして使用されないため、定義するプロパティを使用することが、不可能ではないにしても困難になることがあります。 キューブ内では、ディメンションは常に `Language` と `Collation` を親キューブから継承します。 スタンドアロンのデータベース ディメンション オブジェクトに設定している値は無視されます。  
  
-   **Cube**。 主要なクエリ構造として、キューブ レベルで言語および照合順序を設定できます。 たとえば、英語バージョンと中国語バージョンなど、同じプロジェクト内でキューブの複数の言語バージョンを作成し、各キューブが独自の言語および照合順序を持つようにする場合があります。  
  
     キューブにどの言語と照合順序を設定しても、キューブに含まれるすべてのメジャーとディメンションが使用されます。 照合順序プロパティを詳細に設定する唯一の方法は、ディメンション属性で翻訳を作成する場合です。 それ以外の場合、属性のレベルでの翻訳がない場合は、キューブあたり 1 つの照合順序になります。  
  
 さらに、 `Language` を単独で**変換**オブジェクトに設定することもできます。  
  
 キューブまたはディメンションに翻訳を追加するときに、翻訳オブジェクトが作成されます。 `Language` は、翻訳定義の一部です。 対照的に、`Collation` はキューブ以上で設定され、すべての翻訳で共有されます。 これは、翻訳を含むキューブの XMLA で、複数の言語プロパティが (各翻訳に 1 つ) 表示されるのに、照合順序は 1 つしか表示されないことから明らかです。 ディメンションの属性の翻訳には、1 つの例外があり、キューブの照合順序をオーバーライドして、ソース列と一致する属性の照合順序を指定できます (データベース エンジンは個々の列の照合順序の設定をサポートし、各翻訳が別のソース列からメンバー データを取得するよう構成することは一般的です)。 しかし、そうでない場合は、他のすべての翻訳で `Language` が単独で使用され、`Collation` の推論は使用されません。 詳細については、「[翻訳 &#40;Analysis Services&#41;](translations-analysis-services.md)」を参照してください。  
  
##  <a name="language-support-in-analysis-services"></a><a name="bkmk_lang"></a> Analysis Services での言語サポート  
 `Language` プロパティは、処理中やクエリで、また `Captions` および `Translations` で多言語シナリオをサポートするために使用されるオブジェクトのロケールを設定します。 ロケールは、英語などの言語識別子、および米国やオーストラリアなどの地域に基づき、日付と時刻の表現をさらにきめ細かく調整します。  
  
 インスタンス レベルでは、プロパティはインストール中に設定され、Windows server オペレーティング システムの言語に基づきます (37 言語のいずれか。言語パックがインストールされていると仮定します)。 言語を [設定] で変更することはできません。  
  
 インストール後、Management Studio のサーバーのプロパティ ページを使用するか、msmdsrv.ini 構成ファイルで `Language` をオーバーライドできます。 Windows クライアントでサポートされるすべて言語を含む、多数の言語から選択できます。 インスタンス レベルで設定する場合、サーバー上の `Language` によって、その後に配置されるすべてのデータベースのロケールが決まります。 たとえば、`Language` をドイツ語に設定した場合、インスタンスに配置されるすべてのデータベースは、ドイツ語の LCID である言語プロパティ 1031 になります。  
  
###  <a name="value-of-the-language-property-is-a-locale-identifier-lcid"></a><a name="bkmk_lcid"></a> 言語プロパティの値はロケール識別子 (LCID)  
 有効な値には、ドロップダウン リストに表示される任意の LCID が含まれます。 Management Studio および SQL Server Data Tools では、LCID は同等の文字列で表されます。 `Language` プロパティが明示されると、ツールに関係なく、同じ言語で表示されます。 同一の言語のリストを持つことで、モデル全体で翻訳のテストと実装に一貫性を持たせることができます。  
  
 Analysis Services には、言語が名前順に表示されますが、プロパティについて格納されている実際の値は LCID です。 言語プロパティをプログラムにより設定、または msmdsrv.ini ファイルで設定する場合は、 [ロケール識別子 (LCID)](http://en.wikipedia.org/wiki/Locale) を値として使用します。 LCID は、言語 ID、並べ替え ID、および特定の言語を識別する予約されたビットから構成される 32 ビット値です。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、LCID を使用して、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスおよびオブジェクトに選択された言語を指定します。  
  
 16 進数または 10 進数のいずれかの形式を使用して、LCID を設定することができます。 プロパティの有効な値の例をいくつか次に示し `Language` ます。  
  
-   0x0409 または 1033 ( **英語、米国**)  
  
-   0x0411 または 1041 ( **日本語**)  
  
-   0x0407 または 1031 ( **ドイツ語、ドイツ**)  
  
-   0x0416 または 1046 ( **ポルトガル語、ブラジル**)。  
  
 長いリストを表示するには、「 [Microsoft によって割り当てられているロケール ID](https://msdn.microsoft.com/goglobal/bb964664.aspx)」を参照してください。 背景の詳細については、「[コードページ](/windows/desktop/Intl/code-pages)」を参照してください。  
  
> [!NOTE]  
>  `Language` プロパティは、システム メッセージを返すための言語、またはユーザー インターフェイスに表示される文字列の言語を決定しません。 エラー、警告、およびメッセージは、Office および Office 365 でサポートされているすべての言語にローカライズされ、クライアント接続がサポートされているロケールのいずれかを指定すると、自動的に使用されます。  
  
##  <a name="collation-support-in-analysis-services"></a><a name="bkmk_collations"></a> Analysis Services での照合順序のサポート  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は Windows およびバイナリ照合順序を排他的に使用します。 これには、従来の SQL Server の照合順序は使用されません。 キューブ内では、属性のレベルでの翻訳を除き、単一の照合順序が全体を通じて使用されます。 属性の翻訳の定義の詳細については、「[翻訳 &#40;Analysis Services&#41;](translations-analysis-services.md)」を参照してください。  
  
 照合順序は、2 種類の活字のある言語において、オブジェクト識別子を除くすべての文字列の大文字小文字の区別を制御します。 オブジェクト識別子で大文字と小文字を使用する場合は、オブジェクト識別子の大文字小文字の区別は、照合順序ではなく [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]によって決定されることをあらかじめご了承ください。 英語版のスクリプト内で構成されるオブジェクト識別子の場合、照合順序に関係なく、オブジェクト識別子の大文字小文字の区別は常に無視されます。 キリル語など、2 種類の活字を持つ言語は、逆の処理になります (常に大文字小文字を区別)。 詳細については、「 [グローバリゼーションのヒントとベスト プラクティス (Analysis Services)](globalization-tips-and-best-practices-analysis-services.md) 」をご覧ください。  
  
 Analysis Services での照合順序は、各サービス用に選択した並べ替えオプションでパリティを維持すると仮定した場合、SQL Server リレーショナル データベース エンジンの照合順序と互換性があります。 たとえば、リレーショナル データベースがアクセントを区別する場合、キューブを同じ方法で構成する必要があります。 照合順序の設定が分岐していると、問題が発生する可能性があります。 例と回避策については、「 [Unicode 文字列の空白は照合順序に基づいてさまざまな処理の結果が生成される](https://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx)」を参照してください。 照合順序とデータベース エンジンの詳細については、「 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
###  <a name="collation-types"></a><a name="bkmk_collationtype"></a> 照合順序の種類  
 Analysis Services は、次の 2 つの照合順序の種類をサポートします。  
  
-   **Windows 照合順序**  
  
     Windows の照合順序は、言語における言語特性およびカルチャに関する特性に基づいて文字を並べ替えます。 Windows では、多くの言語が共通のアルファベットおよび文字の並べ替えと比較の規則を共有しているため、照合順序の数が使用されるロケール (または言語) を上回ります。 たとえば、ポルトガル語と英語のすべての Windows ロケールを含む、33 個の Windows ロケールは、Latin1 コード ページ (1252) を使用し、共通の規則に従って文字の並べ替えと比較を行います。  
  
-   **バイナリの照合順序 (BIN または BIN2)**  
  
     バイナリ照合順序は、言語の値ではなく、Unicode コード ポイントでの並べ替えます。 たとえば、Latin1_General_BIN と Japanese_BIN を Unicode データで使用すると、並べ替え結果は同じになります。 ある言語的な並べ替えで aAbBcCdD などの結果が生じ、バイナリの並べ替えが ABCDabcd になる可能性があります。これは、すべての大文字のコード ポイントは、小文字のコード ポイントよりも集合的に高いためです。  
  
###  <a name="sort-order-options"></a><a name="bkmk_sortorder"></a> 並べ替え順オプション  
 並べ替えオプションは、大文字と小文字、アクセント、かな、および幅の区別に基づいて、並べ替えおよび比較ルールの調整に使用されます。 たとえば、`Collation` の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 構成プロパティの既定値は Latin1_General_AS_CS であり、アクセントの区別および大文字と小文字の区別がある並べ替え順で Latin1_General の照合順序を使用することを指定します。  
  
 BIN と BIN2 はその他のら並べ替えオプションと相互に排他的です。BIN または BIN2 を使用する場合は、アクセントの区別の並べ替えオプションをオフにします。 同様に、BIN2 が選択されている場合、大文字と小文字を区別する、大文字と小文字を区別しない、アクセントを区別する、アクセントを区別しない、かなを区別する、および文字幅を区別するオプションは使用できません。  
  
 次の表では、Windows 照合順序の並べ替え順オプションと [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]の関連サフィックスについて説明します。  
  
|並べ替え順 (サフィックス)|並べ替え順の説明|  
|---------------------------|----------------------------|  
|Binary (_BIN) または BIN2 (_BIN2)|SQL Server には、古い BIN 照合順序と新しい BIN2 照合順序の 2 種類のバイナリ照合順序があります。 BIN2 照合順序では、すべての文字がコード ポイントに従って並び替えられます。 BIN 照合順序では、最初の文字だけがコード ポイントに従って並び替えられ、残りの文字はバイト値に従って並び替えられます (Intel プラットフォームはリトル エンディアン アーキテクチャであるため、Unicode コード文字は常にバイト スワップして格納されます)。<br /><br /> Unicode データ型のバイナリ照合順序では、データを並べ替える際にロケールが考慮されません。 たとえば、Unicode データに対して Latin_1_General_BIN と Japanese_BIN を使用した場合、並べ替え結果はどちらも同じになります。<br /><br /> バイナリ並べ替え順では、大文字と小文字が区別され、アクセントが区別されます。 また、バイナリは最速の並べ替え順です。|  
|大文字と小文字を区別する (_CS)|大文字と小文字を区別します。 このオプションを選択すると、大文字より先に小文字が並べ替えられます。 大文字と小文字を区別しないことを明示的に設定するには、_CI と指定します。 照合順序に固有の大文字小文字の設定は、ディメンション、キューブ、およびその他のオブジェクトの ID など、オブジェクト識別子には適用されません。 詳細については、「 [グローバリゼーションのヒントとベスト プラクティス (Analysis Services)](globalization-tips-and-best-practices-analysis-services.md) 」をご覧ください。|  
|アクセントを区別する (_AS)|アクセントのある文字とアクセントのない文字を区別します。 たとえば、"a" と "&#xE1;" は等しくありません。 このオプションが選択されていない場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、アクセントのある文字とアクセントのない文字が並べ替えで同じものと見なされます。 アクセントを区別しないことを明示的に設定するには、_AI と指定します。|  
|かなを区別する (_KS)|ひらがなとカタカナという日本語の 2 種類のかな文字を区別します。 このオプションが選択されていない場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、ひらがなとカタカナが並べ替えで同じものと見なされます。 かなを区別しない並べ替えには、並べ替え順のサフィックスはありません。|  
|文字幅を区別する (_WS)|1 バイト文字と 2 バイト文字として表現された同じ文字を区別します。 このオプションが選択されていない場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、同じ文字の 1 バイト表現と 2 バイト表現が並べ替えで同じものと見なされます。 文字幅を区別しない並べ替えには、並べ替え順のサフィックスはありません。|  
  
##  <a name="change-the-default-language-or-collation-on-the-instance"></a><a name="bkmk_defaultLang"></a> インスタンスの既定の言語や照合順序を変更します。  
 既定の言語および照合順序がセットアップ中に確立されている場合、インストール後の構成の一環として変更することができます。 インスタンス レベルで照合順序を変更することは単純な操作ではなく、以下の要件が求められます。  
  
-   サービスの再起動。  
  
-   既存のオブジェクトの照合順序の設定を更新します。 照合順序の設定は、オブジェクトが作成されるときに継承されます。 その後の照合順序への変更は、手動で加える必要があります。 詳細については、「 [XMLA を使用したデータ モデル内の言語および照合順序の変更](#bkmk_XMLA) 」を参照してください。  
  
-   照合順序が更新された後は、パーティションおよびディメンションを再処理します。  
  
 SQL Server Management Studio または AMO PowerShell を使用して、サーバー レベルの既定の言語または照合順序を変更することができます。 または、msmdsrv.ini ファイルのおよび設定を変更して、言語の LCID を指定することもでき **\<Language>** **\<CollationName>** ます。  
  
1.  Management Studio で、[サーバー名 |] を右クリックします。**プロパティ**  | **言語/照合順序**。  
  
2.  並べ替えオプションを選択します。 [ **バイナリ** ] または [ **バイナリ 2**] のいずれかを選択するには、まず [ **アクセントの区別**] のチェック ボックスをオフにします。  
  
     照合順序と言語は完全に独立した設定であることに注意してください。 いずれかを変更すると、その他の値はフィルター処理されず、一般的な組み合わせが表示されます。  
  
3.  新しい照合順序を使用するには、データ モデルを更新します (次のセクションを参照してください)。  
  
4.  サービスを再起動します。  
  
##  <a name="change-the-language-or-collation-on-a-cube"></a><a name="bkmk_cube"></a> キューブの言語または照合順序を変更します。  
  
1.  ソリューション エクスプローラーで、キューブをダブルクリックしてキューブ デザイナーで開きます。  
  
2.  [メジャー] または [ディメンション] のいずれかのペインで、最上位ノードを選択します。 いずれかのペインの最上位レベルのオブジェクトは、キューブです。  
  
3.  [プロパティ] で、`Language` と `Collation` を設定します。 選択した値は、キューブ ディメンションしメジャーなど、キューブのすべてのオブジェクトによって使用され、処理とクエリ操作に影響を与えます。  
  
     代替言語および照合順序のプロパティをキューブ内のオブジェクトに埋め込む唯一の方法は、翻訳です。 詳細については、「[翻訳 &#40;Analysis Services&#41;](translations-analysis-services.md)」を参照してください。  
  
##  <a name="change-language-and-collation-within-a-data-model-using-xmla"></a><a name="bkmk_XMLA"></a> XMLA を使用したデータ モデル内の言語および照合順序の変更  
 言語と照合順序の設定は、オブジェクトが作成されるときに継承されます。 これらのプロパティへの後続の変更は、手動で加える必要があります。 照合順序を複数のオブジェクトですばやく変更するための方法の 1 つのは、XMLA スクリプトで ALTER コマンドを使用する方法です。  
  
 既定では、照合順序は、データベース レベルで 1 回だけ設定します。 オブジェクト階層の残りの部分では、継承は暗黙的です。 個々 のディメンションの属性で許可される、キューブ内のオブジェクトで `Collation` を明示的に設定する場合は、XMLA の定義に表示されます。 それ以外の場合、最上位レベルの照合順序プロパティのみが存在します。  
  
 XMLA を使用して、既存のデータベースを変更するには、データベースとそれをビルドするために使用するソース ファイルの間の相違点がないことを確認します。 たとえば、XMLA を使用して、概念実証のテストで言語や照合順序をすばやく変更した後、ソース ファイルの変更によるフォローアップをし (「 [キューブの言語または照合順序を変更します。](#bkmk_cube)」を参照)、既に存在する運用手順を使用してソリューションを再展開するということが考えられます。  
  
1.  Management Studio で、データベースを右クリックします。**データベースを**  |  スクリプト化**ALTER**  | **新しいクエリエディターウィンドウ**。  
  
2.  既存の言語または照合順序を検索して別の値に置き換えます。  
  
3.  F5 キーを押してスクリプトを実行します。  
  
4.  キューブを再処理します。  
  
##  <a name="boost-performance-for-english-locales-through-enablefast1033locale"></a><a name="bkmk_enablefast1033"></a> EnableFast1033Locale によって英語版のロケールのパフォーマンスを向上させる  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスの既定の言語として英語 (米国) の言語識別子 (0x0409 または 1033) を使用する場合は、その言語識別子にのみ使用できる高度な構成プロパティである `EnableFast1033Locale` を設定することによって、パフォーマンスをさらに向上させることができます。 このプロパティの値を **true** に設定すると、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は文字列のハッシュおよび比較に高速アルゴリズムを使用できます。 構成プロパティの設定の詳細については、「[Analysis Services のサーバーのプロパティの構成](server-properties/server-properties-in-analysis-services.md)」を参照してください。  
  
##  <a name="gb18030-support-in-analysis-services"></a><a name="bkmk_gb18030"></a> Analysis Services での GB18030 のサポート  
 GB18030 は中華人民共和国が単独で中国語の文字のエンコードに使用している標準規格です。 GB18030 文字の長さは 1 バイト、2 バイト、4 バイトのいずれかです。 Analysis Services では、外部ソースからデータを処理する場合、データ変換はありません。 データは Unicode として格納されます。 クエリ時に、クライアント OS の設定に基づいてテキスト データがクエリの結果として返されると、Analysis Services クライアント ライブラリ (具体的には MSOLAP.dll OLE DB プロバイダー) を介して GB18030 変換が実行されます。 データベース エンジンは、GB18030 もサポートしています。 詳細については、「 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Analysis Services Multiidimensional のグローバリゼーションのシナリオ](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [グローバリゼーションのヒントとベストプラクティス &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)   
 [照合順序と Unicode のサポート](../relational-databases/collations/collation-and-unicode-support.md)  
  
  
