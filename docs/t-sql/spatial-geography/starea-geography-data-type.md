---
title: STArea (tipo de datos geography) | Documentos de Microsoft
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
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e96ee94983746e162990b8eadad4f6affb4f92fd
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="starea-geography-data-type"></a>STArea (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el área expuesta total de un **geography** instancia. Se devuelven resultados para STArea() en el cuadrado de la unidad de medida usada por el identificador de referencia espacial de la **geography** instancia; por ejemplo, si el SRID de la instancia es 4326, STArea() devuelve resultados en metros cuadrados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **float**  
  
 Tipo de valor devuelto de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentarios  
 STArea() devuelve 0 si una **geography** instancia contiene únicamente figuras 0 y 1-dimensiones, o si está vacía.  
  
> [!NOTE]  
>  Métodos en el **geography** que producen una métrica de devolver el valor tendrán resultados distintos en función del SRID de la instancia utilizada en el método de tipo de datos. Para obtener más información acerca de los SRID, vea [identificadores de referencia espacial &#40; SRID &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza `STArea()` para crear un `Polygon``geography` de instancia y se calcula el área del polígono.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de OGC en instancias de Geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

