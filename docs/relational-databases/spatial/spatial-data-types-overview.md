---
title: "Información general de los tipos de datos espaciales | Microsoft Docs"
ms.custom: 
ms.date: 11/01/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- geometry data type [SQL Server], understanding
- geography data type [SQL Server], spatial data
- planar spatial data [SQL Server], geometry data type
- spatial data types [SQL Server]
ms.assetid: 1615db50-69de-4778-8be6-4e058c00ccd4
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4bfd021048962cb632a2d5e553ea9d6bb35a8c20
ms.lasthandoff: 04/11/2017

---
# <a name="spatial-data-types-overview"></a>Información general de los tipos de datos espaciales
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Hay dos tipos de datos espaciales. El tipo de datos **geometry** admite datos planares o euclidianos (planisferio). El tipo de datos **geometry** se ajusta tanto a las características simples de Open Geospatial Consortium (OGC) para la especificación SQL versión 1.1.0 como a SQL MM (estándar ISO).  
  
 Además, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el tipo de datos **geography** , que almacena datos elipsoidales (tierra redonda), como coordenadas de latitud y longitud GPS.  
  
> [!IMPORTANT]  
>  Para obtener una descripción detallada y ejemplos de las características espaciales introducidas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluidas las mejoras en los tipos de datos espaciales, descargue las notas del producto [Nuevas características espaciales de SQL Server Code-Named "Denali"](http://go.microsoft.com/fwlink/?LinkId=226407).  
  
##  <a name="objects"></a> Objetos de datos espaciales  
 Los tipos de datos **geometry** y **geography** admiten dieciséis objetos de datos espaciales o tipos de instancia. Pero solo se pueden *crear instancias*de once de estos tipos de instancia; puede crear y trabajar con estas instancias (o crear instancias de ellas) en una base de datos. Estas instancias obtienen determinadas propiedades de sus tipos de datos primarios que los distinguen como **Points**, **LineStrings, CircularStrings**, **CompoundCurves**, **Polygons**, **CurvePolygons** o como varias instancias de **geometry** o **geography** en una **GeometryCollection**. El tipo**Geography** tiene un tipo de instancia adicional, **FullGlobe**.  
  
 La figura siguiente describe la jerarquía de **geometry** en la que se basan los tipos de datos **geometry** y **geography** . Los tipos a partir de los que pueden crearse instancias de **geometry** y **geography** se indican en azul.  
  
 ![geom_hierarchy](../../relational-databases/spatial/media/geom-hierarchy.gif) 
  
 Como la figura indica, los diez tipos a partir de los que pueden crearse instancias de los tipos de datos **geometry** y **geography** son **Point**, **MultiPoint**, **LineString**, **CircularString**, **MultiLineString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **MultiPolygon**y **GeometryCollection**. Existe un tipo adicional a partir del que pueden crearse instancias para el tipo de datos Geography: **FullGlobe**. Los tipos **geometry** y **geography** pueden reconocer una instancia concreta siempre y cuando se trate de una instancia bien formada, aunque no se haya definido explícitamente. Por ejemplo, si define una instancia **Point** usando explícitamente el método STPointFromText(), **geometry** y **geography** reconocen la instancia como **Point**, con tal de que la entrada de método esté bien formada. Si define la misma instancia mediante el método `STGeomFromText()` , los tipos de datos **geometry** y **geography** reconocen la instancia como **Point**.  
  
 Los subtipos de los tipos Geometry y Geography se dividen en tipos simples y de colección.  Algunos métodos como `STNumCurves()` funcionan solo con los tipos simples.  
  
 Los tipos simples incluyen:  
  
-   [Point](../../relational-databases/spatial/point.md)  
  
-   [LineString](../../relational-databases/spatial/linestring.md)  
  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
  
-   [Polígono](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
 Los tipos de colección incluyen:  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolígono](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
  
##  <a name="differences"></a> Diferencias entre los tipos de datos geometry y geography  
 Los dos tipos de datos espaciales se comportan a menudo de manera bastante similar pero hay algunas diferencias clave en la manera en la que los datos se almacenan y se manipulan.  
  
### <a name="how-connecting-edges-are-defined"></a>Definición de bordes de conexión  
 Los datos de definición para los tipos **LineString** y **Polygon** son solo los vértices.  El borde de conexión entre dos vértices en un tipo Geometría es una línea recta.  Sin embargo, el borde de conexión entre dos vértices en un tipo de geografía es un arco elíptico grande corto entre los dos vértices.  Una elipse grande es la intersección del elipsoide con un plano por su centro y un arco elíptico grande es un segmento de arco de la elipse grande.  
  
### <a name="how-circular-arc-segments-are-defined"></a>Definición de los segmentos de arco circular  
 Los segmentos de arco circular para los tipos Geometry se definen en el plano de coordenadas cartesianas XY (se ignoran los valores Z). Los segmentos de arco circular para los tipos Geography se definen mediante segmentos de curva en una esfera de referencia. Los paralelos de la esfera de referencia se pueden definir mediante dos arcos circulares complementarios en los que los puntos de ambos arcos tienen un ángulo de latitud constante.  
  
### <a name="measurements-in-spatial-data-types"></a>Medidas en tipos de datos espaciales  
 En el sistema plano, o de tierra plana, las medidas de distancias y las áreas se proporcionan en la misma unidad de medida que las coordenadas. Usando el tipo de datos **geometry** , la distancia entre (2, 2) y (5, 6) es 5 unidades, independientemente de las unidades usadas.  
  
 En el sistema elíptico o de tierra redonda, las coordenadas se proporcionan en grados de latitud y longitud. Pero las longitudes y las áreas normalmente se miden en metros y metros cuadrados, aunque la medida puede depender del identificador de referencia espacial (SRID) de la instancia de **geography** . La unidad de medida más común para el tipo de datos **geography** es el metro.  
  
### <a name="orientation-of-spatial-data"></a>Orientación de datos espaciales  
 En el sistema plano, la orientación de anillo de un polígono no es un factor importante. Por ejemplo, un polígono descrito por ((0, 0), (10, 0), (0, 20), (0, 0)) es igual que un polígono descrito por ((0, 0), (0, 20), (10, 0), (0, 0)). Las características simples de OGC para la especificación de SQL no dictan una ordenación de anillos y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no exige la ordenación de anillos.  
  
 En un sistema elíptico, un polígono no tiene ningún significado, o es ambiguo, sin una orientación. Por ejemplo, ¿un anillo alrededor del ecuador describe el hemisferio norte o el hemisferio sur? Si usamos el tipo de datos **geography** para almacenar la instancia espacial, debemos especificar la orientación del anillo y describir con precisión la ubicación de la instancia. El interior del polígono de un sistema elipsoidal se define mediante la regla de la mano izquierda.  
  
 Cuando el nivel de compatibilidad es 100 o menor en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , el tipo de datos **geography** tiene las siguientes restricciones:  
  
-   Cada instancia de **geography** debe ajustarse en un hemisferio único. No se puede almacenar ningún objeto espacial mayor que un hemisferio.  
  
-   Cualquier instancia de **geography** de una representación Well-Known Text (WKT) o Well-Known Binary (WKB) de Open Geospatial Consortium (OGC) que genera un objeto mayor que un hemisferio inicia una **ArgumentException**.  
  
-   Los métodos del tipo de datos **geography** que requieren la entrada de dos instancias de **geography** , como STIntersection(), STUnion(), STDifference() y STSymDifference(), devolverán NULL si los resultados de los métodos no se ajustan en un hemisferio único. STBuffer() también devolverá NULL si la salida supera un único hemisferio.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], **FullGlobe** es un tipo especial de Polygon que abarca el mundo entero. **FullGlobe** tiene un área, pero no tiene bordes o vértices.  
  
### <a name="outer-and-inner-rings-not-important-in-geography-data-type"></a>Anillos externos e internos no importantes en el tipo de datos Geography  
 Las características simples de OGC para la especificación de SQL analizan los anillos externos e internos, pero esta distinción tiene poco sentido para el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** data type; any ring of a polygon can be taken to be the outer ring.  
  
 Para obtener más información acerca de las especificaciones de OGC, vea lo siguiente:  
  
-   [Especificaciones de OGC, Acceso a características simples, Parte 1 - Arquitectura común](http://go.microsoft.com/fwlink/?LinkId=93627)  
  
-   [Especificaciones de OGC; Acceso a características simples, Parte 2 - Opciones de SQL](http://go.microsoft.com/fwlink/?LinkId=93628)  
  
  
##  <a name="circular"></a> Segmentos de arco circular  
 Tres tipos instanciables pueden tomar segmentos de arco circular: **CircularString**, **CompoundCurve**y **CurvePolygon**.  Un segmento de arco circular se define mediante tres puntos en un plano bidimensional y el tercer punto no puede ser igual que el primero.  
  
 Las figuras A y B muestran segmentos de arco circular. Observe que cada uno de los tres puntos pertenece al perímetro de un círculo.  
  
 Las figuras C y D muestran cómo se puede definir el segmento de una línea como segmento de arco circular.  Observe que esos tres puntos continúan siendo necesarios para definir el segmento de arco circular a diferencia de un segmento de línea normal que se puede definir mediante dos puntos únicamente.  
  
 Los métodos que funcionan en tipos de segmentos de arco circular usan segmentos de línea recta para aproximarse al arco circular. El número de segmentos de línea utilizado para aproximarse al arco dependerá de su longitud y curvatura. Los valores Z se pueden almacenar para cada uno de los tipos de segmentos de arco circular; sin embargo, los métodos no usarán los valores Z en sus cálculos.  
  
> [!NOTE]  
>  Si se dan valores Z para los segmentos de arco circular, deben ser iguales para todos los puntos del segmento de arco circular para que se acepte como entrada. Por ejemplo: se acepta `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` , pero no se acepta `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` .  
  
### <a name="linestring-and-circularstring-comparison"></a>Comparación de LineString y CircularString  
 En el siguiente diagrama se muestran triángulos isósceles idénticos (el triángulo A usa segmentos de línea para definir el triángulo y el triángulo B, segmentos de arco circular):  
  
  ![7e382f76-59da-4b62-80dc-caf93e637c14](../../relational-databases/spatial/media/7e382f76-59da-4b62-80dc-caf93e637c14.gif)
  
 En este ejemplo se muestra cómo almacenar los triángulos isósceles anteriores tanto con una instancia de **LineString** como con una instancia de **CircularString** :  
  
```tsql  
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
  
 Tenga en cuenta que una instancia de **CircularString** requiere siete puntos para definir el triángulo, pero una instancia de **LineString** requiere solo cuatro puntos para definir el triángulo. Esto se debe a que una instancia de **CircularString** almacena los segmentos de arco circular y no los de línea. Por tanto, los lados del triángulo almacenado en la instancia de **CircularString** son ABC, CDE y EFA mientras que los del triángulo almacenado en la instancia de **LineString** son AC, CE y EA.  
  
 Considere el fragmento de código siguiente:  
  
```tsql  
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);  
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);  
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];  
```  
  
 Este fragmento de código generará los siguientes resultados:  
  
```  
LS LengthCS Length  
5.65685…6.28318…  
```  
  
 En la ilustración siguiente se muestra cómo se almacena cada tipo (la línea roja indica **LineString** `@g1` y la azul, **CircularString** `@g2`):  
  
 ![e52157b5-5160-4a4b-8560-50cdcf905b76](../../relational-databases/spatial/media/e52157b5-5160-4a4b-8560-50cdcf905b76.gif)  
  
 Como se muestra en la ilustración anterior, las instancias de **CircularString** usan menos puntos para almacenar límites curvos con mayor precisión que las instancias de **LineString** . Las instancias de**CircularString** son útiles para almacenar límites circulares, como un radio de búsqueda de veinte millas desde un punto específico. Las instancias de**LineString** funcionan bien para almacenar límites que son lineales como un bloque de ciudad cuadrado.  
  
### <a name="linestring-and-compoundcurve-comparison"></a>Comparación de LineString y CompoundCurve  
 En los siguientes ejemplos de código se muestra cómo almacenar la misma figura con instancias de **LineString** y **CompoundCurve** :  
  
```tsql  
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');  
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');  
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');  
```  
  
 o  
  
 En los ejemplos anteriores, una instancia de **LineString** o un instancia de **CompoundCurve** pudieron almacenar la figura.  En el siguiente ejemplo se usa **CompoundCurve** para almacenar un segmento de gráfico circular:  
  
```tsql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');  
```  
  
 Una instancia de **CompoundCurve** puede almacenar directamente el segmento de arco circular (2 2, 1 3, 0 2), mientras que una instancia de **LineString** tendría que convertir la curva en varios segmentos de línea más pequeños.  
  
### <a name="circularstring-and-compoundcurve-comparison"></a>Comparación de CircularString y CompoundCurve  
 En el siguiente ejemplo de código se muestra cómo se puede almacenar el segmento de gráfico circular en una instancia de **CircularString** :  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
SELECT @g.ToString(), @g.STLength();  
```  
  
 Para almacenar el segmento de gráfico circular mediante una instancia de **CircularString** se requiere que se usen tres puntos para cada segmento de línea.  Si no se conoce un punto intermedio, se debe calcular o se debe duplicar el extremo del segmento de línea como muestra el siguiente fragmento de código:  
  
