---
title: MultiLineString | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 9244f32b2ee9921d1caaa63b5d6aae9c324049ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014206"
---
# <a name="multilinestring"></a>MultiLineString
  Una `MultiLineString` es una colección de cero o más `geometry` instancias de o **geographyLineString** .  
  
## <a name="multilinestring-instances"></a>Instancias de MultiLineString  
 En la ilustración siguiente se muestran ejemplos de instancias de `MultiLineString`.  
  
 ![Ejemplos de instancias MultiLineString de geometry](../../database-engine/media/multilinestring.gif "Ejemplos de instancias MultiLineString de geometry")  
  
 Como se muestra en la ilustración:  
  
-   La figura 1 es una `MultiLineString` instancia sencilla cuyo límite son los cuatro extremos de sus dos `LineString` elementos.  
  
-   La figura 2 es una instancia sencilla de `MultiLineString` porque solo forman una intersección los extremos de los elementos `LineString`. El límite lo constituyen los dos extremos que no se superponen.  
  
-   La figura 3 es una instancia no sencilla de `MultiLineString` porque el interior de uno de sus elementos `LineString` forma parte de una intersección. El límite de esta instancia de `MultiLineString` lo constituyen los cuatro extremos.  
  
-   La figura 4 es una instancia de `MultiLineString` no sencilla y sin cerrar.  
  
-   La figura 5 es una instancia de `MultiLineString` sencilla y sin cerrar. No está cerrada porque sus `LineStrings` elementos no están cerrados. Es sencilla porque ninguno de los interiores de ninguna de las instancias de `LineStrings` forma parte de una intersección.  
  
-   La figura 6 es una instancia de `MultiLineString` sencilla y cerrada. Está cerrada porque lo están todos sus elementos. Es sencilla porque ninguno de sus elementos forma parte de una intersección con los interiores.  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Para que se acepte una instancia de `MultiLineString`, debe estar vacío o estar formada solo por instancias de `LineString` aceptadas. Para obtener más información sobre `LineString` las instancias aceptadas, vea [LineString](../spatial/linestring.md). A continuación se enumeran ejemplos de instancias `MultiLineString` aceptadas.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 En el siguiente ejemplo se produce una excepción `System.FormatException` porque la segunda instancia de `LineString` no es válida.  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
 Para que una instancia de `MultiLineString` sea válida debe cumplir los siguientes criterios:  
  
1.  Todas las instancias que forman la instancia de `MultiLineString` deben ser instancias válidas de `LineString`.  
  
2.  Dos de las instancias de `LineString` que forman la instancia de `MultiLineString` pueden superponerse durante un intervalo. Las instancias de `LineString` solo pueden formar una intersección o tocarse una a la otra o a otra instancia de `LineString` en un número finito de puntos.  
  
 En el ejemplo siguiente se muestran tres instancias válidas de `MultiLineString` y una instancia de `MultiLineString` que no es válida.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` no es válida porque la segunda instancia de `LineString` se superpone a la primera instancia de `LineString` en un intervalo. Se tocan en un número infinito de puntos.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente crea una instancia sencilla de `geometry``MultiLineString` que contiene dos elementos `LineString` con un SRID de 0.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
 Para crear instancias de esta instancia con otro SRID, utilice `STGeomFromText()` o `STMLineStringFromText()`. También puede utilizar `Parse()` y, a continuación, modificar el SRID, como se muestra en el ejemplo siguiente.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>Consulte también  
 [STLength &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STIsClosed &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [LineString](../spatial/linestring.md)   
 [Datos espaciales &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
