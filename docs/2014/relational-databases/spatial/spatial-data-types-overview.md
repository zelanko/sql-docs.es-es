---
title: Información general de los tipos de datos espaciales | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], understanding
- geography data type [SQL Server], spatial data
- planar spatial data [SQL Server], geometry data type
- spatial data types [SQL Server]
ms.assetid: 1615db50-69de-4778-8be6-4e058c00ccd4
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 340e250fde61f8c246099eadafc148278288dee0
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176655"
---
# <a name="spatial-data-types-overview"></a>Información general de los tipos de datos espaciales
  Hay dos tipos de datos espaciales. El tipo de datos `geometry` admite datos planos o euclidianos (de tierra plana). El tipo de datos `geometry` se ajusta tanto a las características simples de Geospatial Consortium (OGC) para la especificación SQL versión 1.1.0 como a SQL MM (estándar ISO).

 Además, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite el tipo de datos `geography`, que almacena datos elípticos (tierra redonda), como coordenadas de latitud y longitud GPS.

> [!IMPORTANT]
>  Para obtener una descripción detallada y ejemplos de las características espaciales introducidas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluidas las mejoras en los tipos de datos espaciales, descargue las notas del producto [Nuevas características espaciales de SQL Server Code-Named "Denali"](https://go.microsoft.com/fwlink/?LinkId=226407).

##  <a name="objects"></a>Objetos de datos espaciales
 Los tipos de datos `geometry` y `geography` admiten dieciséis objetos de datos espaciales o tipos de instancia. Pero solo se pueden *crear instancias*de once de estos tipos de instancia; puede crear y trabajar con estas instancias (o crear instancias de ellas) en una base de datos. Estas instancias obtienen determinadas propiedades de sus tipos de datos primarios que los `Points`distinguen como, **LineStrings, CircularStrings** `CompoundCurves`,, `Polygons` `CurvePolygons` o `geometry` como `geography` varias instancias de `GeometryCollection`o en. El tipo `Geography` tiene un tipo de instancia adicional, `FullGlobe`.

 La figura siguiente describe la jerarquía de `geometry` en la que se basan los tipos de datos `geometry` y `geography`. Los tipos de instancias `geometry` de `geography` y se indican en azul.

 ![Jerarquía del tipo geometry](../../database-engine/media/geom-hierarchy.gif "Jerarquía del tipo geometry")

 Como indica la ilustración, los diez tipos de instancias de `geometry` los `geography` tipos de datos `Point`y `MultiPoint`son `LineString`, `CircularString`, `MultiLineString`, `CompoundCurve`, `Polygon`, `CurvePolygon`, `MultiPolygon`,, `GeometryCollection`y. Existe un tipo adicional a partir del que pueden crearse instancias para el tipo de datos Geography: `FullGlobe`. Los `geometry` tipos `geography` y pueden reconocer una instancia concreta siempre que sea una instancia bien formada, incluso si la instancia no está definida explícitamente. Por ejemplo, `Point` si define una instancia explícitamente mediante el método STPointFromText (), `geometry` y `geography` reconoce la instancia como `Point`, siempre y cuando la entrada del método tenga el formato correcto. Si define la misma instancia mediante el método `STGeomFromText()`, los tipos de datos `geometry` y `geography` reconocen la instancia como `Point`.

 Los subtipos de los tipos Geometry y Geography se dividen en tipos simples y de colección.  Algunos métodos como `STNumCurves()` funcionan solo con los tipos simples.

 Los tipos simples incluyen:

-   [Point](../spatial/point.md)

-   [LineString](../spatial/linestring.md)

-   [CircularString](../spatial/circularstring.md)

-   [CompoundCurve](../spatial/compoundcurve.md)

-   [Polygon](../spatial/polygon.md)

-   [CurvePolygon](../spatial/curvepolygon.md)

 Los tipos de colección incluyen:

-   [MultiPoint](../spatial/multipoint.md)

-   [MultiLineString](../spatial/multilinestring.md)

-   [MultiPolígono](../spatial/multipolygon.md)

-   [GeometryCollection](../spatial/geometrycollection.md)


##  <a name="differences"></a>Diferencias entre los tipos de datos Geometry y Geography
 Los dos tipos de datos espaciales se comportan a menudo de manera bastante similar pero hay algunas diferencias clave en la manera en la que los datos se almacenan y se manipulan.

### <a name="how-connecting-edges-are-defined"></a>Definición de bordes de conexión
 Los datos de definición para los tipos `LineString` y `Polygon` son solo los vértices.  El borde de conexión entre dos vértices en un tipo Geometría es una línea recta.  Sin embargo, el borde de conexión entre dos vértices en un tipo de geografía es un arco elíptico grande corto entre los dos vértices.  Una elipse grande es la intersección del elipsoide con un plano por su centro y un arco elíptico grande es un segmento de arco de la elipse grande.

### <a name="how-circular-arc-segments-are-defined"></a>Definición de los segmentos de arco circular
 Los segmentos de arco circular para los tipos Geometry se definen en el plano de coordenadas cartesianas XY (se ignoran los valores Z). Los segmentos de arco circular para los tipos Geography se definen mediante segmentos de curva en una esfera de referencia. Los paralelos de la esfera de referencia se pueden definir mediante dos arcos circulares complementarios en los que los puntos de ambos arcos tienen un ángulo de latitud constante.

### <a name="measurements-in-spatial-data-types"></a>Medidas en tipos de datos espaciales
 En el sistema plano, o de tierra plana, las medidas de distancias y las áreas se proporcionan en la misma unidad de medida que las coordenadas. Usando el tipo de datos `geometry`, la distancia entre (2, 2) y (5, 6) es 5 unidades, independientemente de las unidades usadas.

 En el sistema elíptico o de tierra redonda, las coordenadas se proporcionan en grados de latitud y longitud. Sin embargo, las longitudes y las áreas normalmente se miden en metros y metros cuadrados, aunque la medida puede depender del identificador de referencia espacial (SRID) de la instancia de `geography`. La unidad de medida más común para el tipo de datos `geography` es el metro.

### <a name="orientation-of-spatial-data"></a>Orientación de datos espaciales
 En el sistema plano, la orientación de anillo de un polígono no es un factor importante. Por ejemplo, un polígono descrito por ((0, 0), (10, 0), (0, 20), (0, 0)) es igual que un polígono descrito por ((0, 0), (0, 20), (10, 0), (0, 0)). Las características simples de OGC para la especificación de SQL no dictan una ordenación de anillos y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no exige la ordenación de anillos.

 En un sistema elíptico, un polígono no tiene ningún significado, o es ambiguo, sin una orientación. Por ejemplo, ¿un anillo alrededor del ecuador describe el hemisferio norte o el hemisferio sur? Si usamos el tipo de datos `geography` para almacenar la instancia espacial, debemos especificar la orientación del anillo y describir con precisión la ubicación de la instancia. El interior del polígono de un sistema elipsoidal se define mediante la regla de la mano izquierda.

 Cuando el nivel de compatibilidad es 100 o inferior [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] en, `geography` el tipo de datos tiene las restricciones siguientes:

-   Cada instancia de `geography` debe ajustarse en un hemisferio único. No se puede almacenar ningún objeto espacial mayor que un hemisferio.

-   Cualquier instancia de `geography` de una representación Open Geospatial Consortium (OGC) Well-Known Text (WKT) o Well-Known Binary (WKB) que genera un objeto mayor que un hemisferio inicia una `ArgumentException`.

-   Los `geography` métodos de tipo de datos que requieren la entrada `geography` de dos instancias, como STIntersection (), STUnion (), STDifference () y STSymDifference (), devolverán NULL si los resultados de los métodos no caben en un hemisferio único. STBuffer() también devolverá NULL si la salida supera un único hemisferio.

 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], `FullGlobe` es un tipo especial de Polygon que abarca el mundo entero. 
  `FullGlobe` tiene un área, pero no tiene bordes o vértices.

