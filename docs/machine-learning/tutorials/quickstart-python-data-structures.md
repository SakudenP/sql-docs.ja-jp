---
title: クイック スタート:Python のデータ構造
description: このクイックスタートでは、Python と SQL Server Machine Learning Services でデータ構造とデータ オブジェクトを使用する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3023287504cbb7b25e194b53d0957e82405d1ea8
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606695"
---
# <a name="quickstart-data-structures-and-objects-using-python-in-sql-server-machine-learning-services"></a>クイック スタート:SQL Server Machine Learning Services で Python を使用するデータ構造とオブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) または[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)で Python を使用するときに、データ構造体とデータ型を使用する方法について説明します。 Python と SQL Server 間のデータの移動と、発生する可能性のある一般的な問題について説明します。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で Python を使用するときに、データ構造体とデータ型を使用する方法について説明します。 Python と SQL Server 間のデータの移動と、発生する可能性のある一般的な問題について説明します。
::: moniker-end

SQL Server は Python **pandas** パッケージに依存しており、それは表形式データの操作に最適です。 ただし、Python から SQL Server にスカラーを渡して、「ただ動作する」ことを期待することはできません。 このクイックスタートでは、いくつかの基本的なデータ構造の定義を確認し、Python と SQL Server の間で表形式のデータを渡すときに発生する可能性がある他の問題に備えます。

前もって理解しておくべき概念は次のとおりです。

- データ フレームとは_複数の_列を含むテーブルです。
- データ フレームの単一の列は、シリーズと呼ばれるリスト ライクのオブジェクトです。
- データ フレームの単一の値はセルと呼ばれ、インデックスによってアクセスされます。

data.frame に表形式構造が必要な場合、計算の単一の結果をデータ フレームとして公開するにはどうすればよいでしょうか。 1 つの答えは、単一のスカラー値をシリーズとして表すことです。これは、データ フレームに簡単に変換できます。 

> [!NOTE]
> 日付を返す場合、SQL の Python では DATETIME が使用され、日付の範囲は 1753-01-01 (-53690) ~ 9999-12-31 (2958463) に制限されています。 

## <a name="prerequisites"></a>前提条件

このクイック スタートを実行するには、次の前提条件を用意しておく必要があります。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
- SQL Server Machine Learning Services。 Machine Learning Services をインストールする方法については、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)または [Linux インストール ガイド](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)に関するページを参照してください。 [SQL Server ビッグ データ クラスターで Machine Learning Services を有効にする](../../big-data-cluster/machine-learning-services.md)こともできます。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
- SQL Server Machine Learning Services。 Machine Learning Services をインストールする方法については、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)に関するページを参照してください。 
::: moniker-end
- また、Python スクリプトを含む SQL クエリを実行するためのツールも必要です。 これらのスクリプトは、SQL Server インスタンスに接続し、T-SQL クエリまたはストアド プロシージャを実行できる限り、任意のデータベース管理ツールまたはクエリ ツールを使用して実行できます。 このクイックスタートでは [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) を使用します。

## <a name="scalar-value-as-a-series"></a>シリーズとしてのスカラー値

この例では、単純な数値演算を行い、スカラーをシリーズに変換します。

1. シリーズにはインデックスが必要です。このインデックスは、次に示すように手動で割り当てることも、プログラムで割り当てることもできます。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   print(c)
   s = pandas.Series(c, index =["simple math example 1"])
   print(s)
   '
   ```

   シリーズは data.frame に変換されていないため、[メッセージ] ウィンドウには値が返されます。しかし、結果をより表に近い形式で表示することができます。

   **結果**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. シリーズの長さを増やすには、配列を使用して新しい値を追加します。 

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   '
   ```

   インデックスを指定しない場合は、0 から始まり配列の長さで終わる値を持つインデックスが生成されます。

   **結果**

   ```text
   STDOUT message(s) from external script: 
   0    0.5
   1    2.0
   dtype: float64
   ```

1. **index** 値の数を増やしても、新しい **data** 値を追加していない場合、データ値はシリーズを埋めるように繰り返し格納されます。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   '
   ```

   **結果**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   simple math example 2    0.5
   dtype: float64
   ```

## <a name="convert-series-to-data-frame"></a>シリーズをデータ フレームに変換する

スカラー数値演算の結果を表形式構造に変換した後、それらを SQL Server で処理できる形式に変換する必要があります。

1. シリーズを data.frame に変換するには、pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) メソッドを呼び出します。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s)
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   結果は次のようになります。 インデックスを使用して data.frame から特定の値を取得する場合でも、インデックス値は出力の一部とはなりません。

   **結果**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>値を data.frame に出力する

次に、2 つの計算結果のシリーズから特定の値を data.frame に出力します。 最初のものは、Python によって生成される連続値のインデックスをもちます。 2 番目のものは、任意の文字列値のインデックスを使用します。

1. 次の例では、整数インデックスを使用してシリーズから値を取得します。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s, index=[1])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **結果**

   |ResultValue|
   |------|
   |2.0|

   自動生成されたインデックスは 0 から始まることに注意してください。 範囲外のインデックス値を使用して、何が起こるかを確認してください。

1. 次に、文字列インデックスを使用して、他のデータ フレームから 1 つの値を取得します。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   df = pd.DataFrame(s, index=["simple math example 1"])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **結果**

   |ResultValue|
   |------|
   |0.5|

   数値インデックスを使用してこのシリーズから値を取得しようとすると、エラーが発生します。

## <a name="next-steps"></a>次のステップ

SQL Server で高度な Python 関数を記述する方法については、次のクイックスタートを参照してください。

> [!div class="nextstepaction"]
> [SQL Server Machine Learning Services を使用した高度な Python 関数の作成](quickstart-python-functions.md)

SQL Server Machine Learning Services での Python の使用に関する詳細については、次の記事を参照してください。

- [Python での予測モデルの作成とスコア付け](quickstart-python-train-score-model.md)
- [SQL Server Machine Learning Services (Python と R) とは](../sql-server-machine-learning-services.md)
