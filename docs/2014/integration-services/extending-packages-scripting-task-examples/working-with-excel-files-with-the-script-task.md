---
title: スクリプト タスクを使用した Excel ファイルの操作 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Excel files
- Script task [Integration Services], examples
- Excel [Integration Services]
ms.assetid: b8fa110a-2c9c-4f5a-8fe1-305555640e44
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 52fcf25a0334edcff17ba024da501b248e9176cf
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85426469"
---
# <a name="working-with-excel-files-with-the-script-task"></a>スクリプト タスクを使用した Excel ファイルの操作
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には Excel 接続マネージャー、Excel ソース、Excel 変換先が用意されており、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel ファイル形式のスプレッドシートに保存されているデータを操作できます。 このトピックで説明する方法では、スクリプト タスクを使用して、使用可能な Excel のデータベース (ワークブック ファイル) およびテーブル (ワークシートおよび名前付き範囲) に関する情報を取得します。 これらのサンプルに簡単な変更を加えて、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB プロバイダーによってサポートされる他のすべてのファイルベース データ ソースを操作することができます。  
  
 [サンプルをテストするためのパッケージの構成](#configuring)  
  
 [例 1: Excel ファイルが存在するかどうかを確認する](#example1)  
  
 [例 2: Excel テーブルが存在するかどうかを確認する](#example2)  
  
 [例 3: フォルダー内の Excel ファイルの一覧を取得する](#example3)  
  
 [例 4: Excel ファイル内のテーブルの一覧を取得する](#example4)  
  
 [サンプルの結果の表示](#testing)  
  
> [!NOTE]  
>  複数のパッケージでより簡単に再利用できるタスクを作成する場合は、このスクリプト タスク サンプルのコードを基にした、カスタム タスクの作成を検討してください。 詳細については、「 [カスタム タスクの開発](../extending-packages-custom-objects/task/developing-a-custom-task.md)」を参照してください。  
  
##  <a name="configuring-a-package-to-test-the-samples"></a><a name="configuring"></a>サンプルをテストするためのパッケージの構成  
 このトピックのすべてのサンプルをテストする単一のパッケージを構成することができます。 これらのサンプルでは、同じパッケージ変数と同じ [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] クラスを数多く使用します。  
  
#### <a name="to-configure-a-package-for-use-with-the-examples-in-this-topic"></a>このトピックの例で使用するパッケージを構成するには  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で新しい [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] プロジェクトを作成し、編集のために既定のパッケージを開きます。  
  
2.  **変数**。 **[変数]** ウィンドウを開き、次の変数を定義します。  
  
    -   `String` 型の `ExcelFile`。 既存の Excel ワークブックの完全なパスとファイル名を入力します。  
  
    -   `String` 型の `ExcelTable`。 `ExcelFile` 変数の値で指定されたワークブック内の既存のワークシートまたは名前付き範囲の名前を入力します。 この値は、大文字と小文字が区別されます。  
  
    -   `Boolean` 型の `ExcelFileExists`。  
  
    -   `Boolean` 型の `ExcelTableExists`。  
  
    -   `String` 型の `ExcelFolder`。 少なくとも 1 つの Excel ワークブックを含むフォルダーの完全なパスを入力します。  
  
    -   `Object` 型の `ExcelFiles`。  
  
    -   `Object` 型の `ExcelTables`。  
  
3.  **ステートメントをインポート**します。 ほとんどのコード サンプルでは、スクリプト ファイルの先頭で次の [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 名前空間のいずれかまたは両方をインポートする必要があります。  
  
    -   ファイル システム操作用の `System.IO`。  
  
    -   Excel ファイルをデータ ソースとして開くための `System.Data.OleDb`。  
  
4.  **参照**。 Excel ファイルからスキーマ情報を読み取るコード サンプルでは、スクリプト プロジェクトで `System.Xml` 名前空間への追加の参照が必要です。  
  
5.  **[オプション]** ダイアログ ボックスの **[全般]** ページにある **[スクリプト言語]** オプションを使用して、スクリプト コンポーネントの既定のスクリプト言語を設定します。 詳細については、「 [General Page](../general-page-of-integration-services-designers-options.md)」を参照してください。  
  
##  <a name="example-1-description-check-whether-an-excel-file-exists"></a><a name="example1"></a> 例 1 の説明: Excel ファイルが存在するかどうかを確認する  
 この例では、`ExcelFile` 変数で指定された Excel ワークブック ファイルが存在するかどうかを判断し、その結果を `ExcelFileExists` 変数のブール値に設定します。 このブール値は、パッケージのワークフローを分岐させるために使用することができます。  
  
#### <a name="to-configure-this-script-task-example"></a>このスクリプト タスクの例を構成するには  
  
1.  パッケージに新しいスクリプトタスクを追加し、名前をに変更し `ExcelFileExists` ます。  
  
2.  **[スクリプト タスク エディター]** の **[スクリプト]** タブで **[ReadOnlyVariables]** をクリックし、次のいずれかの方法でプロパティ値を入力します。  
  
    -   「`ExcelFile`.  
  
         \- または -  
  
    -   プロパティフィールドの横にある省略記号ボタン ([**...**]) をクリックし、[**変数の選択**] ダイアログボックスで変数を選択し `ExcelFile` ます。  
  
3.  **[ReadWriteVariables]** をクリックし、次のいずれかの方法でプロパティ値を入力します。  
  
    -   「`ExcelFileExists`.  
  
         \- または -  
  
    -   プロパティフィールドの横にある省略記号ボタン ([**...**]) をクリックし、[**変数の選択**] ダイアログボックスで変数を選択し `ExcelFileExists` ます。  
  
4.  **[スクリプトの編集]** をクリックして、スクリプト エディターを開きます。  
  
5.  スクリプト ファイルの先頭に、`Imports` 名前空間の `System.IO` ステートメントを追加します。  
  
6.  次のコードを追加します。  
  
### <a name="example-1-code"></a>例 1 のコード  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    If File.Exists(fileToTest) Then  
      Dts.Variables("ExcelFileExists").Value = True  
    Else  
      Dts.Variables("ExcelFileExists").Value = False  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    string fileToTest;  
  
    fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
    if (File.Exists(fileToTest))  
    {  
      Dts.Variables["ExcelFileExists"].Value = true;  
    }  
    else  
    {  
      Dts.Variables["ExcelFileExists"].Value = false;  
    }  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
##  <a name="example-2-description-check-whether-an-excel-table-exists"></a><a name="example2"></a> 例 2 の説明: Excel テーブルが存在するかどうかを確認する  
 この例では、`ExcelTable` 変数で指定された Excel ワークシートまたは名前付き範囲が `ExcelFile` 変数で指定された Excel ワークブック ファイル内に存在するかどうかを判断し、その結果を `ExcelTableExists` 変数のブール値に設定します。 このブール値は、パッケージのワークフローを分岐させるために使用することができます。  
  
#### <a name="to-configure-this-script-task-example"></a>このスクリプト タスクの例を構成するには  
  
1.  パッケージに新しいスクリプトタスクを追加し、名前をに変更し `ExcelTableExists` ます。  
  
2.  **[スクリプト タスク エディター]** の **[スクリプト]** タブで **[ReadOnlyVariables]** をクリックし、次のいずれかの方法でプロパティ値を入力します。  
  
    -   型 `ExcelTable` を `ExcelFile` コンマで区切って入力します。`.`  
  
         \- または -  
  
    -   プロパティフィールドの横にある省略記号ボタン ([**...**]) をクリックし、[**変数の選択**] ダイアログボックスで、 `ExcelTable` 変数と変数を選択し `ExcelFile` ます。  
  
3.  **[ReadWriteVariables]** をクリックし、次のいずれかの方法でプロパティ値を入力します。  
  
    -   「`ExcelTableExists`.  
  
         \- または -  
  
    -   プロパティフィールドの横にある省略記号ボタン ([**...**]) をクリックし、[**変数の選択**] ダイアログボックスで変数を選択し `ExcelTableExists` ます。  
  
4.  **[スクリプトの編集]** をクリックして、スクリプト エディターを開きます。  
  
5.  スクリプト プロジェクトに `System.Xml` アセンブリへの参照を追加します。  
  
6.  スクリプト ファイルの先頭に、`Imports` 名前空間と `System.IO` 名前空間の `System.Data.OleDb` ステートメントを追加します。  
  
7.  次のコードを追加します。  
  
### <a name="example-2-code"></a>例 2 のコード  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
    Dim tableToTest As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim excelTables As DataTable  
    Dim excelTable As DataRow  
    Dim currentTable As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    tableToTest = Dts.Variables("ExcelTable").Value.ToString  
  
    Dts.Variables("ExcelTableExists").Value = False  
    If File.Exists(fileToTest) Then  
      connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=" & fileToTest & _  
        ";Extended Properties=Excel 8.0"  
      excelConnection = New OleDbConnection(connectionString)  
      excelConnection.Open()  
      excelTables = excelConnection.GetSchema("Tables")  
      For Each excelTable In excelTables.Rows  
        currentTable = excelTable.Item("TABLE_NAME").ToString  
        If currentTable = tableToTest Then  
          Dts.Variables("ExcelTableExists").Value = True  
        End If  
      Next  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
    public void Main()  
        {  
            string fileToTest;  
            string tableToTest;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable excelTables;  
            string currentTable;  
  
            fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
            tableToTest = Dts.Variables["ExcelTable"].Value.ToString();  
  
            Dts.Variables["ExcelTableExists"].Value = false;  
            if (File.Exists(fileToTest))  
            {  
                connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" +  
                "Data Source=" + fileToTest + ";Extended Properties=Excel 8.0";  
                excelConnection = new OleDbConnection(connectionString);  
                excelConnection.Open();  
                excelTables = excelConnection.GetSchema("Tables");  
                foreach (DataRow excelTable in excelTables.Rows)  
                {  
                    currentTable = excelTable["TABLE_NAME"].ToString();  
                    if (currentTable == tableToTest)  
                    {  
                        Dts.Variables["ExcelTableExists"].Value = true;  
                    }  
                }  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
}  
```  
  
##  <a name="example-3-description-get-a-list-of-excel-files-in-a-folder"></a><a name="example3"></a> 例 3 の説明: フォルダー内の Excel ファイルの一覧を取得する  
 この例では、`ExcelFolder` 変数の値で指定されたフォルダー内で検索された Excel ファイルの一覧を配列に代入し、その配列を `ExcelFiles` 変数にコピーします。 Foreach from Variable 列挙子を使用して、配列内のファイルを繰り返し処理することができます。  
  
#### <a name="to-configure-this-script-task-example"></a>このスクリプト タスクの例を構成するには  
  
1.  パッケージに新しいスクリプト タスクを追加し、その名前を **GetExcelFiles** に変更します。  
  
2.  **[スクリプト タスク エディター]** を開き、**[スクリプト]** タブで **[ReadOnlyVariables]** をクリックし、次のいずれかの方法でプロパティ値を入力します。  
  
    -   「`ExcelFolder`」と入力します。  
  
         \- または -  
  
    -   プロパティフィールドの横にある省略記号ボタン ([**...**]) をクリックし、[**変数の選択**] ダイアログボックスで [excelfolder] 変数を選択します。  
  
3.  **[ReadWriteVariables]** をクリックし、次のいずれかの方法でプロパティ値を入力します。  
  
    -   「`ExcelFiles`.  
  
         \- または -  
  
    -   プロパティフィールドの横にある省略記号ボタン ([**...**]) をクリックし、[**変数の選択**] ダイアログボックスで [excelfiles] 変数を選択します。  
  
4.  **[スクリプトの編集]** をクリックして、スクリプト エディターを開きます。  
  
5.  スクリプト ファイルの先頭に、`Imports` 名前空間の `System.IO` ステートメントを追加します。  
  
6.  次のコードを追加します。  
  
### <a name="example-3-code"></a>例 3 のコード  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const FILE_PATTERN As String = "*.xls"  
  
    Dim excelFolder As String  
    Dim excelFiles As String()  
  
    excelFolder = Dts.Variables("ExcelFolder").Value.ToString  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN)  
  
    Dts.Variables("ExcelFiles").Value = excelFiles  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    const string FILE_PATTERN = "*.xls";  
  
    string excelFolder;  
    string[] excelFiles;  
  
    excelFolder = Dts.Variables["ExcelFolder"].Value.ToString();  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN);  
  
    Dts.Variables["ExcelFiles"].Value = excelFiles;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
### <a name="alternate-solution"></a>代替ソリューション  
 スクリプト タスクを使用して Excel ファイルの一覧を配列に集める代わりに、ForEach File 列挙子を使用してフォルダー内のすべての Excel ファイルを繰り返し処理することもできます。 詳細については、「[Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する方法](../control-flow/foreach-loop-container.md)」を参照してください。  
  
##  <a name="example-4-description-get-a-list-of-tables-in-an-excel-file"></a><a name="example4"></a> 例 4 の説明: Excel ファイル内のテーブルの一覧を取得する  
 この例では、`ExcelFile` 変数の値で指定された Excel ワークブック ファイル内で検索されたワークシートまたは名前付き範囲の一覧を配列に代入し、その配列を `ExcelTables` 変数にコピーします。 Foreach from Variable 列挙子を使用して、配列内のテーブルを繰り返し処理することができます。  
  
> [!NOTE]  
>  Excel ブック内のテーブルの一覧には、ワークシート ($ サフィックスが付きます) と名前付き範囲が含まれます。 ワークシートまたは名前付き範囲のみを一覧からフィルター選択する必要がある場合は、そのためのコードを追加する必要があります。  
  
#### <a name="to-configure-this-script-task-example"></a>このスクリプト タスクの例を構成するには  
  
1.  パッケージに新しいスクリプト タスクを追加し、その名前を **GetExcelTables** に変更します。  
  
2.  **[スクリプト タスク エディター]** を開き、**[スクリプト]** タブで **[ReadOnlyVariables]** をクリックし、次のいずれかの方法でプロパティ値を入力します。  
  
    -   「`ExcelFile`.  
  
         \- または -  
  
    -   プロパティフィールドの横にある省略記号ボタン ([**...**]) をクリックし、[**変数の選択**] ダイアログボックスで [excelfile] 変数を選択します。  
  
3.  **[ReadWriteVariables]** をクリックし、次のいずれかの方法でプロパティ値を入力します。  
  
    -   「`ExcelTables`.  
  
         \- または -  
  
    -   プロパティフィールドの横にある省略記号ボタン ([**...**]) をクリックし、[**変数の選択**] ダイアログボックスで [excelitems] 変数を選択します。  
  
4.  **[スクリプトの編集]** をクリックして、スクリプト エディターを開きます。  
  
5.  スクリプトプロジェクト内の名前空間への参照を追加 `System.Xml` します。  
  
6.  スクリプト ファイルの先頭に、`Imports` 名前空間の `System.Data.OleDb` ステートメントを追加します。  
  
7.  次のコードを追加します。  
  
### <a name="example-4-code"></a>例 4 のコード  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim excelFile As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim tablesInFile As DataTable  
    Dim tableCount As Integer = 0  
    Dim tableInFile As DataRow  
    Dim currentTable As String  
    Dim tableIndex As Integer = 0  
  
    Dim excelTables As String()  
  
    excelFile = Dts.Variables("ExcelFile").Value.ToString  
    connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=" & excelFile & _  
        ";Extended Properties=Excel 8.0"  
    excelConnection = New OleDbConnection(connectionString)  
    excelConnection.Open()  
    tablesInFile = excelConnection.GetSchema("Tables")  
    tableCount = tablesInFile.Rows.Count  
    ReDim excelTables(tableCount - 1)  
    For Each tableInFile In tablesInFile.Rows  
      currentTable = tableInFile.Item("TABLE_NAME").ToString  
      excelTables(tableIndex) = currentTable  
      tableIndex += 1  
    Next  
  
    Dts.Variables("ExcelTables").Value = excelTables  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            string excelFile;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable tablesInFile;  
            int tableCount = 0;  
            string currentTable;  
            int tableIndex = 0;  
  
            string[] excelTables = new string[5];  
  
            excelFile = Dts.Variables["ExcelFile"].Value.ToString();  
            connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" +  
                "Data Source=" + excelFile + ";Extended Properties=Excel 8.0";  
            excelConnection = new OleDbConnection(connectionString);  
            excelConnection.Open();  
            tablesInFile = excelConnection.GetSchema("Tables");  
            tableCount = tablesInFile.Rows.Count;  
  
            foreach (DataRow tableInFile in tablesInFile.Rows)  
            {  
                currentTable = tableInFile["TABLE_NAME"].ToString();  
                excelTables[tableIndex] = currentTable;  
                tableIndex += 1;  
            }  
  
            Dts.Variables["ExcelTables"].Value = excelTables;  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
### <a name="alternate-solution"></a>代替ソリューション  
 スクリプト タスクを使用して Excel テーブルの一覧を配列に集める代わりに、ForEach ADO.NET Schema Rowset 列挙子を使用して Excel ワークブック ファイル内のすべてのテーブル (つまり、ワークシートと名前付き範囲) を繰り返し処理することもできます。 詳細については、「[Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する方法](../control-flow/foreach-loop-container.md)」を参照してください。  
  
##  <a name="displaying-the-results-of-the-samples"></a><a name="testing"></a>サンプルの結果を表示する  
 このトピックの各例を同じパッケージで構成した場合は、すべてのスクリプト タスクを、すべての例の出力を表示する追加のスクリプト タスクに接続することができます。  
  
#### <a name="to-configure-a-script-task-to-display-the-output-of-the-examples-in-this-topic"></a>このトピックの例の出力を表示するスクリプト タスクを構成するには  
  
1.  パッケージに新しいスクリプト タスクを追加し、その名前を **DisplayResults** に変更します。  
  
2.  4 つのスクリプト タスク例のそれぞれを互いに接続し、各タスクが、前のタスクが正常に完了した後に実行されるようにして、4 番目のタスク例を **DisplayResults** タスクに接続します。  
  
3.  **[スクリプト タスク エディター]** で **DisplayResults** タスクを開きます。  
  
4.  **[スクリプト]** タブで **[ReadOnlyVariables]** をクリックし、次のいずれかの方法で、「[サンプルをテストするためのパッケージの構成](#configuring)」で一覧表示されている 7 つの変数のすべてを追加します。  
  
    -   各変数の名前をコンマで区切って入力します。  
  
         \- または -  
  
    -   プロパティフィールドの横にある省略記号ボタン ([**...**]) をクリックし、[**変数の選択**] ダイアログボックスで変数を選択します。  
  
5.  **[スクリプトの編集]** をクリックして、スクリプト エディターを開きます。  
  
6.  スクリプト ファイルの先頭に、`Imports` 名前空間と `Microsoft.VisualBasic` 名前空間の `System.Windows.Forms` ステートメントを追加します。  
  
7.  次のコードを追加します。  
  
8.  パッケージを実行し、メッセージ ボックスに表示される結果を調べます。  
  
### <a name="code-to-display-the-results"></a>結果を表示するコード  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const EOL As String = ControlChars.CrLf  
  
    Dim results As String  
    Dim filesInFolder As String()  
    Dim fileInFolder As String  
    Dim tablesInFile As String()  
    Dim tableInFile As String  
  
    results = _  
      "Final values of variables:" & EOL & _  
      "ExcelFile: " & Dts.Variables("ExcelFile").Value.ToString & EOL & _  
      "ExcelFileExists: " & Dts.Variables("ExcelFileExists").Value.ToString & EOL & _  
      "ExcelTable: " & Dts.Variables("ExcelTable").Value.ToString & EOL & _  
      "ExcelTableExists: " & Dts.Variables("ExcelTableExists").Value.ToString & EOL & _  
      "ExcelFolder: " & Dts.Variables("ExcelFolder").Value.ToString & EOL & _  
      EOL  
  
    results &= "Excel files in folder: " & EOL  
    filesInFolder = DirectCast(Dts.Variables("ExcelFiles").Value, String())  
    For Each fileInFolder In filesInFolder  
      results &= " " & fileInFolder & EOL  
    Next  
    results &= EOL  
  
    results &= "Excel tables in file: " & EOL  
    tablesInFile = DirectCast(Dts.Variables("ExcelTables").Value, String())  
    For Each tableInFile In tablesInFile  
      results &= " " & tableInFile & EOL  
    Next  
  
    MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information)  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            const string EOL = "\r";  
  
            string results;  
            string[] filesInFolder;  
            //string fileInFolder;  
            string[] tablesInFile;  
            //string tableInFile;  
  
            results = "Final values of variables:" + EOL + "ExcelFile: " + Dts.Variables["ExcelFile"].Value.ToString() + EOL + "ExcelFileExists: " + Dts.Variables["ExcelFileExists"].Value.ToString() + EOL + "ExcelTable: " + Dts.Variables["ExcelTable"].Value.ToString() + EOL + "ExcelTableExists: " + Dts.Variables["ExcelTableExists"].Value.ToString() + EOL + "ExcelFolder: " + Dts.Variables["ExcelFolder"].Value.ToString() + EOL + EOL;  
  
            results += "Excel files in folder: " + EOL;  
            filesInFolder = (string[])(Dts.Variables["ExcelFiles"].Value);  
            foreach (string fileInFolder in filesInFolder)  
            {  
                results += " " + fileInFolder + EOL;  
            }  
            results += EOL;  
  
            results += "Excel tables in file: " + EOL;  
            tablesInFile = (string[])(Dts.Variables["ExcelTables"].Value);  
            foreach (string tableInFile in tablesInFile)  
            {  
                results += " " + tableInFile + EOL;  
            }  
  
            MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
![Integration Services アイコン (小)](../media/dts-16.gif "Integration Services のアイコン (小)")**は Integration Services で最新の**状態を維持  <br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照する](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [Excel 接続マネージャー](../connection-manager/excel-connection-manager.md)   
 [Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する](../control-flow/foreach-loop-container.md)  
  
  
