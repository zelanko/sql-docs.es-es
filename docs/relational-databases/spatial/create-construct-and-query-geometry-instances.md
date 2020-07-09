---
title: Creación, construcción y consulta de instancias de Geometry | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- planar spatial data [SQL Server], getting started
- geometry data type [SQL Server], getting started
ms.assetid: c6b5c852-37d2-48d0-a8ad-e43bb80d6514
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ed268a5b8097b637c8a7e51eecf2e088aad58e04
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751119"
---
# <a name="create-construct-and-query-geometry-instances"></a>Crear, construir y consultar instancias de Geometry
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  El tipo de datos espaciales planar **geometry**representa los datos en un sistema de coordenadas euclidiano (plano). Implementan este tipo como un tipo de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de Common Language Runtime (CLR).  
  
 El tipo **geometry** está predefinido y está disponible en cada base de datos. Puede crear columnas de tabla de tipo **geometry** y operar con los datos **geometry** de la misma manera que con los demás tipos CLR.  
  
 El tipo de datos **geometry** (planar) admitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cumple con las características simples de Open Geospatial Consortium (OGC) para la especificación SQL versión 1.1.0.  
  
 Para obtener más información acerca de las especificaciones de OGC, vea lo siguiente:  
  
-   [Especificaciones de OGC, Acceso a características simples, Parte 1 - Arquitectura común](https://go.microsoft.com/fwlink/?LinkId=93628)  
  
-   [Especificaciones de OGC, acceso a características simples, parte 2: opciones de SQL](https://go.microsoft.com/fwlink/?LinkId=93629)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite un subconjunto del estándar GML 3.1 existente que se define en el siguiente esquema: [https://schemas.microsoft.com/sqlserver/profiles/gml/SpatialGML.xsd](https://go.microsoft.com/fwlink/?LinkId=230959).  
  
##  <a name="creating-or-constructing-a-new-geometry-instance"></a><a name="creating"></a> Crear o construir una instancia de geometry  
  
###  <a name="creating-a-new-geometry-instance-from-an-existing-instance"></a><a name="existing"></a> Crear una instancia de geometry a partir de una instancia existente  
 El tipo de datos **geometry** proporciona numerosos métodos integrados que puede usar para crear nuevas instancias de **geometry** basadas en instancias existentes.  
  
 **Para crear un búfer alrededor de un objeto geometry**  
 [STBuffer &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)  
  
 [BufferWithTolerance &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)  
  
 **Para crear una versión simplificada de un objeto geometry**  
 [Reduce &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/reduce-geometry-data-type.md)  
  
 **Para crear la forma convexa de un objeto geometry**  
 [STConvexHull &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stconvexhull-geometry-data-type.md)  
  
 **Para crear un objeto geometry a partir de la intersección de dos objetos geometry**  
 [STIntersection &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stintersection-geometry-data-type.md)  
  
 **Para crear un objeto geometry a partir de la unión de dos objetos geometry**  
 [STUnion &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stunion-geometry-data-type.md)  
  
 **Para crear un objeto geometry a partir de los puntos en los que un objeto geometry no se superpone a otro**  
 [STDifference &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stdifference-geometry-data-type.md)  
  
 **Para crear un objeto geometry a partir de los puntos en los que dos objetos geometry no se superponen**  
 [STSymDifference &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stsymdifference-geometry-data-type.md)  
  
 **Para crear una instancia de Point arbitraria que se encuentra en un objeto geometry existente**  
 [STPointOnSurface &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)  
  
  
###  <a name="constructing-a-geometry-instance-from-well-known-text-input"></a><a name="wkt"></a> Construir una instancia de geometry a partir de datos Well-Known Text  
 El tipo de datos **geometry** proporciona varios métodos integrados que generan un objeto geometry a partir de la representación WKT de Open Geospatial Consortium (OGC). La norma WKT consiste en una cadena de texto que permite intercambiar datos de geometría de forma textual.  
  
 **Para construir cualquier tipo de instancia de geometry a partir de datos WKT**  
 [STGeomFromText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stgeomfromtext-geometry-data-type.md)  
  
 [Parse &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/parse-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo Point a partir de datos WKT**  
 [STPointFromText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stpointfromtext-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo MultiPoint a partir de datos WKT**  
 [STMPointFromText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stmpointfromtext-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo LineString a partir de datos WKT**  
 [STLineFromText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stlinefromtext-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo MultiLineString a partir de datos WKT**  
 [STMLineFromText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stmlinefromtext-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo Polygon a partir de datos WKT**  
 [STPolyFromText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stpolyfromtext-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo MultiPolygon a partir de datos WKT**  
 [STMPolyFromText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stmpolyfromtext-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo GeometryCollection a partir de datos WKT**  
 [STGeomCollFromText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stgeomcollfromtext-geometry-data-type.md)  
  
  
###  <a name="constructing-a-geometry-instance-from-well-known-binary-input"></a><a name="wkb"></a> Construir una instancia de geometry a partir de datos Well-Known Binary  
 WKB es un formato binario especificado por Open Geospatial Consortium (OGC) que permite intercambiar datos de tipo **geometry** entre una aplicación cliente y una base de datos SQL. Las funciones siguientes aceptan datos WKB para construir las instancias de geometry:  
  
 **Para construir cualquier tipo de instancia de geometry a partir de datos WKB**  
 [STGeomFromWKB &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stgeomfromwkb-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo Point a partir de datos WKB**  
 [STPointFromWKB &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stpointfromwkb-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo MultiPoint a partir de datos WKB**  
 [STMPointFromWKB &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stmpointfromwkb-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo LineString a partir de datos WKB**  
 [STLineFromWKB &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stlinefromwkb-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo MultiLineString a partir de datos WKB**  
 [STMLineFromWKB &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stmlinefromwkb-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo Polygon a partir de datos WKB**  
 [STPolyFromWKB &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stpolyfromwkb-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo MultiPolygon a partir de datos WKB**  
 [STMPolyFromWKB &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stmpolyfromwkb-geometry-data-type.md)  
  
 **Para construir una instancia de geometry de tipo GeometryCollection a partir de datos WKB**  
 [STGeomCollFromWKB &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stgeomcollfromwkb-geometry-data-type.md)  
  
  
###  <a name="constructing-a-geometry-instance-from-gml-text-input"></a><a name="gml"></a> Para construir una instancia de geometry a partir de datos de texto GML  
 El tipo de datos **geometry** proporciona un método que genera una instancia de **geometry** a partir de GML (lenguaje de marcado de geografía), una representación XML de objetos geométricos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite un subconjunto de GML.  
  
 **Para construir un tipo de instancia de geometry a partir de datos GML**  
 [GeomFromGml &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/geomfromgml-geometry-data-type.md)  
  
  
##  <a name="returning-well-known-text-and-well-known-binary-from-a-geometry-instance"></a><a name="returning"></a> Devolver Well-Known Text y Well-Known Binary a partir una instancia de geometry  
 Puede usar los métodos siguientes para devolver el formato WKT o WKB de una instancia de **geometry** :  
  
 **Para devolver la representación WKT de una instancia de geometry**  
 [STAsText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)  
  
 [ToString &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/tostring-geometry-data-type.md)  
  
 **Para devolver la representación WKT de una instancia de geometry, incluidos cualesquiera valores Z y M.**  
 [AsTextZM &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
 **Para devolver la representación WKB de una instancia de geometry**  
 [STAsBinary &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stasbinary-geometry-data-type.md)  
  
 **Para devolver la representación GML de una instancia de geometry**  
 [AsGml &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/asgml-geometry-data-type.md)  
  
  
##  <a name="querying-the-properties-and-behaviors-of-geometry-instances"></a><a name="querying"></a> Consultar propiedades y comportamientos de instancias de geometry  
 Todas las instancias de **geometry** tienen varias propiedades que se pueden recuperar a través de los métodos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona. Los temas siguientes definen las propiedades y los comportamientos de tipos geometry, y los métodos para consultar cada uno.  
  
###  <a name="validity-instance-type-and-geometrycollection-information"></a><a name="valid"></a> Validez, tipo de instancia e información de GeometryCollection  
 Una vez construida una instancia de **geometry** , puede usar los métodos siguientes para determinar si su formato es correcto, devolver el tipo de instancia o, si es una instancia de una colección, devolver una instancia de **geometry** específica.  
  
 **Para devolver el tipo de instancia de un objeto geometry**  
 [STGeometryType &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
 **Para determinar si un objeto geometry es un tipo de instancia determinado**  
 [InstanceOf &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/instanceof-geometry-data-type.md)  
  
 **Para determinar si el formato de una instancia de geometry es correcto de acuerdo con su tipo de instancia**  
 [STIsValid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
 **Para convertir una instancia de geometry en una instancia de geometry con el formato correcto de acuerdo con su tipo de instancia**  
 [MakeValid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)  
  
 **Para devolver el número de objetos geometry existente en una instancia de GeometryCollection**  
 [STNumGeometries &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stnumgeometries-geometry-data-type.md)  
  
 Para devolver un objeto geometry específico de una instancia de GeometryCollection  
 [STGeometryN &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stgeometryn-geometry-data-type.md)STGeometryN (tipo de datos geometry)  
  
  
###  <a name="number-of-points"></a><a name="number"></a> Número de puntos  
 Todas las instancias de **geometry** no vacías están compuestas de *puntos*. Estos puntos representan las coordenadas X e Y del plano en el cual se dibujan los objetos geometry. El tipo de datos**geometry** proporciona numerosos métodos integrados para consultar los puntos de una instancia.  
  
 **Devolver el número de puntos que comprende una instancia**  
 [STNumPoints &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)  
  
 **Devolver un punto concreto en una instancia**  
 [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)  
  
 **Devolver un punto arbitrario que se encuentra en una instancia**  
 [STPointOnSurface](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)  
  
 **Devolver el punto inicial de una instancia**  
 [STStartPoint](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)  
  
 **Devolver el punto final de una instancia**  
 [STEndpoint](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)  
  
 **Devolver la coordenada X de una instancia de Point**  
 [STX &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)  
  
 **Para devolver la coordenada Y de una instancia de Point**  
 [STY](../../t-sql/spatial-geometry/sty-geometry-data-type.md)  
  
 **Para devolver el punto central geométrico de una instancia de Polygon, CurvePolygon o MultiPolygon**  
 [STCentroid](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)  
  
  
###  <a name="dimension"></a><a name="dimension"></a> Dimensión  
 Una instancia de **geometry** no vacía puede ser no dimensional, unidimensional o bidimensional. Los tipos de datos **geometry**no dimensionales, como **Point** y **MultiPoint**, no tienen ni longitud ni área. Los objetos unidimensionales, como **LineString, CircularString, CompoundCurve**y **MultiLineString**, tienen longitud. Las instancias bidimensionales, como **Polygon**, **CurvePolygon**y **MultiPolygon**, tienen área y longitud. Las instancias vacías informarán de una dimensión de -1 y **GeometryCollection** informará de un área dependiente de los tipos de su contenido.  
  
 **Devolver la dimensión de una instancia**  
 [STDimension](../../t-sql/spatial-geometry/stdimension-geometry-data-type.md)  
  
 **Devolver la longitud de una instancia**  
 [STLength](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)  
  
 **Devolver el área de una instancia**  
 [STArea](../../t-sql/spatial-geometry/starea-geometry-data-type.md)  
  
  
###  <a name="empty"></a><a name="empty"></a> Vacía  
 Una instancia _empty_**geometry** no tiene puntos. La longitud de instancias de **LineString, CircularString**, **CompoundCurve**y **MultiLineString** es cero. El área de las instancias de **Polygon**, **CurvePolygon**y **MultiPolygon** vacías es 0.  
  
 **Para determinar si una instancia está vacía**  
 [STIsEmpty](../../t-sql/spatial-geometry/stisempty-geometry-data-type.md).  
  
  
###  <a name="simple"></a><a name="simple"></a> Simple  
 Para que una **geometry** de la instancia sea *simple*, debe cumplir estos requisitos:  
  
-   Cada figura de la instancia no debe cortarse, excepto en sus extremos.  
  
-   Ninguna de las dos figuras de la instancia puede cortarse en un punto que no esté en ambos de sus límites.  
  
> [!NOTE]  
>  Los objetos geometry vacíos son siempre simples.  
  
 **Determinar si una instancia es simple**  
 [STIsSimple](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md).  
  
  
###  <a name="boundary-interior-and-exterior"></a><a name="boundary"></a> Límite, interior y exterior  
 El *interior* de una instancia de **geometry** es el espacio ocupado por la instancia y el *exterior* es el espacio no ocupado.  
  
 El*límite* lo define OGC de la siguiente manera:  
  
-   La instancias de**Point** y **MultiPoint** no tienen un límite.  
  
-   Los límites de**LineString** y **MultiLineString** boundaries are formed by the start points y end points, removing those that occur an even number of times.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 1, 0 0, 1 0, 0 1), (1 1, 1 0))');  
SELECT @g.STBoundary().ToString();  
```  
  
 El límite de una instancia de **Polygon** o **MultiPolygon** es el conjunto de sus anillos.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0), (1 1, 1 2, 2 2, 2 1, 1 1))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **Devolver el límite de una instancia**  
 [STBoundary](../../t-sql/spatial-geometry/stboundary-geometry-data-type.md)  
   
###  <a name="envelope"></a><a name="envelope"></a> Envolvente  
 La *envolvente* de una instancia de **geometry** , también conocida como el *cuadro de límite*, es el rectángulo alineado con el eje formado por las coordenadas mínimas y máximas (X, Y) de la instancia.  
  
 **Para devolver la envolvente de una instancia**  
 [STEnvelope](../../t-sql/spatial-geometry/stenvelope-geometry-data-type.md)  
  
###  <a name="closure"></a><a name="closure"></a> Clausura  
 Una instancia de **geometry**_cerrada_ es una figura cuyos puntos de inicio y de finalización son los mismos. Las instancias**Polygon** se consideran cerradas. Las instancias**Point** no son cerradas.  
  
 Un anillo es una instancia de **LineString** simple y cerrada.  
  
 **Para determinar si una instancia está cerrada**  
 [STIsClosed](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)  
  
 **Para determinar si una instancia es un anillo**  
 [STIsRing](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)  
  
 **Para devolver el anillo exterior de una instancia de Polygon**  
 [STExteriorRing](../../t-sql/spatial-geometry/stexteriorring-geometry-data-type.md)  
  
 **Para devolver el número de anillos interiores de un Polygon**  
 [STNumInteriorRing](../../t-sql/spatial-geometry/stnuminteriorring-geometry-data-type.md)  
  
 **Devolver un anillo interior especificado de un Polygon**  
 [STInteriorRingN](../../t-sql/spatial-geometry/stinteriorringn-geometry-data-type.md)  
  
  
###  <a name="spatial-reference-id-srid"></a><a name="srid"></a> Identificador de referencia espacial (SRID)  
 El identificador de referencia espacial (SRID) es un identificador que especifica en qué sistema de coordenadas está representada la instancia de **geometry** . Dos instancias con SRID diferentes son incomparables.  
  
 **Para establecer o devolver el SRID de una instancia**  
 [STSrid](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)  
  
> [!NOTE]
> Esta propiedad se puede modificar.  
  
##  <a name="determining-relationships-between-geometry-instances"></a><a name="rel"></a> Determinar las relaciones entre instancias de geometry  
 El tipo de datos **geometry** proporciona muchos métodos integrados que puede usar para determinar las relaciones entre dos instancias de **geometry** .  
  
 **Para determinar si dos instancias comprenden el mismo conjunto de puntos**  
 [STEquals](../../t-sql/spatial-geometry/stequals-geometry-data-type.md)  
  
 **Para determinar si dos instancias no son contiguas**  
 [STDisjoint](../../t-sql/spatial-geometry/stdisjoint-geometry-data-type.md)  
  
 **Para determinar si dos instancias contienen puntos que forman una intersección**  
 [STIntersects](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
 **Para determinar si dos instancias se tocan**  
 [STTouches](../../t-sql/spatial-geometry/sttouches-geometry-data-type.md)  
  
 **Para determinar si dos instancias se superponen**  
 [STOverlaps](../../t-sql/spatial-geometry/stoverlaps-geometry-data-type.md)  
  
 **Para determinar si dos instancias se cruzan**  
 [STCrosses](../../t-sql/spatial-geometry/stcrosses-geometry-data-type.md)  
  
 **Para determinar si una instancia está dentro de otra**  
 [STWithin](../../t-sql/spatial-geometry/stwithin-geometry-data-type.md)  
  
 **Para determinar si una instancia contiene a otra**  
 [STContains](../../t-sql/spatial-geometry/stcontains-geometry-data-type.md)  
  
 **Para determinar si una instancia se superpone a otra**  
 [STOverlaps](../../t-sql/spatial-geometry/stoverlaps-geometry-data-type.md)  
  
 **Para determinar si existe una relación espacial entre dos instancias**  
 [STRelate](../../t-sql/spatial-geometry/strelate-geometry-data-type.md)  
  
 **Para determinar la distancia más corta entre los puntos de dos objetos geometry**  
 [STDistance](../../t-sql/spatial-geometry/stdistance-geometry-data-type.md)  
  
##  <a name="geometry-instances-default-to-zero-srid"></a><a name="defaultsrid"></a> Las instancias de geometry tienen como valor predeterminado SRID cero  
 El SRID predeterminado para instancias de **geometry** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es 0. Con los datos espaciales de **geometry** , no se necesita el SRID específico de la instancia espacial para realizar cálculos; por tanto, las instancias pueden encontrarse en un espacio plano indefinido. Para indicar el espacio plano indefinido en los cálculos de métodos de tipo de datos **geometry** , el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa SRID 0.  
  
##  <a name="examples"></a><a name="examples"></a> Ejemplos  
En los dos ejemplos siguientes se muestra cómo agregar y consultar datos de geometry.  
  
### <a name="example-a"></a>Ejemplo A.
En este ejemplo se crea una tabla con una columna de identidad y una columna de tipo `geometry`, `GeomCol1`. Una tercera columna representa la columna de tipo `geometry` en su representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) y utiliza el método `STAsText()` . A continuación se insertan dos filas: una que contiene una instancia de `LineString` de `geometry`y otra que contiene una instancia de `Polygon` .  
  
```sql  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
DROP TABLE dbo.SpatialTable;  
GO  

CREATE TABLE SpatialTable   
  ( id int IDENTITY (1,1),  
    GeomCol1 geometry,   
    GeomCol2 AS GeomCol1.STAsText() 
  );  
GO  

INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  

INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
GO  
```  
  
### <a name="example-b"></a>Ejemplo B.
En este ejemplo se usa el método `STIntersection()` para devolver los puntos de intersección de las dos instancias de `geometry` insertadas previamente.  
  
```sql  
DECLARE @geom1 geometry;  
DECLARE @geom2 geometry;  
DECLARE @result geometry;  

SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geom1.STIntersection(@geom2);  
SELECT @result.STAsText();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
