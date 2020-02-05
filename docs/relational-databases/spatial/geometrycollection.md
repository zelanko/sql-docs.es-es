---
title: GeometryCollection | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 263f7025bf89b3bb1751d2eb6677c90dbbfb442e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68048678"
---
# <a name="geometrycollection"></a>GeometryCollection
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un **GeometryCollection** es una colección de cero o más **geometry** o **geography** instancias. Un **GeometryCollection** puede estar vacío.  
  
## <a name="geometrycollection-instances"></a>Instancias de GeometryCollection  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Para que se acepte una instancia de **GeometryCollection** , debe ser una instancia de **GeometryCollection** vacía o todas las instancias que comprenden la instancia de **GeometryCollection** deben ser instancias aceptadas. El siguiente ejemplo muestra instancias aceptadas.  
  
```sql  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 El siguiente ejemplo inicia una `System.FormatException` porque la instancia **LinesString** de la instancia **GeometryCollection** no se acepta.  
  
```sql  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
 Una instancia de **GeometryCollection** es válida cuando todas las instancias que comprenden la instancia de **GeometryCollection** son válidas. A continuación se muestran tres instancias de **GeometryCollection** válidas y una instancia que no es válida.  
  
```sql  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` no es válida porque la instancia **Polygon** de la instancia **GeometryCollection** no es válida.  
  
 Para obtener más información de las instancias aceptadas y las instancias válidas, vea [Point](../../relational-databases/spatial/point.md), [MultiPoint](../../relational-databases/spatial/multipoint.md), [LineString](../../relational-databases/spatial/linestring.md), [MultiLineString](../../relational-databases/spatial/multilinestring.md), [Polygon](../../relational-databases/spatial/polygon.md)y [MultiPolygon](../../relational-databases/spatial/multipolygon.md).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente crea `geometry``GeometryCollection` con valores de Z en SRID 1 que contiene una instancia `Point` y una instancia `Polygon` .  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>Consulte también  
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
