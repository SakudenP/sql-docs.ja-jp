---
title: Azure BLOB のアップロード タスク | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobuptask.f1
- sql14.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e903de279e4373e234dab18401465edd997e7407
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298425"
---
# <a name="azure-blob-upload-task"></a>Azure BLOB のアップロード タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


**Azure BLOB のアップロード タスク** を使うと、SSIS パッケージで Azure BLOB ストレージにファイルをアップロードできます。
    
**Azure BLOB のアップロード タスク**を追加するには、SSIS デザイナーにドラッグ アンド ドロップし、ダブルクリックまたは右クリックして、 **[編集]** をクリックし、次の **[Azure Blob Upload Task Editor (Azure BLOB アップロード タスク エディター)]** ダイアログ ボックスを表示します。  
  
 **Azure BLOB のアップロード タスク**は、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。
  
 次の表で、このダイアログ ボックスの各フィールドを説明します。  

|**フィールド**|**説明**|  
|---|---|  
|AzureStorageConnection|既存の Azure ストレージ接続マネージャーを指定するか、Azure ストレージ アカウントを参照する新しい接続マネージャーを作成します。この接続マネージャーは、BLOB ファイルがホストされている場所をポイントします。|  
|BlobContainer|アップロードしたファイルを BLOB として含む BLOB コンテナーの名前を指定します。|  
|BlobDirectory|アップロードしたファイルがブロック BLOB として格納される BLOB ディレクトリを指定します。 BLOB ディレクトリは仮想階層構造です。 BLOB が既に存在する場合は置き換えられます。|  
|LocalDirectory|アップロードするファイルを含むローカル ディレクトリを指定します。|  
|SearchRecursively|サブディレクトリ内で再帰的に検索するかどうかを指定します。|  
|FileName|指定された名前のパターンを使用したファイルを選択するための名前フィルターを指定します。 たとえば、`MySheet*.xls\*` には `MySheet001.xls` や `MySheetABC.xlsx` などのファイルが含まれます。|  
|TimeRangeFrom/TimeRangeTo|時間範囲フィルターを指定します。 **TimeRangeFrom** から **TimeRangeTo** までの間に変更されたファイルが含まれます。|  
