---
title: STConvexHull (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a8376d12352994cd768b806f5ce47463196d4bfd
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
  
  
