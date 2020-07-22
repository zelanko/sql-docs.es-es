---
title: STGeometryN (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryN_TSQL
- STGeometryN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN (geometry Data Type)
ms.assetid: 348c7047-3442-4590-8879-fe841e79058c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fcc6ccdb16dbc7091defe0405588da435f672c88
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552832"
---
# <a name="stgeometryn-geometry-data-type"></a>STGeometryN (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve una geometría especificada en una **colección de geometría**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STGeometryN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *expression*  
 Expresión **int** entre 1 y el número de instancias de **geometry** en la colección **geometrycollection**.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Observaciones  
 Este método devuelve **null** si el parámetro es mayor que el resultado de `STNumGeometries()` y producirá una excepción **ArgumentOutOfRangeException** si el parámetro *expresión* es menor que 1.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una `MultiPoint``geometry collection` y se usa `STGeometryN()` para buscar la segunda instancia de `geometry` de la colección.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

