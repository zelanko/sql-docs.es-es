---
title: ToString (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ToString (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString (geometry Data Type)
ms.assetid: 2e55fa98-aa22-4baa-a516-7c233a33e212
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d8e140a968a86be980f38d1333fc82e28bbc812e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762085"
---
# <a name="tostring-geometry-data-type"></a>ToString (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de geometría ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.ToString ()  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de valor devuelto de CLR: **SqlString**  
  
## <a name="remarks"></a>Observaciones  
 Este método devolverá la cadena "Null" cuando se le llama con instancias NULL.  
  
 En instancias no NULL, este método es equivalente a utilizar `AsTextZM().`  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea una instancia de`LineString` y se usa `ToString()` para obtener la descripción de texto de la instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [STAsText &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)   
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

