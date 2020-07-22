---
title: STGeometryType (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryType_TSQL
- STGeometryType (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryType (geometry Data Type)
ms.assetid: 224cdc83-aa83-4ad4-bb82-b7481031e910
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a842e3ee2dcfb86f293e8ae3feba1a30665ffbe0
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554650"
---
# <a name="stgeometrytype-geometry-data-type"></a>STGeometryType (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve el nombre del tipo de Open Geospatial Consortium (OGC) representado por una instancia de **geometry**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STGeometryType ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de valor devuelto
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(4000)**  
  
 Tipo de valor devuelto de CLR: **SqlString**  
  
## <a name="remarks"></a>Observaciones  
 Los nombres de los tipos de OGC que `STGeometryType()` puede devolver son **Point**, **LineString**, **CircularString**, **CompoundCurve**, **Polygon, CurvePolygon**, **GeometryCollection**, **MultiPoint**, **MultiLineString** y **MultiPolygon**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia `Polygon` y se utiliza `STGeometryType()` para confirmar que es un polígono.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 0);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

