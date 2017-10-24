---
title: STIsSimple (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 12b150546378ef76c0165c6d8e3c166e93db304b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="stissimple-geometry-data-type"></a>STIsSimple (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve 1 si una **geometry** instancia es simple, tal como se define por Open Geospatial Consortium (OGC). Devuelve 0 si una **geometry** instancia no es simple.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STIsSimple ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **bits**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentarios  
 Para ser simple, un **geometry** instancia debe cumplir todos los requisitos siguientes:  
  
-   Cada figura de la instancia no debe cortarse, excepto en sus extremos.  
  
-   Ninguna de las dos figuras de la instancia puede cortarse en un punto que no esté en ambos de sus límites.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `LineString` no sencilla que se corta a sí misma y se usa `STIsSimple()` para comprobar si la instancia de `LineString` es sencilla.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de OGC en instancias de Geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


