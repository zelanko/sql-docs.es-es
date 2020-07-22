---
title: STGeometryType (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryType (geography Data Type)
- STGeometryType_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryType method
ms.assetid: 3e169ead-a98e-44af-8d33-fd59a955cae4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 957615b665641afd3ffbfbcac8d789a2426b35cc
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555410"
---
# <a name="stgeometrytype-geography-data-type"></a>STGeometryType (tipo de datos geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve el nombre del tipo de Open Geospatial Consortium (OGC) representado por una instancia de **geography**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STGeometryType ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de valor devuelto
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(4000)**  
  
 Tipo de valor devuelto de CLR: **SqlString**  
  
## <a name="remarks"></a>Observaciones  
 Los nombres de tipo OGC que `STGeometryType()` puede devolver son **Point**, **LineString**, **CircularString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **GeometryCollection**, **MultiPoint**, **MultiLineString**, **MultiPolygon** y **FullGlobe**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia `Polygon` y se utiliza `STGeometryType()` para confirmar que es un polígono.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
