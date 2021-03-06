---
title: HTTP 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1bf206182c73f179857ab6197fac3b7ae36a1dbc
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438459"
---
# <a name="http-connection-manager"></a>HTTP 接続マネージャー
  HTTP 接続により、パッケージが HTTP を使用してファイルを送受信することで、Web サーバーにアクセスできるようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる Web サービス タスクでは、この接続マネージャーが使用されます。  
  
 HTTP 接続マネージャーをパッケージに追加するときは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって、実行時に HTTP 接続を解決する接続マネージャーを作成し、接続マネージャーのプロパティを設定して、接続マネージャーをパッケージの `Connections` コレクションに追加します。  
  
 `ConnectionManagerType`接続マネージャーのプロパティがに設定されています。`HTTP.`  
  
 HTTP 接続マネージャーは、次の方法で構成できます。  
  
-   資格情報を使用します。 接続マネージャーが資格情報を使用する場合、プロパティにユーザー名、パスワード、およびドメインが含まれます。  
  
    > [!IMPORTANT]  
    >  HTTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
-   クライアント証明書を使用します。 接続マネージャーがクライアント証明書を使用する場合、プロパティに証明書名が含まれます。  
  
-   サーバーへの接続のタイムアウトと、データを書き込むチャンク サイズを指定します。  
  
-   プロキシ サーバーを使用します。 プロキシ サーバーは、資格情報を使用するように構成することや、プロキシ サーバーをバイパスして、代わりにローカル アドレスを使用するように構成することもできます。  
  
## <a name="configuration-of-the-http-connection-manager"></a>HTTP 接続マネージャーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[HTTP 接続マネージャー エディター] ([サーバー] ページ)](../http-connection-manager-editor-server-page.md)  
  
-   [[HTTP 接続マネージャー エディター] ([プロキシ] ページ)](../http-connection-manager-editor-proxy-page.md)  
  
 プログラムによる接続マネージャーの構成の詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Web サービスタスク](../control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41; の接続](integration-services-ssis-connections.md)  
  
  
