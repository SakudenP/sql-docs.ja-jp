---
title: MSSQLSERVER_2527 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 900707634a016ecfd29f9f676e68b4d2f557ccea
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034279"
---
# <a name="mssqlserver_2527"></a>MSSQLSERVER_2527
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2527|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|メッセージ テキスト|テーブル O_NAME のインデックス I_NAME を処理できません。ファイル グループ F_NAME がオフラインです。|  
  
## <a name="explanation"></a>説明  
 この情報メッセージは、インデックスに対応するデータを格納しているファイル グループの 1 つがオフライン状態なので、インデックスをチェックできないことを示しています。 ファイル グループ内のファイルの状態により、ファイル グループ全体の可用性が決まります。 ファイル グループを使用可能にするには、ファイル グループ内のすべてのファイルがオンラインである必要があります。 他に問題がなければ、同じオブジェクトの他のインデックスはすべてチェックされます。  
  
## <a name="user-action"></a>ユーザーの操作  
 指定したファイル グループのファイルの状態を表示するには、**sys.database_files** カタログ ビューまたは **sys.master_files** カタログ ビューにクエリを実行します。  
  
 オフライン ファイルをバックアップから復元します。  
  
## <a name="see-also"></a>参照  
 [database_files &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [master_files &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
