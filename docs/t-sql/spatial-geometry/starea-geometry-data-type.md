---
title: STArea (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geometry Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea (geometry Data Type)
ms.assetid: a7dd6083-c649-4ac3-885d-1234e0db62f1
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fcaad3c2fb8337c64612d5ef5532bcbc4ed4b91d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100990"
---
# <a name="starea-geometry-data-type"></a>STArea (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve el área expuesta total de una instancia de **geometry**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de valor devuelto de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
 `STArea()` devuelve 0 si una instancia de **geometry** contiene únicamente figuras no dimensionales o unidimensionales, o si está vacía. `STArea()` devuelve **NULL** si la instancia de **geometry** no se ha inicializado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-computing-the-area-of-a-polygon-instance"></a>A. Calcular el área de una instancia de Polygon  
 En el siguiente ejemplo se crea una instancia de `Polygon``geometry` y se calcula el área del polígono.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STArea();  
```  
  
### <a name="b-computing-the-area-of-a-curvepolygon-instance"></a>B. Calcular el área de una instancia de CurvePolygon  
 En el siguiente ejemplo se calcula el área de una instancia de `CurvePolygon`.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 2, 2 0, 4 2, 4 2, 0 2))');  
 SELECT @g.STArea() AS Area;
 ```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
