---
title: STInteriorRingN (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STInteriorRingN_TSQL
- STInteriorRingN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STInteriorRingN (geometry Data Type)
ms.assetid: 47310f9f-2cdb-41e0-a6da-7c3cfbf139ac
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e78d4d7fd52e018d4224726c82f1251bb1fe22a1
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554658"
---
# <a name="stinteriorringn-geometry-data-type"></a>STInteriorRingN (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve el anillo interior especificado de una instancia de **geometry** de Polygon.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STInteriorRingN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *expression*  
 Es una expresión **int** entre 1 y el número de anillos interiores en la instancia de **geometry**.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
 Tipo Open Geospatial Consortium (OGC): **LineString**  
  
## <a name="remarks"></a>Observaciones  
 Este método devuelve **null** si la instancia de **geometry** no es un polígono. Este método también producirá una excepción **ArgumentOutOfRangeException** si la expresión es mayor que el número de anillos. El número de anillos se puede devolver usando `STNumInteriorRing``()`.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea una instancia de `Polygon` y se usa `STInteriorRingN()` para devolver el anillo interior del polígono como un elemento **LineString**.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STInteriorRingN(1).ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

