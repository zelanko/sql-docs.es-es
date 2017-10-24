---
title: Filtro (tipo de datos geography) | Documentos de Microsoft
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
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 537e3a05ad368be5278eef9dc9c3d29d19754322
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="filter-geography-data-type"></a>Filter (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Un método que ofrece un método rápido solo para índices de intersección para determinar si un **geography** instancia se corta con otra **geography** instancia, suponiendo que hay un índice disponible.  
  
 Devuelve 1 si una **geography** instancia puede intersectar con otra **geography** instancia. Este método puede generar una respuesta falsa positiva y el resultado exacto puede depender del plan. Devuelve un valor 0 preciso (respuesta verdadera negativa) si no hay ninguna intersección de **geography** instancias encontradas.  
  
 En casos donde un índice no está disponible o no se utiliza, el método devolverá los mismos valores que **STIntersects()** cuando se llama con los mismos parámetros.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.Filter ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 Es otra **geography** instancia va a comparar con la instancia en la que se invoca Filter().  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **bits**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentarios  
 Este método no es determinista y no es preciso.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `Filter()` para determinar si dos instancias de `geography` forman intersección.  
  
```  
CREATE TABLE sample (id int primary key, g geography);  
INSERT INTO sample VALUES  
   (0, geography::Point(45, -120, 4326)),  
   (1, geography::Point(45, -120.1, 4326)),  
   (2, geography::Point(45, -120.2, 4326)),  
   (3, geography::Point(45, -120.3, 4326)),  
   (4, geography::Point(45, -120.4, 4326));  
  
CREATE SPATIAL INDEX sample_idx on sample(g);  
SELECT id  
FROM sample   
WHERE g.Filter(geography::Parse(  
   'POLYGON((-120.1 44.9, -119.9 44.9, -119.9 45.1, -120.1 45.1, -120.1 44.9))')) = 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  

