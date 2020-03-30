---
title: Polygon | Microsoft Docs
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry subtypes [SQL Server]
- Polygon geometry subtype [SQL Server]
ms.assetid: b6a21c3c-fdb8-4187-8229-1c488454fdfb
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bd7b379df56f94710a22684c9cc8d662cfb0a396
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "72907209"
---
# <a name="polygon"></a>Polygon

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Un **Polygon** es una superficie bidimensional almacenada como una secuencia de puntos que definen un anillo delimitador exterior y cero o más anillos interiores.  
  
## <a name="polygon-instances"></a>Instancias de Polygon  
 Una instancia de **Polygon** se puede formar a partir de un anillo que tenga al menos tres puntos distintos. Una instancia de **Polygon** también puede estar vacía.  
  
Los límites de una instancia de **Polygon** los define su anillo exterior junto con los anillos interiores que tenga. El espacio encerrado dentro de los anillos define el interior de la instancia de **Polygon**.  
  
En la ilustración siguiente se muestran ejemplos de instancias de **Polygon** .  
  
 ![Ejemplos de instancias Polygon de geometry](../../relational-databases/spatial/media/polygon.gif "Ejemplos de instancias Polygon de geometry")  
  
Como se muestra en la ilustración:  
  
1.  La figura 1 es una instancia de **Polygon** cuyo límite está definido mediante un anillo exterior.  
  
2.  La figura 2 es una instancia de **Polygon** cuyo límite está definido mediante un anillo exterior y dos anillos interiores. El área situada dentro de los anillos interiores forma parte del exterior de la instancia de **Polygon** .  
  
3.  La figura 3 es una instancia de **Polygon** válida porque la intersección de sus anillos interiores se realiza en un solo punto tangente.  

### <a name="accepted-instances"></a>Instancias aceptadas  
 Las instancias aceptadas de **Polygon** son las instancias que pueden almacenarse en una variable de tipo **geometry** o **geography** sin generar una excepción. Se aceptan las siguientes instancias de **Polygon** :  
  
-   Una instancia vacía de **Polygon** .  
-   Una instancia de **Polygon** que tiene un anillo exterior aceptable ring (**LineString**) y cero o más anillos interiores aceptables (**LineString**s).  
  
Deben cumplirse necesariamente los criterios siguientes para que un anillo (**LineString**) sea aceptable.  
  
-   La instancia de **LineString** debe ser aceptada.  
-   La instancia de **LineString** debe tener al menos cuatro puntos.  
-   Los puntos inicial y final de la instancia de **LineString** deben ser el mismo.  
  
El siguiente ejemplo muestra instancias aceptadas de **Polygon** .  
  
```sql  
DECLARE @g1 geometry = 'POLYGON EMPTY';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 1))';  
DECLARE @g3 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 3 3, 0 3, 0 0))';  
DECLARE @g4 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(3 0, 6 0, 6 3, 3 3, 3 0))';  
DECLARE @g5 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
```  
  
Como muestran `@g4` y `@g5` , una instancia aceptada de **Polygon** puede no ser una instancia de **Polygon** válida. `@g5` también muestra que una instancia de Polygon solo necesita contener un anillo con cuatro puntos cualquiera para que se acepte.  
  
Los ejemplos siguientes generan una excepción `System.FormatException` , porque las instancias de **Polygon** no se aceptan.  
  
```sql  
DECLARE @g1 geometry = 'POLYGON((1 1, 3 3, 1 1))';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 5))';  
```  
  
`@g1` no se acepta porque la instancia de **LineString** para el anillo exterior no contiene suficientes puntos. `@g2` no se acepta porque el punto inicial de la instancia de **LineString** del anillo exterior no es igual que el punto final. En el ejemplo siguiente hay un anillo exterior aceptable, pero el anillo interior no lo es. También en este caso se genera una excepción `System.FormatException`.  
  
