---
title: Azure SQL DB への接続 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 12da1aa42f468b92e1833410e635183aabf3a384
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103242"
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Azure SQL DB への接続 (MySQLToSQL)
[SQL Azure への接続] ダイアログボックスを使用して、移行する SQL Azure データベースに接続します。  
  
このダイアログボックスにアクセスするには、[**ファイル**] メニューの [ **SQL Azure に接続**] を選択します。 以前に接続している場合、コマンドは**SQL Azure に再接続します。**  
  
## <a name="options"></a>オプション  
**サーバー名**  
  
SQL Azure に接続するためのサーバー名を選択または入力します。  
  
**[データベース]**  
  
データベース名を選択、入力、または**参照**します。  
  
> [!IMPORTANT]  
> SSMA for MySQL は、SQL Azure の master データベースへの接続をサポートしていません。  
  
**ユーザー名**  
  
SSMA が SQL Azure データベースへの接続に使用するユーザー名を入力します。  
  
**パスワード**  
  
ユーザー名に対応するパスワードを入力します。  
  
**Encrypt**  
  
SSMA では、SQL Azure への暗号化接続を推奨しています。  
  
## <a name="create-azure-database"></a>Azure データベースの作成  
SQL Azure アカウントにデータベースがない場合は、最初のデータベースを作成できます。  
  
初めて新しいデータベースを作成するには、次の手順に従います。  
  
1.  [SQL Azure への接続] ダイアログボックスに表示されている [参照] ボタンをクリックします。  
  
2.  データベースが存在しない場合は、次の2つのメニュー項目が表示されます。  
  
    1.  **(データベースが見つかりません)** が無効化され、常にグレー表示になっている  
  
    2.  SQL Azure アカウントにデータベースが存在しない場合にのみ有効になる**新しいデータベースを作成**します。 このメニュー項目をクリックすると、[Azure データベースの作成] ダイアログボックスにデータベースの名前とサイズが表示されます。  
  
3.  データベースの作成時には、次の2つのパラメーターが入力として指定されます。  
  
    1.  **データベース名:** データベース名を入力します。  
  
    2.  **データベースサイズ:** SQL Azure アカウントで作成する必要のあるデータベースのサイズを選択します。  
  
