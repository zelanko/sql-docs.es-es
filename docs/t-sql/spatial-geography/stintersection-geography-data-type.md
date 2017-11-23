---
title: STIntersection (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIntersection_TSQL
- STIntersection (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STIntersection method
ms.assetid: 7e09468f-499f-4a38-ba4b-bb30b8821e3b
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5fa4496e09192a7c17928dc6a2af6f5ef06f51b5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="stintersection-geography-data-type"></a>STIntersection (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve un objeto que representa los puntos donde un **geography** instancia se corta con otra **geography** instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STIntersection ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 Es otra **geography** instancia va a comparar con la instancia en la que se está llamando a stintersection ().  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 Se devuelve la intersección de dos instancias de geography.  
  
 Stintersection () siempre devuelve null si los identificadores de referencia espacial (SRID) de la **geography** instancias no coinciden.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite instancias espaciales mayores que un hemisferio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]puede incluir **FullGlobe** instancias en el conjunto de resultados posibles devuelven en el servidor.  
  
 El resultado puede contener segmentos de arco circulares solo si las instancias de entrada contienen segmentos de arco circulares.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-computing-the-intersection-of-a-polygon-and-a-linestring"></a>A. Calcular la intersección de un tipo Polygon y un tipo LineString  
 En el ejemplo siguiente se usa `STIntersection()` para calcular la intersección de un tipo `Polygon` y un tipo `LineString`.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="b-computing-the-intersection-of-a-polygon-and-a-curvepolygon"></a>B. Calcular la intersección de un tipo Polygon y un tipo CurvePolygon  
 En el siguiente ejemplo se devuelve una instancia que contiene un segmento de arco circular.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="c-computing-the-symmetric-difference-with-fullglobe"></a>C. Calcular la diferencia simétrica con FullGlobe  
 En el siguiente ejemplo se compara la diferencia simétrica de un `Polygon` con `FullGlobe`.  
  
```  
DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
SELECT @g.STIntersection('FULLGLOBE').ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
