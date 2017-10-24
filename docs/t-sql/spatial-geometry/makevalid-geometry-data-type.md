---
title: MakeValid (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MakeValid
- MakeValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid (geometry Data Type)
ms.assetid: 38673010-ab77-4ebb-9c4d-b26b79e3b7ea
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cbb400b17584ef349609d876b2e700b8257ca4a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="makevalid-geometry-data-type"></a>MakeValid (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Convierte un válido **geometry** instancia en un **geometry** instancia con un tipo de Open Geospatial Consortium (OGC) válido.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentarios  
 Este método puede producir un cambio en el tipo de la **geometry** de instancia, así como para provocar que los puntos de un **geometry** instancia se desplacen ligeramente.  
  
## <a name="examples"></a>Ejemplos  
 En el primer ejemplo se crea una instancia de `LineString` no válida que se superpone a sí misma y usa `STIsValid()` para confirmar que es una instancia no válida. `STIsValid()` devuelve el valor 0 para una instancia no válida.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 0);  
SELECT @g.STIsValid();  
```  
  
 En el segundo ejemplo se usa `MakeValid()` para convertir la instancia en válida y comprobar que de hecho es así. `STIsValid()` devuelve el valor 1 para una instancia válida.  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 En el tercer ejemplo se comprueba cómo se ha cambiado la instancia para convertirla en una instancia válida.  
  
```  
SELECT @g.ToString();  
```  
  
 En este ejemplo, cuando se selecciona la instancia de `LineString`, los valores se devuelven como una instancia de `MultiLineString` válida.  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
 El siguiente ejemplo convierte la instancia CircularString en una instancia Point.  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 1 1, 1 1)';  
SELECT @g.MakeValid().ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [STIsValid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Métodos extendidos en instancias de Geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


