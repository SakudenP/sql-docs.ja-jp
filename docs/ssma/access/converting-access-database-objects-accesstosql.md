---
title: Access データベースオブジェクトの変換 (アクセスデータベースオブジェクト) |Microsoft Docs
description: SQL Server/Azure SQL Database に接続した後、データベースオブジェクトへのアクセスを選択してから、スキーマを SQL Server/SQL Database スキーマに変換する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f15fc6cee7f66128af7646b9605234e60830b8db
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84302807"
---
# <a name="converting-access-database-objects-accesstosql"></a>Access データベースオブジェクトの変換 (アクセス許可 Sql)
Access データベースを追加し、または SQL Azure に接続すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、SSMA によって、access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースオブジェクトまたは SQL Azure データベースオブジェクトのメタデータが表示されます。 これで、Access データベースオブジェクトを選択して、スキーマを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure スキーマに変換できるようになりました。  
  
## <a name="the-conversion-process"></a>変換処理  
データベースオブジェクトを変換すると、Access メタデータからオブジェクトの定義が取得され、それが同等の構文に変換され [!INCLUDE[tsql](../../includes/tsql-md.md)] て、この情報がプロジェクトに読み込まれます。 または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure メタデータエクスプローラーを使用して、または SQL Azure オブジェクトとそのプロパティを表示でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!IMPORTANT]  
> オブジェクトを変換しても、または SQL Azure にオブジェクトは作成されません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 このメソッドは、オブジェクト定義を変換し、その情報を SSMA プロジェクトに格納します。  
  
変換中、SSMA は [出力] ウィンドウに状態を出力し、[エラー一覧] ウィンドウにエラーメッセージ、警告メッセージ、および情報メッセージを出力します。 この情報を使用して、アクセスデータベースまたは変換プロセスを変更して目的の変換結果を取得する必要があるかどうかを判断します。 また、「[移行のために Access データベースを準備](preparing-access-databases-for-migration-accesstosql.md)する」の情報を使用して、どのような処理を行うかを決定することもできます。  
  
## <a name="setting-conversion-options"></a>変換オプションの設定  
オブジェクトを変換する前に、[**プロジェクトの設定**] ダイアログボックスでプロジェクトの変換オプションを確認してください。 このダイアログボックスを使用すると、インデックス付きの memo 列、主キー、外部キー制約、タイムスタンプ、およびインデックスを持たないテーブルを SSMA で変換する方法を設定できます。 詳細については、「[プロジェクトの設定 (変換)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388) 」を参照してください。  
  
## <a name="conversion-results"></a>変換結果  
次の表は、変換されるアクセスオブジェクトと、結果の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトまたは SQL Azure オブジェクトを示しています。  
  
|Access オブジェクト|結果の SQL Server オブジェクト|  
|-----------------|-------------------------------|  
|table|table|  
|列|列|  
|インデックス (index)|インデックス (index)|  
|外部キー (foreign key)|外部キー (foreign key)|  
|query|ビュー<br /><br />ほとんどの SELECT クエリはビューに変換されます。 更新クエリなどの他のクエリは移行されません。<br /><br />パラメーターを受け取るクエリは変換されません。また、クロス集計クエリも選択できません。|  
|report|未変換|  
|フォーム|未変換|  
|マクロ|未変換|  
|name|未変換|  
|既定値|既定値|  
|長さ0の列プロパティを許可する|check 制約|  
|列検証ルール|check 制約|  
|テーブル検証ルール|check 制約|  
|主キー (primary key)|主キー (primary key)|  
  
## <a name="converting-access-objects"></a>アクセスオブジェクトの変換  
Access データベースオブジェクトを変換するには、まず、変換するオブジェクトを選択してから、SSMA が変換を実行する必要があります。 変換中に出力メッセージを表示するには、[**表示**] メニューの [**出力**] をクリックします。  
  
**Access データベースオブジェクトを選択して SQL Server または SQL Azure 構文に変換するには**  
  
1.  Access Metadata Explorer で、[**アクセス-メタベース**] を展開し、[**データベース**] を展開します。  
  
2.  次のうち1 つ以上を行います。  
  
    -   すべてのデータベースを変換するには、[**データベース**] の横にあるチェックボックスをオンにします。  
  
    -   個々のデータベースを変換または除外するには、データベース名の横にあるチェックボックスをオンまたはオフにします。  
  
    -   クエリを変換または省略するには、データベースを展開し、[**クエリ**] チェックボックスをオンまたはオフにします。  
  
    -   個々のテーブルを変換または省略するには、データベースを展開し、[**テーブル**] を展開して、テーブルの横にあるチェックボックスをオンまたはオフにします。  
  
3.  次のいずれかの操作を行います。  
  
    -   スキーマを変換するには、[**データベース**] を右クリックし、[**スキーマの変換**] をクリックします。  
  
        また、個々のオブジェクトを変換することもできます。 オブジェクトを変換するには、どのオブジェクトが選択されているかに関係なく、オブジェクトを右クリックし、[**スキーマの変換**] をクリックします。  
  
        オブジェクトが変換されると、Access メタデータエクスプローラーに太字で表示されます。  
  
    -   スキーマとデータを1回の手順で変換、読み込み、移行するには、[データベース] を右クリックし、[**変換、読み込み、移行**] を選択します。  
  
4.  [**出力**] ウィンドウのメッセージと、[**エラー一覧**] ウィンドウのエラーと警告を確認します。  
  
## <a name="altering-tables-and-indexes"></a>テーブルとインデックスの変更  
アクセスメタデータをまたは SQL Azure メタデータに変換した後、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure に読み込む前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルとインデックスを変更または SQL Azure できます。  
  
**テーブルまたはインデックスのプロパティを変更するには**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータエクスプローラーで、変更するテーブルまたはインデックスを選択します。  
  
2.  [**テーブル**] タブで、変更するプロパティをクリックし、新しい設定を入力または選択します。 たとえば、nvarchar (15) を nvarchar (20) に変更するか、チェックボックスをオンにしてテーブル列を null 許容にすることができます。  
  
    変更されたプロパティセルからカーソルを移動します。 これを行うには、別の行をクリックするか、Tab キーを押します。  
  
3.  **[適用]** をクリックします。  
  
これで、コードの変更を [ **SQL** ] タブで確認できるようになりました。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順では、 [SQL Server に変換](loading-converted-database-objects-into-sql-server-accesstosql.md)されたデータベースオブジェクトを読み込みます。  
  
## <a name="see-also"></a>参照  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