### <a name="outer-and-inner-rings-not-important-in-geography-data-type"></a>Anillos externos e internos no importantes en el tipo de datos Geography
 Las características simples de OGC para la especificación de SQL analizan los anillos externos y los anillos internos, pero esta distinción [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `geography` tiene poco sentido para el tipo de datos; se puede tomar cualquier anillo de un polígono como anillo externo.

 Para obtener más información acerca de las especificaciones de OGC, vea lo siguiente:

-   [Especificaciones de OGC, Acceso a características simples, Parte 1 - Arquitectura común](https://go.microsoft.com/fwlink/?LinkId=93627)

-   [Especificaciones de OGC, acceso a características simples, parte 2: opciones de SQL](https://go.microsoft.com/fwlink/?LinkId=93628)


##  <a name="circular"></a>Segmentos de arco circular
 Tres tipos instanciables pueden tomar segmentos de arco circular: `CircularString`, `CompoundCurve` y `CurvePolygon`.  Un segmento de arco circular se define mediante tres puntos en un plano bidimensional y el tercer punto no puede ser igual que el primero.

 Las figuras A y B muestran segmentos de arco circular. Observe que cada uno de los tres puntos pertenece al perímetro de un círculo.

 Las figuras C y D muestran cómo se puede definir el segmento de una línea como segmento de arco circular.  Observe que esos tres puntos continúan siendo necesarios para definir el segmento de arco circular a diferencia de un segmento de línea normal que se puede definir mediante dos puntos únicamente.

 Los métodos que funcionan en tipos de segmentos de arco circular usan segmentos de línea recta para aproximarse al arco circular. El número de segmentos de línea que se usan para aproximarse al arco dependerá de la longitud y curvatura del arco. Los valores Z se pueden almacenar para cada uno de los tipos de segmentos de arco circulares. sin embargo, los métodos no usarán los valores Z en sus cálculos.

> [!NOTE]
>  Si se dan valores Z para los segmentos de arco circular, deben ser iguales para todos los puntos del segmento de arco circular para que se acepte como entrada. Por ejemplo: se acepta `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` , pero no se acepta `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` .

### <a name="linestring-and-circularstring-comparison"></a>Comparación de LineString y CircularString
 En el siguiente diagrama se muestran triángulos isósceles idénticos (el triángulo A usa segmentos de línea para definir el triángulo y el triángulo B, segmentos de arco circular):

 ![](../../database-engine/media/7e382f76-59da-4b62-80dc-caf93e637c14.png "7e382f76-59da-4b62-80dc-caf93e637c14")

 En este ejemplo se muestra cómo almacenar los triángulos isósceles anteriores tanto con una instancia de `LineString` como con una instancia de `CircularString`:

```sql
DECLARE @g1 geometry;
DECLARE @g2 geometry;
SET @g1 = geometry::STGeomFromText('LINESTRING(1 1, 5 1, 3 5, 1 1)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(1 1, 3 1, 5 1, 4 3, 3 5, 2 3, 1 1)', 0);
IF @g1.STIsValid() = 1 AND @g2.STIsValid() = 1
  BEGIN
      SELECT @g1.ToString(), @g2.ToString()
      SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length]
  END
```

 Tenga en cuenta que una instancia de `CircularString` requiere siete puntos para definir el triángulo, pero una instancia de `LineString` requiere solo cuatro puntos para definir el triángulo. Esto se debe a que una instancia de `CircularString` almacena los segmentos de arco circular y no los de línea. Por tanto, los lados del triángulo almacenado en la instancia de `CircularString` son ABC, CDE y EFA mientras que los del triángulo almacenado en la instancia de `LineString` son AC, CE y EA.

 Considere el fragmento de código siguiente:

```sql
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];
```

 Este fragmento de código generará los siguientes resultados:

```
LS LengthCS Length
5.65685...6.28318...
```

 En la ilustración siguiente se muestra cómo se almacena cada tipo (se `LineString``@g1`muestran las líneas rojas `CircularString``@g2`, las líneas azules):

 ![](../../database-engine/media/e52157b5-5160-4a4b-8560-50cdcf905b76.png "e52157b5-5160-4a4b-8560-50cdcf905b76")

 Como se muestra en la ilustración anterior, las instancias de `CircularString` usan menos puntos para almacenar límites curvos con mayor precisión que las instancias de `LineString` . Las instancias de `CircularString` son útiles para almacenar límites circulares como un radio de búsqueda de veinte millas desde un punto específico. Las instancias de `LineString` funcionan bien para almacenar límites que son lineales como un bloque de ciudad cuadrado.

### <a name="linestring-and-compoundcurve-comparison"></a>Comparación de LineString y CompoundCurve
 En los siguientes ejemplos de código se muestra cómo almacenar la misma figura con instancias de `LineString` y `CompoundCurve`:

```sql
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');
```

 or

 En los ejemplos anteriores, una instancia de `LineString` o un instancia de `CompoundCurve` pudieron almacenar la figura.  En el siguiente ejemplo se usa `CompoundCurve` para almacenar un segmento de gráfico circular:

```sql
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');
```

 Una instancia de `CompoundCurve` puede almacenar el segmento de arco circular (2 2, 1 3, 0 2) directamente mientras que una instancia de `LineString` tendría que convertir la curva en varios segmentos de línea más pequeños.

### <a name="circularstring-and-compoundcurve-comparison"></a>Comparación de CircularString y CompoundCurve
 En el siguiente ejemplo de código se muestra cómo se puede almacenar el segmento de gráfico circular en una instancia de `CircularString`:

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');
SELECT @g.ToString(), @g.STLength();
```

 Para almacenar el segmento de gráfico circular mediante una instancia de `CircularString` se requiere que se usen tres puntos para cada segmento de línea.  Si no se conoce un punto intermedio, se debe calcular o se debe duplicar el extremo del segmento de línea como muestra el siguiente fragmento de código:

```sql
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');
```

 `CompoundCurve`las instancias de `LineString` permiten `CircularString` los componentes y para que solo se necesiten conocer dos puntos en los segmentos de línea del segmento de gráfico circular.  En este ejemplo de código se muestra cómo usar `CompoundCurve` para almacenar la misma figura:

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');
SELECT @g.ToString(), @g.STLength();
```

### <a name="polygon-and-curvepolygon-comparison"></a>Comparación de Polygon y CurvePolygon
 Las instancias de `CurvePolygon` pueden usar las instancias de `CircularString` y `CompoundCurve` cuando se definen sus anillos exterior e interior.  Las instancias de `Polygon` no pueden usar los tipos de segmento de arco circular: `CircularString` y `CompoundCurve`.


## <a name="see-also"></a>Consulte también
 [&#40;de datos espaciales SQL Server&#41;](../spatial/spatial-data-sql-server.md) [tipo de datos Geometry referencia](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql) del método de [tipo de datos Geography](/sql/t-sql/spatial-geography/spatial-types-geography) [STNumCurves &#40;Geometry Data Type&#41;](/sql/t-sql/spatial-geometry/stnumcurves-geometry-data-type) [STNumCurves &#40;Geography Data](/sql/t-sql/spatial-geography/stnumcurves-geography-data-type) Type&#41;[STGeomFromText &#40;geometry Data Type&#41;](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type) [STGeomFromText &#40;Geography Data Type&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)


