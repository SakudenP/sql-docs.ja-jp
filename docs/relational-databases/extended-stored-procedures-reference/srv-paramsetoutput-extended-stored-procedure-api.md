---
title: srv_paramsetoutput (拡張ストアド プロシージャ API)
ms.custom: seo-dt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramsetoutput
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b00f2fedd9c1053e332aaee8691207fbf990649
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755956"
---
# <a name="srv_paramsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput (拡張ストアド プロシージャ API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 戻りパラメーターの値を設定します。 この関数は、**srv_paramset** 関数に代わるものです。  
  
## <a name="syntax"></a>構文  
  
```  
  
int srv_paramsetoutput (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbData  
,  
ULONG   
cbLen  
,  
BOOL  
fNull   
);  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 クライアント接続のためのハンドルです。  
  
 *n*  
 設定するパラメーターの序数です。 最初のパラメーターは 1 です。  
  
 *pbData*  
 プロシージャの戻りパラメーターとしてクライアントに返されるデータ値を指すポインターです。  
  
 *cbLen*  
 返されるデータの実際の長さです。 パラメーターのデータ型が固定長の値を指定しており、NULL 値を許容しない型 (*srvbit*、*srvint1* など) である場合、*cbLen* は無視されます。 *fNull* が FALSE の場合、値 0 は長さ 0 のデータを示します。  
  
 *fNull*  
 戻りパラメーターの値が NULL かどうかを示すフラグです。 パラメーターを NULL に設定する必要がある場合は、このフラグを TRUE に設定します。 既定値は FALSE です。 *fNull* を TRUE に設定した場合は、*cbLen* を 0 に設定する必要があります。このように設定しないと関数は失敗します。  
  
## <a name="returns"></a>戻り値  
 パラメーター情報が正常に設定された場合は SUCCEED を返し、それ以外の場合は FAIL を返します。 FAIL が返されるのは、次の場合です。  
  
-   パラメーターが戻りパラメーターでない場合。  
  
-   *cbLen* 引数が無効である場合。  
  
## <a name="remarks"></a>Remarks  
 **セキュリティに関する注意** 拡張ストアド プロシージャのソース コードを十分に確認し、コンパイルした DLL をテストしたうえで実稼働サーバーにインストールしてください。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
  
