---
title: M (tipo de datos geography) | Documentos de Microsoft
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
f1_keywords:
- M (geography Data Type)
- M_TSQL
dev_langs: TSQL
helpviewer_keywords: M method
ms.assetid: cdba04f0-4e17-48f6-bafb-b1f918c5a501
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df8a2eb38891ba584d6ffee666b4df5312996b44
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="m-geography-data-type"></a>M (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  El **M** (medida) valor de la **geography** instancia. La semántica del valor de medida la define el usuario, pero normalmente describe la distancia en un linestring. Por ejemplo, el valor de medida se podría usar para realizar un seguimiento de los mojones a lo largo de una carretera.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.M  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentarios  
 El valor de esta propiedad es null si el **geography** instancia no es un **punto**, así como a cualquier **punto** instancia para que no se establece.  
  
 Esta propiedad es de solo lectura.  
  
 Valores M no se usan en los cálculos realizados por la biblioteca y no se llevará a través de los cálculos de biblioteca.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` con valores Z (elevación) y M (medida), y se usa `M` para capturar el valor `M` de la instancia.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
