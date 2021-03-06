---
title: オブジェクトを使用した RDS プログラミングモデル |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: rothja
ms.author: jroth
ms.openlocfilehash: 5f41fd577b470493aa6a53c8ea9ad760287a3507
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747744"
---
# <a name="rds-programming-model-with-objects"></a>RDS のプログラミング モデルとオブジェクト
RDS の目標は、IIS などの中継局を介してデータソースにアクセスし、更新することです。 プログラミングモデルは、この目標を達成するために必要なアクティビティのシーケンスを指定します。 オブジェクトモデルは、メソッドとプロパティがプログラミングモデルに影響を与えるオブジェクトを指定します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および[Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416)」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)に移行する必要があります。  
  
 RDS には、次の一連の操作を実行するための手段が用意されています。  
  
-   サーバーで呼び出されるプログラムを指定し、クライアント (RDS) から参照する方法 (プロキシ) を取得し[ます。領域スペース](../../../ado/reference/rds-api/dataspace-object-rds.md))。  
  
-   サーバープログラムを起動します。 データソースを識別するパラメーターと、発行するコマンド (プロキシまたは RDS) をサーバープログラムに渡し[ます。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md))。  
  
-   サーバープログラムは、通常は ADO を使用して、データソースから[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトを取得します。 必要に応じて、**レコードセット**オブジェクトがサーバー上で処理されます ([RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md))。  
  
-   サーバープログラムは、最後の**レコードセット**オブジェクトをクライアントアプリケーション (プロキシ) に返します。  
  
-   クライアントでは、**レコードセット**オブジェクトは、ビジュアルコントロール (ビジュアルコントロールおよび RDS) で簡単に使用できるフォームに配置され**ます。DataControl**)。  
  
-   **Recordset**オブジェクトへの変更は、サーバーに送り返され、データソースの更新に使用され**ます (RDS.DataControl**または**RDSServer**)。  
  
## <a name="see-also"></a>参照  
 [RDS オブジェクトモデルの概要](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [領域スペースオブジェクト (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS のシナリオ](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS チュートリアル](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS の使用方法とセキュリティ](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


