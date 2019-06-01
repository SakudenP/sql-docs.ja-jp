---
title: Linux への PolyBase のインストール | Microsoft Docs
description: この記事では、Linux に SQL Server フルテキスト検索をインストールする方法について説明します。
author: aboke
ms.author: aboke
manager: craigg
ms.date: 4/12/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.openlocfilehash: 69c256ef52d9c302d55ef1499059d959ed55b528
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759069"
---
# <a name="install-polybase-on-linux"></a>Linux への PolyBase のインストール

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux に [PolyBase](../../relational-databases/search/full-text-search.md) (**mssql server-polybase**) をインストールする手順を以下に示します。 PolyBase を使用すると、リモート データ ソースに対して外部クエリを実行することができます。 

>[!NOTE]
> Polybase をインストールする前に、まず [SQL Server をインストール](../../linux/sql-server-linux-setup.md#platforms)します。 これにより **mssql server-polybase** パッケージをインストールするときに使用するキーとリポジトリが構成されます。

> Linux での PolyBase のスケール アウトは、現在ご利用いただけません。


ご利用のオペレーティング システムに PolyBase をインストールします。

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)



## <a name="RHEL">RHEL へのインストール</a>

Red Hat Enterprise Linux に **mssql-server-polybase** をインストールするには、次のコマンドを使用します。 

```bash
sudo yum install -y mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>インストール後に、[PolyBase 機能を有効にする](#enable)必要があります。

オフライン インストールが必要な場合は、[リリース ノート](../../linux/sql-server-linux-release-notes.md)の PolyBase パッケージのダウンロードを参照してください。 次に、[SQL Server のインストール](../../linux/sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

## <a name="ubuntu">Ubuntu へのインストール</a>

Ubuntu に **mssql-server-polybase** をインストールするには、次のコマンドを使用します。 

```bash
sudo apt-get install mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>インストール後に、[PolyBase 機能を有効にする](#enable)必要があります。

オフライン インストールが必要な場合は、[リリース ノート](../../linux/sql-server-linux-release-notes.md)の PolyBase パッケージのダウンロードを参照してください。 次に、[SQL Server のインストール](../../linux/sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

## <a name="SLES">SLES へのインストール</a>

SUSE Linux Enterprise Server に **mssql-server-polybase** をインストールするには、次のコマンドを使用します。 

```bash
sudo zypper install mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>インストール後に、[PolyBase 機能を有効にする](#enable)必要があります。


オフライン インストールが必要な場合は、[リリース ノート](../../linux/sql-server-linux-release-notes.md)の PolyBase パッケージのダウンロードを参照してください。 次に、[SQL Server のインストール](../../linux/sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。


## <a name="enable">PolyBase を有効にする</a> 

インストールが完了したら、PolyBase を有効にしてその機能にアクセスできるようにする必要があります。 インストールされている SQL Server インスタンスに接続し、次の Transact-SQL コマンドを使用して有効にします。

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE [WITH OVERRIDE];
```

## <a name="update-polybase"></a>PolyBase を更新する

**mssql server-polybase** が既にインストールされている場合、次のコマンドを使用して最新バージョンに更新できます。

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```
sudo systemctl restart mssql-server
```

### <a name="sles"></a>SLES

```bash
sudo zypper remove mssql-server-polybase
sudo zypper refresh
sudo zypper install mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```
sudo systemctl restart mssql-server
```

>[!NOTE]
>インストール後に、[PolyBase 機能を有効にする](#enable)必要があります。

## <a name="next-steps"></a>次の手順

### <a name="supported-external-data-sources-on-linux"></a>Linux でサポートされている外部データ ソース

Linux 上の PolyBase は、次のデータ ソースにアクセスできます。 PolyBase が有効になっているこれらのソースから外部テーブルを作成する方法の詳細については、提供されているリンクを参照してください。 

- [SQL Server (& SQL DB、Azure SQL DW)](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB (& Cosmos DB)](../../relational-databases/polybase/polybase-configure-mongodb.md)

これを使用する方法について詳しくは、[CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) に関する Transact-SQL 参照記事をご覧ください。