```sql  
DECLARE @g geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 0 0))';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
 Los anillos interiores de una instancia de **Polygon** pueden tocarse a sí mismos y unos con otros en puntos tangentes únicos, pero si dichos anillos se cruzan, la instancia de **Polygon** no es válida.  
  
 En el siguiente ejemplo se muestran instancias válidas de **Polygon** .  
  
```sql  
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, -5 -10, -10 0))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g3` es válido porque los dos anillos interiores se tocan en un mismo punto y no se cruzan. El siguiente ejemplo muestra instancias de `Polygon` no válidas.  
  
```sql   
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (20 0, 0 10, 0 -20, 20 0))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (5 0, 1 5, 1 -5, 5 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, 0 -10, -10 0))';  
DECLARE @g4 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 1 5, 0 -10, -10 0))';  
DECLARE @g5 geometry = 'POLYGON((10 0, 0 10, 0 -10, 10 0), (-20 -20, -20 20, 20 20, 20 -20, -20 -20) )';  
DECLARE @g6 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid(), @g5.STIsValid(), @g6.STIsValid();  
```  
  
 `@g1` no es válido porque el anillo interior toca el anillo exterior en dos lugares. `@g2` no es válido porque el segundo anillo interior está dentro del interior del primer anillo interior. `@g3` no es válido porque los dos anillos interiores se tocan en varios puntos consecutivos. `@g4` no es válido porque los interiores de los dos anillos interiores se superponen. `@g5` no es válido porque el anillo exterior no es el primer anillo. `@g6` no es válido porque el anillo no tiene al menos tres puntos distintos.  
  
## <a name="examples"></a>Ejemplos  
### <a name="example-a"></a>Ejemplo A.  
En el siguiente ejemplo se crea una instancia sencilla de `geometry` `Polygon` con un hueco y un SRID de 10.
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STPolyFromText(
    'POLYGON((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1))',
    10);
```  
  

### <a name="example-b"></a>Ejemplo B.   
Una instancia que no es válida se puede especificar y convertir en una instancia de `geometry` válida. En el ejemplo siguiente de `Polygon`, se superponen los anillos interiores y el exterior, y la instancia no es válida.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse(
    'POLYGON((1 0, 0 1, 1 2, 2 1, 1 0), (2 0, 1 1, 2 2, 3 1, 2 0))'
    );  
```  
  
### <a name="example-c"></a>Ejemplo C.  
En el ejemplo siguiente, la instancia no válida se hace válida con `MakeValid()`.  
  
```sql  
SET @g = @g.MakeValid();  
SELECT @g.ToString();  
```  
  
La instancia de `geometry` devuelta por el ejemplo anterior es de tipo `MultiPolygon`.  
  
```sql  
MULTIPOLYGON (((2 0, 3 1, 2 2, 1.5 1.5, 2 1, 1.5 0.5, 2 0)),
              ((1 0, 1.5 0.5, 1 1, 1.5 1.5, 1 2, 0 1, 1 0)))
```  
  
### <a name="example-d"></a>Ejemplo D.  
Este es otro ejemplo de conversión de una instancia no válida en una instancia de geometría válida. En el siguiente ejemplo la instancia de `Polygon` se ha creado con tres puntos que son exactamente iguales:  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::Parse('POLYGON((1 3, 1 3, 1 3, 1 3))');  
SET @g = @g.MakeValid();  
SELECT @g.ToString()  
```  
  
La instancia de geometry devuelta es `Point(1 3)`.  Si el objeto `Polygon` proporcionado es `POLYGON((1 3, 1 5, 1 3, 1 3))` , entonces `MakeValid()` devolverá `LINESTRING(1 3, 1 5)`.  
  
## <a name="see-also"></a>Consulte también  
 [STArea &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/starea-geometry-data-type.md)   
 [STExteriorRing &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stexteriorring-geometry-data-type.md)   
 [STNumInteriorRing &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stnuminteriorring-geometry-data-type.md)   
 [STInteriorRingN &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stinteriorringn-geometry-data-type.md)   
 [STCentroid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)   
 [STPointOnSurface &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [MultiPolígono](../../relational-databases/spatial/multipolygon.md)   
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [STIsValid &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)   
 [STIsValid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
  
