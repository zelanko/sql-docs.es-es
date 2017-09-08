---
title: EnvelopeCenter (tipo de datos geography) | Documentos de Microsoft
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
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0638e8793c75ad78aafa12bec1d1f8a3061022c2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve un punto que se puede usar como el centro de un círculo límite para la **geography** instancia.  
  
 Para determinar el círculo límite, cada punto de la instancia se describe como un vector desde el centro de la Tierra al punto en la superficie de la Tierra. Para calcular el punto central del círculo límite, se calcula el promedio de todos los vectores. Bucles cerrados, ya sea en un **polígono** instancia o un **linestring** de instancia, el primer y último punto se utiliza una sola vez.  
  
 Esto **geography** admite el método de tipo de datos **FullGlobe** instancias o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 Este método devuelve un **punto**. Cuando se usa con `EnvelopeAngle()`, `EnvelopeCenter()` devuelve un círculo de límite de un **geography** instancia.  
  
> [!NOTE]  
>  `EnvelopeCenter()`Devuelve un círculo límite para un **geography** instancia, pero los resultados no se garantiza para generar el círculo de límite mínimo. En cambio, el **geometry** método de tipo de datos `STEnvelope()` se garantiza para devolver el cuadro de límite mínimo cuando se aplica a un **geometry** instancia.  
  
 En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores, devuelve el centro del círculo que representa el envolvente de esta instancia como un **punto**. Para todos los objetos grandes como está definido en `EnvelopeAngle()` = 180, `EnvelopeCenter()` devolverá (90,0).  
  
 Este método no es preciso.  
  
## <a name="examples"></a>Ejemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
