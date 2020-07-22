---
title: InstanceOf (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 09d468b4f39ba50a0c195287961f3c3dc76e0ccd
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552930"
---
# <a name="instanceof-geography-data-type"></a>InstanceOf (tipo de datos geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Comprueba si la instancia de **geography** es del tipo especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
  
.InstanceOf ( 'geography_type')  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*tipo_de_geography*  
La cadena **nvarchar(4000)** en la que se especifica uno de los 16 tipos expuestos en la jerarquía de tipos de **geography**.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Observaciones  
Devuelve 1 si el tipo de una instancia de **geography** coincide con el tipo especificado, o si el tipo especificado es un antecesor del tipo de la instancia; en caso contrario, devuelve 0.  
  
Este método del tipo de datos **geography** admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
La entrada para el método deben ser uno de estos tipos: Geometry, Point, Curve, LineString, CircularString, Surface, Polygon, CurvePolygon, **GeometryCollection**, **MultiSurface**, **MultiPolygon, MultiCurve, MultiLineString**, **MultiPoint** o **FullGlobe**.  
  
Este método inicia una excepción `ArgumentException` si se usa cualquier otra cadena para la entrada.  
  
Este método no es exacto.  
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se crea una instancia de `MultiPoint` y se usa `InstanceOf()` para comprobar si la instancia es de tipo `GeometryCollection`.  
  
```sql  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
