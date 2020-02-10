---
title: Creación, construcción y consulta de instancias de Geography | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server]
- geodetic data type [SQL Server]
- geography data type [SQL Server], about geography data type
ms.assetid: b585851e-d15b-411f-adeb-aeabeb777c0b
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 5dde7575a3f657b89d29fefa0da52002bcd6af28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014296"
---
# <a name="create-construct-and-query-geography-instances"></a>Crear, construir y consultar instancias de Geography
  El tipo de datos espacial geography, `geography`, representa los datos en un sistema de coordenadas de tierra redonda. Se implementa como un tipo de datos de .NET CLR (Common Language Runtime) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `geography` almacena los datos elipsoidales (globo), como coordenadas de latitud y longitud de GPS.  
  
 El tipo `geography` está predefinido y está disponible en cada base de datos. Puede crear columnas de tabla de tipo `geography` y operar con los datos `geography` de la misma manera que con los demás tipos proporcionados por el sistema.  
  
##  <a name="creating"></a>Crear o construir una nueva instancia de Geography  
  
###  <a name="existing"></a>Crear una nueva instancia de Geography a partir de una instancia existente  
 El tipo de datos `geography` proporciona numerosos métodos integrados que puede usar para crear nuevas instancias de `geography` basadas en instancias existentes.  
  
 **Para crear un búfer alrededor de una geografía**  
 [STBuffer &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stbuffer-geography-data-type)  
  
 **Para crear un búfer alrededor de una geografía, permitiendo una tolerancia**  
 [BufferWithTolerance &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/bufferwithtolerance-geography-data-type)  
  
 **Para crear una geografía a partir de la intersección de dos instancias de geografía**  
 [STIntersection &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Para crear una geografía a partir de la Unión de dos instancias de geografía**  
 [STUnion &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stunion-geography-data-type)  
  
 **Para crear una geografía a partir de los puntos en los que una geografía no se superpone a otra**  
 [STDifference &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
###  <a name="wkt"></a>Construir una instancia de Geography a partir de datos Well-Known Text  
 El tipo de datos `geography` proporciona varios métodos integrados que generan un objeto geography a partir de la representación WKT de Open Geospatial Consortium (OGC). La norma WKT consiste en una cadena de texto que permite intercambiar datos de geography de forma textual.  
  
 **Para construir cualquier tipo de instancia de Geography a partir de datos WKT**  
 [STGeomFromText &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)  
  
 [Analizar &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/parse-geography-data-type)  
  
 **Para construir una instancia de tipo Geography a partir de datos WKT**  
 [STPointFromText &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stpointfromtext-geography-data-type)  
  
 **Para construir una instancia de Multipoint de geografía a partir de datos WKT**  
 [STMPointFromText &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stmpointfromtext-geography-data-type)  
  
 **Para construir una instancia de Geography de LineString a partir de datos WKT**  
 STLineFromText (tipo de datos geography)  
  
 **Para construir una instancia de Geography de MultiLineString a partir de datos WKT**  
 [STMLineFromText &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stmlinefromtext-geography-data-type)  
  
 **Para construir una instancia de tipo Polygon de geografía a partir de datos WKT**  
 [STPolyFromText &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stpolyfromtext-geography-data-type)  
  
 **Para construir una instancia de Geography a partir de datos WKT**  
 [STMPolyFromText &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stmpolyfromtext-geography-data-type)  
  
 **Para construir una instancia de Geography de GeometryCollection a partir de datos WKT**  
 [STGeomCollFromText &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stgeomcollfromtext-geography-data-type)  
  
###  <a name="wkb"></a>Construir una instancia de Geography a partir de datos Well-Known Binary  
 WKB es un formato binario especificado por OGC que permite intercambiar datos de tipo `Geography` entre una aplicación cliente y una base de datos SQL. Las funciones siguientes aceptan datos WKB para construir las instancias de geography:  
  
 **Para construir cualquier tipo de instancia de Geography a partir de datos WKB**  
 [STGeomFromWKB &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stgeomfromwkb-geography-data-type)  
  
 **Para construir una instancia de tipo Geography a partir de datos WKB**  
 [STPointFromWKB &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stpointfromwkb-geography-data-type)  
  
 **Para construir una instancia de Multipoint de geografía a partir de datos WKB**  
 [STMPointFromWKB &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stmpointfromwkb-geography-data-type)  
  
 **Para construir una instancia de Geography de LineString a partir de datos WKB**  
 [STLineFromWKB &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stlinefromwkb-geography-data-type)  
  
 **Para construir una instancia de Geography de MultiLineString a partir de datos WKB**  
 [STMLineFromWKB &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stmlinefromwkb-geography-data-type)  
  
 **Para construir una instancia de tipo Polygon de geografía a partir de datos WKB**  
 [STPolyFromWKB &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stpolyfromwkb-geography-data-type)  
  
 **Para construir una instancia de Geography a partir de datos WKB**  
 [STMPolyFromWKB &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stmpolyfromwkb-geography-data-type)  
  
 **Para construir una instancia de Geography de GeometryCollection a partir de datos WKB**  
 [STGeomCollFromWKB &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeomcollfromwkb-geography-data-type) STGeomCollFromWKB (tipo de datos Geography)  
  
###  <a name="gml"></a>Construir una instancia de Geography a partir de entrada de texto GML  
 El `geography` tipo de datos proporciona un método que genera `geography` una instancia de GML, una representación XML de `geography` una instancia de. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite un subconjunto de GML.  
  
 Para obtener más información sobre el lenguaje de marcado de geografía, vea las especificaciones de OGC: [OGC Specifications, Geography Markup Language.](https://go.microsoft.com/fwlink/?LinkId=93629)  
  
 **Para construir cualquier tipo de instancia de Geography a partir de datos GML**  
 [GeomFromGML &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/geomfromgml-geography-data-type)  
  
##  <a name="returning"></a>Devolver texto conocido y binario conocido de una instancia de Geography  
 Puede usar los métodos siguientes para devolver el formato WKT o WKB de una instancia de `geography`:  
  
 **Para devolver la representación WKT de una instancia de Geography**  
 [STAsText &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stastext-geography-data-type)  
  
 [ToString &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/tostring-geography-data-type)  
  
 **Para devolver la representación WKT de una instancia de Geography, incluidos los valores Z y M**  
 [AsTextZM &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/astextzm-geography-data-type)  
  
 **Para devolver la representación WKB de una instancia de Geography**  
 [STAsBinary &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stasbinary-geography-data-type)  
  
 **Para devolver una representación GML de una instancia de Geography**  
 [AsGml &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/asgml-geography-data-type)  
  
##  <a name="query"></a>Consultar las propiedades y los comportamientos de las instancias de Geography  
 Todas `geography` las instancias de tienen varias propiedades que se pueden recuperar a través de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los métodos que proporciona. Los temas siguientes definen las propiedades y los comportamientos de los tipos geography y los métodos para consultar cada uno.  
  
###  <a name="valid"></a>Validez, tipo de instancia e información de GeometryCollection  
 Una vez construida una instancia de `geography`, puede usar los métodos siguientes para devolver el tipo de instancia o, si es una instancia de `GeometryCollection`, devolver una instancia de `geography` específica.  
  
 **Para devolver el tipo de instancia de una geografía**  
 [STGeometryType &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeometrytype-geography-data-type)  
  
 **Para determinar si una geografía es un tipo de instancia determinado**  
 [Instancia de &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/instanceof-geography-data-type)  
  
 **Para determinar si una instancia de Geography tiene el formato correcto para su tipo de instancia**  
 [STNumGeometries &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stnumgeometries-geography-data-type)  
  
 **Para devolver una geografía específica en una instancia de GeometryCollection**  
 [STGeometryN &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeometryn-geography-data-type) STGeometryN (tipo de datos Geography)  
  
###  <a name="number"></a>Número de puntos  
 Todas las instancias `geography` no vacías se componen de *puntos*. Estos puntos representan las coordenadas de latitud y longitud de la tierra en la que se dibujan las instancias de `geography`. El tipo `geography` de datos proporciona numerosos métodos integrados para consultar los puntos de una instancia.  
  
 **Para devolver el número de puntos que componen una instancia**  
 [STNumPoints &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stnumpoints-geography-data-type)  
  
 **Devolver un punto concreto en una instancia**  
 [STPointN &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **Para devolver el punto inicial de una instancia**  
 [STStartPoint &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/ststartpoint-geography-data-type)  
  
 **Para devolver el punto final de una instancia**  
 [STEndpoint &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stendpoint-geography-data-type)  
  
###  <a name="dimension"></a>Galería  
 Una instancia de `geography` no vacía puede ser no dimensional, unidimensional o bidimensional. Las instancias de `geography` no dimensionales, `Point` como `MultiPoint`y, no tienen ninguna longitud ni área. Los objetos unidimensionales, como `LineString, CircularString`, `CompoundCurve` y `MultiLineString`, tienen longitud. Las instancias bidimensionales, como `Polygon, CurvePolygon` y `MultiPolygon`, tienen área y longitud. Las instancias vacías informan de una dimensión de -1 y `GeometryCollection` informa de la dimensión máxima de su contenido.  
  
 **Para devolver la dimensión de una instancia**  
 [STDimension &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stdimension-geography-data-type)  
  
 **Para devolver la longitud de una instancia**  
 [STLength &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stlength-geography-data-type)  
  
 **Para devolver el área de una instancia**  
 [STArea &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/starea-geography-data-type)  
  
###  <a name="empty"></a>Vacía  
 Una instancia *vacía* `geography` no tiene ningún punto. La longitud de las instancias de `LineString, CircularString`, `CompoundCurve` y `MultiLineString` vacías es 0. El área de las instancias de `Polygon, CurvePolygon` y `MultiPolygon` vacías es 0.  
  
 **Para determinar si una instancia está vacía**  
 [STIsEmpty &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stisempty-geography-data-type)  
  
###  <a name="closure"></a>Incidencia  
 Una instancia *cerrada* `geography` es una figura cuyos puntos de inicio y de finalización son los mismos. Las instancias `Polygon` se consideran cerradas. Las instancias `Point` no son cerradas.  
  
 Un anillo es una instancia de `LineString` simple y cerrada.  
  
 **Para determinar si una instancia está cerrada**  
 [STIsClosed &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stisclosed-geography-data-type)  
  
 **Para devolver el número de anillos en una instancia de Polygon**  
 [NumRings &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/numrings-geography-data-type)  
  
 **Para devolver un anillo especificado de una instancia de Geography**  
 [&#41;de datos de tipo Geography &#40;ring](/sql/t-sql/spatial-geography/ringn-geography-data-type)  
  
###  <a name="srid"></a>IDENTIFICADOR de referencia espacial (SRID)  
 El identificador de referencia espacial (SRID) es un identificador que especifica en qué sistema de coordenadas elíptico está representada la instancia `geography`. No se pueden comparar dos instancias `geography` con SRID diferentes.  
  
 **Para establecer o devolver el SRID de una instancia**  
 [STSrid &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stsrid-geography-data-type)  
  
 Esta propiedad se puede modificar.  
  
##  <a name="rel"></a>Determinar las relaciones entre instancias de Geography  
 El tipo de datos `geography` proporciona muchos métodos integrados que puede usar para determinar las relaciones entre dos instancias de `geography`.  
  
 **Para determinar si dos instancias comprenden el mismo conjunto de puntos**  
 [STEquals &#40;tipo de datos Geometry&#41;](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **Para determinar si dos instancias de son disjuntas**  
 [STDisjoint &#40;tipo de datos Geometry&#41;](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **Para determinar si dos instancias de forman una intersección**  
 [STIntersects &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **Para determinar los puntos en los que dos instancias se cruzan**  
 [STIntersection &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Determinar la distancia más corta entre los puntos de dos instancias de geografía**  
 [STDistance &#40;tipo de datos Geometry&#41;](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
 **Determinar la diferencia en puntos entre dos instancias geográficas**  
 [STDifference &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
 **Para obtener la diferencia simétrica, o puntos únicos, de una instancia de Geography comparada con otra instancia**  
 [STSymDifference &#40;tipo de datos Geography&#41;](/sql/t-sql/spatial-geography/stsymdifference-geography-data-type)  
  
##  <a name="supportedsrid"></a>Las instancias de Geography deben usar SRID compatibles  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite SRID basados en las normas de EPSG. Se debe usar un SID compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instancias de `geography` cuando se realicen cálculos o se usen los métodos con datos espaciales de geografía. El SRID debe coincidir con uno de los SRID mostrados en la vista de catálogo **sys.spatial_reference_systems** . Como se mencionó anteriormente, al realizar cálculos en sus datos espaciales usando el tipo de datos `geography`, sus resultados dependerán de qué elipsoide se usó en la creación de sus datos, ya que cada elipsoide está asignado a un identificador de referencia espacial concreto (SRID).  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa el SRID predeterminado de 4326, que se asigna al sistema de referencia espacial WGS 84, al usar métodos en instancias de `geography`. Si usa datos de un sistema de referencia espacial distinto de WGS 84 (o SRID 4326), tendrá que determinar el SRID concreto para sus datos espaciales de geography.  
  
##  <a name="examples"></a>Example  
 En los ejemplos siguientes se muestra cómo agregar y consultar datos geography.  
  
-   En el primer ejemplo se crea una tabla con una columna de identidad y una columna de tipo `geography` , `GeogCol1`. Una tercera columna representa la columna de tipo `geography` en su representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) y utiliza el método `STAsText()` . A continuación se insertan dos filas: una que contiene una instancia de `LineString` de `geography`y otra que contiene una instancia de `Polygon` .  
  
    ```  
    IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
        DROP TABLE dbo.SpatialTable;  
    GO  
  
    CREATE TABLE SpatialTable   
        ( id int IDENTITY (1,1),  
        GeogCol1 geography,   
        GeogCol2 AS GeogCol1.STAsText() );  
    GO  
  
    INSERT INTO SpatialTable (GeogCol1)  
    VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326));  
  
    INSERT INTO SpatialTable (GeogCol1)  
    VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
    GO  
    ```  
  
-   En el segundo ejemplo se usa el método `STIntersection()` para devolver los puntos de intersección de las dos instancias de `geography` insertadas previamente.  
  
    ```  
    DECLARE @geog1 geography;  
    DECLARE @geog2 geography;  
    DECLARE @result geography;  
  
    SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geog1.STIntersection(@geog2);  
    SELECT @result.STAsText();  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Datos espaciales &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
