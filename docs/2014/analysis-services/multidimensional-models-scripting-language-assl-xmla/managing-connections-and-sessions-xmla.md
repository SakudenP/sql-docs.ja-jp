---
title: 接続とセッションの管理 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- statefulness [XML for Analysis]
- statelessness [XML for Analysis]
- XML for Analysis, sessions
- states [XML for Analysis]
- XMLA, sessions
- sessions [XML for Analysis]
ms.assetid: b83bb3ff-09be-4fda-9d1d-6248e04ffb21
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7bfe876f6874193fd0885f16d91caa9f6fe8b172
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544944"
---
# <a name="managing-connections-and-sessions-xmla"></a>接続およびセッションの管理 (XMLA)
  *状態保持*は、サーバーがメソッド呼び出し間でクライアントの id とコンテキストを保持する条件です。 *状態*は、メソッドの呼び出しが完了した後に、サーバーがクライアントの id とコンテキストを記憶しない条件です。  
  
 状態保持を提供するために、XML for Analysis (XMLA) は、一連のステートメントをまとめて実行できる*セッション*をサポートしています。 そのような一連のステートメントの例としては、後続のクエリで使用するための計算されるメンバーの作成があります。  
  
 一般に、XMLA のセッションは、OLE DB 2.6 の仕様で概説されている以下の動作に従います。  
  
-   セッションはトランザクションとコマンド コンテキストのスコープを定義します。  
  
-   複数のコマンドを単一のセッションのコンテキストで実行できます。  
  
-   XMLA コンテキストでのトランザクションのサポートは、 [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)メソッドと共に送信されるプロバイダー固有のコマンドを介して行われます。  
  
 XMLA は、Distributed Authoring and Versioning (DAV) プロトコルが疎結合環境でロックを実装するために使用しているアプローチと同様の手法で、Web 環境のセッションをサポートする方法を定義します。 この実装は、プロバイダーがさまざまな理由 (たとえば、タイムアウトや接続エラーなど) でセッションの有効期限を終了させることができるという点で、DAV と類似しています。 セッションがサポートされる場合、Web サービスは、中断されて再開が必要なコマンドのセットを認識し、処理する準備を整えている必要があります。  
  
 World Wide Web Consortium (W3C) による Simple Object Access Protocol (SOAP) 仕様は、新しいプロトコルを作成するには SOAP メッセージの先頭に SOAP ヘッダーを使用することを推奨しています。 次の表は、XMLA がセッションの開始、維持、終了のために定義する SOAP ヘッダー要素と属性の一覧を示しています。  
  
|SOAP ヘッダー|説明|  
|-----------------|-----------------|  
|BeginSession|プロバイダーに新しいセッションの作成を要求します。 プロバイダーは、新しいセッションを作成し、SOAP 応答の Session ヘッダーの一部としてセッション ID を返すことによって応答します。|  
|SessionId|値域には、セッションの残りの部分での各メソッド呼び出しで使用する必要のあるセッション ID が含まれます。 プロバイダーは SOAP 応答の中でこのタグを送信します。クライアントも、Session ヘッダー要素ごとに、この属性を送信する必要があります。|  
|セッション|このヘッダーは、セッションで生じるメソッド呼び出しごとに使用する必要があります。値域にはセッション ID が含まれている必要があります。|  
|EndSession|セッションを終了するには、このヘッダーを使用します。 セッション ID がこの値域に含まれている必要があります。|  
  
> [!NOTE]  
>  セッション ID は、そのセッションが引き続き有効であることを保証するものではありません。 セッションの有効期限が切れた場合 (たとえば、タイムアウトが生じた場合や、接続が失われた場合など)、プロバイダーはそのセッションのアクションを終了してロールバックすることができます。 その結果、同じセッション ID でのクライアントからの後続のメソッド呼び出しはすべて、セッションが有効でないことを示すエラーによって失敗します。 クライアントは、この状況に対処し、そのセッションのメソッド呼び出しを最初から再送信するよう準備する必要があります。  
  
## <a name="legacy-code-example"></a>レガシ コードの例  
 以下の例は、セッションがどのようにサポートされるかを示しています。  
  
1.  セッションを開始するには、クライアントからのアウトバウンド XMLA メソッド呼び出しに SOAP の BeginSession ヘッダーを追加します。 セッション ID がまだ不明なため、値域が最初は空白になっています。  
  
    ```  
    <SOAP-ENV:Envelope  
       xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
       SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
       <SOAP-ENV:Header>  
          <XA:BeginSession  
             xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
             xsi:type="xsd:int"  
             mustUnderstand="1"/>  
       </SOAP-ENV:Header>  
       <SOAP-ENV:Body>  
          ...<!-- Discover or Execute call goes here.-->  
       </SOAP-ENV:Body>  
    </SOAP-ENV:Envelope>  
    ```  
  
2.  プロバイダーからの SOAP 応答メッセージには、XMLA ヘッダータグを使用して、リターンヘッダー領域にセッション ID が含まれてい \<SessionId> ます。  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
3.  セッションのメソッド呼び出しごとに、プロバイダーから返されたセッション ID を含む Session ヘッダーを追加する必要があります。  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
4.  セッションが完了すると、 \<EndSession> 関連するセッション ID 値を含むタグが使用されます。  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:EndSession  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          xsi:type="xsd:int"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
## <a name="see-also"></a>参照  
 [Analysis Services での XMLA による開発](developing-with-xmla-in-analysis-services.md)  
  
  
