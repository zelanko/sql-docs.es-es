---
title: ShortestLineTo (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc8843ceefe8819d2f314d76b019720863866ed1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve un **LineString** instancia con dos puntos que representan la distancia más corta entre los dos **geometry** instancias. La longitud de la **LineString** instancia devuelta es la distancia entre los dos **geometry** instancias.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_other*  
 El segundo **geometry** instancia que la llamada a **geometry** instancia está intentando determinar la distancia más corta.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentarios  
 El método devuelve un **LineString** instancia con los extremos que quedan en los bordes de las dos programaciones **geometry** instancias que se están comparadas. La longitud de la **LineString** devuelta es igual a la distancia más corta entre las dos **geometry** instancias. Vacío **LineString** instancia se devuelve cuando las dos **geometry** instancias tienen la intersección entre sí.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. Llamar a ShortestLineTo() en las instancias que no se cruzan  
 En este ejemplo se busca la distancia más corta entre una instancia de `CircularString` y una instancia de `LineString`, y se devuelven las instancias de `LineString` que conectan los dos extremos:  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(-4 7, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. Llamar a ShortestLineTo() en las instancias que se cruzan  
 En este ejemplo se devuelve una instancia de `LineString` vacía porque la instancia de `LineString` se cruza con la instancia de `CircularString`:  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(0 5, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
## <a name="see-also"></a>Vea también  
 [ShortestLineTo &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md)  
  
  


