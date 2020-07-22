---
title: STGeometryN (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1deed4d716bbee62dac425a9d71780aec445602e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555801"
---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN (tipo de datos geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve un elemento **geography** especificado en una colección **GeometryCollection** o en uno de sus subtipos. Cuando STGeometryN() se usa en un subtipo de **GeometryCollection**, como **MultiPoint** o **MultiLineString**, este método devuelve la instancia de **geography**  si se llama con N = 1.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STGeometryN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *expression*  
 Expresión **int** entre 1 y el número de instancias de **geography** en la colección **GeometryCollection**.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Observaciones  
 Este método devuelve NULL si el parámetro es mayor que el resultado de [STNumGeometries()](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md) y producirá una excepción **ArgumentOutOfRangeException** si el parámetro *expression* es menor que 1.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea una instancia de `MultiPoint``geography` y se usa `STGeometryN()` para hallar la segunda instancia de `geography` de **GeometryCollection**.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
