---
title: '[データベースのバックアップ] ダイアログボックス (Analysis Services-多次元データ) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Backup.f1
ms.assetid: 7811ce7d-6c37-4189-bfa6-ef36fb4932db
author: minewiskan
ms.author: owend
ms.openlocfilehash: 96ddf88bd6f071c667a021678b6f5cd2613ae8db
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527829"
---
# <a name="backup-database-dialog-box-analysis-services---multidimensional-data"></a>[データベースのバックアップ] ダイアログ ボックス (Analysis Services - 多次元データ)
  **の** [データベースのバックアップ] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ダイアログ ボックスを使用すると、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースを [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] バックアップ ファイル (.abf) 形式でバックアップ ファイルにバックアップできます。  
  
> [!IMPORTANT]  
>  バックアップ ファイルごとに、バックアップ コマンドを実行するユーザーは、各ファイルに指定されたバックアップ場所に対する書き込み権限を持っている必要があります。 また、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスのサーバー ロールのメンバーであるか、バックアップするデータベースに対してフル コントロール (管理者) 権限を持つデータベース ロールのメンバーであることが条件となります。  
  
 **[データベースのバックアップ] ダイアログ ボックスを表示するには**  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]の **オブジェクト エクスプローラー** で、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスの **[データベース]** フォルダー、またはデータベースを右クリックし、 **[バックアップ]** をクリックします。  
  
## <a name="options"></a>オプション  
 **スクリプト**  
 ダイアログ ボックスで選択したオプションに基づいたバックアップ スクリプトを作成します。 復元用スクリプトは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] スクリプト言語 (ASSL) で記述されています。  
  
 **[スクリプト]** アイコンをクリックすると、既定では、新しいクエリ ウィンドウにバックアップ スクリプトが送信されます。  
  
 **[スクリプト]** の矢印をクリックすると、バックアップ スクリプトの送信先を次の中から選択できるメニューが表示されます。  
  
-   新しいクエリ ウィンドウ (既定)。  
  
-   ファイル。  
  
-   クリップボード。  
  
-   ジョブ。  
  
 **[データベース]**  
 現在選択されている [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースの名前を表示します。  
  
 **[バックアップ ファイル]**  
 使用するバックアップ ファイルの完全なパスとファイル名を入力します。  
  
 **参照**  
 クリックすると、**[ファイル名を付けて保存]** ダイアログ ボックスが表示され、使用するバックアップ ファイルのパスおよびファイル名を選択できます。 **[ファイル名を付けて保存]** ダイアログ ボックスの詳細については、「[[ファイル名を付けて保存] ダイアログ ボックス (Analysis Services - 多次元データ)](save-file-as-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **[ファイルの上書きを許可する]**  
 選択すると、既存のバックアップ ファイル、またはリモート バックアップ ファイルが存在する場合にファイルが上書きされます。  
  
> [!NOTE]  
>   このオプションが選択されていない状態で、 **[バックアップ ファイル]** に指定されたバックアップ ファイルまたは **[リモート バックアップ ファイル]** に指定されたリモート バックアップ ファイルが存在する場合は、エラーが発生します。  
  
 **[圧縮を適用する]**  
 選択すると、バックアップ ファイル (および指定された場合はリモート バックアップ ファイル) の内容が圧縮されます。  
  
 **[バックアップ ファイルを暗号化する]**  
 選択すると、バックアップ ファイルは **[パスワード]** に指定されたパスワードを使用して暗号化されます。  
  
 **パスワード**  
 バックアップ ファイル (および指定された場合はリモート バックアップ ファイル) を暗号化するときに使用するパスワードを入力します。  
  
> [!NOTE]  
>   このオプションは、 **[バックアップ ファイルを暗号化する]** が選択されている場合にのみ有効です。  
  
 **パスワードの確認**  
 バックアップ ファイル (および指定された場合はリモート バックアップ ファイル) のパスワードを確認するために、 **[パスワード]** に入力したパスワードを入力します。  
  
> [!NOTE]  
>   このオプションは、 **[バックアップ ファイルを暗号化する]** が選択されている場合にのみ有効です。  
  
 **[リモート パーティションのバックアップを作成する]**  
 選択すると、リモート パーティションの位置情報およびデータをバックアップ ファイルに含めることができます。  
  
> [!NOTE]  
>  このオプションは、現在選択されている [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースでリモート パーティションが使用されている場合にのみ有効です。  
  
 **[リモート パーティションのバックアップの場所]**  
 選択されているデータベースに関連付けられているリモート パーティションの位置と、リモート パーティションのデータおよびメタデータをバックアップするためのリモート バックアップ ファイルを表示します。 次の列があります。  
  
|Column|説明|  
|------------|-----------------|  
|**[サーバー]**|リモート パーティションを管理する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスを表示します。|  
|**[データベース]**|リモート パーティションが格納されている [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースを表示します。|  
|**パーティション一覧**|**[データベース]** に表示されるデータベースに含まれているリモート パーティションの一覧を表示します。|  
|**[リモート バックアップ ファイル]**|使用するリモート バックアップ ファイルの完全なパスとファイル名を入力するか、**[...]** ボタンをクリックして **[ファイル名を付けて保存]** ダイアログ ボックスを表示し、使用するリモート バックアップ ファイルのパスとファイル名を選択します。 **[ファイル名を付けて保存]** ダイアログ ボックスの詳細については、「[[ファイル名を付けて保存] ダイアログ ボックス (Analysis Services - 多次元データ)](save-file-as-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [多次元データ &#40;Analysis Services のデザイナーとダイアログボックス&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Analysis Services データベースのバックアップと復元](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
