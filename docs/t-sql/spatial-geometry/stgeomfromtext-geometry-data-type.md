---
title: STGeomFromText (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromText (geometry Data Type)
- STGeomFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromText (geometry Data Type)
ms.assetid: 20cace39-02e5-46c1-a9a5-841d04d0da16
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6d8a79e1bc9ddbbfc86243df0be1caf4f8d8b1c8
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552845"
---
# <a name="stgeomfromtext-geometry-data-type"></a>STGeomFromText (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve una instancia de **geometry** a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STGeomFromText ( 'geometry_tagged_text' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *geometry_tagged_text*  
 Es la representación WKT de la instancia de **geometry** que se quiere devolver. *geometry_tagged_text* es una expresión **nvarchar(max)** .  
  
 *SRID*  
 Es una expresión **int** que representa el identificador de referencia espacial (SRID) de la instancia de **geometry** que se quiere devolver.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Observaciones  
 El tipo OGC de la instancia de **geometry** devuelta por `STGeomFromText()` se establece en la entrada WKT correspondiente.  
  
 Este método produce una excepción **FormatException** si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STGeomFromText()` para crear una instancia de `geometry`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de geometría estáticos de OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

