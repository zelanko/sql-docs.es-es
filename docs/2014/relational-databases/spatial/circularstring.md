---
title: CircularString | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 9fe06b03-d98c-4337-9f89-54da98f49f9f
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: e14aafe004ffd94f0711161fac73ce59c57cd810
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176725"
---
# <a name="circularstring"></a>CircularString
  Una `CircularString` es una colección con cero o más segmentos de arco circular continuos. Un segmento de arco circular es un segmento curvado definido por tres puntos en un plano bidimensional; el primer punto no puede ser igual que el tercero. Si los tres puntos de un segmento de arco circular son colineales, el segmento de arco se trata como un segmento de línea.

> [!IMPORTANT]
>  Para obtener una descripción detallada y ejemplos de las nuevas características espaciales [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]introducidas en `CircularString` , incluido el subtipo, descargue las notas del producto [nuevas características espaciales en SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).

## <a name="circularstring-instances"></a>Instancias de CircularString
 En el dibujo siguiente se muestran instancias válidas de `CircularString`:

 ![](../../database-engine/media/5ff17e34-b578-4873-9d33-79500940d0bc.png "5ff17e34-b578-4873-9d33-79500940d0bc")

### <a name="accepted-instances"></a>Instancias aceptadas
 Una `CircularString` instancia de se acepta si está vacía o contiene un número impar de puntos, n, donde n > 1. Se aceptan las siguientes instancias de `CircularString`.

```sql
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 2 0, 1 1)';
```

 
  `@g3` muestra que la instancia de `CircularString` se puede aceptar, pero no es válida. La siguiente declaración de instancia de CircularString no se acepta. Esta declaración inicia una excepción `System.FormatException`.

```sql
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1)';
```

### <a name="valid-instances"></a>Instancias válidas
 Una instancia de `CircularString` válida debe estar vacía o tener los siguientes atributos:

-   Debe contener al menos un segmento de arco circular (es decir, con un mínimo de tres puntos).

-   El último extremo de cada segmento de arco circular de la secuencia, salvo el último segmento, debe ser el primer extremo del siguiente segmento de la secuencia.

-   Debe tener un número impar de puntos.

-   No se puede superponer sobre un intervalo.

-   Aunque las instancias de `CircularString` pueden contener segmentos de línea, dichos segmentos deben estar definidos por tres puntos colineales.

 En el siguiente ejemplo se muestran instancias válidas de `CircularString`.

```sql
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1, 0 1)';
DECLARE @g4 geometry = 'CIRCULARSTRING(1 1, 2 2, 2 2)';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(),@g4.STIsValid();
```

 Una instancia de `CircularString` debe contener al menos dos segmentos de arco circular para definir un círculo completo. Una instancia de `CircularString` no puede utilizar solo un segmento de arco circular, por ejemplo (1 1, 3 1, 1 1), para definir un círculo completo. Utilice (1 1, 2 2, 3 1, 2 0, 1 1) para definir el círculo.

 En el siguiente ejemplo se muestran instancias de CircularString no válidas.

```sql
DECLARE @g1 geometry = 'CIRCULARSTRING(1 1, 2 0, 1 1)';
DECLARE @g2 geometry = 'CIRCULARSTRING(0 0, 0 0, 0 0)';
SELECT @g1.STIsValid(), @g2.STIsValid();
```

### <a name="instances-with-collinear-points"></a>Instancias con puntos colineales
 En los siguientes casos, un segmento de arco circular se tratará como un segmento de línea:

-   Cuando los tres puntos son colineales, por ejemplo (1 3, 4 4, 7 5).

-   Cuando los puntos primero y medio son el mismo, pero el tercer punto es diferente, por ejemplo (1 3, 1 3, 7 5).

-   Cuando los puntos medio y último son el mismo, pero el primer punto es diferente, por ejemplo (1 3, 4 4, 4 4).

## <a name="examples"></a>Ejemplos

