---
title: LineString | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- LineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: e50d0b86-8b31-4285-be71-ad05c7712cbd
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5a0f77959cfe4492eca6c38951ba2868452d41ad
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "84996329"
---
# <a name="linestring"></a>LineString
  `LineString` es un objeto unidimensional que representa una secuencia de puntos y los segmentos de línea que los conectan.

## <a name="linestring-instances"></a>Instancias de LineString
 En la ilustración siguiente se muestran ejemplos de instancias de `LineString`.

 ![Ejemplos de instancias de LineString de geometry](../../database-engine/media/linestring.gif "Ejemplos de instancias de LineString de geometry")

 Como se muestra en la ilustración:

-   La figura 1 es una instancia de `LineString` sencilla y sin cerrar.

-   La figura 2 es una instancia de `LineString` no sencilla y sin cerrar.

-   La figura 3 es una instancia de `LineString` cerrada y sencilla; por ello, es un anillo.

-   La figura 4 es una instancia de `LineString` cerrada y no sencilla; por ello, no es un anillo.

### <a name="accepted-instances"></a>Instancias aceptadas
 Las instancias de `LineString` aceptadas se pueden especificar en una variable geometry, pero puede que no sean instancias de `LineString` válidas. Los siguientes criterios se deben cumplir para que una instancia de `LineString` sea aceptada. La instancia de estar formada como mínimo por dos puntos o debe estar vacía. Se aceptan las siguientes instancias de LineString.

```
DECLARE @g1 geometry = 'LINESTRING EMPTY';
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';
```

 `@g3` muestra que se puede aceptar una instancia de `LineString`, pero no es válida.

 No se acepta la siguiente instancia de `LineString`. Producirá una `System.FormatException`.

```
DECLARE @g geometry = 'LINESTRING(1 1)';
```

### <a name="valid-instances"></a>Instancias válidas
 Para que una instancia de `LineString` sea válida debe cumplir los siguientes criterios.

1.  La instancia de `LineString` debe ser aceptada.

2.  Si una instancia de `LineString` no está vacía debe contener dos puntos distintos por lo menos.

3.  La instancia de `LineString` no se puede superponer sobre un intervalo de dos o más puntos consecutivos.

 Las siguientes instancias de `LineString` son válidas.

```
DECLARE @g1 geometry= 'LINESTRING EMPTY';
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();

```

 Las siguientes instancias de `LineString` no son válidas.

```
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';
SELECT @g1.STIsValid(), @g2.STIsValid();
```

> [!WARNING]
>  La detección de superposiciones de `LineString` se basa en los cálculos de coma flotante, que no son exactos.

## <a name="examples"></a>Ejemplos
 En el ejemplo siguiente se muestra cómo crear una instancia de `geometry``LineString` con tres puntos y un SRID de 0:

```
DECLARE @g geometry;
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);
```

 Cada punto de la instancia de `LineString` puede contener valores Z (elevación) y M (medida). Este ejemplo agrega valores M a la instancia de `LineString` creada en el ejemplo anterior. M y Z pueden ser valores nulos.

```
DECLARE @g geometry;
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);
```

 En el ejemplo siguiente se muestra cómo crear una instancia de `geometry LineString` con dos puntos que son iguales. Una llamada a `IsValid` indica que la instancia de `LineString` no es válida y una llamada a `MakeValid` convertirá la instancia de `LineString` en un `Point`.

```sql
DECLARE @g geometry
SET @g = geometry::STGeomFromText('LINESTRING(1 3, 1 3)',0);
IF @g.STIsValid() = 1
  BEGIN
     SELECT @g.ToString() + ' is a valid LineString.';  
  END
ELSE
  BEGIN
     SELECT @g.ToString() + ' is not a valid LineString.';
     SET @g = @g.MakeValid();
     SELECT @g.ToString() + ' is a valid Point.';  
  END

```

 El fragmento de código anterior devolverá lo siguiente:

```
LINESTRING(1 3, 1 3) is not a valid LineString
POINT(1 3) is a valid Point.
```

## <a name="see-also"></a>Consulte también
 [STLength &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type) [STStartPoint &#40;tipo](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type) de datos Geometry&#41;[STEndpoint &#40;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type) tipo de datos Geometry&#41;[STPointN &#40;tipo de datos Geometry&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type) STNumPoints &#40;tipo de datos [Geometry](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type) [&#41;STIsRing &#40;tipo de datos Geometry&#41;](/sql/t-sql/spatial-geometry/stisring-geometry-data-type) [STIsClosed &#40;tipo de datos Geometry&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type) [STPointOnSurface &#40;tipo de datos Geometry](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)&#41;[datos espaciales](../spatial/spatial-data-sql-server.md) &#40;SQL Server&#41;


