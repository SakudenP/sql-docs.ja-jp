---
title: ポリシー ベースの管理ファセットの操作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- viewing Policy-Based Management facets
- facets [Policy-Based Management], copying
- facets [Policy-Based Management], viewing
- copying Policy-Based Management facets
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 179b5431f0531b29b4867f405ee88e4567ddb5d8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "68054399"
---
# <a name="working-with-policy-based-management-facets"></a>ポリシー ベースの管理ファセットの操作
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ポリシー ベースの管理ファセットは、管理対象の領域に関連する一連の論理プロパティです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、いくつかの定義済みファセットが用意されています。 たとえば、セキュリティ構成ファセットは既定で無効になる機能をプロパティとして定義します。  
  
 同様の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境を多数管理する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の 1 つのインスタンスでファセットを構成し、ファセットの状態をファイルにコピーして、そのファイルを別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにポリシーとしてインポートできます。 状態がポリシーに変換されたら、そのポリシーを別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス、インスタンス オブジェクト、データベース、またはデータベース オブジェクトに適用できます。  
  
 このトピックでは、ファセットの状態を XML ファイルにコピーする方法について説明します。  
  
##  <a name="permissions"></a><a name="BeforeYouBegin"></a> Permissions  
 このトピックの手順では、msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="viewing-and-copying-facet-states"></a>ファセットの状態の表示とコピー  
 [SQL Server オブジェクトのポリシーベースの管理ファセットの表示](../../relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [XML ファイルへのポリシーベースの管理ファセットの状態のコピー](../../relational-databases/policy-based-management/copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