### <a name="a-instantiating-a-geometry-instance-with-an-empty-circularstring"></a>A. Crear instancias de una instancia de geometry con una CircularString vacía
 En este ejemplo se muestra cómo crear una instancia de `CircularString` vacía:

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('CIRCULARSTRING EMPTY');
```

### <a name="b-instantiating-a-geometry-instance-using-a-circularstring-with-one-circular-arc-segment"></a>B. Crear instancias de una instancia de geometry usando una CircularString con un segmento de arco circular
 En el siguiente ejemplo se muestra cómo crear una instancia de `CircularString` con un único segmento de arco de circular (medio círculo):

```sql
DECLARE @g geometry;
SET @g = geometry:: STGeomFromText('CIRCULARSTRING(2 0, 1 1, 0 0)', 0);
SELECT @g.ToString();
```

### <a name="c-instantiating-a-geometry-instance-using-a-circularstring-with-multiple-circular-arc-segments"></a>C. Crear instancias de una instancia de geometry usando una CircularString con varios segmentos de arco circular
 En el siguiente ejemplo se muestra cómo crear una instancia de `CircularString` con más de un segmento de arco circular (círculo completo):

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('CIRCULARSTRING(2 1, 1 2, 0 1, 1 0, 2 1)');
SELECT 'Circumference = ' + CAST(@g.STLength() AS NVARCHAR(10));  
```

 Produce el siguiente resultado:

```
Circumference = 6.28319
```

 Compare con el resultado obtenido cuando se utiliza `LineString` en lugar de `CircularString`:

```sql
DECLARE @g geometry;
SET @g = geometry::STGeomFromText('LINESTRING(2 1, 1 2, 0 1, 1 0, 2 1)', 0);
SELECT 'Perimeter = ' + CAST(@g.STLength() AS NVARCHAR(10));
```

 Produce el siguiente resultado:

```
Perimeter = 5.65685
```

 Observe que el valor del `CircularString` ejemplo es cercano a 2&#x03c0; (2 * PI), que es la circunferencia real del círculo.

### <a name="d-declaring-and-instantiating-a-geometry-instance-with-a-circularstring-in-the-same-statement"></a>D. Declarar y crear instancias de una instancia de geometry con una CircularString en la misma instrucción
 Este fragmento de código muestra cómo declarar y crear instancias de una instancia de `geometry` con una `CircularString` en la misma instrucción:

```sql
DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';
```

### <a name="e-instantiating-a-geography-instance-with-a-circularstring"></a>E. Crear instancias de una instancia de geography con una CircularString
 En el siguiente ejemplo, se muestra cómo declarar y crear una instancia de `geography` con una `CircularString`:

```sql
DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';
```

### <a name="f-instantiating-a-geometry-instance-with-a-circularstring-that-is-a-straight-line"></a>F. Crear instancias de una instancia de geometry con una CircularString que es una línea recta
 En el siguiente ejemplo se muestra cómo crear una instancia de `CircularString` que es una línea recta:

```sql
DECLARE @g geometry;
SET @g = geometry::STGeomFromText('CIRCULARSTRING(0 0, 1 2, 2 4)', 0);
```

## <a name="see-also"></a>Consulte también
 [Información general sobre los tipos de datos espaciales](spatial-data-types-overview.md) [CompoundCurve](compoundcurve.md) [MakeValid &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/makevalid-geography-data-type) [MakeValid &#40;tipo de datos Geometry&#41;](/sql/t-sql/spatial-geometry/makevalid-geometry-data-type) [STIsValid &#40;tipo de datos Geometry](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)&#41;STIsValid &#40;tipo de datos [Geography](/sql/t-sql/spatial-geography/stisvalid-geography-data-type)&#41;STLength &#40;tipo de [datos Geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type) STStartPoint &#40;tipo de datos [Geometry&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type) [STEndpoint &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type) STPointN &#40;tipo de datos [Geometry](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)&#41;[STNumPoints &#40;tipo de datos](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type) Geometry&#41;STIsRing [&#40;tipo de datos Geometry&#41;](/sql/t-sql/spatial-geometry/stisring-geometry-data-type) tipo de datos [STIsClosed &#40;Geometry&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type) [STPointOnSurface &#40;tipo de datos Geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type) [LineString](linestring.md)


