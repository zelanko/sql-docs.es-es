---
title: STEquals (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STEquals (geometry Data Type)
- STEquals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEquals (geometry Data Type)
ms.assetid: 808f0e25-9e68-4ba7-9329-07ec950698f3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: af6fdaff361ae845000455bf53cb952466a0ef30
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554311"
---
# <a name="stequals-geometry-data-type"></a>STEquals (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve 1 si una instancia de **geometry** representa el mismo conjunto de puntos que otra instancia de **geometry**. Devuelve 0 en caso contrario.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STEquals ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *other_geometry*  
 Es otra instancia de **geometry** con la que se compara la instancia en la que se invoca `STEquals()`.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Observaciones  
 Este método siempre devuelve NULL si no coinciden los identificadores de referencia espacial (SRID) de las instancias de **geometry**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crean dos instancias de `geometry` con `STGeomFromText()` que son iguales, pero no trivialmente iguales, y se usa `STEquals()` para comprobar su igualdad.  
  
```  
DECLARE @g geometry  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('MULTILINESTRING((4 2, 2 0), (0 2, 2 0))', 0);  
SELECT @g.STEquals(@h);  
```  
  
## <a name="see-also"></a>Consulte también  
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

