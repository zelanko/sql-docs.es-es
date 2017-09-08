---
title: InstanceOf (tipo de datos geography) | Documentos de Microsoft
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
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0edbebbb6754fd09ff834e4ffe8d453853b6f240
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="instanceof-geography-data-type"></a>InstanceOf (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Comprueba si el **geography** instancia es el mismo que el tipo especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.InstanceOf ( 'geography_type')  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_type*  
 Es un **nvarchar (4000)** cadena que especifica uno de los 16 tipos expuestos en el **geography** jerarquía de tipos.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **bits**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentarios  
 Devuelve 1 si el tipo de un **geography** instancia es el mismo que el tipo especificado, o si el tipo especificado es un antecesor del tipo de instancia; en caso contrario, devuelve 0.  
  
 Esto **geography** admite el método de tipo de datos **FullGlobe** instancias o instancias espaciales mayores que un hemisferio.  
  
 La entrada para el método debe ser uno de los siguientes: Geometry, punto, Curve, LineString, CircularString, superficie, Polygon, CurvePolygon, **GeometryCollection**, **MultiSurface**,  **MultiPolygon, MultiCurve, MultiLineString**, **MultiPoint**, o **FullGlobe**.  
  
 Este método produce una excepción `ArgumentException` si se utiliza cualquier otra cadena para la entrada.  
  
 Este método no es preciso.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea un `MultiPoint` instancia y se utiliza `InstanceOf()` para ver si la instancia es un `GeometryCollection`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
