---
title: クイック スタート:Python 関数
description: このクイックスタートでは、SQL Server Machine Learning Services で Python の数学関数とユーティリティ関数を使用する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/28/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6afe1685956c43e30ace59f3e5cc794a2abbd88f
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606707"
---
# <a name="quickstart-python-functions-with-sql-server-machine-learning-services"></a>クイック スタート:SQL Server Machine Learning Services での Python 関数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
このクイックスタートでは、[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)上の [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で Python の数学関数とユーティリティ関数を使用する方法について説明します。 多くの場合、統計関数は T-SQL での実装が複雑ですが、Python では、わずか数行のコードで行うことができます。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で Python の数学関数とユーティリティ関数を使用する方法について説明します。 多くの場合、統計関数は T-SQL での実装が複雑ですが、Python では、わずか数行のコードで行うことができます。
::: moniker-end

## <a name="prerequisites"></a>前提条件

- このクイックスタートでは、Python 言語がインストールされた [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) を持つ SQL Server のインスタンスへのアクセスが必要となります。

  あなたの SQL Server インスタンスは、Azure 仮想マシンまたはオンプレミスに配置できます。 外部スクリプト機能が既定で無効になっていることに注意してください。そのため、開始する前に、[外部スクリプトを有効にし](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)、**SQL Server Launchpad サービス**が実行されていることを確認する必要があります。

- また、Python スクリプトを含む SQL クエリを実行するためのツールも必要です。 これらのスクリプトは、SQL Server インスタンスに接続し、T-SQL クエリまたはストアド プロシージャを実行できる限り、任意のデータベース管理ツールまたはクエリ ツールを使用して実行できます。 このクイックスタートでは [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) を使用します。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>乱数を生成するストアド プロシージャを作成する

わかりやすくするために、Python `numpy` パッケージを使用します。このパッケージは、Python がインストールされた SQL Server Machine Learning Services が既定でインストールおよびロードされていてます。 パッケージには、一般的な統計タスク用の数百の関数が含まれますが、その中の `random.normal` 関数は、指定された標準偏差と平均に対し、正規分布を使用して、指定された個数の乱数を生成します。

たとえば、次の Python コードは、指定された 3 の標準偏差で、平均値が 50 の 100 個の数値を返します。

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

この Python の行を T-SQL から呼び出すには、`sp_execute_external_script` の Python スクリプト パラメーターに Python 関数を追加します。 出力にはデータ フレームが必要であるため、`pandas` を使用して変換します。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=100, loc=50, scale=3));
'
    , @input_data_1 = N'   ;'
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

さまざまな乱数のセットを簡単に生成するにはどうすればよいでしょうか。

これは、SQL Server と組み合わせると簡単です。 ユーザーから引数を取得し、これらの引数を変数として Python スクリプトに渡すストアド プロシージャを定義します。

```sql
CREATE PROCEDURE MyPyNorm (
      @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=mynumbers, loc=mymean, scale=mysd));
'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 最初の行は、ストアド プロシージャを実行するときに必要になる SQL 入力パラメーターそれぞれを定義します。

- `@params` で始まる行は、Python コードで使用されるすべての変数と、対応する SQL データ型を定義します。

- それに続く行は、SQL パラメーター名を対応する Python 変数名にマップします。

ストアド プロシージャで Python 関数をラップしたので、次のように関数を簡単に呼び出し、別の値を渡すことができます。

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>トラブルシューティングのための Python ユーティリティ関数の使用

Python パッケージは、現在の Python 環境を調査するためのさまざまなユーティリティ関数を提供します。 これらの関数は、SQL Server と外部環境で Python コードが実行する方法に不一致が見つかった場合に役立つ可能性があります。

たとえば、`time` パッケージでシステム タイミング関数を使用して、Python プロセスによって使用される時間を計測し、パフォーマンスの問題を分析することができます。

```sql
EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
import time
start_time = time.time()

# Run Python processes

elapsed_time = time.time() - start_time
'
    , @input_data_1 = N' ;';
```

## <a name="next-steps"></a>次のステップ

SQL Server で Python を使用して機械学習モデルを作成するには、次のクイック スタートに従ってください。

> [!div class="nextstepaction"]
> [クイック スタート: SQL Server Machine Learning Services を使用して Python で予測モデルを作成してスコア付けする](quickstart-python-train-score-model.md)

SQL Server Machine Learning Services の詳細については、次を参照してください。

- [SQL Server Machine Learning Services (Python と R) とは](../sql-server-machine-learning-services.md)
