---
title: WMI Provider for Server Events のクラスとプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b0f6a4cbb18ad1c746b98c3aae9643127a9c098e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85013612"
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>WMI Provider for Server Events のクラスとプロパティ
  次に示すサーバー イベントは、WMI Provider for Server Events のプログラミング モデルを構成しています。 プロバイダーに対する WQL クエリの実行によってクエリを実行できるイベントには、2 つの主なカテゴリがあります。 その 2 つとは、データ定義言語 (DDL) イベントおよびトレース イベントです。 また、QUEUE_ACTIVATION および BROKER_QUEUE_DISABLED の Service Broker イベントも照会することができます。 次のツリー ダイアグラムの包含的な性質に注意してください。 たとえば、DDL_ASSEMBLY_EVENTS イベントには、ALTER_ASSEMBLY、CREATE_ASSEMBLY、および DROP_ASSEMBLY イベントが含まれています。 同様に、TRC_FULL_TEXT イベントには、FT_CRAWL_ABORTED、FT_CRAWL_STARTED、および FT_CRAWL_STOPPED イベントが含まれています。 ALL_EVENTS は、すべての DDL イベント、トレース イベント、QUEUE_ACTIVATION、および BROKER_QUEUE_DISABLED をカバーします。  
  
 イベントまたはイベント グループから照会できるプロパティについては、イベント スキーマを参照してください。 既定では、イベント スキーマは、[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd ディレクトリにインストールされます。  
  
 または、で公開されているイベントスキーマを参照することもでき [https://schemas.microsoft.com/sqlserver](https://go.microsoft.com/fwlink/?linkid=43100) ます。  
  
 たとえば、ALTER_DATABASE イベントを参照すると、その親イベントが DDL_SERVER_LEVEL_EVENTS で、そのプロパティが `TSQLCommand` と `DatabaseName` であることがわかります。 また、プロパティ `SQLInstance`、`PostTime`、`ComputerName`、`SPID`、および `LoginName` が継承されています。 イベントには、子イベントはありません。  
  
> [!NOTE]  
>  DDL と同様の操作を実行するシステム ストアド プロシージャもイベント通知を起動できます。 イベント通知はテストして、実行されているシステム ストアド プロシージャに応答するかどうか、確認してください。 たとえば、CREATE TYPE ステートメントと**sp_addtype**ストアドプロシージャはどちらも、CREATE_TYPE イベントで作成されたイベント通知を起動します。 詳細については、「[DDL イベント](../../relational-databases/triggers/ddl-events.md)」を参照してください。  
  
 **データ定義言語イベントおよびイベント グループ**  
  
 ![サーバー イベントのイベント ツリーの WMI プロバイダー](../../../2014/database-engine/dev-guide/media/sql-wmi-ddl-events-ktm.gif "サーバー イベントのイベント ツリーの WMI プロバイダー")  
  
 **トレース イベントおよびイベント グループ**  
  
 ![トレースイベントとイベントグループ](../../../2014/database-engine/dev-guide/media/sql-wmi-trc-all-events.gif "トレース イベントとイベント グループ")  
  
## <a name="see-also"></a>参照  
 [WMI Provider for Server Events の概念](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [WMI Provider for Server Events と WQL の使用](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
