---
title: MySQL データの SQL Server への移行-Azure SQL DB (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 83a4a2d1bea5074cc268590d4074bde631f28694
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2020
ms.locfileid: "67908832"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>MySQL データの SQL Server への移行-Azure SQL DB (MySQLToSQL)
変換されたオブジェクトを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure に正常に同期した後、MySQL から[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure にデータを移行できます。  
  
> [!IMPORTANT]  
> 使用されているエンジンがサーバー側のデータ移行エンジンである場合、データを移行する前に、ssma を実行しているコンピューターに SSMA for MySQL Extension Pack と MySQL プロバイダーをインストールする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントサービスも実行されている必要があります。 拡張機能パックをインストールする方法の詳細については、「 [SQL Server での SSMA コンポーネントのインストール (MySQL から SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1) 」を参照してください。  
  
## <a name="setting-migration-options"></a>移行オプションの設定  
または SQL Azure に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データを移行する前に、[プロジェクトの**設定**] ダイアログボックスでプロジェクトの移行オプションを確認してください。  
  
-   このダイアログボックスを使用すると、移行バッチサイズ、テーブルロック、制約チェック、null 値処理、id 値処理などのオプションを設定できます。 プロジェクトの移行設定の詳細については、「[プロジェクトの設定 (移行)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9)」を参照してください。  
  
    **拡張データ移行設定**の詳細については、「[データ移行の設定](data-migration-settings-mysqltosql.md)」を参照してください。  
  
-   [**プロジェクトの設定**] ダイアログボックスの**移行エンジン**を使用すると、ユーザーは2種類のデータ移行エンジンを使用して移行プロセスを実行できます。  
  
    1.  クライアント側のデータ移行エンジン  
  
    2.  サーバー側のデータ移行エンジン  
  
**クライアント側のデータ移行:**  
  
-   クライアント側でデータ移行を開始するには、[**プロジェクトの設定**] ダイアログボックスで [**クライアント側のデータ移行エンジン**] オプションを選択します。  
  
-   [**プロジェクトの設定**] で、[**クライアント側のデータ移行エンジン**] オプションが設定されています。  
  
    > [!NOTE]  
    > **クライアント側のデータ移行エンジン**は ssma アプリケーション内に存在するため、拡張パックの可用性には依存しません。  
  
**サーバー側のデータ移行:**  
  
-   サーバー側のデータ移行中に、エンジンはターゲットデータベースに配置されます。 拡張機能パックを使用してインストールされます。 拡張機能パックをインストールする方法の詳細については、「 [SQL Server での SSMA コンポーネントのインストール (MySQL から SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1) 」を参照してください。  
  
-   サーバー側で移行を開始するには、[**プロジェクトの設定**] ダイアログボックスで [**サーバー側のデータ移行エンジン**] オプションを選択します。  
  
> [!IMPORTANT]  
> **クライアント側のデータ移行**オプションは、SQL Azure に対してのみ使用できます。  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>SQL Server または SQL Azure へのデータの移行  
データの移行は、データの行を MySQL テーブルからまたはトランザクション内の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure テーブルに移動する一括読み込み操作です。 各トランザクションでに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]読み込まれる行の数は、プロジェクトの設定で構成されます。  
  
移行メッセージを表示するには、[出力] ウィンドウが表示されていることを確認します。 それ以外の場合は、[**表示**] メニューの [**出力**] を選択します。  
  
**データを移行するには**  
  
1.  次の点を確認します。  
  
    -   MySQL プロバイダーは、SSMA を実行しているコンピューターにインストールされます。  
  
    -   変換されたオブジェクトをターゲットデータベース (SQL Server/SQL Azure) と同期しました。  
  
2.  MySQL メタデータエクスプローラーで、移行するデータを含むオブジェクトを選択します。  
  
    -   すべてのスキーマのデータを移行するには、[**スキーマ**] の横にあるチェックボックスをオンにします。  
  
    -   データを移行するか、個々のテーブルを省略するには、まずスキーマを展開し、[**テーブル**] を展開して、テーブルの横にあるチェックボックスをオンまたはオフにします。  
  
3.  データを移行するには、次の2つのケースが発生します。  
  
    **クライアント側のデータ移行:**  
  
    -   **クライアント側のデータ移行**を実行するには、[**プロジェクトの設定**] ダイアログボックスで [**クライアント側のデータ移行エンジン**] オプションを選択します。  
  
    **サーバー側のデータ移行:**  
  
    -   サーバー側でデータ移行を実行する前に、次のことを確認してください。  
  
        1.  SSMA for MySQL Extension Pack は SQL Server のインスタンスにインストールされます。  
  
        2.  エージェント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービスは、のインスタンスで実行されて SQL Server  
  
    -   **サーバー側のデータ移行**を実行するには、[**プロジェクトの設定**] ダイアログボックスで [**サーバー側のデータ移行エンジン**] オプションを選択します。  
  
4.  MySQL メタデータエクスプローラーで [**スキーマ**] を右クリックし、[**データの移行**] をクリックします。 また、個々のオブジェクトまたはオブジェクトのカテゴリのデータを移行することもできます。オブジェクトまたはその親フォルダーを右クリックします。[**データの移行**] オプションを選択します。  
  
    > [!NOTE]  
    > SSMA for MySQL 拡張パックが SQL Server のインスタンスにインストールされておらず、**サーバー側のデータ移行エンジン**が選択されている場合、ターゲットデータベースにデータを移行しているときに、次のエラーが発生します。 "Ssma データ移行コンポーネントが SQL Server に見つかりませんでした。サーバー側のデータ移行は実行できません。 拡張パックが正しくインストールされているかどうかを確認してください。 [**キャンセル**] をクリックして、データ移行を終了します。  
  
5.  [ **MySQL への接続**] ダイアログボックスで、接続の資格情報を入力し、[**接続**] をクリックします。 MySQL への接続の詳細については、「 [Connect To mysql &#40;MySQLToSQL](../../ssma/mysql/connect-to-mysql-mysqltosql.md) 」を参照してください&#41;  
  
    ターゲットデータベースが SQL Server 場合は、[ **SQL Server への接続**] ダイアログボックスで接続資格情報を入力し、[**接続**] をクリックします。 SQL Server に接続する方法の詳細については、「 [Connect to SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536) 」を参照してください。  
  
    ターゲットデータベースが SQL Azure 場合は、[ **SQL Azure への接続**] ダイアログボックスで接続資格情報を入力し、[**接続**] をクリックします。 SQL Azure に接続する方法の詳細については、「 [AZURE SQL DB への接続 &#40;MySQLToSQL](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md) 」を参照してください&#41;  
  
    メッセージが [**出力**] ウィンドウに表示されます。 移行が完了すると、**データ移行レポート**が表示されます。 データが移行されなかった場合は、エラーが含まれている行をクリックし、[**詳細**] をクリックします。 レポートの作成が完了したら、[**閉じる**] をクリックします。 データ移行レポートの詳細については、「[データ移行レポート (SSMA Common)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241) 」を参照してください。  
  
> [!NOTE]  
> ターゲットデータベースとして SQL Express edition を使用すると、クライアント側のデータの移行のみが許可され、サーバー側のデータ移行はサポートされません。  
  
## <a name="see-also"></a>参照  
[MySQL データベースの SQL Server への移行-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
