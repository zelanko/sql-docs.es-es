---
title: STOverlaps (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STOverlaps (geometry Data Type)
- STOverlaps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STOverlaps (geometry Data Type)
ms.assetid: 1813cba1-5780-456a-9489-6b40a79569b3
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 018939e7b25b6544bb4d9b5724371dc080905be1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="stoverlaps-geometry-data-type"></a>STOverlaps (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve 1 si una instancia de **geometry** se superpone con otra instancia de **geometry**. Devuelve 0 en caso contrario.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STOverlaps ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 Es otra instancia de **geometry** con la que se compara la instancia en la que se invoca `STOverlaps()`.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Notas  
 Dos instancias de **geometry** se superponen si la región que representa su intersección tiene la misma dimensión que tienen las instancias y la región no es igual a ninguna instancia.  
  
 `STOverlaps()` siempre devuelve 0 si los puntos de intersección de las instancias de **geometry** no son de la misma dimensión.  
  
 Este método siempre devuelve NULL si no coinciden los identificadores de referencia espacial (SRID) de las instancias de **geometry**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STOverlaps()` para ver si se superponen dos instancias de **geometry**.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STOverlaps(@h);  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

