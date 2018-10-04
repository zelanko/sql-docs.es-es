---
title: Polygon | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- dbe-spatial
ms.topic: conceptual
helpviewer_keywords:
- geometry subtypes [SQL Server]
- Polygon geometry subtype [SQL Server]
ms.assetid: b6a21c3c-fdb8-4187-8229-1c488454fdfb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a78f615493ad531b8607abb0764891ffcb2805f3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194485"
---
# <a name="polygon"></a>Polygon
  Un `Polygon` es una superficie bidimensional almacenada como una secuencia de puntos que definen un anillo delimitador exterior y cero o más anillos interiores.  
  
## <a name="polygon-instances"></a>Instancias de Polygon  
 Un `Polygon` instancia puede formarse a partir de un anillo que tenga al menos tres puntos distintos. Un `Polygon` instancia también puede estar vacía.  
  
 El anillo exterior junto con los anillos interiores de un `Polygon` definir su límite. El espacio encerrado dentro de los anillos define el interior de la instancia de `Polygon`.  
  
 La ilustración siguiente muestra ejemplos de `Polygon` instancias.  
  
 ![Ejemplos de instancias Polygon de geometry](../../database-engine/media/polygon.gif "Ejemplos de instancias Polygon de geometry")  
  
 Como se muestra en la ilustración:  
  
1.  Figura 1 es un `Polygon` instancia cuyo límite está definido por un anillo exterior.  
  
2.  La figura 2 es una instancia de `Polygon` cuyo límite está definido mediante un anillo exterior y dos anillos interiores. El área situada dentro de los anillos interiores forma parte del exterior de la instancia de `Polygon`.  
  
3.  La figura 3 es una instancia de `Polygon` válida porque la intersección de sus anillos interiores se realiza en un solo punto tangente.  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Las instancias aceptadas de `Polygon` son las instancias que pueden almacenarse en una variable de tipo `geometry` o `geography` sin generar una excepción. Se aceptan las siguientes `Polygon` instancias:  
  
-   Un valor vacío `Polygon` instancia  
  
-   Una instancia de `Polygon` que tiene un anillo exterior aceptable y cero o más anillos interiores aceptables.  
  
 Deben cumplirse necesariamente los criterios siguientes para que un anillo sea aceptable.  
  
-   El `LineString` instancia debe ser aceptada.  
  
-   La instancia de `LineString` debe tener al menos cuatro puntos.  
  
-   Los puntos inicial y final de la instancia de `LineString` deben ser el mismo.  
  
 El ejemplo siguiente se muestra aceptado `Polygon` instancias.  
  
```  
DECLARE @g1 geometry = 'POLYGON EMPTY';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 1))';  
DECLARE @g3 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 3 3, 0 3, 0 0))';  
DECLARE @g4 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(3 0, 6 0, 6 3, 3 3, 3 0))';  
DECLARE @g5 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
```  
  
 Como muestran `@g4` y `@g5`, una instancia aceptada de `Polygon` puede no ser una instancia de `Polygon` válida. `@g5` también muestra que una instancia de Polygon solo necesita contener un anillo con cuatro puntos cualquiera para que se acepte.  
  
 Los ejemplos siguientes generan una excepción `System.FormatException`, porque las instancias de `Polygon` no se aceptan.  
  
```  
DECLARE @g1 geometry = 'POLYGON((1 1, 3 3, 1 1))';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 5))';  
```  
  
 `@g1` no se acepta porque la instancia de `LineString` para el anillo exterior no contiene suficientes puntos. `@g2` no se acepta porque el punto inicial de la instancia de `LineString` del anillo exterior no es igual que el punto final. En el ejemplo siguiente hay un anillo exterior aceptable, pero el anillo interior no lo es. También en este caso se genera una excepción `System.FormatException`.  
  
```  
DECLARE @g geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 0 0))';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
 Los anillos interiores de un `Polygon` pueden tocarse a sí mismos y unos con otros en tangentes únicos puntos, pero si los anillos interiores de un `Polygon` cross, la instancia no es válida.  
  
 El ejemplo siguiente se muestra válido `Polygon` instancias.  
  
```  
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, -5 -10, -10 0))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g3` es válido porque los dos anillos interiores se tocan en un mismo punto y no se cruzan. El siguiente ejemplo muestra instancias de `Polygon` no válidas.  
  
```  
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (20 0, 0 10, 0 -20, 20 0))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (5 0, 1 5, 1 -5, 5 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, 0 -10, -10 0))';  
DECLARE @g4 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 1 5, 0 -10, -10 0))';  
DECLARE @g5 geometry = 'POLYGON((10 0, 0 10, 0 -10, 10 0), (-20 -20, -20 20, 20 20, 20 -20, -20 -20) )';  
DECLARE @g6 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid(), @g5.STIsValid(), @g6.STIsValid();  
```  
  
 `@g1` no es válido porque el anillo interior toca el anillo exterior en dos lugares. `@g2` no es válido porque el segundo anillo interior está dentro del interior del primer anillo interior. `@g3` no es válido porque el los dos anillos interiores se tocan en varios puntos consecutivos. `@g4` no es válido porque los interiores de los dos anillos interiores se superponen. `@g5` no es válido porque el anillo exterior no es el primer anillo. `@g6` no es válido porque el anillo no tiene al menos tres puntos distintos.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente crea una instancia sencilla de `geometry``Polygon` con un hueco y un SRID de 10.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STPolyFromText('POLYGON((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1))', 10);  
```  
  
 Es posible especificar una instancia no válida y convertirla en una instancia de `geometry` válida. En el ejemplo siguiente de `Polygon`, se superponen los anillos interiores y el exterior, y la instancia no es válida.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((1 0, 0 1, 1 2, 2 1, 1 0), (2 0, 1 1, 2 2, 3 1, 2 0))');  
```  
  
 En el ejemplo siguiente, la instancia no válida se hace válida con `MakeValid()`.  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.ToString();  
```  
  
 La instancia de `geometry` devuelta por el ejemplo anterior es de tipo `MultiPolygon`.  
  
```  
MULTIPOLYGON (((2 0, 3 1, 2 2, 1.5 1.5, 2 1, 1.5 0.5, 2 0)), ((1 0, 1.5 0.5, 1 1, 1.5 1.5, 1 2, 0 1, 1 0)))  
```  
  
 A continuación se muestra otro ejemplo de convertir una instancia no válida a una instancia de geometry válida. En el siguiente ejemplo la instancia de `Polygon` se ha creado con tres puntos que son exactamente iguales:  
  
```tsql  
DECLARE @g geometry  
SET @g = geometry::Parse('POLYGON((1 3, 1 3, 1 3, 1 3))');  
SET @g = @g.MakeValid();  
SELECT @g.ToString()  
```  
  
 La instancia de geometry devuelta es `Point(1 3)`.  Si el objeto `Polygon` proporcionado es `POLYGON((1 3, 1 5, 1 3, 1 3))` , entonces `MakeValid()` devolverá `LINESTRING(1 3, 1 5)`.  
  
## <a name="see-also"></a>Vea también  
 [STArea &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type)   
 [STExteriorRing &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type)   
 [STNumInteriorRing &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type)   
 [STInteriorRingN &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type)   
 [STCentroid &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)   
 [STPointOnSurface &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [MultiPolígono](../spatial/polygon.md)   
 [Datos espaciales &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)   
 [STIsValid &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stisvalid-geography-data-type)   
 [STIsValid &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)  
  
  
