---
title: STNumCurves (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STNumCurves
- STNumCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geography)
ms.assetid: e98a56c2-8496-4dfd-9b37-7f3c4ca9b2b5
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c92c6dec90faf08d69ed49de506ba8c4371141ba
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="stnumcurves-geography-data-type"></a>STNumCurves (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve el número de curvas de una unidimensional **geography** instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 Los tipos de datos espaciales unidimensionales incluyen **LineString**, **CircularString**, y **CompoundCurve**. Unidimensional vacía **geography** instancia devuelve 0.  
  
 `STNumCurves`() funciona solo en tipos simples; no funciona con **geography** colecciones como **MultiLineString**. **NULL** se devuelve cuando la **geography** instancia no es un tipo de datos unidimensional.  
  
 **NULL** se devuelve para que no se ha inicializado **geography** instancias.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. Usar STNumCurves() en una instancia de CircularString  
 En el siguiente ejemplo se muestra cómo obtener el número de curvas de una instancia de `CircularString`:  
  
```
 DECLARE @g geography; 
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. Usar STNumCurves() en una instancia de CompoundCurve  
 En el siguiente ejemplo se utiliza `STNumCurves()` para devolver el número de curvas de una instancia de `CompoundCurve`.  
  
```
 DECLARE @g geography;  
 SET @g = geography::Parse('COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>Vea también  
 [Información general de los tipos de datos espaciales](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Métodos de OGC en instancias de Geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

