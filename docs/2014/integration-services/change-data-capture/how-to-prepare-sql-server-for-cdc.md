---
title: CDC 用に SQL Server を準備する方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38e13d715eaeee5e9ec5dc53c2297b0bbb697260
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85435719"
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>CDC 用に SQL Server を準備する方法
  Oracle CDC サービスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのターゲット インスタンスに MSXDBCDC データベースが含まれている必要があります。 このデータベースを作成するには、CDC Service 構成コンソールの "SQL Server の準備" アクションを使用します。このタスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各ターゲット インスタンスに対して一度だけ実行します。  
  
 次に、CDC Service 構成コンソールを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを Oracle Change Data Capture 用に準備する方法について説明します。 このプロセスによって、MSXDBCDC データベースが作成され、必要なテーブル、ストアド プロシージャ、およびその他のアーティファクトが定義されます。  
  
 Oracle CDC 用の SQL Server の準備は、Oracle CDC Service の管理者が実行します。 CDC Service の管理者ロールの詳細については、「 [Change Data Capture Service for Oracle のユーザーロール](user-roles.md)」を参照してください。  
  
### <a name="to-enable-sql-server-for-cdc"></a>CDC 用に SQL Server を有効にするには  
  
1.  **[スタート]** メニューの **[CDC Service Configuration for Oracle]** をクリックします。  
  
2.  左ペインで **[ローカルの CDC Service]** を選択してから、 **[アクション]** ペインの **[SQL Server の準備]** をクリックします。  
  
     **[ローカルの CDC Service]** を右クリックして **[SQLServer の準備]** をクリックすることもできます。  
  
3.  [Oracle CDC 用 SQL Server インスタンスの準備] ダイアログ ボックスに必要な情報を入力します。 このダイアログ ボックスに必要な情報を入力する方法については、「 [Prepare SQL Server for CDC](prepare-sql-server-for-cdc.md)」を参照してください。  
  
     Oracle CDC 用に SQL Server インスタンスを準備するには、ログインが MSXDBCDC データベースに対する書き込み権限を持っている必要があります。 `sysasmin` ロールのメンバーなど、MSXDBCDC データベースに対する書き込み権限を持つログインの資格情報を入力します。  
  
 **注**: **[スクリプトの表示]** をクリックすると、セットアップ スクリプトの読み取り専用バージョンを表示できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム管理者は、必要に応じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理コンソールにこのスクリプトをコピーして編集および実行することができます。  
  
## <a name="see-also"></a>参照  
 [CDC 用の SQL Server の準備](prepare-sql-server-for-cdc.md)  
  
  
