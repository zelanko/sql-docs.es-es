---
title: STDimension (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDimension_TSQL
- STDimension (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDimension (geometry Data Type)
ms.assetid: 4fbd27dd-317b-4916-a8ae-4df1b8a6f27c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b0a53e3eca76e5798b891943aff775844618dbf8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748673"
---
# <a name="stdimension-geometry-data-type"></a>STDimension (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve la dimensión máxima de una instancia de **geometry**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STDimension ( )  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de valor devuelto de CLR: **SqlInt32**  
  
## <a name="remarks"></a>Observaciones  
 `STDimension()` devuelve -1 si la instancia de **geometry** está vacía.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una variable de tabla para contener las instancias de **geometry** y se inserta un `Point`, una `LineString` y un `Polygon`.  Después, se usa `STDimension()` para devolver las dimensiones de cada instancia de **geometry**.  
  
```  
DECLARE @temp table ([name] varchar(10), [geom] geometry);  
INSERT INTO @temp values ('Point', geometry::STGeomFromText('POINT(3 3)', 0));  
INSERT INTO @temp values ('LineString', geometry::STGeomFromText('LINESTRING(0 0, 3 3)', 0));  
INSERT INTO @temp values ('Polygon', geometry::STGeomFromText('POLYGON((0 0, 3 0, 0 3, 0 0))', 0));  
SELECT [name], [geom].STDimension() as [dim]  
FROM @temp;  
```  
  
 A continuación, el ejemplo devuelve las dimensiones de cada instancia de `geometry`.  
  
|name|dim|  
|----------|---------|  
|Punto|0|  
|LineString|1|  
|Polygon|2|  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

