---
title: STIntersection (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STIntersection_TSQL
- STIntersection (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersection method
ms.assetid: 7e09468f-499f-4a38-ba4b-bb30b8821e3b
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5e1c632bf87c0c4a00229e350dfa33b69bec8e24
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993057"
---
# <a name="stintersection-geography-data-type"></a>STIntersection (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve un objeto que representa los puntos donde una instancia de **geography** forma intersección con otra instancia de **geography**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STIntersection ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 Es otra instancia de **geography** con la que se compara la instancia en la que se está invocando STIntersection().  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Notas  
 Se devuelve la intersección de dos instancias de geography.  
  
 STIntersection() siempre devuelve NULL si no coinciden los identificadores de referencia espacial (SRID) de las instancias de **geography**.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite instancias espaciales mayores que un hemisferio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede incluir instancias de **FullGlobe** en el conjunto de resultados posibles devuelto en el servidor.  
  
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
  
## <a name="see-also"></a>Ver también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
