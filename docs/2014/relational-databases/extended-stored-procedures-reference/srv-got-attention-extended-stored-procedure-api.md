---
title: srv_got_attention (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_got_attention
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
author: rothja
ms.author: jroth
ms.openlocfilehash: f808fcd368f73c33d7bf9e7cd5f3dda26a8211cf
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050774"
---
# <a name="srv_got_attention-extended-stored-procedure-api"></a>srv_got_attention (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 現在の接続またはタスクを中断する必要があるかどうかをチェックし、接続が強制終了された場合、またはバッチが中断された場合に TRUE を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
BOOL srv_got_attention  
(SRV_PROC *  
srvproc  
);  
  
```  
  
#### <a name="parameters"></a>パラメーター  
 *srvproc*  
 データベース接続を特定するポインターです。  
  
## <a name="return-value"></a>戻り値  
 接続が強制終了されたか、バッチが中断された場合に TRUE を返します。 接続またはバッチがアクティブであれば FALSE を返します。  
  
## <a name="remarks"></a>Remarks  
 実行時間の長い拡張ストアド プロシージャの場合は、**srv_got_attention** を定期的に呼び出してサーバーのアテンションをチェックすることにより、接続が強制終了されたかバッチが中断されたときに、そのプロシージャが自身を終了できるようにする必要があります。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
  
