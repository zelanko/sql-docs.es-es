---
title: GeometryCollection | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1a5c21c01ab776a17d3e160fee51167c426dfa0c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198647"
---
# <a name="geometrycollection"></a>Colección Geometry
  A `GeometryCollection` es una colección de cero o más `geometry` o `geography` instancias. Un `GeometryCollection` puede estar vacío.  
  
## <a name="geometrycollection-instances"></a>Instancias de GeometryCollection  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Para que se acepte una instancia de `GeometryCollection`, debe ser una instancia de `GeometryCollection` vacía o todas las instancias que comprenden la instancia de `GeometryCollection` deben ser instancias aceptadas. El siguiente ejemplo muestra instancias aceptadas.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 En el ejemplo siguiente se inicia una `System.FormatException` porque el `LinesString` de instancia de la `GeometryCollection` no se acepta la instancia.  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
 Una instancia de `GeometryCollection` es válida cuando todas las instancias que comprenden la instancia de  `GeometryCollection` son válidas. La continuación muestran tres válido `GeometryCollection` instancias y una instancia que no es válida.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Datos espaciales &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  