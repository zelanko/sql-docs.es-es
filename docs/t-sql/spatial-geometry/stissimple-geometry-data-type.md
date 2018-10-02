---
title: STIsSimple (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e974d8cda1a6c21e7b3d568f242d36c96d81b5f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718303"
---
# <a name="stissimple-geometry-data-type"></a>STIsSimple (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve 1 si una instancia de **geometry** es sencilla, según la definición de Open Geospatial Consortium (OGC). Devuelve 0 si una instancia de **geometry** no es sencilla.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STIsSimple ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Notas  
 Para que una instancia de **geometry** sea sencilla, debe cumplir estos requisitos:  
  
-   Cada figura de la instancia no debe cortarse, excepto en sus extremos.  
  
-   Ninguna de las dos figuras de la instancia puede cortarse en un punto que no esté en ambos de sus límites.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `LineString` no sencilla que se corta a sí misma y se usa `STIsSimple()` para comprobar si la instancia de `LineString` es sencilla.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

