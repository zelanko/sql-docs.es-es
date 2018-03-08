---
title: STConvexHull (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d797c6e2b0e4f7163aae0e1b6ecb37af95051942
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve un objeto que representa la forma convexa de un **geography** instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 Devuelve un `FullGlobe` objeto **geography** instancia que tiene un ángulo envolvente mayor de 90 grados.  
  
 Devuelve una instancia vacía **geography** colección para vacío **geography** instancia.  
  
 Devuelve **null** para una sin inicializar **geography** instancia.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>A. Usar STConvexHull() en una instancia de geography no inicializada  
 En el ejemplo siguiente se utiliza `STConvexHull()` en una variable **geography** instancia.  
  
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
 En el ejemplo siguiente se utiliza `STConvexHull()` en un **geography** instancia con un ángulo envolvente mayor de 90 grados.  
  
```
 DECLARE @g geography = 'POLYGON((20.533 46.566, -18.283 46.1, -22.3 47.45, 20.533 46.566))';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
  
