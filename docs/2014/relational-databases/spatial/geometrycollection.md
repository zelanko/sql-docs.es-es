---
title: GeometryCollection | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 5aceabe5a263cfa53572be6f818ddc905f9742a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014227"
---
# <a name="geometrycollection"></a>GeometryCollection
  Un `GeometryCollection` es una colección de cero o más `geometry` o `geography` instancias. Un `GeometryCollection` puede estar vacío.  
  
## <a name="geometrycollection-instances"></a>Instancias de GeometryCollection  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Para que se acepte una instancia de `GeometryCollection`, debe ser una instancia de `GeometryCollection` vacía o todas las instancias que comprenden la instancia de `GeometryCollection` deben ser instancias aceptadas. El siguiente ejemplo muestra instancias aceptadas.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 El siguiente ejemplo inicia una `System.FormatException` porque la instancia de `LinesString` en la instancia `GeometryCollection` no se acepta.  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
 Una instancia de `GeometryCollection` es válida cuando todas las instancias que comprenden la instancia de  `GeometryCollection` son válidas. A continuación se muestran tres instancias de `GeometryCollection` válidas y una instancia que no es válida.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 
  `@g4` no es válida porque la instancia de `Polygon` en la instancia de `GeometryCollection` no es válida.  
  
 Para obtener más información de las instancias aceptadas y las instancias válidas, vea [Point](point.md), [MultiPoint](multipoint.md), [LineString](linestring.md), [MultiLineString](multilinestring.md), [Polygon](polygon.md)y [MultiPolygon](multipolygon.md).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente crea `geometry``GeometryCollection` con valores de Z en SRID 1 que contiene una instancia `Point` y una instancia `Polygon` .  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>Consulte también  
 [Datos espaciales &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
