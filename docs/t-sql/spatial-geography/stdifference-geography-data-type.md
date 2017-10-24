---
title: STDifference (tipo de datos geography) | Documentos de Microsoft
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
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5afb37eb29e63d8cf08e9c158b94385a66d4c41f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="stdifference-geography-data-type"></a>STDifference (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve un objeto que representa el punto establecido desde una **geography** instancia que se encuentra fuera de otra **geography** instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STDifference ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 Es otra **geography** instancia que indica que apunta a quitar de la instancia en la que se está llamando a STDifference().  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Excepciones  
 Este método produce una **ArgumentException** si la instancia contiene un borde opuesto.  
  
## <a name="remarks"></a>Comentarios  
 Este método siempre devuelve null si los identificadores de referencia espacial (SRID) de la **geography** instancias no coinciden.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el conjunto de resultados posibles devuelto en el servidor se ha ampliado a **FullGlobe** instancias. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite instancias espaciales mayores que un hemisferio. El resultado puede contener segmentos de arco circulares solo si las instancias de entrada contienen segmentos de arco circulares. Este método no es preciso.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>A. Calcular la diferencia entre dos instancias de geografía  
 En el ejemplo siguiente se utiliza `STDifference()` para calcular la diferencia entre dos **geography** instancias.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-using-a-fullglobe-with-stdifference"></a>B. Utilizar FullGlobe con STDifference()  
 En el ejemplo siguiente se utiliza la instancia de `FullGlobe`. El primer resultado es un elemento `GeometryCollection` vacío y el segundo resultado es una instancia de `Polygon`. `STDifference()` devuelve un elemento `GeometryCollection` vacío cuando una instancia de `FullGlobe` es el parámetro. Todos los puntos de una instancia de `geography` que se invoca están contenidos en una instancia de `FullGlobe`.  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 DECLARE @h geography = 'FULLGLOBE';  
 SELECT @g.STDifference(@h).ToString(),  
 @h.STDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de OGC en instancias de Geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

