---
title: STDistance (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDistance_TSQL
- STDistance (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDistance (geometry Data Type)
ms.assetid: ac815bc7-5342-4cc4-af40-c80a1c4c8b68
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2a93c1063ceb29ef4c67a568b6630e9e44f9f5f8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748657"
---
# <a name="stdistance-geometry-data-type"></a>STDistance (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve la distancia más corta entre un punto de una instancia de **geometry** y un punto de otra instancia de **geometry**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STDistance ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 Es otra instancia de **geometry** a partir de la que medir la distancia entre la instancia en la que se invoca a `STDistance()`. Si *other_geometry* es un conjunto vacío, `STDistance()` devuelve NULL.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de valor devuelto de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Observaciones  
 `STDistance()` siempre devuelve NULL si no coinciden los identificadores de referencia espacial (SRID) de las instancias de **geometry**.  
  
## <a name="examples"></a>Ejemplos  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POINT(10 10)', 0);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>Consulte también  
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
