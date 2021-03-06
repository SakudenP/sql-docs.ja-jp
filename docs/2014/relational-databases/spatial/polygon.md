---
title: 多角形 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry subtypes [SQL Server]
- Polygon geometry subtype [SQL Server]
ms.assetid: b6a21c3c-fdb8-4187-8229-1c488454fdfb
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 040bb8a2558cc57b1b99a3ce984bec3c8925bc0d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062986"
---
# <a name="polygon"></a>多角形
  は、 `Polygon` 外部境界リングと0個以上の内部リングを定義する一連の点として格納される2次元サーフェイスです。

## <a name="polygon-instances"></a>Polygon インスタンス
 `Polygon` インスタンスは、3 つ以上の異なる点を持つリングで形成され、 `Polygon` インスタンスは空にすることもできます。

 `Polygon` の外部および内部のリングは、その境界を定義します。 リング内の空間は `Polygon` の内部を定義します。

 次の図は、`Polygon` インスタンスの例です。

 ![geometry Polygon インスタンスの例](../../database-engine/media/polygon.gif "geometry Polygon インスタンスの例")

 この図は次のことを示しています。

1.  図 1 は、外部リングによって境界が定義されている `Polygon` インスタンスです。

2.  図 2 は、1 つの外部リングと 2 つの内部リングによって境界が定義されている `Polygon` インスタンスです。 内部リングの内側の領域は、`Polygon` インスタンスの外部の一部です。

3.  図 3 の `Polygon` インスタンスは、内部リングが 1 つの接点で交差しているため有効です。

### <a name="accepted-instances"></a>許容されるインスタンス
 許容される `Polygon` インスタンスとは、例外をスローすることなく  `geometry` 変数または `geography` 変数に格納できるインスタンスです。 次に示す `Polygon` インスタンスは許容されます。

-   空の `Polygon` インスタンス。

-   1 つの許容される外部境界リングと 0 個以上の許容される内部リングを持つ `Polygon` インスタンス。

 リングが許容されるためには、次の条件を満たす必要があります。

-   `LineString` インスタンスが許容されていること。

-   `LineString` インスタンスに 4 つ以上の点があること。

-   `LineString` インスタンスの始点と終点が同じであること。

 次の例は、許容される `Polygon` インスタンスを示しています。

```
DECLARE @g1 geometry = 'POLYGON EMPTY';
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 1))';
DECLARE @g3 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 3 3, 0 3, 0 0))';
DECLARE @g4 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(3 0, 6 0, 6 3, 3 3, 3 0))';
DECLARE @g5 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';
```

 `@g4` および `@g5` が示すように、許容される `Polygon` インスタンスが有効な `Polygon` インスタンスではない場合があります。 `@g5` また、Polygon インスタンスが許容されるためには、4 つの点を持つリングのみが含まれている必要があることを示しています。

 次の例では、`Polygon` インスタンスが許容されないため、`System.FormatException` がスローされます。

```
DECLARE @g1 geometry = 'POLYGON((1 1, 3 3, 1 1))';
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 5))';
```

 `@g1` は、外部リングの `LineString` インスタンスが十分な数の点を含んでいないため、許容されません。 `@g2` は、外部リングの `LineString` インスタンスの始点が終点と同じでないため、許容されません。 次の例では、外部リングは許容されますが、内部リングが許容されません。 この場合も `System.FormatException`がスローされます。

```
DECLARE @g geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 0 0))';
```

### <a name="valid-instances"></a>有効なインスタンス
 `Polygon` の内部リングは、1 つの接点で自身および他の内部リングと接することができますが、`Polygon` の内部リングが互いに交差しているとインスタンスが無効になります。

 次の例は、有効な `Polygon` インスタンスを示しています。

```
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20))';
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0))';
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, -5 -10, -10 0))';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();
```

 `@g3` 2 つの内部リングが 1 つの点で接し、互いに交差していないため、有効です。 次の例は、無効な `Polygon` インスタンスを示しています。

```
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (20 0, 0 10, 0 -20, 20 0))';
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (5 0, 1 5, 1 -5, 5 0))';
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, 0 -10, -10 0))';
DECLARE @g4 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 1 5, 0 -10, -10 0))';
DECLARE @g5 geometry = 'POLYGON((10 0, 0 10, 0 -10, 10 0), (-20 -20, -20 20, 20 20, 20 -20, -20 -20) )';
DECLARE @g6 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid(), @g5.STIsValid(), @g6.STIsValid();
```

 `@g1` 内部リングが 2 か所で外部リングに接しているため、無効です。 `@g2` 2 つ目の内部リングが 1 つ目の内部リングの内側にあるため、無効です。 `@g3` 2 つの内部リングが連続する複数の点で接しているため、無効です。 `@g4` 2 つの内部リングの内部が交差しているため、無効です。 `@g5` 外部リングが 1 つ目のリングでないため、無効です。 `@g6` リングが 3 つ以上の異なる点を持たないため、無効です。

## <a name="examples"></a>例
 次の例では、1 つの穴を持つ単純な `geometry``Polygon` インスタンスを作成しています。このインスタンスの SRID は 10 です。

```
DECLARE @g geometry;
SET @g = geometry::STPolyFromText('POLYGON((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1))', 10);
```

 無効なインスタンスを入力して、有効な `geometry` インスタンスに変換することもできます。 次の例の `Polygon`は、内部と外部のリングが重なっているため無効です。

```
DECLARE @g geometry;
SET @g = geometry::Parse('POLYGON((1 0, 0 1, 1 2, 2 1, 1 0), (2 0, 1 1, 2 2, 3 1, 2 0))');
```

 次の例では、 `MakeValid()`を使用して、無効なインスタンスを有効なインスタンスにしています。

```
SET @g = @g.MakeValid();
SELECT @g.ToString();
```

 上の例で返される `geometry` インスタンスは `MultiPolygon`です。

```
MULTIPOLYGON (((2 0, 3 1, 2 2, 1.5 1.5, 2 1, 1.5 0.5, 2 0)), ((1 0, 1.5 0.5, 1 1, 1.5 1.5, 1 2, 0 1, 1 0)))
```

 無効なインスタンスを有効なジオメトリ インスタンスに変換する別の例を示します。 次の例では、まったく同じ 3 つの点を使用して `Polygon` インスタンスが作成されています。

```sql
DECLARE @g geometry
SET @g = geometry::Parse('POLYGON((1 3, 1 3, 1 3, 1 3))');
SET @g = @g.MakeValid();
SELECT @g.ToString()
```

 上の例で返されるジオメトリ インスタンスは `Point(1 3)`です。  `Polygon` が `POLYGON((1 3, 1 5, 1 3, 1 3))` の場合、 `MakeValid()` は `LINESTRING(1 3, 1 5)`を返します。

## <a name="see-also"></a>参照
 [Starea &#40;Geometry データ型&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type) [STExteriorRing &#40;](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type) geometry データ型&#41;[STInteriorRingN](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type) &#40;geometry データ[型&#41;](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type) [starea &#40;geometry](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)データ型&#41;[stpointonsurface &#40;geometry データ](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)型&#41;[multipolygon](../spatial/polygon.md) [空間データ &#40;](../spatial/spatial-data-sql-server.md)&#41;&#40;[starea SQL Server geography データ型&#41;](/sql/t-sql/spatial-geography/stisvalid-geography-data-type) [starea &#40;geometry データ型](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)&#41;。 &#40;


