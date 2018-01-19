---
title: Z (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs: TSQL
helpviewer_keywords: Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60ca49605233bcdc374341c7d481cc12b03328c5
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="z-geometry-data-type"></a>Z (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

El valor (elevación) Z de la instancia. La semántica del valor de elevación la define el usuario.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentarios  
 El valor de esta propiedad será null si la instancia de geometry no es un punto, así como a cualquier **punto** instancia para que no se establece.  
  
 Esta propiedad es de solo lectura.  
  
 Las coordenadas z no se usan en los cálculos realizados por la biblioteca y, por lo tanto, no se incluirán en ninguno de dichos cálculos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` con valores Z (elevación) y M (medida), y se usa `Z` para capturar el valor Z de la instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>Vea también  
 [M &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [AsTextZM &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