```tsql  
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');  
```  
  
 Las instancias de**CompoundCurve** permiten componentes tanto de **LineString** como de **CircularString** para que solo se necesiten conocer dos puntos en los segmentos de línea del segmento de gráfico circular.  En este ejemplo de código se muestra cómo usar **CompoundCurve** para almacenar la misma figura:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');  
SELECT @g.ToString(), @g.STLength();  
```  
  
### <a name="polygon-and-curvepolygon-comparison"></a>Comparación de Polygon y CurvePolygon  
 Las instancias de**CurvePolygon** pueden usar las instancias de **CircularString** y **CompoundCurve** instances when defining their exterior y interior rings.  Las instancias de**Polygon** no pueden usar los tipos de segmento de arco circular: **CircularString** y **CompoundCurve**.  
 
  
## <a name="see-also"></a>Vea también  

- [Datos espaciales (SQL Server)](https://msdn.microsoft.com/library/bb933790.aspx) 
- [Referencia de los métodos del tipo de datos geometry](https://msdn.microsoft.com/library/bb933973.aspx) 
- [Referencia de los métodos del tipo de datos geography](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)   
- [STNumCurves &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
- [STNumCurves &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)   
- [STGeomFromText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stgeomfromtext-geometry-data-type.md)   
- [STGeomFromText &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  

