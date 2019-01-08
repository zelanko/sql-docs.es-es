---
title: CircularString | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 9fe06b03-d98c-4337-9f89-54da98f49f9f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 001c489d9abf887495ea83cee00cede1463514ca
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376667"
---
# <a name="circularstring"></a>CircularString
  Una `CircularString` es una colección con cero o más segmentos de arco circular continuos. Un segmento de arco circular es un segmento curvado definido por tres puntos en un plano bidimensional; el primer punto no puede ser igual que el tercero. Si los tres puntos de un segmento de arco circular son colineales, el segmento de arco se trata como un segmento de línea.  
  
> [!IMPORTANT]  
>  Para obtener una descripción detallada y ejemplos de las nuevas características espaciales introducidas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluido el `CircularString` subtipo, descargue las notas del producto, [nuevas características espaciales de SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
## <a name="circularstring-instances"></a>Instancias de CircularString  
 En el dibujo siguiente se muestran instancias válidas de `CircularString`:  
  
 ![](../../database-engine/media/5ff17e34-b578-4873-9d33-79500940d0bc.png "5ff17e34-b578-4873-9d33-79500940d0bc")  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Un `CircularString` se acepta la instancia si está vacía o contiene un número impar de puntos, n, donde n > 1. Se aceptan las siguientes instancias de `CircularString`.  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 2 0, 1 1)';  
```  
  
 `@g3` muestra que la instancia de `CircularString` se puede aceptar, pero no es válida. La siguiente declaración de instancia de CircularString no se acepta. Esta declaración inicia una excepción `System.FormatException`.  
  
```  
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
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1, 0 1)';  
DECLARE @g4 geometry = 'CIRCULARSTRING(1 1, 2 2, 2 2)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(),@g4.STIsValid();  
```  
  
 Una instancia de `CircularString` debe contener al menos dos segmentos de arco circular para definir un círculo completo. Una instancia de `CircularString` no puede utilizar solo un segmento de arco circular, por ejemplo (1 1, 3 1, 1 1), para definir un círculo completo. Utilice (1 1, 2 2, 3 1, 2 0, 1 1) para definir el círculo.  
  
 En el siguiente ejemplo se muestran instancias de CircularString no válidas.  
  
```  
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
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING EMPTY');  
```  
  
### <a name="b-instantiating-a-geometry-instance-using-a-circularstring-with-one-circular-arc-segment"></a>b. Crear instancias de una instancia de geometry usando una CircularString con un segmento de arco circular  
 En el siguiente ejemplo se muestra cómo crear una instancia de `CircularString` con un único segmento de arco de circular (medio círculo):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry:: STGeomFromText('CIRCULARSTRING(2 0, 1 1, 0 0)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="c-instantiating-a-geometry-instance-using-a-circularstring-with-multiple-circular-arc-segments"></a>C. Crear instancias de una instancia de geometry usando una CircularString con varios segmentos de arco circular  
 En el siguiente ejemplo se muestra cómo crear una instancia de `CircularString` con más de un segmento de arco circular (círculo completo):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING(2 1, 1 2, 0 1, 1 0, 2 1)');  
SELECT 'Circumference = ' + CAST(@g.STLength() AS NVARCHAR(10));    
```  
  
 Produce el siguiente resultado:  
  
```  
Circumference = 6.28319  
```  
  
 Compare con el resultado obtenido cuando se utiliza `LineString` en lugar de `CircularString`:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(2 1, 1 2, 0 1, 1 0, 2 1)', 0);  
SELECT 'Perimeter = ' + CAST(@g.STLength() AS NVARCHAR(10));  
```  
  
 Produce el siguiente resultado:  
  
```  
Perimeter = 5.65685  
```  
  
 Tenga en cuenta que el valor de la `CircularString` ejemplo está cerca de 2???, que es la longitud real de la circunferencia.  
  
### <a name="d-declaring-and-instantiating-a-geometry-instance-with-a-circularstring-in-the-same-statement"></a>D. Declarar y crear instancias de una instancia de geometry con una CircularString en la misma instrucción  
 Este fragmento de código muestra cómo declarar y crear instancias de una instancia de `geometry` con una `CircularString` en la misma instrucción:  
  
```tsql  
DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
```  
  
### <a name="e-instantiating-a-geography-instance-with-a-circularstring"></a>E. Crear instancias de una instancia de geography con una CircularString  
 En el siguiente ejemplo, se muestra cómo declarar y crear una instancia de `geography` con una `CircularString`:  
  
```tsql  
DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
```  
  
### <a name="f-instantiating-a-geometry-instance-with-a-circularstring-that-is-a-straight-line"></a>F. Crear instancias de una instancia de geometry con una CircularString que es una línea recta  
 En el siguiente ejemplo se muestra cómo crear una instancia de `CircularString` que es una línea recta:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('CIRCULARSTRING(0 0, 1 2, 2 4)', 0);  
```  
  
## <a name="see-also"></a>Vea también  
 [Información general de los tipos de datos espaciales](spatial-data-types-overview.md)   
 [CompoundCurve](compoundcurve.md)   
 [MakeValid &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/makevalid-geography-data-type)   
 [MakeValid &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/makevalid-geometry-data-type)   
 [STIsValid &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)   
 [STIsValid &#40;tipo de datos geography&#41;](/sql/t-sql/spatial-geography/stisvalid-geography-data-type)   
 [STLength &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STStartPoint &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)   
 [STEndpoint &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)   
 [STPointN &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)   
 [STNumPoints &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)   
 [STIsRing &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)   
 [STIsClosed &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [STPointOnSurface &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [LineString](linestring.md)  
  
  
