---
title: SetEnable メソッド (ServerNetworkProtocolIPAddress)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetEnable Method (ServerNetworkProtocolIPAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetEnable method
ms.assetid: baa86deb-95dd-416f-b2c7-cec1dfb91ab4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f5b002d205ea7077fded8c2d253e78017536b753
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "73659389"
---
# <a name="setenable-method-servernetworkprotocolipaddress-class"></a>SetEnable メソッド (ServerNetworkProtocolIPAddress クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  IP アドレスを有効にします。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.SetEnable()  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]の[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンス上のネットワークプロトコルの IP アドレスを表す[ServerNetworkProtocolIPAdress クラス](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md)オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 **uint32** 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>参照  
 [サーバーのネットワーク プロトコルと Net-Library の構成](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
