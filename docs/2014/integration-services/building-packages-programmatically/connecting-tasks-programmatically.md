---
title: プログラムによるタスクの接続 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- constraints [Integration Services]
ms.assetid: 23668e88-cef4-4009-a9cf-38e607eab7a2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ef26da592675d9d3b6c7a08b08ebc112a84e55e9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439229"
---
# <a name="connecting-tasks-programmatically"></a>プログラムによるタスクの接続
  優先順位制約は、<xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> クラスとしてオブジェクト モデル内に表されるもので、パッケージ内での <xref:Microsoft.SqlServer.Dts.Runtime.Executable> オブジェクトの実行順序を確立します。 優先順位制約を使用すると、パッケージ内のコンテナーやタスクを、直前のコンテナーやタスクの実行結果に依存して実行させることができます。 2 つの <xref:Microsoft.SqlServer.Dts.Runtime.Executable> オブジェクト間の優先順位制約は、コンテナー オブジェクトの <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints.Add%2A> コレクションにある <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints> メソッドを呼び出すことによって確立されます。 2 つの実行可能オブジェクト間の制約を作成したら、<xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> プロパティを設定して、制約で定義されている 2 番目の実行可能オブジェクトを実行する条件を設定します。  
  
 次の表で説明するように、<xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.EvalOp%2A> プロパティに指定する値に応じて、1 つの優先順位制約内で制約と式の両方を使用できます。  
  
|EvalOp プロパティの値|説明|  
|----------------------------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Constraint>|制約付きコンテナーまたは制約付きタスクを実行するかどうかを実行結果が決定するように指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> プロパティを <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列挙の目的の値に設定します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Expression>|制約付きコンテナーまたは制約付きタスクを実行するかどうかを式の値で決定するように指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> プロパティを設定します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionAndConstraint>|実行する制約付きコンテナーまたは制約付きタスクに対して、制約結果が発生し、式が評価するように指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> プロパティおよび <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> プロパティの両方を設定し、その <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> プロパティを `true` に設定します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionOrConstraint>|実行する制約付きコンテナーまたは制約付きタスクに対して、制約結果が発生するか、または式が評価するように指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> プロパティおよび <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> プロパティの両方を設定し、その <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> プロパティを `false` に設定します。|  
  
 次のコード例では、パッケージにタスクを 2 つ追加します。 次に、タスクの間に <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> を作成し、第 1 のタスクが終了するまで第 2 のタスクは実行しないように設定します。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      // Add a File System task.  
      Executable eFileTask1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost1 = eFileTask1 as TaskHost;  
  
      // Add a second File System task.  
      Executable eFileTask2 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost2 = eFileTask2 as TaskHost;  
  
      // Put a precedence constraint between the tasks.  
      // Set the constraint to specify that the second File System task cannot run  
      // until the first File System task finishes.  
      PrecedenceConstraint pcFileTasks =   
        p.PrecedenceConstraints.Add((Executable)thFileHost1, (Executable)thFileHost2);  
      pcFileTasks.Value = DTSExecResult.Completion;  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task.  
    Dim eFileTask1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost1 As TaskHost = CType(eFileTask1, TaskHost)  
  
    ' Add a second File System task.  
    Dim eFileTask2 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost2 As TaskHost = CType(eFileTask2, TaskHost)  
  
    ' Put a precedence constraint between the tasks.  
    ' Set the constraint to specify that the second File System task cannot run  
    ' until the first File System task finishes.  
    Dim pcFileTasks As PrecedenceConstraint = _  
      p.PrecedenceConstraints.Add(CType(thFileHost1, Executable), CType(thFileHost2, Executable))  
    pcFileTasks.Value = DTSExecResult.Completion  
  
  End Sub  
  
End Module  
```  
  
![Integration Services アイコン (小)](../media/dts-16.gif "Integration Services のアイコン (小)")**は Integration Services で最新の**状態を維持  <br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照する](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [プログラムによるデータ フロー タスクの追加](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
  
  
