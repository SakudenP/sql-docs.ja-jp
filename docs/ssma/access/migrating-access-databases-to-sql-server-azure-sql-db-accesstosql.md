---
title: Access データベースを SQL Server に移行する-Azure SQL DB |Microsoft Docs
description: SQL Server Migration Assistant (SSMA) を使用して SQL Server または Azure SQL Database にアクセスデータベースを移行するには、この推奨プロセスを使用します。
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: d3cbe1565642d43aabf3e36604fac5bfc2979c65
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293739"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>SQL Server への Access データベースの移行-Azure SQL DB (アクセス許可 Sql)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant (SSMA) は、Access データベースをまたは SQL Azure に迅速に移行するのに役立つ包括的な環境を提供するツールです [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 SSMA を使用することにより、データベースオブジェクトへのアクセスや SQL Azure を確認したり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、access データベースの移行を評価したり、access データベースオブジェクトを変換したり、SQL Azure に読み込んだり、データを移行したりすることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="recommended-migration-process"></a>推奨される移行プロセス  
オブジェクトとデータをアクセスからまたは SQL Azure に正常に移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次の手順を使用します。  
  
1.  [新しい SSMA プロジェクトを作成](creating-and-managing-projects-accesstosql.md)します。 プロジェクトを作成した後、変換オプション、移行オプション、データ型マッピングなどの[プロジェクトオプションを設定](setting-conversion-and-migration-options-accesstosql.md)できます。  
  
2.  [Access データベースファイル](adding-and-removing-access-database-files-accesstosql.md)をプロジェクトに追加します。  
  
    コンピューターまたはネットワーク上のファイルなど、個々のファイルを追加できます。  
  
3.  [SQL Server のターゲットインスタンスに接続する](connecting-to-sql-server-accesstosql.md)か[、SQL Azure のターゲットインスタンスに接続](connecting-to-azure-sql-db-accesstosql.md)します。  
  
    SQL Server または SQL Azure に接続できます。  
  
4.  1つ以上の Access データベースと SQL Azure スキーマ間のマッピングをカスタマイズするに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、[ソースデータベースとターゲットデータベースをマップ](mapping-source-and-target-databases-accesstosql.md)します。  
  
5.  必要に応じて、[評価レポートを作成](assessing-access-database-objects-for-conversion-accesstosql.md)して、Access データベースオブジェクトを正常にまたは SQL Azure に変換できるかどうかを判断でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
6.  [Access データベースオブジェクト](converting-access-database-objects-accesstosql.md)を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure オブジェクト定義に変換します。  
  
7.  [変換されたデータベースオブジェクトを SQL Server に読み込み](loading-converted-database-objects-into-sql-server-accesstosql.md)ます。  
  
    SSMA を使用してデータベースオブジェクトをまたは SQL Azure に読み込むことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。または、スクリプトを保存することもでき [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。  
  
8.  [アクセスデータを SQL Server に移行](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)します。  
  
    > [!NOTE]  
    > スキーマとデータを1回の手順で変換、読み込み、移行することができます。 ワンクリックでの移行を実行するには、[**変換、読み込み、移行**] ボタンをクリックします。  
  
9. Access アプリケーションでまたは SQL Azure のデータを使用する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、「 [access テーブルを SQL Server テーブルにリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)する」を使用します。  
  
また、移行ウィザードを使用して、このプロセスを進めることもできます。 詳細については、「[移行ウィザード](migration-wizard-accesstosql.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
[SQL Server Migration Assistant にアクセスするためのはじめに](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)
