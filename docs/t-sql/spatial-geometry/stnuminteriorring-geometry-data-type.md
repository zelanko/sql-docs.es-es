---
title: STNumInteriorRing (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumInteriorRing_TSQL
- STNumInteriorRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STNumInteriorRing (geometry Data Type)
ms.assetid: 48e78948-5b14-41dd-85d1-169bba1c4195
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a13ae1a62d6a1cac3059f4b149d7d828698202fb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762273"
---
# <a name="stnuminteriorring-geometry-data-type"></a>STNumInteriorRing (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve el número de anillos interiores de una instancia de **Polygongeometry**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STNumInteriorRing ( )  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de valor devuelto de CLR: **SqlInt32**  
  
## <a name="remarks"></a>Observaciones  
 Este método devuelve NULL si la instancia de **geometry** no es un polígono.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Polygon` y se usa `STNumInteriorRing()` para averiguar cuántos anillos interiores tiene dicha instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STNumInteriorRing();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

