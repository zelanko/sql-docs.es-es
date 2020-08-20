---
description: STIsValid (tipo de datos geometry)
title: STIsValid (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 65e86550626b1461cb8b0abc5e7fb354e6b4e3a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472437"
---
# <a name="stisvalid-geometry-data-type"></a>STIsValid (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve true si una instancia de **geometry** tiene el formato correcto, en función de su tipo de Open Geospatial Consortium (OGC). Devuelve false si una instancia de **geometry** no tiene el formato correcto.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STIsValid ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de valor devuelto
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Observaciones  
 El tipo de OGC de una instancia de **geometry** se puede determinar mediante la invocación de [STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo produce instancias válidas de **geometry**, pero permite el almacenamiento y la recuperación de instancias no válidas. El método `MakeValid()` permite recuperar una instancia válida que representa el mismo conjunto de puntos que cualquier instancia no válida.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `geometry` y se usa `STIsValid()` para comprobar si dicha instancia es válida.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>Consulte también  
 [STGeometryType &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

