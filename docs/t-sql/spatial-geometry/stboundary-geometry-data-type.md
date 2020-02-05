---
title: STBoundary (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBoundary (geometry Data Type)
- STBoundary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBoundary (geometry Data Type)
ms.assetid: f0551674-e6e8-4926-9038-df03f2c807d7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1a15d3bdc505c4406c1c5d09dbc9d6f007c34fe0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67930385"
---
# <a name="stboundary-geometry-data-type"></a>STBoundary (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el límite de una instancia de **geometry**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STBoundary ( )  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Observaciones  
 `STBoundary()` devuelve una instancia vacía de **GeometryCollection** cuando los extremos de una instancia de **LineString**, **CircularString** o **CompoundCurve** son los mismos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-stboundary-on-a-linestring-instance-with-different-endpoints"></a>A. Usar STBoundary () en una instancia de LineString con extremos diferentes  
 En el ejemplo siguiente se crea una instancia de `LineString``geometry`. `STBoundary()` devuelve el límite de `LineString`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STBoundary().ToString();  
```  
  
### <a name="b-using-stboundary-on-a-linestring-instance-with-the-same-endpoints"></a>B. Usar STBoundary () en una instancia de LineString con los mismos extremos  
 En el ejemplo siguiente se crea una instancia de `LineString` válida con los mismos extremos. `STBoundary()` devuelve una instancia vacía de `GeometryCollection`.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, -2 2, 0 0)', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
### <a name="c-using-stboundary-on-a-curvepolygon-instance"></a>C. Usar STBoundary() en una instancia de CurvePolygon  
 En el ejemplo siguiente se utiliza `STBoundary()` en una instancia de `CurvePolygon`. `STBoundary()` devuelve una instancia de `CircularString`.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(0 0, 2 2, 0 2, -2 2, 0 0))', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
