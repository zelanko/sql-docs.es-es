---
title: ShortestLineTo (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f2d92d90c363cd17844d905a7d0108b0f148a007
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631853"
---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve una instancia de **LineString** con dos puntos que representan la distancia más corta entre las dos instancias de **geometry**. La longitud de la instancia de **LineString** devuelta es la distancia entre las dos instancias de **geometry**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
## <a name="arguments"></a>Argumentos  
 *otra_geometría*  
 La segunda instancia de **geometry** a la que la instancia de **geometry** que realiza la llamada está intentando determinar la distancia más corta.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Notas  
 El método devuelve una instancia de **LineString** con los extremos en los bordes de las dos instancias de **geometry** que no se cruzan y que se comparan. La longitud de la instancia de **LineString** devuelta es igual a la distancia más corta entre las dos instancias de **geometry**. Se devuelve una instancia vacía de **LineString** cuando las dos instancias de **geometry** se cruzan.  
  
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
  
## <a name="see-also"></a>Ver también  
 [ShortestLineTo &#40;geography Data Type&#41;](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md) (ShortestLineTo [tipo de datos geography])  
  
  

