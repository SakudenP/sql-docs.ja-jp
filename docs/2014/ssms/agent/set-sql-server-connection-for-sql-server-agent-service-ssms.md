---
title: SQL Server エージェントサービス (SQL Server Management Studio) の SQL Server 接続を設定します。Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
author: stevestein
ms.author: sstein
ms.openlocfilehash: 686e7026495c827101b279ee779db0e30852bb49
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067586"
---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service-sql-server-management-studio"></a>SQL Server エージェント サービスの SQL Server 接続の設定 (SQL Server Management Studio)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssDE](../../includes/ssde-md.md)] を使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] エージェントと [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]間の接続を設定する方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスでは、Windows 認証を使用して、SQL Server のローカル インスタンスに接続できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **SQL Server エージェントの SQL Server 接続を設定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   オブジェクト エクスプローラーに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ノードが表示されるのは、このノードの使用権限がある場合に限られます。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証がサポートされません。 このオプションは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を管理している場合にのみ使用できます。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの機能を実行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固定サーバー ロールの **sysadmin** のメンバーであるアカウントの資格情報を使用するように構成する必要があります。 このアカウントには、次の Windows 権限が必要です。  
  
-   サービスとしてログオン (SeServiceLogonRight)  
  
-   プロセス レベル トークンを置き換える (SeAssignPrimaryTokenPrivilege)  
  
-   スキャン チェックを行わない (SeChangeNotifyPrivilege)  
  
-   プロセスに対してメモリ クォータを調整する (SeIncreaseQuotaPrivilege)  
  
 エージェントサービスアカウントに必要な Windows アクセス許可の詳細については [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、「 [SQL Server エージェントサービスのアカウントの選択](select-an-account-for-the-sql-server-agent-service.md)」および「 [Windows サービスアカウントとアクセス許可の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-set-the-sql-server-connection"></a>SQL Server の接続を設定するには  
  
1.  **オブジェクト エクスプローラー**で、SQL Server エージェント サービスへの接続を設定するサーバーをプラス記号をクリックして展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** を選択します。  
  
3.  **[SQL Server エージェントのプロパティ]** ダイアログ ボックスの **[ページの選択]** で **[接続]** をクリックします。  
  
4.  **[SQL Server 接続]** で、**[Windows 認証を使用する]** を選択して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが  Windows 認証を使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続できるようにします。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のデータベースへの接続には Windows 認証が必要です。  
  
  
