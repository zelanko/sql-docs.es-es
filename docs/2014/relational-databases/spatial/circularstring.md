---
title: CircularString | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- dbe-spatial
ms.topic: conceptual
ms.assetid: 9fe06b03-d98c-4337-9f89-54da98f49f9f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4602b251d7e0674c206fe85830b0abc35d92684b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128895"
---
# <a name="circularstring"></a>CircularString
  Un `CircularString` es una colección de cero o más segmentos de arco circular continuos. Un segmento de arco circular es un segmento curvado definido por tres puntos en un plano bidimensional; el primer punto no puede ser igual que el tercero. Si los tres puntos de un segmento de arco circular son colineales, el segmento de arco se trata como un segmento de línea.  
  
> [!IMPORTANT]  
>  Para obtener una descripción detallada y ejemplos de las nuevas características espaciales introducidas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluido el `CircularString` subtipo, descargue las notas del producto, [nuevas características espaciales de SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407).  
  
## <a name="circularstring-instances"></a>Instancias de CircularString  
 El dibujo siguiente se muestran válido `CircularString` instancias:  
  
 ![](../../database-engine/media/5ff17e34-b578-4873-9d33-79500940d0bc.png "5ff17e34-b578-4873-9d33-79500940d0bc")  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Un `CircularString` se acepta la instancia si está vacía o contiene un número impar de puntos, n, donde n > 1. La siguiente `CircularString` se aceptan las instancias.  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 2 0, 1 1)';  
```  
  
 `@g3` muestra que `CircularString` instancia puede ser aceptado, pero no es válida. La siguiente declaración de instancia de CircularString no se acepta. Esta declaración inicia una excepción `System.FormatException`.  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1)';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
 Válido `CircularString` instancia debe estar vacía o tener los siguientes atributos:  
  
-   Debe contener al menos un segmento de arco circular (es decir, con un mínimo de tres puntos).  
  
-   El último extremo de cada segmento de arco circular de la secuencia, salvo el último segmento, debe ser el primer extremo del siguiente segmento de la secuencia.  
  
-   Debe tener un número impar de puntos.  
  
-   No se puede superponer sobre un intervalo.  
  
-   Aunque `CircularString` instancias pueden contener segmentos de línea, dichos segmentos deben definirse por tres puntos colineales.  
  
 El ejemplo siguiente se muestra válido `CircularString` instancias.  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1, 0 1)';  
DECLARE @g4 geometry = 'CIRCULARSTRING(1 1, 2 2, 2 2)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(),@g4.STIsValid();  
```  
  
 Una instancia de `CircularString` debe contener al menos dos segmentos de arco circular para definir un círculo completo. Un `CircularString` instancia no puede usar un segmento de arco circular único (como (1 1, 3 1, 1 1)) para definir un círculo completo. Utilice (1 1, 2 2, 3 1, 2 0, 1 1) para definir el círculo.  
  
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
  
### <a name="b-instantiating-a-geometry-instance-using-a-circularstring-with-one-circular-arc-segment"></a>B. Crear instancias de una instancia de geometry usando una CircularString con un segmento de arco circular  
 En el siguiente ejemplo se muestra cómo crear una instancia de `CircularString` con un único segmento de arco de circular (medio círculo):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry:: STGeomFromText('CIRCULARSTRING(2 0, 1 1, 0 0)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="c-instantiating-a-geometry-instance-using-a-circularstring-with-multiple-circular-arc-segments"></a>C. Crear instancias de una instancia de geometry usando una CircularString con varios segmentos de arco circular  
 El ejemplo siguiente muestra cómo crear un `CircularString` instancia con más de un segmento de arco circular (círculo completo):  
  
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
  
 Tenga en cuenta que el valor de la `CircularString` ejemplo está cerca de 2∏, que es la longitud real de la circunferencia.  
  
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
  
  
