---
title: MultiPolygon | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3ae25be65e0fdf0cf88bf8dec6cf5c3f59f9c9e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37311415"
---
# <a name="multipolygon"></a>MultiPolígono
  Un `MultiPolygon` instancia es una colección de cero o más `Polygon` instancias.  
  
## <a name="polygon-instances"></a>Instancias Polygon  
 La ilustración siguiente muestra ejemplos de `MultiPolygon` instancias.  
  
 ![Ejemplos de instancias MultiPolygon de geometry](../../database-engine/media/multipolygon.gif "Ejemplos de instancias MultiPolygon de geometry")  
  
 Como se muestra en la ilustración:  
  
-   Figura 1 es un `MultiPolygon` instancia con dos `Polygon` elementos. El límite se define mediante los dos anillos exteriores y los tres interiores.  
  
-   La Figura 2 es una instancia de `MultiPolygon` con dos elementos `Polygon`. El límite se define mediante los dos anillos exteriores y los tres interiores. Los dos elementos `Polygon` forman una intersección en un punto tangente.  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Un `MultiPolygon` se acepta la instancia se cumple una de las siguientes condiciones.  
  
-   Es un valor vacío `MultiPolygon` instancia.  
  
-   Todas las instancias que comprenden la `MultiPolygon` se aceptan instancia `Polygon` instancias. Para obtener más información sobre aceptado `Polygon` instancias, consulte [polígono](../spatial/polygon.md).  
  
 Los ejemplos siguientes muestran instancias `MultiPolygon` aceptadas.  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
```  
  
 En el siguiente ejemplo se muestra una instancia MultiPolygon que producirá una excepción `System.FormatException`.  
  
```  
DECLARE @g geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3)))';  
```  
  
 La segunda instancia en MultiPolygon es una instancia LineString y no una instancia Polygon aceptada.  
  
### <a name="valid-instances"></a>Instancias válidas  
 Una instancia `MultiPolygon` es válida si es una instancia `MultiPolygon` vacía o si cumple los siguientes criterios.  
  
1.  Todas las instancias que comprenden la instancia `MultiPolygon` son instancias `Polygon` válidas. Para válido `Polygon` instancias, consulte [polígono](../spatial/polygon.md).  
  
2.  Ninguna de las instancias `Polygon` que comprenden la instancia `MultiPolygon` se superponen.  
  
 En el siguiente ejemplo se muestran dos instancias `MultiPolygon` válidas y una instancia `MultiPolygon` no válida.  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g2` es válido porque los dos `Polygon` instancias se tocan solo en un punto tangente. `@g3` no es válido porque los interiores de los dos `Polygon` instancias superponen entre sí.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra la creación de una instancia de `geometry``MultiPolygon` y devuelve el valor Well-Known Text (WKT) del segundo componente.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON(((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1)), ((9 9, 9 10, 10 9, 9 9)))');  
SELECT @g.STGeometryN(2).STAsText();  
```  
  
 Este ejemplo crea instancias de una instancia de `MultiPolygon` vacía.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON EMPTY');  
```  
  
## <a name="see-also"></a>Vea también  
 [Polygon](../spatial/polygon.md)   
 [STArea &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type)   
 [STCentroid &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)   
 [STPointOnSurface &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [Datos espaciales &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
