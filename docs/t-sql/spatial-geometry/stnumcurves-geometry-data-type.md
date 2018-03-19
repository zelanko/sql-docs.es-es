---
title: STNumCurves (tipo de datos geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92cf7af65b64c412aff37311ccf1e9b44484968b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Este método devuelve el número de curvas en una instancia de **geometry** cuando la instancia es un tipo de datos espacial unidimensional. Los tipos de datos espaciales unidimensionales incluyen **LineString**, **CircularString** y **CompoundCurve**. `STNumCurves`() solo funciona en tipos simples; no funciona con colecciones de **geometry** como **MultiLineString**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Notas  
 Una instancia vacía unidimensional de **geometry** devuelve 0. Se devuelve **NULL** cuando la instancia de **geometry** no es una instancia unidimensional o es una instancia no inicializada.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. Usar STNumCurves() en una instancia de CircularString  
 En el siguiente ejemplo se muestra cómo obtener el número de curvas de una instancia de `CircularString`:  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. Usar STNumCurves() en una instancia de CompoundCurve  
 En el siguiente ejemplo se utiliza `STNumCurves()` para devolver el número de curvas de una instancia de `CompoundCurve`.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>Ver también  
 [Información general de los tipos de datos espaciales](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

