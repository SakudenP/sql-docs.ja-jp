---
title: ソリューションとプロジェクトを管理するためのファイル | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4d1599e7f762cc35c91389e170abcc32b559c2a2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062051"
---
# <a name="files-that-manage-solutions-and-projects"></a>ソリューションとプロジェクトを管理するためのファイル
  このトピックでは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 固有のファイルの種類について説明します。 既定では、すべてのソリューションとプロジェクトが \My Documents\SQL Server Management Studio\Projects に作成されます。  
  
## <a name="management-studio-solution-files"></a>Management Studio のソリューション ファイル  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] や [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio とは異なるファイルの種類が使用されます。 そのため、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のソリューションを [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] や Visual Studio で開くことはできません。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のソリューション ファイルの場合、ソリューション エクスプローラーを使用して、ファイルを管理するためのグラフィカル インターフェイスを表示できます。  
  
|拡張機能|ファイルの種類|説明|作成者|  
|---------------|---------------|-----------------|----------------|  
|.ssmssln|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ソリューション オブジェクト|環境に対して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプロジェクト、プロジェクト項目、およびソリューションのディスク上の場所に対する参照を提供します。|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
  
## <a name="management-studio-project-files"></a>Management Studio のプロジェクト ファイル  
 ソリューションにソリューション ファイル (つまり、ソリューション内のオブジェクトを管理するためのファイル) があるのと同じように、プロジェクトにはプロジェクト ファイルがあります。 プロジェクトのために [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] によって作成されるプロジェクト ファイルの種類は、プロジェクトの作成に使用するテンプレートによって異なります。 次の表に、各プロジェクトで作成されるファイルの種類をまとめます。  
  
|拡張機能|プロジェクト テンプレート|  
|---------------|----------------------|  
|.ssmssqlproj|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スクリプト プロジェクト|  
|.ssmsasproj|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] スクリプト プロジェクト|  
  
## <a name="location-of-solution-level-files"></a>ソリューション レベルのファイルの場所  
 既定では、ソリューション レベルのファイルは、そのソリューションで作成された最初のプロジェクトの物理ディレクトリに作成されます。 ソリューションを作成することによってソリューションのディレクトリを指定することも、新しいプロジェクトを作成するときにディレクトリを指定することも可能です。  
  
 ソリューション エクスプローラーに表示される論理構造とよく似たディレクトリ構造があれば、プロジェクト ファイルとソリューション ファイルを見つけることや、チーム内の他の開発者と共有することが容易になります。  
  
## <a name="see-also"></a>参照  
 [エンコードを使用したファイルの管理](manage-files-with-encoding.md)   
 [その他のファイル](miscellaneous-files.md)   
 [ソリューション エクスプローラー](solution-explorer.md)   
 [ソリューション &#40;SQL Server Management Studio&#41;](solutions-sql-server-management-studio.md)   
 [プロジェクト &#40;SQL Server Management Studio&#41;](projects-sql-server-management-studio.md)   
 [ソリューション エクスプローラーのソース管理](../../database-engine/solution-explorer-source-control.md)  
  
  
