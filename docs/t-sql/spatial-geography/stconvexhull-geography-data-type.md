---
title: STConvexHull (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: c823f686909be54890b3c1686da615233c3e9da2
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937127"
---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve un objeto que representa la envolvente convexa de una instancia de **geography**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Notas  
 Devuelve un objeto `FullGlobe` para una instancia de **geography** que tiene un ángulo envolvente mayor de 90 grados.  
  
 Devuelve una colección vacía de **geography** para una instancia vacía de **geography**.  
  
 Devuelve **null** para una instancia no inicializada de **geography**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>A. Usar STConvexHull() en una instancia de geography no inicializada  
 En el ejemplo siguiente se usa `STConvexHull()` en una instancia no inicializada de **geography**.  
  
```
 DECLARE @g geography;  
 SELECT @g.STConvexHull();
 ```  
  
### <a name="b-using-stconvexhull-on-an-empty-geography-instance"></a>B. Usar STConvexHull en una instancia vacía de geography  
 En el ejemplo siguiente se usa `STConvexHull()` en una instancia vacía de `Polygon`.  
  
```
 DECLARE @g geography = 'POLYGON EMPTY';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
### <a name="c-finding-the-convex-hull-of-a-non-convex-polygon-instance"></a>C. Buscar la forma convexa de una instancia de Polygon no convexa  
 En el siguiente ejemplo se usa `STConvexHull()` para buscar la forma convexa de una instancia no convexa de `Polygon`.  
  
```  
 DECLARE @g geography;  
 SET @g = geography::Parse('POLYGON((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
 SELECT @g.STConvexHull().ToString();  
```  
  
### <a name="d-finding-the-convex-hull-on-a-geography-instance-with-an-envelope-angle-larger-than-90-degrees"></a>D. Buscar la forma convexa de una instancia de geography con un ángulo envolvente mayor de 90 grados  
 En el ejemplo siguiente se usa `STConvexHull()` en una instancia de **geography** con un ángulo envolvente mayor de 90 grados.  
  
```
 DECLARE @g geography = 'POLYGON((20.533 46.566, -18.283 46.1, -22.3 47.45, 20.533 46.566))';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
  
