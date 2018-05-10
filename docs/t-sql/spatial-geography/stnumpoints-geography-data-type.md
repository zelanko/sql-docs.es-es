---
title: STNumPoints (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STNumPoints (geography Data Type)
- STNumPoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints method
ms.assetid: 25ff7ad1-ba5f-4cfb-816a-59255ac1591d
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dcd18303d88fd13e867837dab61c0f7b293398cd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="stnumpoints-geography-data-type"></a>STNumPoints (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el número total de puntos de cada una de las figuras de una instancia de **geography**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de valor devuelto de CLR: **SqlInt32**  
  
## <a name="remarks"></a>Notas  
 Este método cuenta los puntos de la descripción de una instancia de **geography**. Se cuentan los puntos duplicados; sin embargo, los puntos de conexión entre segmentos se cuentan solo una vez. Si esta instancia es una colección, este método devuelve el número total de puntos de la colección.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-retrieving-the-total-number-of-points-in-a-linestring"></a>A. Recuperar el número total de puntos en un objeto LineString  
 En el ejemplo siguiente se crea una instancia de `LineString` y se utiliza `STNumPoints()` para determinar el número de puntos que se utilizaron en la descripción de la instancia.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STNumPoints();  
```  
  
### <a name="b-retrieving-the-total-number-of-points-in-a-geometrycollection"></a>B. Recuperar el número total de puntos en un objeto GeometryCollection  
 En el siguiente ejemplo se devuelve una suma de los puntos de todos los elementos de `GeometryCollection`.  
  
```  
DECLARE @g geography = 'GEOMETRYCOLLECTION(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)  
    ,CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.STNumPoints();  
```  
  
### <a name="c-returning-the-number-of-points-in-a-compoundcurve"></a>C. Devolver el número de puntos en un objeto CompoundCurve  
 En el siguiente ejemplo se devuelve el número de puntos de una instancia CompoundCurve. La consulta devuelve 5 en lugar de 6 porque STNumPoints () solo cuenta una vez el punto de conexión entre los segmentos.  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658),( -122.348 47.658, -121.56 48.12, -122.358 47.653))'  
 SELECT @g.STNumPoints();
 ```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
