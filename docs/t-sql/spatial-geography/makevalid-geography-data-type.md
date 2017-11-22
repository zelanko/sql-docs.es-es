---
title: MakeValid (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: becd452525b999e0a23810aefd2455ee74ab0c67
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="makevalid-geography-data-type"></a>MakeValid (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Convierte un **geography** instancia que no es válido en válido **geography** instancia con un tipo de Open Geospatial Consortium (OGC) válido.  
  
 Si un objeto de entrada devuelve False para STIsValid(), `MakeValid()` convierte la instancia que no es válida en una instancia válida.  
  
 Admite el método de tipo de este datos geography **FullGlobe** instancias o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 Este método puede cambiar el tipo de la **geography** instancia. Además, los puntos de un **geography** instancia puede desplazarse ligeramente. Pueden cambiar los resultados de algunos métodos como NumPoint().  
  
 En casos donde la instancia espacial no válida se corta con el Ecuador y tiene un EnvelopeAngle() = 180, un **FullGlobe** se devolverá la instancia. El `MakeValid()` **geography** método de tipo de datos hará lo posible pare de devolver instancias válidas, pero no se garantiza que los resultados precisos ni exactos.  
  
> [!NOTE]  
>  Los objetos no válidos se pueden almacenar en la base de datos. Los métodos que se pueden ejecutar en instancias no válidas (aquellas instancias en las que STIsValid() devuelven False) son métodos que comprueban la validez o permiten la exportación: STIsValid(), MakeValid(), STAsText(), STAsBinary(), ToString(), AsTextZM() y AsGml().  
  
 Este método no es preciso.  
  
## <a name="examples"></a>Ejemplos  
 En el primer ejemplo se crea una instancia de `LineString` no válida que se superpone a sí misma y usa `STIsValid()` para confirmar que es una instancia no válida. `STIsValid()` devuelve el valor 0 para una instancia no válida.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 4326);  
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
  
## <a name="see-also"></a>Vea también  
 [STIsValid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
