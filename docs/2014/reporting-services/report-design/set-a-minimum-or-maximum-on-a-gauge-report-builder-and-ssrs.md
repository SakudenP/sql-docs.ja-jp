---
title: ゲージへの最小値または最大値の設定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b4c260c0-5a88-4f30-8977-eb5cc78fc146
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c7a9ad23124105443349720d2d5769fb9227db2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105024"
---
# <a name="set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs"></a>ゲージへの最小値または最大値の設定 (レポート ビルダーおよび SSRS)
  複数のグループが定義されるグラフとは異なり、ゲージには 1 つの値しか表示されません。 レポート ビルダーおよびレポート デザイナーは、ゲージに表示される値のコンテキストや相対的な有意性を判断することができないため、スケールの最小値と最大値は独自に定義する必要があります。 たとえば、データの値が 0 ～ 10 のランキングを表している場合は、最小値を 0 に、最大値を 10 に設定します。 間隔の数は、最小値と最大値として指定された値に基づいて自動的に計算されます。 既定では、最小値と最大値はそれぞれ 0 および 100 に設定されますが、これらは恣意的な値であり、必要に応じて変更する必要があります。 アプリケーションによって値がパーセンテージとして計算されることはありません。  
  
 値の範囲が大きい場合は (0 ～ 10000 など)、乗数を使って、ゲージに表示されるゼロの数を減らすことを検討してください。 乗数によって小さくなるのは、ゲージ上に表示される数値の尺度だけです。値そのものが小さくなるわけではありません。  
  
 式を使用して **[最小]** オプションと **[最大]** オプションの値を設定できます。 詳細については、「[式 (レポート ビルダーおよび SSRS)](expressions-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-minimum-and-maximum-on-the-gauge"></a>ゲージに最小値または最大値を設定するには  
  
1.  スケールを右クリックし、 **[スケールのプロパティ]** を選択します。 **[スケールのプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[全般]** で、 **[最小]** の値を指定します。 既定では、この値は 0 です。 必要に応じて、 **式** ([*fx*]) ボタンをクリックし、オプションの値を設定する式を編集します。  
  
3.  **[最大]** の値を指定します。 既定では、この値は 100 です。 必要に応じて、 **式** ([*fx*]) ボタンをクリックし、オプションの値を設定する式を編集します。  
  
4.  (省略可) 最小と最大の値が大きい場合は、 **[スケール ラベルの乗数値]** オプションに値を指定します。 尺度を小さくするための乗数は、小数値を使って指定します。 たとえば、0 ～ 1000 の尺度が存在する場合は、乗数値を「0.01」とすることで 0 ～ 10 の尺度に変更できます。  
  
## <a name="see-also"></a>参照  
 [ゲージのスケールの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [ゲージのポインターの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [ゲージ (レポート ビルダーおよび SSRS)](gauges-report-builder-and-ssrs.md)  
  
  
