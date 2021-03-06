---
title: IBM DB2 サブスクライバー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- non-SQL Server Subscribers, IBM DB2
- data types [SQL Server replication], non-SQL Server Subscribers
- IBM DB2 Subscribers
- mapping data types [SQL Server replication]
- heterogeneous Subscribers, IBM DB2
ms.assetid: a1a27b1e-45dd-4d7d-b6c0-2b608ed175f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 54263e75c0f4c7da7c6d9c24ea499c202372aa64
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068619"
---
# <a name="ibm-db2-subscribers"></a>IBM DB2 サブスクライバー
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host Integration Server に含まれている OLE DB プロバイダーを経由した IBM DB2/AS 400、DB2/MVS、および DB2/Universal Database へのプッシュ サブスクリプションをサポートします。  
  
## <a name="configuring-an-ibm-db2-subscriber"></a>IBM DB2 サブスクライバーの構成  
 IBM DB2 サブスクライバーを構成するには、次の手順を実行してください。  
  
1.  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for DB2 の最新バージョンをディストリビューターにインストールします。  
  
    -   [!INCLUDE[ssEnterpriseEd11](../../../includes/ssenterpriseed11-md.md)]を使用している場合は、 [SQL Server 2008 ダウンロード](https://go.microsoft.com/fwlink/?LinkId=149256) Web ページの「 **関連ダウンロード** 」セクションで、Microsoft SQL Server 2008 Feature Pack の最新バージョンのリンクをクリックします。 **Microsoft SQL Server 2008 用 Feature Pack** の Web ページで、 **Microsoft OLE DB Provider for DB2**を検索します。  
  
    -   [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Standard を使用している場合は、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] (HIS) サーバーの最新バージョンをインストールしてください。この製品にプロバイダーが含まれています。  
  
     プロバイダーのインストールに加えて、データ アクセス ツールをインストールすることをお勧めします。データ アクセス ツールは次の手順で使用します (データ アクセス ツールは、既定では、 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Enterprise のダウンロードでインストールされます)。 データ アクセス ツールのインストールと使用に関する詳細については、プロバイダーのドキュメントまたは HIS のドキュメントを参照してください。  
  
2.  サブスクライバーの接続文字列を作成します。 この接続文字列は任意のテキスト エディターで作成できますが、データ アクセス ツールを使用することをお勧めします。 データ アクセス ツールで接続文字列を作成するには、次の手順を実行します。  
  
    1.  **[スタート]** ボタンをクリックし、 **[プログラム]** をポイントします。次に、 **[Microsoft OLE DB Provider for DB2]** をポイントし、 **[データ アクセス ツール]** をクリックします。  
  
    2.  **[データ アクセス ツール]** で、手順に従って DB2 サーバーに関する情報を指定します。 このツールを完了すると、関連付けられている接続文字列を使用してユニバーサル データ リンク (UDL) が作成されます (レプリケーションでは、実際にはこの UDL は使用されず、接続文字列が使用されます)。  
  
    3.  接続文字列にアクセスします。[データ アクセス ツール] で UDL を右クリックし、 **[接続文字列の表示]** を選択します。  
  
     接続文字列は、次のようになります (この例は、読みやすくするために改行されています)。  
  
    ```  
    Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
    PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
    Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
    Persist Security Info=False;Connection Pooling=True;  
    ```  
  
     文字列のほとんどのオプションは構成している DB2 サーバー固有の値になりますが、 `Process Binary as Character` オプションは、常に `False`に設定する必要があります。 サブスクリプション データベースを識別するには、 `Initial Catalog` オプションに値を入力する必要があります。 接続文字列は、サブスクリプションを作成するときに、サブスクリプションの新規作成ウィザードに入力します。  
  
3.  スナップショット パブリケーションまたはトランザクション パブリケーションを作成して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーに対して有効にしてから、サブスクライバーに対してプッシュ サブスクリプションを作成します。 詳細については、「 [SQL Server 以外のサブスクライバーのサブスクリプションの作成](../create-a-subscription-for-a-non-sql-server-subscriber.md)」を参照してください。  
  
4.  必要に応じて、1 つ以上のアーティクルに対してカスタム作成スクリプトを指定します。 テーブルがパブリッシュされると、そのテーブルに対して CREATE TABLE スクリプトが作成されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーでは、このスクリプトが [!INCLUDE[tsql](../../../includes/tsql-md.md)] 言語で作成されます。その後、このスクリプトは、サブスクライバーで適用される前に、ディストリビューション エージェントによって、より汎用的な SQL 言語に翻訳されます。 カスタム作成スクリプトを指定するには、既存の [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを変更するか、DB2 SQL 言語を使用する完全なスクリプトを作成します。DB2 スクリプトを作成する場合は、 **bypass_translation** ディレクティブを使用して、ディストリビューション エージェントがサブスクライバーでスクリプトを翻訳しないで適用できるようにします。  
  
     スクリプトはさまざまな理由によって変更することができますが、最も一般的な理由はデータ型マッピングの変更です。 詳細については、このトピックの「データ型マッピングに関する注意点」を参照してください。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを変更する場合、変更はデータ型マッピングの変更に制限する必要があります (スクリプトにコメントを含めることもできません)。 より大きな変更を行う必要がある場合は、DB2 スクリプトを作成します。  
  
     **アーティクル スクリプトを変更し、それをカスタム作成スクリプトとして指定するには**  
  
    1.  スナップショットがパブリケーションに対して生成されたら、パブリケーションのスナップショット フォルダーに移動します。  
  
    2.  MyArticle.sch など、アーティクルと同じ名前が付いた .sch ファイルを検索します。  
  
    3.  メモ帳やその他のテキスト エディターを使用して、このファイルを開きます。  
  
    4.  ファイルを変更し、別のディレクトリに保存します。  
  
    5.  sp_changearticle を実行し、*creation_script* プロパティに対してファイルのパスと名前を指定します。 詳細については、「[sp_changearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)」を参照してください。  
  
     **アーティクル スクリプトを作成し、それをカスタム作成スクリプトとして指定するには**  
  
    1.  DB2 SQL 言語を使用してアーティクル スクリプトを作成します。 ファイルの最初の行が **bypass_translation**であり、この行に他に記述がないことを確認します。  
  
    2.  sp_changearticle を実行し、*creation_script* プロパティに対してファイルのパスと名前を指定します。  
  
## <a name="considerations-for-ibm-db2-subscribers"></a>IBM DB2 サブスクライバーに関する注意点  
 「 [Non-SQL Server Subscribers](non-sql-server-subscribers.md)」で説明した注意点の他に、DB2 サブスクライバーへのレプリケートでは以下の問題に注意してください。  
  
-   レプリケートされた各テーブルのデータとインデックスは、DB2 テーブルスペースに割り当てられます。 DB2 テーブルスペースのページ サイズは、テーブルスペースに属するテーブルの列の最大数と最大行サイズを制御します。 レプリケートされたテーブルに関連付けられたテーブルスペースが、テーブルのレプリケート済み列数と最大行サイズに基づいて、適切であることを確認します。  
  
-   テーブル内の 1 つ以上の主キー列がデータ型 DECIMAL(32-38, 0-38) または NUMERIC(32-38, 0-38) である場合は、トランザクション レプリケーションを使用して DB2 サブスクライバーにテーブルをパブリッシュしないでください。 トランザクション レプリケーションは、主キーを使用して行を識別します。この結果、これらのデータ型はサブスクライバーでは VARCHAR(41) にマップされるため、エラーになります。 これらのデータ型を使用する主キーを持つテーブルは、スナップショット レプリケーションを使用してパブリッシュできます。  
  
-   サブスクライバーでテーブルを事前作成する場合は、レプリケーションによって作成するのではなく、replication support only オプションを使用します。 詳細については、「 [スナップショットを使用しないトランザクション サブスクリプションの初期化](../initialize-a-transactional-subscription-without-a-snapshot.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、DB2 よりも長いテーブル名と列名を使用できます。  
  
    -   サブスクライバーの DB2 のバージョンでサポートされているテーブル名よりも長い名前のテーブルがパブリケーション データベースに含まれている場合、destination_table アーティクル プロパティに代替名を指定します。 パブリケーションの作成時のプロパティの設定の詳細については、「[Create a Publication](../publish/create-a-publication.md)」(パブリケーションの作成) および「[Define an Article](../publish/define-an-article.md)」(アーティクルの定義) を参照してください。  
  
    -   代替列名を指定することはできません。 パブリッシュするテーブルに、サブスクライバーの DB2 のバージョンでサポートされている列名よりも長い列名がテーブルに含まれていないことを確認する必要があります。  
  
## <a name="mapping-data-types-from-sql-server-to-ibm-db2"></a>SQL Server から IBM DB2 へのデータ型マッピング  
 次の表は、IBM DB2 を実行しているサブスクライバーへのデータのレプリケーションで使用される、データ型のマッピングを示しています。  
  
|SQL Server のデータ型|IBM DB2 データ型|  
|--------------------------|-----------------------|  
|`bigint`|DECIMAL(19,0)|  
|`binary(1-254)`|CHAR(1-254) FOR BIT DATA|  
|`binary(255-8000)`|VARCHAR(255-8000) FOR BIT DATA|  
|`bit`|SMALLINT|  
|`char(1-254)`|CHAR(1-254)|  
|`char(255-8000)`|VARCHAR(255-8000)|  
|`date`|DATE|  
|`datetime`|timestamp|  
|`datetime2(0-7)`|VARCHAR(27)|  
|`datetimeoffset(0-7)`|VARCHAR(34)|  
|`decimal(1-31, 0-31)`|DECIMAL(1-31, 0-31)|  
|`decimal(32-38, 0-38)`|VARCHAR(41)|  
|`float(53)`|DOUBLE|  
|`float`|FLOAT|  
|`geography`|イメージ|  
|`geometry`|イメージ|  
|`hierarchyid`|イメージ|  
|`image`|BIT データ<sup>1</sup>の場合は VARCHAR (0)|  
|`into`|INT|  
|`money`|DECIMAL(19,4)|  
|`nchar(1-4000)`|VARCHAR(1-4000)|  
|`ntext`|VARCHAR (0)<sup>1</sup>|  
|`numeric(1-31, 0-31)`|DECIMAL(1-31,0-31)|  
|`numeric(32-38, 0-38)`|VARCHAR(41)|  
|`nvarchar(1-4000)`|VARCHAR(1-4000)|  
|`nvarchar(max)`|VARCHAR (0)<sup>1</sup>|  
|`real`|real|  
|`smalldatetime`|timestamp|  
|`smallint`|SMALLINT|  
|`smallmoney`|DECIMAL(10,4)|  
|`sql_variant`|N/A|  
|`sysname`|VARCHAR(128)|  
|`text`|VARCHAR (0)<sup>1</sup>|  
|`time(0-7)`|VARCHAR(16)|  
|`timestamp`|CHAR(8) FOR BIT DATA|  
|`tinyint`|SMALLINT|  
|`uniqueidentifier`|CHAR(38)|  
|`varbinary(1-8000)`|VARCHAR(1-8000) FOR BIT DATA|  
|`varchar(1-8000)`|VARCHAR(1-8000)|  
|`varbinary(max)`|BIT データ<sup>1</sup>の場合は VARCHAR (0)|  
|`varchar(max)`|VARCHAR (0)<sup>1</sup>|  
|`xml`|VARCHAR (0)<sup>1</sup>|  
  
 <sup>1</sup> VARCHAR (0) へのマッピングの詳細については、次のセクションを参照してください。  
  
### <a name="data-type-mapping-considerations"></a>データ型マッピングに関する注意点  
 DB2 サブスクライバーにレプリケートするときは、次に示すデータ型のマッピングに関する問題点について考慮してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `char` 、 `varchar` 、 `binary` および `varbinary` を db2 CHAR、varchar、CHAR for bit data、および varchar for bit data にマップする場合、レプリケーションでは、db2 データ型の長さが型の長さと同じになるように設定され [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ます。  
  
     これによって、DB2 ページ サイズ制約が行の最大サイズに対応するために十分な大きさである限り、生成されるテーブルはサブスクライバーで正常に作成できます。 DB2 データベースにアクセスするために使用されるログインに、DB2 にレプリケートされているテーブルに対して十分なサイズを持つテーブル スペースにアクセスするための権限があることを確認します。  
  
-   DB2 は、32 KB の VARCHAR 列をサポートできます。このため、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の LOB 列の一部は問題なく DB2 VARCHAR 列にマップできる可能性があります。 ただし、レプリケーションが DB2 に対して使用する OLE DB プロバイダーでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の LOB を DB2 の LOB にマップする処理はサポートしていません。 このため、、、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `text` `varchar(max)` 、およびの各 `ntext` `nvarchar(max)` 列は、生成された create スクリプトでは VARCHAR (0) にマップされます。 長さの値が 0 の場合は、サブスクライバーにスクリプトを適用する前に、適切な値に変更する必要があります。 データ型の長さが変更されない場合、DB2 サブスクライバーでテーブルの作成を試みると、DB2 でエラー 604 が発生します (エラー 604 は、データ型の有効桁数または長さの属性が有効でないことを示します)。  
  
     レプリケートするソース テーブルの情報に基づいて、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の LOB を可変長の DB2 項目にマップすることが適切であるかどうかを判断し、カスタム作成スクリプトで適切な最大長を指定してください。 カスタム作成スクリプトの指定の詳細については、このトピックの「IBM DB2 サブスクライバーの構成」の手順 5. を参照してください。  
  
    > [!NOTE]  
    >  DB2 のデータ型に対して指定された長さは、他の列の長さと組み合わせた場合、テーブル データが割り当てられている DB2 テーブルスペースに基づいた最大行サイズを超えることはできません。  
  
     LOB 列が適切にマップされていない場合は、アーティクルに列フィルターを使用して、列がレプリケートされないようにすることを検討してください。 詳細については、「[パブリッシュされたデータのフィルター選択](../publish/filter-published-data.md)」を参照してください。  
  
-   とを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `nchar` `nvarchar` DB2 CHAR および VARCHAR にレプリケートする場合、レプリケーションでは、型と同じ長さ指定子が db2 型に対して使用され [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ます。 ただし、データ型の長さが、生成された DB2 テーブルには小さくなりすぎる可能性があります。  
  
     DB2 環境によっ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `char` ては、データ項目が1バイト文字に限定されない場合があります。 CHAR または VARCHAR 項目の長さは、これを考慮する必要があります。 また、必要に応じて、 *シフト イン* 文字と *シフト アウト* 文字についても考慮する必要があります。 列と列を含むテーブルをレプリケートする場合は `nchar` `nvarchar` 、カスタム作成スクリプトでデータ型の最大長を指定する必要があります。 カスタム作成スクリプトの指定の詳細については、このトピックの「IBM DB2 サブスクライバーの構成」の手順 5. を参照してください。  
  
## <a name="see-also"></a>参照  
 [Non-SQL Server Subscribers](non-sql-server-subscribers.md)   
 [Subscribe to Publications](../subscribe-to-publications.md)  
  
  
