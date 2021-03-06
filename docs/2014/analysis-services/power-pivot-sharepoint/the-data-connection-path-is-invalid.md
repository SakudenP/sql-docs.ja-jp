---
title: 'ブックのデータ接続パスがローカル ドライブ上のファイルを指しているか、無効な URI です。 次の接続を更新できませんでした: PowerPivot Data |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: bd22e41a-0931-4d32-888a-633a3046fc5e
author: minewiskan
ms.author: owend
ms.openlocfilehash: f9000b78601bfb4ea9abae5cd1c63387fe502256
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547784"
---
# <a name="the-data-connection-path-in-the-workbook-points-to-a-file-on-the-local-drive-or-is-an-invalid-uri-the-following-connections-failed-to-refresh-powerpivot-data"></a>ブックのデータ接続パスがローカル ドライブ上のファイルを指しているか、無効な URI です。 次の接続の更新に失敗しました:PowerPivot データ
  PowerPivot データを含む Excel ブックで、Excel Services は、埋め込みデータ ソースに接続できない場合にこのエラーを返します。  
  
## <a name="details"></a>詳細情報  
  
|||  
|-|-|  
|適用対象|PowerPivot for SharePoint|  
|製品バージョン|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|信頼できるデータ接続ライブラリにある .odc ファイルからのデータ接続のみ許可するように Excel Services が構成されています。|  
|メッセージ テキスト|ブックのデータ接続パスがローカル ドライブ上のファイルを指しているか、無効な URI です。 次の接続の更新に失敗しました:PowerPivot データ|  
  
## <a name="explanation"></a>説明  
 PowerPivot ブックには、埋め込みデータ接続が含まれています。 スライサーやフィルターを介したブックの操作をサポートするには、埋め込まれている接続情報を使用した外部データ アクセスを許可するように Excel Services を構成する必要があります。 外部データ アクセスは、ファームの PowerPivot サーバーに読み込まれる PowerPivot データを取得するのに必要です。  
  
## <a name="user-action"></a>ユーザーの操作  
 埋め込みデータ ソース接続を許可するように構成設定を変更します。  
  
1.  サーバーの全体管理で、[アプリケーション管理] の [**サービスアプリケーションの管理**] をクリックします。  
  
2.  **[Excel Services アプリケーション]** をクリックします。  
  
3.  **[信頼できるファイル保存場所]** をクリックします。  
  
4.  **[http://]** または構成する場所をクリックします。  
  
5.  [外部データ] の [外部データの許可] で、 **[信頼できるデータ接続ライブラリと、埋め込まれている接続]** をクリックします。  
  
6.  **[OK]** をクリックします。  
  
 または、PowerPivot ブックが含まれるサイト用に新しく信頼できる場所を作成し、そのサイトの構成設定だけを変更することもできます。 詳細については、「 [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)」を参照してください。  
  
  
