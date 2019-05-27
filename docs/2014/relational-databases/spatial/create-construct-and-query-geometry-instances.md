---
title: Creación, construcción y consulta de instancias de Geometry | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- planar spatial data [SQL Server], getting started
- geometry data type [SQL Server], getting started
ms.assetid: c6b5c852-37d2-48d0-a8ad-e43bb80d6514
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: cb99c2ff07f30d268980c5c1c4d43a34904cdec9
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014309"
---
# <a name="create-construct-and-query-geometry-instances"></a>Crear, construir y consultar instancias de Geometry
  El tipo de datos espacial plano `geometry` representa los datos en un sistema de coordenadas euclidiano (plano). Implementan este tipo como un tipo de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de Common Language Runtime (CLR).  
  
 El tipo `geometry` está predefinido y está disponible en cada base de datos. Puede crear columnas de tabla de tipo `geometry` y operar con los datos `geometry` de la misma manera que con los demás tipos CLR.  
  
 El tipo de datos `geometry` (plano) admitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cumple con las características simples de Geospatial Consortium (OGC) para la especificación SQL versión 1.1.0.  
  
 Para obtener más información acerca de las especificaciones de OGC, vea lo siguiente:  
  
-   [Especificaciones de OGC, Acceso a características simples, Parte 1 - Arquitectura común](https://go.microsoft.com/fwlink/?LinkId=93628)  
  
-   [Especificaciones de OGC, acceso a características simples, parte 2: opciones de SQL](https://go.microsoft.com/fwlink/?LinkId=93629)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite un subconjunto del estándar GML 3.1 existente que se define en el siguiente esquema: [https://schemas.microsoft.com/sqlserver/profiles/gml/SpatialGML.xsd](https://go.microsoft.com/fwlink/?LinkId=230959).  
  
##  <a name="creating"></a> Crear o construir una instancia de geometry  
  
###  <a name="existing"></a> Crear una instancia de geometry a partir de una instancia existente  
 El tipo de datos `geometry` proporciona numerosos métodos integrados que puede usar para crear nuevas instancias de `geometry` basadas en instancias existentes.  
  
 **Para crear un búfer alrededor de un objeto geometry**  
 [STBuffer &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stbuffer-geometry-data-type)  
  
 [BufferWithTolerance &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type)  
  
 **Para crear una versión simplificada de un objeto geometry**  
 [Reduce &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/reduce-geometry-data-type)  
  
 **Para crear la forma convexa de un objeto geometry**  
 [STConvexHull &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stconvexhull-geometry-data-type)  
  
 **Para crear un objeto geometry a partir de la intersección de dos objetos geometry**  
 [STIntersection &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stintersection-geometry-data-type)  
  
 **Para crear un objeto geometry a partir de la unión de dos objetos geometry**  
 [STUnion &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stunion-geometry-data-type)  
  
 **Para crear un objeto geometry a partir de los puntos en los que un objeto geometry no se superpone a otro**  
 [STDifference &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stdifference-geometry-data-type)  
  
 **Para crear un objeto geometry a partir de los puntos en los que dos objetos geometry no se superponen**  
 [STSymDifference &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stsymdifference-geometry-data-type)  
  
 **Para crear una instancia de Point arbitraria que se encuentra en un objeto geometry existente**  
 [STPointOnSurface &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
  
  
###  <a name="wkt"></a> Construir una instancia de geometry a partir de datos Well-Known Text  
 El tipo de datos `geometry` proporciona varios métodos integrados que generan un objeto geometry a partir de la representación WKT de Open Geospatial Consortium (OGC). La norma WKT consiste en una cadena de texto que permite intercambiar datos de geometría de forma textual.  
  
 **Para construir cualquier tipo de instancia de geometry a partir de datos WKT**  
 [STGeomFromText &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type)  
  
 [Parse &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/parse-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo Point a partir de datos WKT**  
 [STPointFromText &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpointfromtext-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo MultiPoint a partir de datos WKT**  
 [STMPointFromText &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stmpointfromtext-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo LineString a partir de datos WKT**  
 [STLineFromText &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stlinefromtext-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo MultiLineString a partir de datos WKT**  
 [STMLineFromText &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stmlinefromtext-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo Polygon a partir de datos WKT**  
 [STPolyFromText &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpolyfromtext-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo MultiPolygon a partir de datos WKT**  
 [STMPolyFromText &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stmpolyfromtext-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo GeometryCollection a partir de datos WKT**  
 [STGeomCollFromText &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromtext-geometry-data-type)  
  
  
  
###  <a name="wkb"></a> Construir una instancia de geometry a partir de datos Well-Known Binary  
 WKB es un formato binario especificado por Open Geospatial Consortium (OGC) que permite intercambiar datos de tipo `geometry` entre una aplicación cliente y una base de datos SQL. Las funciones siguientes aceptan datos WKB para construir las instancias de geometry:  
  
 **Para construir cualquier tipo de instancia de geometry a partir de datos WKB**  
 [STGeomFromWKB &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stgeomfromwkb-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo Point a partir de datos WKB**  
 [STPointFromWKB &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpointfromwkb-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo MultiPoint a partir de datos WKB**  
 [STMPointFromWKB &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stmpointfromwkb-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo LineString a partir de datos WKB**  
 [STLineFromWKB &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stlinefromwkb-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo MultiLineString a partir de datos WKB**  
 [STMLineFromWKB &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stmlinefromwkb-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo Polygon a partir de datos WKB**  
 [STPolyFromWKB &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpolyfromwkb-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo MultiPolygon a partir de datos WKB**  
 [STMPolyFromWKB &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stmpolyfromwkb-geometry-data-type)  
  
 **Para construir una instancia de geometry de tipo GeometryCollection a partir de datos WKB**  
 [STGeomCollFromWKB &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromwkb-geometry-data-type)  
  
  
  
###  <a name="gml"></a> Para construir una instancia de geometry a partir de datos de texto GML  
 El `geometry` tipo de datos proporciona un método que genera un `geometry` instancia a partir de GML, una representación XML de objetos geométricos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite un subconjunto de GML.  
  
 **Para construir un tipo de instancia de geometry a partir de datos GML**  
 [GeomFromGml &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/geomfromgml-geometry-data-type)  
  
  
  
##  <a name="returning"></a> Devolver Well-Known Text y Well-Known Binary a partir una instancia de geometry  
 Puede usar los métodos siguientes para devolver el formato WKT o WKB de una instancia de `geometry`:  
  
 **Para devolver la representación WKT de una instancia de geometry**  
 [STAsText &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stastext-geometry-data-type)  
  
 [ToString &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/tostring-geometry-data-type)  
  
 **Para devolver la representación WKT de una instancia de geometry, incluidos cualesquiera valores Z y M.**  
 [AsTextZM &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/astextzm-geometry-data-type)  
  
 **Para devolver la representación WKB de una instancia de geometry**  
 [STAsBinary &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stasbinary-geometry-data-type)  
  
 **Para devolver la representación GML de una instancia de geometry**  
 [AsGml &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/asgml-geometry-data-type)  
  
  
  
##  <a name="querying"></a> Consultar propiedades y comportamientos de instancias de geometry  
 Todos los `geometry` instancias tienen un número de propiedades que se pueden recuperar a través de métodos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona. Los temas siguientes definen las propiedades y los comportamientos de tipos geometry, y los métodos para consultar cada uno.  
  
###  <a name="valid"></a> Validez, tipo de instancia e información de GeometryCollection  
 Una vez construida una instancia de `geometry`, puede usar los métodos siguientes para determinar si su formato es correcto, devolver el tipo de instancia o, si es una instancia de una colección, devolver una instancia de `geometry` específica.  
  
 **Para devolver el tipo de instancia de un objeto geometry**  
 [STGeometryType &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stgeometrytype-geometry-data-type)  
  
 **Para determinar si un objeto geometry es un tipo de instancia determinado**  
 [InstanceOf &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/instanceof-geometry-data-type)  
  
 **Para determinar si el formato de una instancia de geometry es correcto de acuerdo con su tipo de instancia**  
 [STIsValid &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)  
  
 **Para convertir una instancia de geometry en una instancia de geometry con el formato correcto de acuerdo con su tipo de instancia**  
 [MakeValid &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/makevalid-geometry-data-type)  
  
 **Para devolver el número de objetos geometry existente en una instancia de GeometryCollection**  
 [STNumGeometries &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stnumgeometries-geometry-data-type)  
  
 Para devolver un objeto geometry específico de una instancia de GeometryCollection  
 [STGeometryN &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stgeometryn-geometry-data-type)STGeometryN (tipo de datos geometry)  
  
  
  
###  <a name="number"></a> Número de puntos  
 Vacía todos los `geometry` están formadas por instancias *puntos*. Estos puntos representan las coordenadas X e Y del plano en el cual se dibujan los objetos geometry. El tipo de datos de `geometry` proporciona numerosos métodos integrados para consultar los puntos de una instancia.  
  
 **Devolver el número de puntos que comprende una instancia**  
 [STNumPoints &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)  
  
 **Devolver un punto concreto en una instancia**  
 [STPointN](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **Devolver un punto arbitrario que se encuentra en una instancia**  
 [STPointOnSurface](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
 **Devolver el punto inicial de una instancia**  
 [STStartPoint](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)  
  
 **Devolver el punto final de una instancia**  
 [STEndpoint](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)  
  
 **Devolver la coordenada X de una instancia de Point**  
 [STX &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stx-geometry-data-type)  
  
 **Para devolver la coordenada Y de una instancia de Point**  
 [STY](/sql/t-sql/spatial-geometry/sty-geometry-data-type)  
  
 **Para devolver el punto central geométrico de una instancia de Polygon, CurvePolygon o MultiPolygon**  
 [STCentroid](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)  
  
  
  
###  <a name="dimension"></a> Dimensión  
 Una instancia de `geometry` no vacía puede ser no dimensional, unidimensional o bidimensional. `geometries` no dimensionales, como `Point` y `MultiPoint`, no tienen ninguna longitud ni área. Los objetos unidimensionales, como `LineString, CircularString, CompoundCurve` y `MultiLineString`, tienen longitud. Las instancias bidimensionales, como `Polygon`, `CurvePolygon` y `MultiPolygon`, tienen área y longitud. Las instancias vacías informarán de una dimensión de -1 y `GeometryCollection` informará de un área dependiente de los tipos de su contenido.  
  
 **Devolver la dimensión de una instancia**  
 [STDimension](/sql/t-sql/spatial-geometry/stdimension-geometry-data-type)  
  
 **Devolver la longitud de una instancia**  
 [STLength](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)  
  
 **Devolver el área de una instancia**  
 [STArea](/sql/t-sql/spatial-geometry/starea-geometry-data-type)  
  
  
  
###  <a name="empty"></a> Vacía  
 Un *vacía* `geometry` instancia no tiene puntos. La longitud de instancias de `LineString, CircularString`, `CompoundCurve` y `MultiLineString` es cero. El área de las instancias de `Polygon`, `CurvePolygon` y `MultiPolygon` vacías es 0.  
  
 **Para determinar si una instancia está vacía**  
 [STIsEmpty](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type).  
  
  
  
###  <a name="simple"></a> Simple  
 Para un `geometry` de la instancia sea *simple*, debe cumplir estos requisitos:  
  
-   Cada figura de la instancia no debe cortarse, excepto en sus extremos.  
  
-   Ninguna de las dos figuras de la instancia puede cortarse en un punto que no esté en ambos de sus límites.  
  
> [!NOTE]  
>  Los objetos geometry vacíos son siempre simples.  
  
 **Determinar si una instancia es simple**  
 [STIsSimple](/sql/t-sql/spatial-geometry/stissimple-geometry-data-type).  
  
  
  
###  <a name="boundary"></a> Límite, interior y exterior  
 El *interiores* de un `geometry` instancia es el espacio ocupado por la instancia y el *exterior* es el espacio no ocupado.  
  
 El*límite* lo define OGC de la siguiente manera:  
  
-   La instancias de `Point` y `MultiPoint` no tienen un límite.  
  
-   Los límites de `LineString` y `MultiLineString` están formados por los puntos de inicio y de fin, quitando los que se producen un número par de veces.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 1, 0 0, 1 0, 0 1), (1 1, 1 0))');  
SELECT @g.STBoundary().ToString();  
```  
  
 El límite de una instancia de `Polygon` o `MultiPolygon` es el conjunto de sus anillos.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0), (1 1, 1 2, 2 2, 2 1, 1 1))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **Devolver el límite de una instancia**  
 [STBoundary](/sql/t-sql/spatial-geometry/stboundary-geometry-data-type)  
  
  
  
###  <a name="envelope"></a> Envolvente  
 El *sobres* de un `geometry` , también conocida como instancia el *rectángulo*, es el rectángulo alineado con el eje formado por el mínimo y máximo (X, Y) coordenadas de la instancia.  
  
 **Para devolver la envolvente de una instancia**  
 [STEnvelope](/sql/t-sql/spatial-geometry/stenvelope-geometry-data-type)  
  
  
  
###  <a name="closure"></a> Clausura  
 Un *cerrado* `geometry` instancia es una figura cuyos puntos de inicio y puntos de conexión son los mismos. Las instancias `Polygon` se consideran cerradas. Las instancias `Point` no son cerradas.  
  
 Un anillo es una instancia de `LineString` simple y cerrada.  
  
 **Para determinar si una instancia está cerrada**  
 [STIsClosed](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)  
  
 **Para determinar si una instancia es un anillo**  
 [STIsRing](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)  
  
 **Para devolver el anillo exterior de una instancia de Polygon**  
 [STExteriorRing](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type)  
  
 **Para devolver el número de anillos interiores de un Polygon**  
 [STNumInteriorRing](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type)  
  
 **Devolver un anillo interior especificado de un Polygon**  
 [STInteriorRingN](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type)  
  
  
  
###  <a name="srid"></a> Identificador de referencia espacial (SRID)  
 El identificador de referencia espacial (SRID) es un identificador que especifica en qué sistema de coordenadas está representada la instancia de `geometry`. Dos instancias con SRID diferentes son incomparables.  
  
 **Para establecer o devolver el SRID de una instancia**  
 [STSrid](/sql/t-sql/spatial-geometry/stsrid-geometry-data-type)  
  
 Esta propiedad se puede modificar.  
  
  
  
##  <a name="rel"></a> Determinar las relaciones entre instancias de geometry  
 El tipo de datos `geometry` proporciona muchos métodos integrados que puede usar para determinar las relaciones entre dos instancias de `geometry`.  
  
 **Para determinar si dos instancias comprenden el mismo conjunto de puntos**  
 [STEquals](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **Para determinar si dos instancias no son contiguas**  
 [STDisjoint](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **Para determinar si dos instancias contienen puntos que forman una intersección**  
 [STIntersects](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **Para determinar si dos instancias se tocan**  
 [STTouches](/sql/t-sql/spatial-geometry/sttouches-geometry-data-type)  
  
 **Para determinar si dos instancias se superponen**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **Para determinar si dos instancias se cruzan**  
 [STCrosses](/sql/t-sql/spatial-geometry/stcrosses-geometry-data-type)  
  
 **Para determinar si una instancia está dentro de otra**  
 [STWithin](/sql/t-sql/spatial-geometry/stwithin-geometry-data-type)  
  
 **Para determinar si una instancia contiene a otra**  
 [STContains](/sql/t-sql/spatial-geometry/stcontains-geometry-data-type)  
  
 **Para determinar si una instancia se superpone a otra**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **Para determinar si existe una relación espacial entre dos instancias**  
 [STRelate](/sql/t-sql/spatial-geometry/strelate-geometry-data-type)  
  
 **Para determinar la distancia más corta entre los puntos de dos objetos geometry**  
 [STDistance](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
  
  
##  <a name="defaultsrid"></a> Las instancias de geometry tienen como valor predeterminado SRID cero  
 El SRID predeterminado para instancias de `geometry` en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es 0. Con los datos espaciales de `geometry`, no se necesita el SRID específico de la instancia espacial para realizar cálculos; por tanto, las instancias pueden encontrarse en un espacio plano indefinido. Para indicar el espacio plano indefinido en los cálculos de métodos de tipo de datos `geometry`, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa SRID 0.  
  
##  <a name="examples"></a> Ejemplos  
 En los dos ejemplos siguientes se muestra cómo agregar y consultar datos de geometry.  
  
-   En el primer ejemplo se crea una tabla con una columna de identidad y una columna de tipo `geometry` , `GeomCol1`. Una tercera columna representa la columna de tipo `geometry` en su representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) y utiliza el método `STAsText()` . A continuación se insertan dos filas: una que contiene una instancia de `LineString` de `geometry`y otra que contiene una instancia de `Polygon` .  
  
    ```  
    IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
        DROP TABLE dbo.SpatialTable;  
    GO  
  
    CREATE TABLE SpatialTable   
        ( id int IDENTITY (1,1),  
        GeomCol1 geometry,   
        GeomCol2 AS GeomCol1.STAsText() );  
    GO  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
    GO  
    ```  
  
-   En el segundo ejemplo se usa el método `STIntersection()` para devolver los puntos de intersección de las dos instancias de `geometry` insertadas previamente.  
  
    ```  
    DECLARE @geom1 geometry;  
    DECLARE @geom2 geometry;  
    DECLARE @result geometry;  
  
    SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geom1.STIntersection(@geom2);  
    SELECT @result.STAsText();  
    ```  
  
  
  
## <a name="see-also"></a>Vea también  
 [Datos espaciales &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
