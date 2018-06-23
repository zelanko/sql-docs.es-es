---
title: Creación, construcción y consulta de instancias de Geography | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- geography data type [SQL Server]
- geodetic data type [SQL Server]
- geography data type [SQL Server], about geography data type
ms.assetid: b585851e-d15b-411f-adeb-aeabeb777c0b
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ec18679f1d466917e99f249c75c6ebf3bc42ff8c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198417"
---
# <a name="create-construct-and-query-geography-instances"></a>Crear, construir y consultar instancias de Geography
  El tipo de datos espacial geography, `geography`, representa los datos en un sistema de coordenadas de tierra redonda. Se implementa como un tipo de datos de .NET CLR (Common Language Runtime) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `geography` tipo de datos almacena datos elípticos (tierra redonda), como coordenadas de latitud y longitud GPS.  
  
 El `geography` es de tipo predefinido y está disponible en cada base de datos. Puede crear columnas de tabla de tipo `geography` y operar con los datos `geography` de la misma manera que con los demás tipos proporcionados por el sistema.  
  
##  <a name="creating"></a> Crear o construir una instancia de geography  
  
###  <a name="existing"></a> Crear una instancia de geography a partir de una instancia existente  
 El `geography` tipo de datos proporciona numerosos métodos integrados que puede usar para crear nuevas `geography` instancias basan en instancias existentes.  
  
 **Crear un búfer alrededor de un objeto geography**  
 [STBuffer &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stbuffer-geography-data-type)  
  
 **Para crear un búfer alrededor de un objeto geography, permitiendo una tolerancia**  
 [BufferWithTolerance &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/bufferwithtolerance-geography-data-type)  
  
 **Crear una geografía a partir de la intersección de dos instancias de geografía**  
 [STIntersection &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Crear una geografía a partir de la unión de dos instancias de geografía**  
 [STUnion &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stunion-geography-data-type)  
  
 **Para crear un objeto geography a partir de los puntos en los que un objeto geography no se superpone a otro**  
 [STDifference &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
###  <a name="wkt"></a> Construir una instancia de geography a partir de datos Well-Known Text  
 El `geography` tipo de datos proporciona varios métodos integrados que generan una objeto geography a partir de la representación WKT de Open Geospatial Consortium (OGC). La norma WKT consiste en una cadena de texto que permite intercambiar datos de geography de forma textual.  
  
 **Para construir cualquier tipo de instancia de geography a partir de datos WKT**  
 [STGeomFromText &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)  
  
 [Parse &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/parse-geography-data-type)  
  
 **Para construir una instancia de geography de tipo Point a partir de datos WKT**  
 [STPointFromText &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stpointfromtext-geography-data-type)  
  
 **Para construir una instancia de geography de tipo MultiPoint a partir de datos WKT**  
 [STMPointFromText &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stmpointfromtext-geography-data-type)  
  
 **Para construir una instancia de geography de tipo LineString a partir de datos WKT**  
 STLineFromText (tipo de datos geography)  
  
 **Para construir una instancia de geography de tipo MultiLineString a partir de datos WKT**  
 [STMLineFromText &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stmlinefromtext-geography-data-type)  
  
 **Para construir una instancia de geography de tipo Polygon a partir de datos WKT**  
 [STPolyFromText &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stpolyfromtext-geography-data-type)  
  
 **Para construir una instancia de geography de tipo MultiPolygon a partir de datos WKT**  
 [STMPolyFromText &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stmpolyfromtext-geography-data-type)  
  
 **Para construir una instancia de geography de tipo GeometryCollection a partir de datos WKT**  
 [STGeomCollFromText &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeomcollfromtext-geography-data-type)  
  
###  <a name="wkb"></a> Construir una instancia de geography a partir de datos Well-Known Binary  
 WKB es un formato binario especificado por OGC que permite `Geography` datos que se intercambie entre una aplicación cliente y una base de datos SQL. Las funciones siguientes aceptan datos WKB para construir las instancias de geography:  
  
 **Para construir cualquier tipo de instancia de geography a partir de datos WKB**  
 [STGeomFromWKB &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeomfromwkb-geography-data-type)  
  
 **Para construir una instancia de geography de tipo Point a partir de datos WKB**  
 [STPointFromWKB &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stpointfromwkb-geography-data-type)  
  
 **Para construir una instancia de geography de tipo MultiPoint a partir de datos WKB**  
 [STMPointFromWKB &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stmpointfromwkb-geography-data-type)  
  
 **Para construir una instancia de geography de tipo LineString a partir de datos WKB**  
 [STLineFromWKB &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stlinefromwkb-geography-data-type)  
  
 **Para construir una instancia de geography de tipo MultiLineString a partir de datos WKB**  
 [STMLineFromWKB &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stmlinefromwkb-geography-data-type)  
  
 **Para construir una instancia de geography de tipo Polygon a partir de datos WKB**  
 [STPolyFromWKB &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stpolyfromwkb-geography-data-type)  
  
 **Para construir una instancia de geography de tipo MultiPolygon a partir de datos WKB**  
 [STMPolyFromWKB &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stmpolyfromwkb-geography-data-type)  
  
 **Para construir una instancia de geography de tipo GeometryCollection a partir de datos WKB**  
 [STGeomCollFromWKB &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeomcollfromwkb-geography-data-type)STGeomCollFromWKB (tipo de datos geography)  
  
###  <a name="gml"></a> Para construir una instancia de geography a partir de datos de texto GML  
 El `geography` tipo de datos proporciona un método que genera un `geography` instancia a partir de GML, una representación XML de un `geography` instancia. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite un subconjunto de GML.  
  
 Para obtener más información sobre el lenguaje de marcado de geografía, vea las especificaciones de OGC: [OGC Specifications, Geography Markup Language.](http://go.microsoft.com/fwlink/?LinkId=93629)  
  
 **Para construir cualquier tipo de instancia de geography a partir de datos de GML**  
 [GeomFromGML &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/geomfromgml-geography-data-type)  
  
##  <a name="returning"></a> Devolver Well-Known Text y Well-Known Binary a partir una instancia de geography  
 Puede usar los métodos siguientes para devolver en el formato WKT o WKB de una `geography` instancia:  
  
 **Para devolver la representación WKT de una instancia de geography**  
 [STAsText &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stastext-geography-data-type)  
  
 [ToString &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/tostring-geography-data-type)  
  
 **Para devolver la representación WKT de una instancia de geography, incluidos cualesquiera valores Z y M.**  
 [AsTextZM &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/astextzm-geography-data-type)  
  
 **Para devolver la representación WKB de una instancia de geography**  
 [STAsBinary &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stasbinary-geography-data-type)  
  
 **Para devolver la representación GML de una instancia de geography**  
 [AsGml &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/asgml-geography-data-type)  
  
##  <a name="query"></a> Consultar propiedades y comportamientos de instancias de geography  
 Todos los `geography` instancias tienen un número de propiedades que se pueden recuperar a través de métodos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona. Los temas siguientes definen las propiedades y los comportamientos de los tipos geography y los métodos para consultar cada uno.  
  
###  <a name="valid"></a> Validez, tipo de instancia e información de GeometryCollection  
 Después de un `geography` se construye la instancia, puede usar los métodos siguientes para devolver el tipo de instancia, o si es un `GeometryCollection` de la instancia, devolver un determinado `geography` instancia.  
  
 **Para devolver el tipo de instancia de una geografía**  
 [STGeometryType &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeometrytype-geography-data-type)  
  
 **Para determinar si una geografía es un tipo de instancia determinado**  
 [InstanceOf &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/instanceof-geography-data-type)  
  
 **Para determinar si el formato de una instancia de geografía es correcto de acuerdo con su tipo de instancia**  
 [STNumGeometries &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stnumgeometries-geography-data-type)  
  
 **Para devolver un objeto geography específico de una instancia de GeometryCollection**  
 [STGeometryN &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stgeometryn-geography-data-type)STGeometryN (tipo de datos geography)  
  
###  <a name="number"></a> Número de puntos  
 Vacía todos los `geography` instancias están formadas por *puntos*. Estos puntos representan las coordenadas de latitud y longitud de la tierra en la que se dibujan las instancias de `geography`. El tipo de datos `geography` proporciona numerosos métodos integrados para consultar los puntos de una instancia.  
  
 **Devolver el número de puntos que comprende una instancia**  
 [STNumPoints &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stnumpoints-geography-data-type)  
  
 **Devolver un punto concreto en una instancia**  
 [STPointN &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **Devolver el punto inicial de una instancia**  
 [STStartPoint &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/ststartpoint-geography-data-type)  
  
 **Devolver el punto final de una instancia**  
 [STEndpoint &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stendpoint-geography-data-type)  
  
###  <a name="dimension"></a> Dimensión  
 Un nonempty `geography` instancia puede ser 0, 1-, o 2 dimensional. Dimensionales `geography` instancias, como `Point` y `MultiPoint`, no tienen ninguna longitud ni área. Los objetos unidimensionales, como `LineString, CircularString`, `CompoundCurve` y `MultiLineString`, tienen longitud. Instancias bidimensionales, como `Polygon, CurvePolygon`, y `MultiPolygon`, tienen área y longitud. Las instancias vacías informan de una dimensión de -1 y `GeometryCollection` informa de la dimensión máxima de su contenido.  
  
 **Devolver la dimensión de una instancia**  
 [STDimension &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stdimension-geography-data-type)  
  
 **Devolver la longitud de una instancia**  
 [STLength &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stlength-geography-data-type)  
  
 **Devolver el área de una instancia**  
 [STArea &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/starea-geography-data-type)  
  
###  <a name="empty"></a> Vacía  
 Un *vacía* `geography` instancia no tiene ningún punto. La longitud de las instancias de `LineString, CircularString`, `CompoundCurve` y `MultiLineString` vacías es 0. El área de vacío `Polygon, CurvePolygon` y `MultiPolygon` instancias es 0.  
  
 **Para determinar si una instancia está vacía**  
 [STIsEmpty &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stisempty-geography-data-type)  
  
###  <a name="closure"></a> Clausura  
 A *cerrado* `geography` instancia es una figura cuyos puntos de inicio y final son los mismos. `Polygon` instancias se consideran cerradas. Las instancias `Point` no son cerradas.  
  
 Un anillo es una sencilla y cerrada `LineString` instancia.  
  
 **Para determinar si una instancia está cerrada**  
 [STIsClosed &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stisclosed-geography-data-type)  
  
 **Para devolver el número de anillos en una instancia de Polygon**  
 [NumRings &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/numrings-geography-data-type)  
  
 **Para devolver un anillo especificado de una instancia de Geography**  
 [RingN &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/ringn-geography-data-type)  
  
###  <a name="srid"></a> Identificador de referencia espacial (SRID)  
 La referencia espacial (SRID) de Id. es un identificador que especifica qué sistema de coordenadas elíptico el `geography` instancia se representa en. No se pueden comparar dos instancias `geography` con SRID diferentes.  
  
 **Para establecer o devolver el SRID de una instancia**  
 [STSrid &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stsrid-geography-data-type)  
  
 Esta propiedad se puede modificar.  
  
##  <a name="rel"></a> Determinar las relaciones entre instancias de geography  
 El `geography` tipo de datos proporciona muchos métodos integrados que puede usar para determinar las relaciones entre dos `geography` instancias.  
  
 **Para determinar si dos instancias comprenden el mismo conjunto de puntos**  
 [STEquals &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **Para determinar si dos instancias no son contiguas**  
 [STDisjoint &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **Para determinar si dos instancias contienen puntos que forman una intersección**  
 [STIntersects &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **Determinar los puntos en los que dos instancias tienen la intersección**  
 [STIntersection &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Determinar la distancia más corta entre los puntos de dos instancias geográficas**  
 [STDistance &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
 **Determinar la diferencia en puntos entre dos instancias geográficas**  
 [STDifference &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
 **Para obtener la diferencia simétrica, o puntos únicos, de una instancia de geography comparada con otra instancia**  
 [STSymDifference &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stsymdifference-geography-data-type)  
  
##  <a name="supportedsrid"></a> Las instancias de geography deben usar SRID compatibles  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite SRID basados en las normas de EPSG. Se debe usar un SID compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instancias de `geography` cuando se realicen cálculos o se usen los métodos con datos espaciales de geografía. El SRID debe coincidir con uno de los SRID mostrados en la vista de catálogo **sys.spatial_reference_systems** . Como se mencionó anteriormente, al realizar cálculos en sus datos espaciales usando el `geography` tipo de datos, los resultados dependerán de qué elipsoide se usó en la creación de los datos, ya que cada elipsoide está asignado un identificador de referencia espacial concreto () SRID).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa el SRID predeterminado de 4326, que se asigna al sistema de referencia espacial WGS 84, al usar métodos en instancias de `geography`. Si usa datos de un sistema de referencia espacial distinto de WGS 84 (o SRID 4326), tendrá que determinar el SRID concreto para sus datos espaciales de geography.  
  
##  <a name="examples"></a> Ejemplos  
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
  
## <a name="see-also"></a>Vea también  
 [Datos espaciales &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
